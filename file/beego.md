# 控制器

# beego 路由设置

路由指的就是一个url请求由谁来处理，在beego设计中，url请求可以由控制器的函数来处理，也可以由一个单独的函数来处理，因此路由设置由两部分组成：**url路由** 和 **处理函数**。

beego提供两种设置处理函数的方式:

- 直接绑定一个函数
- 绑定一个控制器对象 （RESTful方式）

## 1.直接绑定处理函数

这种方式直接将一个url路由和一个函数绑定起来。

例子：

```go
// 这就是将url / 和一个闭包函数绑定起来, 这个url的Get请求由这个闭包函数处理。
beego.Get("/",func(ctx *context.Context){
     ctx.Output.Body([]byte("hi tizi365.com"))
})

// 定义一个处理函数
func Index(ctx *context.Context){
     ctx.Output.Body([]byte("欢迎访问 tizi365.com"))
}

// 注册路由, 将url /index 和Index函数绑定起来，由Index函数处理这个url的Post请求
beego.Post("/index", Index)
```

下面是beego支持的基础函数：

- beego.Get(router, beego.FilterFunc)
- beego.Post(router, beego.FilterFunc)
- beego.Put(router, beego.FilterFunc)
- beego.Patch(router, beego.FilterFunc)
- beego.Head(router, beego.FilterFunc)
- beego.Options(router, beego.FilterFunc)
- beego.Delete(router, beego.FilterFunc)
- beego.Any(router, beego.FilterFunc) - 处理任意http请求，就是不论请求方法（Get,Post,Delete等等）是什么，都由绑定的函数处理

根据不同的http请求方法（Get,Post等等）选择不同的函数设置路由即可。

## 2.RESTful路由方式

RESTful 是一种目前比较流行的url风格，beego默认支持这种风格。
在beego项目中，RESTful路由方式就是将url路由跟一个控制器对象绑定，然后Get请求由控制的Get函数处理，Post请求由Post函数处理，以此类推。

RESTful路由使用**beego.Router**函数设置路由。

例子:

```go
// url: / 的所有http请求方法都由MainController控制器的对应函数处理
beego.Router("/", &controllers.MainController{})

// url: /user 的所有http请求方法都由UserController控制器的对应函数处理
// 例如: GET /user请求，由Get函数处理, POST /user 请求，由Post函数处理
beego.Router("/user", &controllers.UserController{})
```

## 3.url路由方式

上面介绍了设置处理函数的方式，下面介绍beego支持的url路由方式。

> 提示： 下面介绍的所有url路由规则，都适用于上面介绍的所有路由设置函数。

### 3.1.固定路由

前面介绍的url路由例子，都属于固定路由方式，固定路由指的是url规则是固定的一个url。
例子:

```go
beego.Router("/user", &controllers.UserController{})
beego.Router("/shop/order", &controllers.OrderController{})
beego.Router("/shop/comment", &controllers.CommentController{})
```

### 3.2.正则路由

正则路由比较灵活，一个正则路由设置代表的是一序列的url, 正则路由更像是一种url模板。
url路由例子:

- **/user/:id**
  匹配/user/132，参数 :id=132
- **/user/:id([0-9]+)**
  匹配/user/123，参数 :id=123， 跟上面例子的区别就是只能匹配数字
- **/user/:username([\w]+)**
  匹配/user/tizi, 参数 :username=tizi
- **/list_:cat([0-9]+)_:page([0-9]+).html**
  匹配/list_2_1.html, 参数 :cat=2, :page=1
- **/api/***
  匹配/api为前缀的所有url, 例子: /api/user/1 , 参数: :splat=user/1

在 Controller 对象中，可以通过下面的方式获取url路由匹配的参数：

```go
this.Ctx.Input.Param(":id")
this.Ctx.Input.Param(":username")
this.Ctx.Input.Param(":cat")
this.Ctx.Input.Param(":page")
this.Ctx.Input.Param(":splat")
```

### 3.3.自动路由

自动路由指的是通过反射获取到控制器的名字和控制器实现的所有函数名字，自动生成url路由。

使用自动路由首先需要beego.AutoRouter函数注册控制器。
例子:

```go
beego.AutoRouter(&controllers.UserController{})
```

url自动路由例子:

```go
/user/login   调用 UserController 中的 Login 方法
/user/logout  调用 UserController 中的 Logout 方法
```

除了前缀两个 /:controller/:method 的匹配之外，剩下的 url beego 会帮你自动化解析为参数，保存在 this.Ctx.Input.Params 当中：

```go
/user/list/2019/09/11  调用 UserController 中的 List 方法，参数如下：map[0:2019 1:09 2:11]
```

> 提示：自动路由会将url和控制器名字、函数名字转换成小写。

### 3.4.namespace

路由名字空间(namespace)，一般用来做api版本处理。

例子:

```go
// 创建版本1的名字空间
ns1 := beego.NewNamespace("/v1",
    // 内嵌一个/user名字空间
    beego.NSNamespace("/user",
        // 下面开始注册路由
        // url路由: /v1/user/info
        beego.NSRouter("/info", &controllers.UserController{}),
        // url路由: /v1/user/order
        beego.NSRouter("/order", &controllers.UserOrderController{}),
    ),
    // 内嵌一个/shop名字空间
    beego.NSNamespace("/shop",
        // 下面开始注册路由
        // url路由: /v1/shop/info
        beego.NSRouter("/info", &controllers.ShopController{}),
        // url路由: /v1/shop/order
        beego.NSRouter("/order", &controllers.ShopOrderController{}),
    ),
)

// 创建版本2的名字空间
ns2 := beego.NewNamespace("/v2",
    beego.NSNamespace("/user",
        // url路由: /v2user/info
        beego.NSRouter("/info", &controllers.User2Controller{}),
    ),
    beego.NSNamespace("/shop",
        // url路由: /v2/shop/order
        beego.NSRouter("/order", &controllers.ShopOrder2Controller{}),
    ),
)

//注册 namespace
beego.AddNamespace(ns1)
beego.AddNamespace(ns2)
```

通过NewNamespace函数创建多个名字空间，NSNamespace函数可以无限嵌套名字空间,  根据上面的例子可以看出来，名字空间的作用其实就是定义url路由的前缀，如果一个名字空间定义url路由为/user,  那么这个名字空间下面定义的所有路由的前缀都是以/user开头。

下面是namespace支持的路由设置函数:

- NewNamespace(prefix string, funcs …interface{})
- NSNamespace(prefix string, funcs …interface{})
- NSInclude(cList …ControllerInterface)
- NSRouter(rootpath string, c ControllerInterface, mappingMethods …string)
- NSGet(rootpath string, f FilterFunc)
- NSPost(rootpath string, f FilterFunc)
- NSDelete(rootpath string, f FilterFunc)
- NSPut(rootpath string, f FilterFunc)
- NSHead(rootpath string, f FilterFunc)
- NSOptions(rootpath string, f FilterFunc)
- NSPatch(rootpath string, f FilterFunc)
- NSAny(rootpath string, f FilterFunc)
- NSHandler(rootpath string, h http.Handler)
- NSAutoRouter(c ControllerInterface)
- NSAutoPrefix(prefix string, c ControllerInterface)

这些路由设置函数的参数，跟前面的路由设置函数一样，区别就是namespace的函数名前面多了NS前缀。

# 控制器函数

## 1.beego.FilterFunc函数

这是最简单的请求处理函数，函数原型定义：

```go
type FilterFunc func(*context.Context)
```

也就是只要定义一个函数，并且接收一个Context参数，那么这个函数就可以作为处理用户请求的函数。

例子:

```go
func DoLogin(ctx *context.Context) {
     // ..处理请求的逻辑...
     // 可以通过Context 获取请求参数，返回请求结果
}
```

有了处理函数，我们就可以将处理函数跟一个url路由绑定起来.

例子:

```go
beego.Get("/user/login", DoLogin)
```

> 提示: 新版的beego设计，默认不推荐使用beego.FilterFunc函数方式，这种方式处理请求的方式比较原始，后面介绍的控制器函数拥有更多高级特性，后续的教程以控制器函数为主。

## 2.控制器函数

控制器函数是beego的RESTful api的实现方式，在beego的设计中，控制器就是一个嵌套了**beego.Controller**的结构体对象。

例子:

```go
// 定义一个新的控制器
type UserController struct {
    // 嵌套beego基础控制器
    beego.Controller
}
```

前面介绍过，struct嵌套，就类似其他高级语言的 **继承** 特性，嵌套了beego.Controller控制器，就拥有了beego.Controller定义的属性和函数。

控制器命名规则约定：**Xxx**Controller
**Xxx**就是我们的控制器名字, 这是为了便于阅读，看到Controller结尾的struct就知道是一个控制器。

下面看一个完整控制器的例子:

```go
type UserController struct {
    // 嵌套beego基础控制器
    beego.Controller
}

// 在调用其他控制器函数之前，会优先调用Prepare函数
func (this *UserController) Prepare() {
    // 这里可以跑一些初始化工作
}

// 处理get请求
func (this *UserController) Get() {
    // 处理逻辑
}

// 处理post请求
func (this *UserController) Post() {
    // 处理逻辑
}
```

注册路由

```go
// 在这里参数:id是可选的
beego.Router("/user/?:id", &controllers.UserController{})
```

根据上面注册的路由规则, 下面的展示对应的http请求和处理函数:

- GET /user/2 - 由Get函数处理
- POST /user - 由Post函数处理

> 提示：前面路由设置章节介绍过控制器的路由规则是Get请求由Get函数处理，Post请求由Post函数处理，以此类推。

下表展示了beego.Controller默认为我们提供了哪些可选的函数:

> 提示: 根据业务需要，控制器可以覆盖下表中的函数。

| 函数名    | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| Prepare() | 这个函数会优先执行，才会执行Get、Post之类的函数, 可以在Prepare做一些初始化工作。 |
| Get()     | 处理get请求， 如果没有实现该函数，默认会返回405错误。        |
| Post()    | 处理Post请求, 默认会返回405错误。                            |
| Delete()  | 处理Delete请求, 默认会返回405错误。                          |
| Put()     | 处理PUT请求, 默认会返回405错误。                             |
| Finish()  | 执行完Get、Post之类http请求函数之后执行，我们可以在Finish函数处理一些回收工作。 |

## 3.如何提前结束请求

如果我们在Prepare函数处理用户的权限验证，验证不通过，我们一般都希望结束请求，不要执行后面的函数，beego提供了StopRun函数来结束请求。
例子:

```go
func (this *UserController) Prepare() {
    // 处理权限验证逻辑
    
    // 验证不通过，返回错误信息，结束请求
    this.Data["json"] = map[string]interface{}{"error":"没有权限", "errno":401}
	this.ServeJSON()
    this.StopRun()
}
```

> 提示：调用 StopRun 之后，不会再执行Finish函数，如果有需要可以在调用StopRun之后，手动调用Finish函数。

# beego处理请求参数

beego.Controller基础控制器，为我们提供了多种读取请求参数的函数，下面分别介绍各种获取参数的场景。

## 1.默认获取参数方式

beego.Controller基础控制器为我们提供了GetXXX序列获取参数的函数, XXX指的就是返回不同的数据类型。
例子：

```go
// 处理get请求
func (this *UserController) Get() {
	// 获取参数, 返回int类型
	id ,_:= this.GetInt("id")
	
	// 获取参数，返回string类型, 如果参数不存在返回none作为默认值
	username := this.GetString("username", "none")
	
	// 获取参数，返回float类型, 参数不存在则返回 0
	price, _ := this.GetFloat("price", 0)
}
```

下面是常用的获取参数的函数定义：

- GetString(key string, def ...string) string
- GetInt(key string, def ...int) (int, error)
- GetInt64(key string, def ...int64) (int64, error)
- GetFloat(key string, def ...float64) (float64, error)
- GetBool(key string, def ...bool) (bool, error)

默认情况用户请求的参数都是 **字符串** 类型，如果要转换成其他类型，就可能会出现类型转换失败的可能性，因此除了GetString函数，其他GetXXX函数，都返回两个值，第一个值是需要获取的参数值，第二个就是error，表示是数据类型转换是否失败。

## 2.绑定struct方式

除了上面一个一个的获取请求参数，针对POST请求的表单数据，beego支持直接将表单数据绑定到一个struct变量。

例子:

```go
// 定义一个struct用来保存表单数据
// 通过给字段设置tag， 指定表单字段名， - 表示忽略这个字段不进行赋值
// 默认情况下表单字段名跟struct字段名同名（小写）
type UserForm struct {
    // 忽略掉Id字段
    Id    int         `form:"-"`
    // 表单字段名为username
    Name  string      `form:"username"`
    Phone string      
}
```

> 说明： 如果表单字段跟struct字段（小写）同名，不需要设置form标签。 表单html代码:

```javascript
<form action="/user" method="POST">
    手机号：<input name="phone" type="text" /><br/>
    用户名：<input name="username" type="text" />
    <input type="submit" value="提交" />
</form>
```

控制器函数:

```go
func (this *UserController) Post() {
    // 定义保存表单数据的struct对象
    u := UserForm{}
    // 通过ParseForm函数，将请求参数绑定到struct变量。
    if err := this.ParseForm(&u); err != nil {
        // 绑定参数失败
    }
}
```

> 提示：使用struct绑定请求参数的方式，仅适用于POST请求。

## 3.处理json请求参数

一般在接口开发的时候，有时候会将json请求参数保存在http请求的body里面。我们就不能使用前的方式获取json数据，需要直接读取请求body的内容，然后格式化数据。

**处理json参数的步骤**：

1. 在app.conf配置文件中，添加CopyRequestBody=true
2. 通过this.Ctx.Input.RequestBody获取请求body的内容
3. 通过json.Unmarshal反序列化json字符串，将json参数绑定到struct变量。

例子:

定义struct用于保存json数据

```go
// 如果json字段跟struct字段名不一样，可以通过json标签设置json字段名
type UserForm struct {
    // 忽略掉Id字段
    Id    int         `json:"-"`
    // json字段名为username
    Name  string      `json:"username"`
    Phone string      
}
```

控制器代码:

```go
func (this *UserController) Post() {
    // 定义保存json数据的struct对象
    u := UserForm{}
    
    // 获取body内容
    body := this.Ctx.Input.RequestBody
    
    // 反序列json数据，结果保存至u
    if err := json.Unmarshal(body, &u); err == nil {
        // 解析参数失败
    }
}
```

> 提示: 如果将请求参数是xml格式，xml参数也是保存在body中，处理方式类似，就是最后一步使用xml反序列化函数进行处理。

# beego处理响应数据

我们处理完用户的请求之后，通常我们都会返回html代码，然后浏览器就可以显示html内容；除了返回html，在api接口开发中，我们还可以返回json、xml、jsonp格式的数据。

下面分别介绍beego返回不同数据类型的处理方式。

> 注意：如果使用beego开发api，那么在app.conf中设置AutoRender = false， 禁止自动渲染模板，否则beego每次处理请求都会尝试渲染模板，如果模板不存在则报错。

## 1.返回json数据

下面是返回json数据的例子:

```go
// 定义struct
// 如果struct字段名跟json字段名不一样，可以使用json标签,指定json字段名
type User struct {
    // - 表示忽略id字段
	Id       int	`json:"-"`
	Username string `json:"name"`
	Phone    string
}

func (this *UserController) Get() {
    // 定义需要返回给客户端的数据
    user := User{1, "tizi365", "13089818901"}
    
    // 将需要返回的数据赋值给json字段
    this.Data["json"] = &user
    
    // 将this.Data["json"]的数据，序列化成json字符串，然后返回给客户端
    this.ServeJSON()
}
```

> 提示：请参考Go处理json数据教程，了解详细的json数据处理方式。

## 2.返回xml数据

下面是返回xml数据的处理方式跟json类似。

例子:

```go
// 定义struct
// 如果struct字段名跟xml字段名不一样，可以使用xml标签,指定xml字段名
type User struct {
    // - 表示忽略id字段
	Id       int	`xml:"-"`
	Username string `xml:"name"`
	Phone    string
}

func (this *UserController) Get() {
    // 定义需要返回给客户端的数据
    user := User{1, "tizi365", "13089818901"}
    
    // 将需要返回的数据赋值给xml字段
    this.Data["xml"] = &user
    
    // 将this.Data["xml"]的数据，序列化成xml字符串，然后返回给客户端
    this.ServeXML()
}
```

> 提示：请参考Go处理xml数据教程，了解详细的xml数据处理方式。

## 3.返回jsonp数据

返回jsonp数据，于返回json数据方式类似。

例子:

```go
func (this *UserController) Get() {
    // 定义需要返回给客户端的数据
    user := User{1, "tizi365", "13089818901"}
    
    // 将需要返回的数据赋值给jsonp字段
    this.Data["jsonp"] = &user
    
    // 将this.Data["json"]的数据，序列化成json字符串，然后返回给客户端
    this.ServeJSONP()
}
```

## 4.返回html

如果我们开发的是网页，那么通常需要返回html代码，在beego项目中关于html视图部分，使用的是模板引擎技术，渲染html，然后将结果返回给浏览器。

例子:

```go
func (c *MainController) Get() {
    // 设置模板参数
	c.Data["Website"] = "tizi365.com"
	c.Data["Email"] = "tizi365@demo.com"
	
	// 需要渲染的模板， beego会渲染这个模板，然后返回结果
	c.TplName = "index.tpl"
}
```

## 5.添加响应头

为http请求添加header

```go
func (c *MainController) Get() {
    // 通过this.Ctx.Output.Header设置响应头
    this.Ctx.Output.Header("Content-Type", "message/http")
    this.Ctx.Output.Header("Cache-Control", "no-cache, no-store, must-revalidate")
}
```

> 提示：后续会有关于beego视图开发的详细的教程。

# 模型

# orm数据库操作入门

Beego ORM框架是一个独立的ORM模块，主要用于数据库操作。

> 说明: 对象-关系映射（Object/Relation Mapping，简称ORM）, 在Go语言中就是将struct类型和数据库记录进行映射。

下面介绍如何操作mysql数据库。

## 1.安装包

因为beego orm是独立的模块，所以需要单独安装包。

```go
// 安装beego orm包
go get github.com/astaxie/beego/orm
```

安装mysql驱动

```go
go get github.com/go-sql-driver/mysql
```

beego orm包操作什么数据库，就需要单独安装对应的数据库驱动。

## 2.导入包

```go
import (
    // 导入orm包
    "github.com/astaxie/beego/orm"
    
    // 导入mysql驱动
    _ "github.com/go-sql-driver/mysql"
)
```

## 3.连接mysql数据库

操作数据库之前首先需要配置好mysql数据库连接参数，通常在beego项目中，我们都会在main.go文件，对数据库进行配置，方便整个项目操作数据库。

例子：

```go
package main

import (
	_ "beegodemo/routers"
	"github.com/astaxie/beego"
	// 导入orm包
	"github.com/astaxie/beego/orm"
	// 导入mysql驱动
	_ "github.com/go-sql-driver/mysql"
)

// 通过init函数配置mysql数据库连接信息
func init() {
    // 这里注册一个default默认数据库，数据库驱动是mysql.
    // 第三个参数是数据库dsn, 配置数据库的账号密码，数据库名等参数
    //  dsn参数说明：
    //      username    - mysql账号
    //      password    - mysql密码
    //      db_name     - 数据库名
    //      127.0.0.1:3306 - 数据库的地址和端口
	orm.RegisterDataBase("default", "mysql", "username:password@tcp(127.0.0.1:3306)/db_name?charset=utf8&parseTime=true&loc=Local")
	
	// 打开调试模式，开发的时候方便查看orm生成什么样子的sql语句
	orm.Debug = true
}

func main() {
	beego.Run()
}
```

## 4.定义模型(Model)

orm操作通常都是围绕struct对象进行，我们先定义一个表结构，方便后面演示数据库操作。

### 4.1.定义表结构

这里我们创建一个简单的订单表。

```sql
CREATE TABLE `orders` (
  `id` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT '自增ID',
  `shop_id` int(10) unsigned NOT NULL COMMENT '店铺id',
  `customer_id` int(10) unsigned NOT NULL COMMENT '用户id',
  `nickname` varchar(20) DEFAULT NULL COMMENT '用户昵称',
  `address` varchar(200) NOT NULL DEFAULT '' COMMENT '用户地址',
  `init_time` datetime NOT NULL COMMENT '创建订单的时间',
   PRIMARY KEY (`id`)
  ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

### 4.2.定义模型

所谓模型(Model)指的就是关联数据库表的struct类型。
这里我们定义个Order结构体， 他们的字段对应着上面的orders表结构。

```go
// 默认情况struct字段名按照下面规则转换成mysql表字段名：
// 规则:  以下滑线分割首字母大写的单词，然后转换成小写字母。
type Order struct {
    // 对应表字段名为: id
	Id int
	// 对应表字段名为: shop_id , 下面字段名转换规则以此类推。
	ShopId int
	// struct字段名跟表字段名不一样，通过orm标签指定表字段名为customer_id
	Uid int	`orm:"column(customer_id)"`
	Nickname string
	Address string
	// 数据库init_time字段是datetime类型，支持自动转换成Go的time.Time类型，但是数据库连接参数必须设置参数parseTime=true
	InitTime time.Time
}

// 指定Order结构体默认绑定的表名
func (o *Order) TableName() string {
	return "orders"
}

// 注册模型
orm.RegisterModel(new(Order))
```

## 5.插入数据

例子1:

```go
// 创建orm对象, 后面都是通过orm对象操作数据库
o := orm.NewOrm()

// 创建一个新的订单
order := Order{}
// 对order对象赋值
order.ShopId = 1
order.Uid = 1002
order.Nickname = "大锤"
order.Address = "深圳南山区"
order.InitTime = time.Now()

// 调用orm的Insert函数插入数据
// 等价sql： INSERT INTO `orders` (`shop_id`, `customer_id`, `nickname`,
`address`, `init_time`) VALUES (1, 1002, '大锤', '深圳南山区', '2019-06-24 23:08:57')
id, err := o.Insert(&order)

if err != nil {
    fmt.Println("插入失败")
} else {
    // 插入成功会返回插入数据自增字段，生成的id
    fmt.Println("新插入数据的id为:", id)
}
```

例子2 批量插入数据：

```go
o := orm.NewOrm()

orders := []Order{
    {ShopId:1, Uid:1001, Nickname:"大锤1", Address:"深圳南山区", InitTime: time.Now()},
    {ShopId:1, Uid:1002, Nickname:"大锤2", Address:"深圳南山区", InitTime: time.Now()},
    {ShopId:1, Uid:1003, Nickname:"大锤3", Address:"深圳南山区", InitTime: time.Now()},
}

// 调用InsertMulti函数批量插入， 第一个参数指的是要插入多少数据
nums, err := o.InsertMulti(3, orders)
```

## 6.更新数据

orm的Update函数是根据主键id进行更新数据的，因此需要预先对id赋值。

例子:

```go
o := orm.NewOrm()

// 需要更新的order对象
order := Order{}
// 先对主键id赋值, 更新数据的条件就是where id=2
order.Id = 2

// 对需要更新的数据进行赋值
order.Nickname = "小锤"
order.Address = "深圳宝安区"

// 调用Update函数更新数据, 默认Update根据struct字段，更新所有字段值，如果字段值为空也一样更新。
// 等价sql: update orders set shop_id=0, customer_id=0, nickname='小锤', address='深圳宝安区', init_time='0000:00:00'  where id = 2
num, err := o.Update(&order)
if err != nil {
    fmt.Println("更新失败")
} else {
    fmt.Println("更新数据影响的行数:", num)
}


// 上面Update直接更新order结构体的所有字段，如果只想更新指定字段，可以这么写
num, err := o.Update(&order, "Nickname", "Address")
// 这里只是更新Nickname和Address两个字段
```

## 7.查询数据

默认orm的Read函数也是通过主键id查询数据。

例子:

```go
o := orm.NewOrm()
// 定义order
order := Order{}
// 先对主键id赋值, 查询数据的条件就是where id=2
order.Id = 2

// 通过Read函数查询数据
// 等价sql: select id, shop_id, customer_id, nickname, address, init_time from orders where id = 2
err := o.Read(&order)

if err == orm.ErrNoRows {
    fmt.Println("查询不到")
} else if err == orm.ErrMissPK {
    fmt.Println("找不到主键")
} else {
    fmt.Println(order.Id, order.Nickname)
}

// 通过ReadOrCreate函数，先尝试根据主键id查询数据，如果数据不存在则插入一条数据
created, id, err := o.ReadOrCreate(&order, "Id")
// ReadOrCreate返回三个参数，第一个参数表示是否插入了一条数据，第二个参数表示插入的id
```

## 8.删除数据

orm的Delete函数根据主键id删除数据。

例子:

```go
o := orm.NewOrm()
// 定义order
order := Order{}
// 先对主键id赋值, 删除数据的条件就是where id=2
order.Id = 2

if num, err := o.Delete(&order); err != nil {
    fmt.Println("删除失败")
} else {
    fmt.Println("删除数据影响的行数:", num)
}
```

# orm数据库连接设置

## 1.beego支持的数据库类型

目前 ORM 支持三种数据库，分别是:

- mysql
- sqlite3
- Postgres

使用不通的数据库，需要导入不通的数据库驱动：

```go
import (
    // 导入mysql驱动
    _ "github.com/go-sql-driver/mysql"
    // 导入sqlite3驱动
    _ "github.com/mattn/go-sqlite3"
    // 导入Postgres驱动
    _ "github.com/lib/pq"
)
```

根据需要导入自己想要的驱动即可。

## 2.mysql数据库连接

这里介绍mysql数据库的详细链接参数，要想连接mysql数据库，首先得注册一个数据库，在调用查询函数会自动创建连接。

ORM 必须注册一个别名为 **default** 的数据库，作为默认使用的数据库。

注册数据库的函数原型：

func RegisterDataBase(aliasName, driverName, dataSource string, params ...int) error

**参数说明**：

| 参数名     | 说明                                      |
| ---------- | ----------------------------------------- |
| aliasName  | 数据库的别名，用来在 ORM 中切换数据库使用 |
| driverName | 驱动名字                                  |
| dataSource | 数据库连接字符串                          |
| params     | 附加参数                                  |

例子:

```go
// 注册默认数据库，驱动为mysql, 第三个参数就是我们的数据库连接字符串。
orm.RegisterDataBase("default", "mysql", "root:123456@tcp(localhost:3306)/tizi?charset=utf8")
```

mysql数据库连接字符串DSN (Data Source Name)详解：

格式:

```go
username:password@protocol(address)/dbname?param=value
```

**参数说明**：

| 参数名      | 说明                                                         |
| ----------- | ------------------------------------------------------------ |
| username    | 数据库账号                                                   |
| password    | 数据库密码                                                   |
| protocol    | 连接协议，一般就是tcp                                        |
| address     | 数据库地址，可以包含端口。例: localhost:3306 , 127.0.0.1:3306 |
| dbname      | 数据库名字                                                   |
| param=value | 最后面问号（?)之后可以包含多个键值对的附加参数,多个参数之间用&连接。 |

常用附加参数说明：

| 参数名      | 默认值 | 说明                                                         |
| ----------- | ------ | ------------------------------------------------------------ |
| charset     | none   | 设置字符集，相当于 SET NAMES <value> 语句                    |
| loc         | UTC    | 设置时区，可以设置为Local，表示根据本地时区走                |
| parseTime   | false  | 是否需要将 mysql的 DATE 和 DATETIME 类型值转换成GO的time.Time类型。 |
| readTimeout | 0      | I/O 读超时时间, sql查询超时时间. 单位 ("ms", "s", "m", "h"), 例子: "30s", "0.5m" or "1m30s". |
| timeout     | 0      | 连接超时时间，单位("ms", "s", "m", "h"), 例子: "30s", "0.5m" or "1m30s". |

例子:

```go
root:123456@(123.180.11.30:3306)/tizi?charset=utf8&timeout=5s&loc=Local&parseTime=true
```

## 3.数据库连接池设置

数据库连接词参数主要有下面两个：

### 3.1. SetMaxIdleConns

根据数据库的别名，设置数据库的最大空闲连接

```go
orm.SetMaxIdleConns("default", 20)
```

### 3.2. SetMaxOpenConns

根据数据库的别名，设置数据库的最大数据库连接

```go
orm.SetMaxOpenConns("default", 100)
```

## 4.数据库调试模式

打开调试模式，当执行orm查询的时候，会打印出对应的sql语句。

```go
orm.Debug = true
```

# orm高级查询

针对业务比较复杂，涉及复杂的查询条件的场景，beego orm为我们提供了QuerySeter 对象，用来组织复杂的查询条件。

## 1.QuerySeter入门

因为QuerySeter是专门针对ORM的模型对象进行操作的，所以在使用QuerySeter之前必须先定义好模型。

## 1.1.表定义

模型（model）是跟表结构一一对应的，作为例子这里先定义下表结构。

```sql
// 定义用户表
CREATE TABLE `users` (
  `id` int(10) UNSIGNED NOT NULL COMMENT '自增ID',
  `username` varchar(30) NOT NULL COMMENT '账号',
  `password` varchar(100) NOT NULL COMMENT '密码',
  `city` varchar(50) DEFAULT NULL COMMENT '城市',
  `init_time` datetime DEFAULT NULL COMMENT '创建时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

## 1.2.模型定义

```go
//定义User模型，绑定users表结构
type User struct {
	Id int
	Username string
	Password string
	City string
	// 驼峰式命名，会转换成表字段名，表字段名使用蛇形命名风格，即用下划线将单词连接起来
    // 这里对应数据库表的init_time字段名
	InitTime time.Time
}

// 定义模型表名
func (u *User) TableName() string {
	return "users"
}
```

## 1.3.QuerySeter例子

```go
// 创建orm对象
o := orm.NewOrm()

// 获取 QuerySeter 对象，并设置表名orders
qs := o.QueryTable("users")

// 定义保存查询结果的变量
var users []User

// 使用QuerySeter 对象构造查询条件，并执行查询。
num, err := qs.Filter("city", "shenzhen").  // 设置查询条件
		Filter("init_time__gt", "2019-06-28 22:00:00"). // 设置查询条件
		Limit(10). // 限制返回行数
		All(&users, "id", "username") // All 执行查询，并且返回结果，这里指定返回id和username字段，结果保存在users变量
// 上面代码的等价sql: SELECT T0.`id`, T0.`username` FROM `users` T0 WHERE T0.`city` = 'shenzhen' AND T0.`init_time` > '2019-06-28 22:00:00' LIMIT 10

if err != nil {
	panic(err)
}
fmt.Println("结果行数:", num)
```

## 2.QuerySeter查询表达式

beego orm针对QuerySeter设置一套查询表达式，用于编写查询条件。

> 提示：下面例子，使用Filter函数描述查询表达式，实际上其他查询函数也支持查询表达式。

**表达式格式1**：

```go
qs.Filter("id", 1) // 相当于条件 id = 1
```

**表达式格式2**：
使用**双下划线** __ 作为分隔符，尾部连接操作符

```go
qs.Filter("id__gt", 1) // 相当于条件 id > 1
qs.Filter("id__gte", 1) // 相当于条件 id >= 1
qs.Filter("id__lt", 1) // 相当于条件 id < 1
qs.Filter("id__lte", 1) // 相当于条件 id <= 1
qs.Filter("id__in", 1,2,3,4,5) // 相当于In语句 id in (1,2,3,4,5)
```

下面是支持的操作符：

- exact / iexact 等于
- contains / icontains 包含
- gt / gte 大于 / 大于等于
- lt / lte 小于 / 小于等于
- startswith / istartswith 以…起始
- endswith / iendswith 以…结束
- in
- isnull 后面以 i 开头的表示：大小写不敏感

例子:

```go
qs.Filter("Username", "大锤") // 相当于条件 name = '大锤'
qs.Filter("Username__exact", "大锤") // 相当于条件 name = '大锤'
qs.Filter("Username__iexact", "大锤") // 相当于条件 name LIKE '大锤'
qs.Filter("Username__iexact", "大锤") // 相当于条件 name LIKE '大锤'
qs.Filter("Username__contains", "大锤") // 相当于条件 name LIKE BINARY '%大锤%'   , BINARY 区分大小写
qs.Filter("Username__icontains", "大锤") // 相当于条件 name LIKE '%大锤%'
qs.Filter("Username__istartswith", "大锤") // 相当于条件 name LIKE '大锤%'
qs.Filter("Username__iendswith", "大锤") // 相当于条件 name LIKE '%大锤'
qs.Filter("Username__isnull", true) // 相当于条件 name is null
qs.Filter("Username__isnull", false) // 相当于条件 name is not null
```

多个Filter函数调用使用 **and** 连接查询条件。
例子:

```go
qs.Filter("id__gt", 1).Filter("id__lt", 100) // 相当于条件 id > 1 and id < 100
```

## 3.处理复杂的查询条件

上面的例子多个Filter函数调用只能生成and连接的查询条件，那么如果要设置or条件就不行了；beego orm为我们提供了Condition对象，用于生成查询条件。

例子:

```go
//  创建一个Condition对象
cond := orm.NewCondition()

// 组织查询条件, 并返回一个新的Condition对象
cond1 := cond.And("Id__gt", 100).Or("City","shenzhen")
// 相当于条件 id > 100 or city = 'shenzhen'

var users []User

qs.SetCond(cond1). // 设置查询条件
  Limit(10). // 限制返回数据函数
  All(&users) // 查询多行数据
```

## 3.查询数据

### 3.1.查询多行数据

使用All函数可以返回多行数据。

例子:

```go
// 创建orm对象
o := orm.NewOrm()

// 获取 QuerySeter 对象，并设置表名orders
qs := o.QueryTable("users")

// 定义保存查询结果的变量
var users []User

// 使用QuerySeter 对象构造查询条件，并执行查询。
// 等价sql: select * from users where id > 1 and id < 100 limit 10
num, err := qs.Filter("Id__gt", 1).
		Filter("Id__lt", 100).
		Limit(10). // 限制返回行数
		All(&users) // 返回多行数据， 也可以设置返回指定字段All(&users, "id", "username")
```

### 3.2.查询一行数据

使用One函数返回一条记录

```go
var user User

// 等价sql: select * from users where id = 1 limit 1
err := o.QueryTable("users").Filter("id", 1).One(&user)

if err == orm.ErrNoRows {
    fmt.Printf("查询不到数据")
}
```

One也可以返回指定字段值, 例: One(&user, "id", "username")

### 3.3. Group By & Order BY

这里介绍一个包含group by, order by语句的例子

```go
// 创建orm对象
o := orm.NewOrm()

// 获取 QuerySeter 对象，并设置表名orders
qs := o.QueryTable("users")

// 定义保存查询结果的变量
var users []User

// 使用QuerySeter 对象构造查询条件，并执行查询。
// 等价sql: select * from users where id > 1 and id < 100 group by city order by init_time desc limit 10
num, err := qs.Filter("Id__gt", 1).
		Filter("Id__lt", 100).
		GroupBy("City").   // 根据city字段分组
		OrderBy("-InitTime").   // order by字段名前面的减号 - , 代表倒序。
		Limit(10). // 限制返回行数
		All(&users)

if err != nil {
	panic(err)
}
fmt.Println("结果行数:", num)
```

### 3.4. Count统计总数

sql语句中的count语句的例子

```go
// 这里可以忽略错误。
num, _ := o.QueryTable("users").Filter("Id__gt", 1).Filter("Id__lt", 100).Count()

// 等价sql: select count(*) from users where id > 1 and id < 100

fmt.Printf("总数: %s", num)
```

## 4.更新数据

使用QuerySeter更新数据，可以根据复杂的查询条件更新数据, 用法组织好查询条件后调用Update函数即可。

例子:

```go
// Update参数，使用的是orm.Params对象，这是一个map[string]interface{}类型, 用于指定我们要更新的数据
num, err := o.QueryTable("users").Filter("Id__gt", 1).Filter("Id__lt", 100).Update(orm.Params{
    "City": "深圳",
    "Password": "123456",
})

// 等价sql: update users set city = '深圳', password = '123456' where id > 1 and id < 100

fmt.Printf("影响行数: %s, %s", num, err)
```

## 5,删除数据

组织好查询条件后，调用Delete函数即可。

```go
num, err := o.QueryTable("users").Filter("Id__gt", 1).Filter("Id__lt", 100).Delete()

// 等价sql: delete from users where id > 1 and id < 100

fmt.Printf("影响行数: %s, %s", num, err)
```

# orm如何执行SQL查询

beego orm包除了支持model查询的方式，也支持直接编写sql语句的方式查询数据。

sql原生查询有如下特点:

- 使用 Raw SQL 查询，无需使用 ORM 表定义
- 多数据库，都可直接使用占位符号 ?，自动转换
- 查询时的参数，支持使用 Model Struct 和 Slice, Array

## 1.原生sql查询

在遇到比较复杂的查询的时候，使用sql语句更加灵活和直观，也比较容易把控sql查询的性能。

## 1.1. 执行插入、更新、删除SQL语句

执行insert、update、delete语句，需要使用Exec函数，执行后返回 sql.Result 对象，通过sql.Result对象我们可以查询最新插入的自增ID，影响行数。

例子:

```go
// 创建orm对象
o := orm.NewOrm()

// insert
// 使用Raw函数设置sql语句和参数
res, err := o.Raw("insert into users(username, password) values(?, ?)", "tizi365", "123456").Exec()

// 插入数据的自增id
id := res.LastInsertId()

// update
res, err := o.Raw("update users set password=? where username=?", "654321", "tizi365").Exec()

// 获取更新数据影响的行数
rows := res.RowsAffected()

// delete
o.Raw("delete from users where username=?", "tizi365").Exec()
```

## 1.2. 查询语句

查询数据主要通过QueryRow和QueryRows两个函数，分别对应查询一条数据还是多条数据，这两个函数都支持将查询结果保存到struct中.

### 1.2.1. 查询一行数据

```go
type User struct {
    Id       int
    Username string
}

var user User
err := o.Raw("SELECT id, username FROM users WHERE id = ?", 1).QueryRow(&user)
```

### 1.2.2. 查询多行数据

```go
type User struct {
    Id       int
    UserName string
}

var users []User

num, err := o.Raw("SELECT id, username FROM users WHERE id > ? and id < ?", 1, 100).QueryRows(&users)

if err == nil {
    fmt.Println("查询总数: ", num)
}
```

## 2.QueryBuilder sql生成工具

除了上面直接手写sql语句之外，beego orm也为我们提供了一个工具QueryBuilder对象，可以用来生成sql语句.

例子:

```go
// 定义保存用户信息的struct
type User struct {
	Id int
	Username string
	Password string
}

// 定义保存结果的数组变量
var users []User

// 获取 QueryBuilder 对象. 需要指定数据库驱动参数。
// 第二个返回值是错误对象，在这里略过
qb, _ := orm.NewQueryBuilder("mysql")

// 组织sql语句, 跟手写sql语句很像，区别就是sql语句的关键词都变成函数了
qb.Select("id", "username", "password").
	From("users").
	Where("id > ?").
	And("id < ?").
	Or("init_time > ?").
	OrderBy("init_time").Desc().
	Limit(10)

// 生成SQL语句
sql := qb.String()
// 生成这样的sql语句 SELECT id, username, password FROM users WHERE id > ? AND id < ? OR init_time > ? ORDER BY init_time DESC LIMIT 10

// 执行SQL
o := orm.NewOrm()
// 上面sql有三个参数(问号)，这里传入三个参数。
o.Raw(sql, 1, 100, "2019-06-20 11:10:00").QueryRows(&users)
```

> 提示： 使用QueryBuilder生成sql语句还是直接手写sql，这个就看个人喜好了。

# orm数据库事务处理

通常在一些订单交易业务都会涉及多个表的更新/插入操作，这个时候就需要数据库事务处理了，下面介绍beego orm如何处理mysql事务。

```go
// 创建orm对象
o := orm.NewOrm()

//  开始事务
o.Begin()

// 开始执行各种sql语句，更新数据库，这里可以使用beego orm支持任何一种方式操作数据库

// 例如,更新订单状态
_, err1 := o.QueryTable("orders").Filter("Id", 1001).Update(orm.Params{
    "Status": "SUCCESS",
})

// 给用户加积分
_, err2 := o.Raw("update users set points = points + ? where username=?", "tizi365", 100).Exec()

// 检测事务执行状态
if err1 != nil || err2 != nil {
    // 如果执行失败，回滚事务
    o.Rollback()
} else {
    // 任务执行成功，提交事务
    o.Commit()
}
```

# 视图

# 模板入门教程

beego 的视图(view)模板引擎是基于Go原生的模板库（html/template）进行开发的，因此在开始编写view模板代码之前需要先学习下Go内置模板引擎的语法。

> 提示: 如果还不了解Go内置模板引擎(html/template)的模板语法，[可以点击这里学习下Go内置模板引擎教程](https://www.tizi365.com/archives/85.html)

beego模板，默认支持 tpl 和 html 的后缀名。

## 1.基础例子

下面看个视图模板的例子。
模板文件: views/user/index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>用户个人信息:</h1>
<p>
    {{ if ne .user nil}}
        用户名: {{.user.Username}} <br/>
        注册时间: {{.user.InitTime}}
    {{else}}
        用户不存在!
    {{end}}}
</p>
</body>
</html>
```

下面看控制器如何渲染这个模板文件。

```go
// 处理get请求
func (this *UserController) Get() {
    // 初始化，模板渲染需要的数据
	user := &User{1, "tizi365", time.Now()}
	
	// 通过Data， 将参数传入模板,  Data是map类型支持任意类型数据
	this.Data["user"] = user
	
	// 设置我们要渲染的模板路径， 也就是views目录下面的相对路径
	// 如果你不设置TplName，那么beego就按照 <控制器名字>/<方法名>.tpl 这种格式去查找模板文件。
	this.TplName = "user/index.html"
	
	// 如果你关闭了自动渲染，则需要手动调用渲染函数, beego 默认是开启自动渲染的
	// this.Render()
}
```

> 提示：在app.conf配置文件中配置AutoRender参数为true或者false,表示是否开启自动渲染。

## 2.模板标签冲突

默认情况，模板引擎使用 **{{ 模板表达式 }}** 作为模板标签，如果我们前端开发使用的是Vue、angular之类的框架，这些前端框架也是使用 **{{ 模板表达式 }}** 作为模板标签，这样就造成冲突了。

我们可以通过修改Go模板引擎的默认标签解决模板标签冲突问题。

例子:

```go
// 修改Go的模板标签
beego.TemplateLeft = "<<<"
beego.TemplateRight = ">>>"
```

修改后的模板表达式:

```go
<<<.user.username>>>
```

你可以改成你喜欢的样式。

# 模板函数

这里介绍下beego默认新增加的模板函数，Go内置模板引擎也自带了一些模板函数。

> 提示：点击连接了解[Go html/template内置模板函数](https://www.tizi365.com/archives/96.html)。

## 1.beego内置模板函数

| 函数名      | 说明                                                         | 例子                                               |
| ----------- | ------------------------------------------------------------ | -------------------------------------------------- |
| dateformat  | 实现了时间的格式化，返回字符串                               | {{dateformat .Time "2006-01-02T15:04:05Z07:00"}}。 |
| date        | 类似php的date函数，用于格式化时间                            | {{date .Time "Y-m-d H:i:s"}}                       |
| compare     | 实现了比较两个对象的比较，如果相同返回 true，否者 false      | {{compare .A .B}}                                  |
| substr      | 实现了字符串的截取                                           | {{substr .Str 0 20}}                               |
| html2str    | 实现了把 html 转化为字符串，剔除一些 script、css 之类的元素  | {{html2str .Htmlinfo}}                             |
| str2html    | 实现了把相应的字符串当作 HTML 来输出，不转义                 | {{str2html .Strhtml}}                              |
| htmlquote   | 实现了基本的 html 字符转义                                   | {{htmlquote .content}}                             |
| htmlunquote | 实现了基本的反转移字符                                       | {{htmlunquote .content}}                           |
| renderform  | 根据 StructTag 直接生成对应的表单                            | {{&structData \| renderform}}                      |
| assets_js   | 为 js 文件生成一个 <script> 标签                             | {{assets_js srcPath}}                              |
| assets_css  | 为 css 文件生成一个 <link> 标签                              | {{assets_css srcPath}}                             |
| config      | 获取 AppConfig 的值, 用于读取配置文件信息， 可选的 configType 有 String, Bool, Int, Int64, Float, DIY | {{config configType configKey defaultValue}}       |
| urlfor      | 获取控制器方法的 URL                                         | {{urlfor "UserController.Get"}}                    |

## 2.自定义模板函数

除了使用beego提供的默认模板函数，我们也可以定义新的模板函数，下面是beego对html/template封装后定义模板函数的例子:

```go
// 定义模板函数, 自动在字符串后面加上标题
func demo(in string)(out string){
    out = in + " - 欢迎访问梯子教程"
    return
}

// 注册模板函数
beego.AddFuncMap("helloFunc",demo)
```

下面是调用自定义模板函数例子:

```go
{{.title | helloFunc}}
```

# 静态资源路径设置

我们在使用beego开发项目的时候，除了html模板之外，往往还存在js/css/jpg之类的静态资源文件，beego如何处理这些静态文件呢？

通过[快速入门教程](https://www.tizi365.com/archives/104.html)的例子，我们知道beego默认静态资源都是保存在static目录，访问静态资源的url是 **[http://域名/static/资源路径名](http://xn--eqrt2g/static/资源路径名)** 。

下面例子介绍如何自定义静态资源路径和访问url

主要通过beego.SetStaticPath函数设置静态资源路由和目录

```go
// 通过 /images/资源路径  可以访问static/images目录的内容
// 例: /images/user/1.jpg 实际访问的是 static/images/user/1.jpg 
beego.SetStaticPath("/images","static/images")

// 通过 /css/资源路径  可以访问static/css目录的内容
beego.SetStaticPath("/css","static/css")

// 通过 /js/资源路径  可以访问static/js目录的内容
beego.SetStaticPath("/js","static/js")
```

> 提示: 如果静态资源文件不存在，则返回404错误.

# 应用专题

# session处理

本章介绍beego的内置session模块， 通常session实现机制都是在客户端放一个session ID (cookie)，然后服务端存储一份session数据与之对应，那么服务端的session数据存储在什么地方，在beego的设计中可以自由配置。

目前session模块支持的常用的存储引擎如下:

- memory
- cookie
- file
- mysql
- redis

> 提示：用户也可以自定义自己喜欢的存储引擎

## 1.session基本配置

> 提示：下文提到的配置，在app.conf配置文件中加入面配置，然后重启beego程序即可生效。

打开session，这个配置是必须的，否则beego默认不会开启session

```go
sessionon = true
```

设置session id的名字，这个通常都是保存在客户端cookie里面

```go
sessionname = "beegosessionID"
```

设置 Session 过期的时间, 默认3600秒

```go
sessiongcmaxlifetime = 3600
```

设置session id的过期时间, 因为session id是保存在cookie中的。

```go
SessionCookieLifeTime = 3600
```

## 2.session读写例子

下面是在控制器函数中操作session的例子

```go
// 下面是个简单计数器的例子，通过session的count字段累计访问量
func (this *MainController) Get() {
    // 读取session数据
    v := this.GetSession("count")
    if v == nil {
        // 写入session数据
        this.SetSession("count", int(1))
        this.Data["num"] = 0
    } else {
        // 写入session数据
        this.SetSession("count", v.(int)+1)
        this.Data["num"] = v.(int)
    }
    this.TplName = "user/index.html"
}
```

session 数据的读写函数如下：

- SetSession(name string, value interface{}) - 设置session值
- GetSession(name string) interface{} - 读取session值
- DelSession(name string) - 删除指定session值
- SessionRegenerateID() - 生成新的session id
- DestroySession() - 销毁session

## 3.配置session的存储引擎

本节介绍Session存储引擎，默认是 memory, 也就是session数据默认保存在运行beego程序的机器内存中，如果是使用默认配置可以跳过本节内容。

下面分别介绍常用的session存储引擎配置方式。

### 3.1. session数据保存到文件中

```go
# 设置session保存到文件中
sessionprovider = "file"

# session数据保存目录
sessionproviderconfig = "./data/session"
```

### 3.2. session数据保存到redis中

将session数据保存到redis中，需要先安装redis驱动，然后在main.go文件中导入redis驱动。

配置:

```go
# 设置session存储引擎
sessionprovider = "redis"

# redis存储引擎配置
# redis配置格式: redis地址,redis连接池最大连接数,redis密码
# redis连接池和redis密码配置，没有保持为空，例子: 127.0.0.1:6379
sessionproviderconfig = "127.0.0.1:6379,1000,123456"
```

安装redis驱动:

```go
go get github.com/astaxie/beego/session/redis
```

在main.go入口文件，导入redis驱动

```go
import _ "github.com/astaxie/beego/session/redis"
```

### 3.3. session数据保存到mysql中

将session数据保存到mysql中，需要先安装mysql驱动，然后在main.go文件中导入mysql驱动。

配置:

```go
# 设置session存储引擎
sessionprovider = "mysql"

# mysql存储引擎配置
sessionproviderconfig = "root:123456@tcp(localhost:3306)/tizi365?charset=utf8"
```

> 提示：mysql存储引擎配置使用的是mysql dsn格式，如果不熟悉可以参考[数据库设置章节](https://www.tizi365.com/archives/122.html)。

安装mysql驱动:

```go
go get github.com/astaxie/beego/session/mysql
```

在main.go入口文件，导入mysql驱动

```go
import _ "github.com/astaxie/beego/session/mysql"
```

# 日志处理

beego设计了一个专门处理日志的库，方便我在项目中打印各种错误日志，调试日志，使用日志库需要先安装日志库。

## 1.安装日志库

```go
go get github.com/astaxie/beego/logs
```

## 2.导入包

```go
import (
    "github.com/astaxie/beego/logs"
)
```

## 3.日志配置

### 3.1. 设置日志级别

```go
// debug级别
logs.SetLevel(logs.LevelDebug)
```

下面是常用的日志级别： 由高到底，高于当前日志级别的日志不展示。

- LevelDebug - 对应数字 7
- LevelInfo - 对应数字 6
- LevelWarn - 对应数字 4
- LevelError - 对应数字 3

### 3.2. 将日志输出到控制台(console)

如果想将日志直接输出到console，则设置

```go
logs.SetLogger("console")
```

### 3.3. 将日志输出到文件

日志输出到文件的配置

```go
logs.SetLogger(logs.AdapterFile, `{"filename":"app.log", "level":6}`)
```

将日志输出到文件，详细参数主要通过SetLogger的第二个参数配置，这是一个json格式的配置。

详细配置：

| 参数名   | 说明                                               |
| -------- | -------------------------------------------------- |
| filename | 日志文件名                                         |
| maxlines | 每个文件保存的最大行数，默认值 1000000             |
| maxsize  | 每个文件保存的最大尺寸，默认值是 1 << 28, //256 MB |
| daily    | 是否按照每天 logrotate，默认是 true                |
| maxdays  | 文件最多保存多少天，默认保存 7 天                  |
| rotate   | 是否开启 logrotate，默认是 true                    |
| level    | 日志保存的时候的级别，默认是 Trace 级别            |
| perm     | 日志文件权限                                       |

### 3.4 将日志输出到阿里云日志服务

如果使用阿里云的服务器的话，可以选择将日志输出到阿里云的日志服务。

> 提示：新版本的日志库才支持阿里云日志服务，留意自己使用的版本

配置:

```go
logs.SetLogger(logs.AdapterAliLS, `{"project":"tizi365", "endpoint":"cn-hangzhou.log.aliyuncs.com","key_id":"IjihsgaiiiJ", "key_secret":"SADIJAYhh", "log_store":"demo"}`)
```

参数说明：

| 参数名         | 说明               |
| -------------- | ------------------ |
| **project**    | 日志服务项目名     |
| **endpoint**   | 日志服务地址       |
| **key_id**     | 阿里云accessKeyId  |
| **key_secret** | 阿里云accessSecret |
| **log_store**  | 日志库             |

## 4.打印日志的例子

```go
// 日志打印到console
logs.SetLogger("console")

// 设置日志级别
logs.SetLevel(logs.LevelDebug)

// 输出文件名和行号
logs.EnableFuncCallDepth(true)
	
// 设置日志前缀
logs.SetPrefix("tizi365")

// 下面分别调用不同的日志级别打印日志
logs.Debug("这是一条debug日志, 后面是参数 ", 2019,2018)
logs.Info("携带参数1: %s, 参数2: %d", "tizi365", 2019)
logs.Warn("可以直接打印map类型数据 ", map[string]int{"key": 2019})
logs.Error("参数1", "参数2", "后面可以加入任意参数")
```

> 提示：你也可以使用beego.Info(),  beego.Debug(), beego.Error() 打印日志，这些函数其实是对logs进行封装了，跟logs的用法一致。  

输出日志:

```go
2019/06/30 18:38:23.075 [D] [main.go:29] tizi365 这是一条debug日志, 后面是参数  2019 2018
2019/06/30 18:38:23.149 [I] [main.go:29] tizi365 携带参数1: tizi365, 参数2: 2019
2019/06/30 18:38:23.149 [W] [main.go:29] tizi365 可以直接打印map类型数据  map[key:2019]
2019/06/30 18:38:23.149 [E] [main.go:29] tizi365 参数1 参数2 后面可以加入任意参数
```

> 提示：在实际项目中，建议在main.go入口文件，统一对日志库进行配置。

# 错误处理

在web开发的中时候，如果遇到错误，例如: 404, 500错误等等，我们一般都会展示一个错误页面提示用户，beego默认提供了一些内置的错误页面，本章主要介绍如使用错误页面和定制错误页面。

## 1.默认错误处理

beego 框架默认支持 401、403、404、500、503 这几种错误的处理。

如果要跳转到错误页面，结束当前执行流程主要通过控制器的Abort函数实现。

例子:

```go
func (this *MainController) Get() {
    // 调用Abort函数终止执行，参数是错误类型
    this.Abort("500")
    
    // 其他处理逻辑
    // .....
    
    this.TplName = "index.tpl"
}
```

默认情况，调用Abort会展示beego框架默认的错误页面。

![img](https://www.tizi365.com/wp-content/uploads/2019/06/beego-500.png)

## 2.自定义错误处理

除了上面那几种错误类型，我们也可以自定义错误类型，自定义个性化的错误页面。

自定义错误处理步骤：

1. 定义错误控制器
2. 注册错误控制器

### 2.1. 定义错误控制器

```go
package controllers

import (
	"fmt"
	"github.com/astaxie/beego"
)

// 定义错误控制器
type ErrorController struct {
	beego.Controller
}

// 定义404错误, 调用例子: this.Abort("404")
func (this *ErrorController) Error404() {
    // 模板参数
	this.Data["content"] = "页面不见了"
	
	// 自定义404错误页面模板
	this.TplName = "404.tpl"
}

// 定义500错误, 调用例子: this.Abort("500")
func (this *ErrorController) Error500() {
	this.Data["content"] = "服务跑了"
	this.TplName = "500.tpl"
}


// 定义db错误， 调用例子: this.Abort("Db")
func (this *ErrorController) ErrorDb() {
	this.Data["content"] = "数据库挂逼了"
	this.TplName = "dberror.tpl"
}
```

> 提示: 自定义错误的函数名格式为： ErrorXXX , XXX就是我们要定义的错误类型，展示错误则调用this.Abort("XXX")

### 2.2. 注册错误控制器

自定义的错误控制器需要在main.go入口文件，向beego框架注册。

```go
package main

import (
    _ "btest/routers"
    "btest/controllers"

    "github.com/astaxie/beego"
)

func main() {
    // 注册错误控制器
    beego.ErrorController(&controllers.ErrorController{})
    beego.Run()
}
```

# 文件上传和下载

本章主要介绍beego如何处理文件的上传和下载。

## 1.beego处理文件上传

Beego 控制器提供了两个很方便的函数来处理文件上传：

- GetFile(key string) (multipart.File, *multipart.FileHeader, error)
  主要用于读取表单中的文件信息，可以根据这些信息来处理文件上传、过滤、保存文件等。
- SaveToFile(fromfile, tofile string) error
  这个函数就是用于实现快速保存文件到本地路径

例子:

表单

```html
<form enctype="multipart/form-data" method="post">
    <input type="file" name="filename" />
    <input type="submit">
</form>
```

> 提示：文件上传，表单<form>记得加上enctype="multipart/form-data"属性，否则浏览器不会上传文件。

处理文件上传代码

```go
func (this *UserController) Post() {
    // 读取文件信息
    f, h, err := this.GetFile("filename")
    
    if err != nil {
        log.Fatal("读取文件错误", err)
    }
    
    // 延迟关闭文件
    defer f.Close()
    
    // 保存文件, 本地文件路径static/upload/上传文件名
    // 需要提前创建好static/upload目录
    this.SaveToFile("filename", "static/upload/" + h.Filename)
}
```

如果你不想将文件保存到本地路径，想直接读取文件内容进行处理。

```go
func (this *UserController) Post() {
    // 读取文件信息
    f, h, err := this.GetFile("filename")
    
    if err != nil {
        log.Fatal("读取文件错误", err)
    }
    
    // 延迟关闭文件
    defer f.Close()
    
    // 读取上传文件内容, data就是文件的内容
    // ioutil.ReadAll返回[]byte类型数据
    data, err := ioutil.ReadAll(f)
}
```

## 2.beego处理文件下载

如果你想实现动态处理文件下载，例如：在文件下载的时候验证下用户的权限，这种情况就不能直接返回一个静态地址给用户。

例子:

```go
func (this *FileController) Get() {
    // 业务逻辑处理，例如先检测用户权限

    // 下载服务器上当前目录/data/file.zip文件， 下载后的文件名为:压缩包1.zip
    this.Ctx.Output.Download("data/file.zip", "压缩包1.zip")
}
```

# 项目部署与热更新

本章主要介绍beego项目的部署和热更新（又叫平滑部署、平滑更新等等）

## 1.beego项目部署

一般服务器都是linux，这里主要介绍linux系统的项目部署。

### 1.1.项目打包

之前介绍过bee工具， 在项目根目录执行下面命令完成项目打包。

```go
bee pack
```

打包完成后当前目录得到一个tar.gz后缀的压缩包。

### 1.2.独立部署

独立部署就是直接将上面得到的压缩包，上传到服务器，解压缩后直接运行go程序。

```go
# 先进入项目目录
cd appdir

# 在后台执行beego程序
nohup ./beepkg &
```

## 2.beego热更新

热更新指的是在不中断服务的情况下，完成程序升级。beego项目默认已经实现了热更新。

下面介绍beego如何实现热更新。

首先在app.conf配置文件中打开热更新配置。

```go
Graceful = true
```

假设目前老版本的程序正在运行，进程ID是1880。

现在将新版本的beego程序压缩包上传到服务器，解压缩，直接覆盖老的文件。

下面是触发beego程序热更新的命令：

```go
kill -HUP 进程ID
```

上面这个命令的意思就是给指定进程发送一个HUB信号，beego程序接收到这个信号后就开始处理热更新操作。

因为我们老版本的进程ID是1880, 因此命令是：

```go
kill -HUP 1880
```

执行命令就可以完成热更新操作。

