### Go语言基本语法



#### 设置 GOPATH 环境变量

开始写 go 项目代码之前，需要我们先配置好环境变量。编辑 ~/.bash_profile（在终端中运行 `vi ~/.bash_profile` 即可）来添加下面这行代码（如果你找不到 .bash_profile，那自己创建一个就可以了）

export GOPATH=$HOME/go

保存然后退出你的编辑器。然后在终端中运行下面命令

source ~/.bash_profile

> 提示：$HOME 是每个电脑下的用户主目录，每个电脑可能不同，可以在终端运行 echo $HOME 获取

GOROOT 也就是 Go 开发包的安装目录默认是在 /usr/local/go，如果没有，可以在 bash_profile 文件中设置。

export GOROOT=/usr/local/go

然后保存并退出编辑器，运行 `source ~/.bash_profile `命令即可。



#### 短变量声明并初始化

var 的变量声明还有一种更为精简的写法，例如：

```
hp := 100
```

这是Go语言的推导声明写法，编译器会自动根据右值类型推断出左值的对应类型。

> 注意：由于使用了`:=`，而不是赋值的`=`，因此推导声明写法的左值变量必须是没有定义过的变量。若定义过，将会发生编译错误。

如果 hp 已经被声明过，但依然使用`:=`时编译器会报错，代码如下：

```
// 声明 hp 变量var hp int// 再次声明并赋值hp := 10
```

编译报错如下：

no new variables on left side of :=

意思是，在“:=”的左边没有新变量出现，意思就是“:=”的左边变量已经被声明了。

 短变量声明的形式在开发中的例子较多，比如：

```
conn, err := net.Dial("tcp","127.0.0.1:8080")
```

net.Dial 提供按指定协议和地址发起网络连接，这个函数有两个返回值，一个是连接对象（conn），一个是错误对象（err）。如果是标准格式将会变成：

```
var conn net.Connvar err errorconn, err = net.Dial("tcp", "127.0.0.1:8080")
```

因此，短变量声明并初始化的格式在开发中使用比较普遍。

 注意：在多个短变量声明和赋值中，至少有一个新声明的变量出现在左值中，即便其他变量名可能是重复声明的，编译器也不会报错，代码如下：

```
conn, err := net.Dial("tcp", "127.0.0.1:8080")conn2, err := net.Dial("tcp", "127.0.0.1:8080")
```

上面的代码片段，编译器不会报 err 重复定义。



#### 匿名变量

匿名变量的特点是一个下画线“_”，“_”本身就是一个特殊的标识符，被称为空白标识符。它可以像其他标识符那样用于变量的声明或赋值（任何类型都可以赋值给它），但任何赋给这个标识符的值都将被抛弃，因此这些值不能在后续的代码中使用，也不可以使用这个标识符作为变量对其它变量进行赋值或运算。使用匿名变量时，只需要在变量声明的地方使用下画线替换即可。例如：

```go
func GetData() (int, int) {
    return 100, 200
}
func main(){
    a, _ := GetData()
    _, b := GetData()
    fmt.Println(a, b)
}
```

代码运行结果：

```
100 200
```

GetData() 是一个函数，拥有两个整型返回值。每次调用将会返回 100 和 200 两个数值。

 代码说明如下：

- 第 5 行只需要获取第一个返回值，所以将第二个返回值的变量设为下画线（匿名变量）。
- 第 6 行将第一个返回值的变量设为匿名变量。



#### 使用指针修改值

通过指针不仅可以取值，也可以修改值。

 前面已经演示了使用多重赋值的方法进行数值交换，使用指针同样可以进行数值交换，代码如下：

```
package main

import "fmt"

// 交换函数
func swap(a, b *int) {
    // 取a指针的值, 赋给临时变量t
    t := *a
    // 取b指针的值, 赋给a指针指向的变量
    *a = *b
    // 将a指针的值赋给b指针指向的变量
    *b = t
}

func main() {
 // 准备两个变量, 赋值1和2
   x, y := 1, 2
   // 交换变量值
   swap(&x, &y)
   // 输出变量值
   fmt.Println(x, y)
}
```

运行结果：

```
2 1
```

代码说明如下：

- 第 6 行，定义一个交换函数，参数为 a、b，类型都为 *int 指针类型。
- 第 9 行，取指针 a 的值，并把值赋给变量 t，t 此时是 int 类型。
- 第 12 行，取 b 的指针值，赋给指针 a 指向的变量。注意，此时`*a`的意思不是取 a 指针的值，而是“a 指向的变量”。
- 第 15 行，将 t 的值赋给指针 b 指向的变量。
- 第 21 行，准备 x、y 两个变量，分别赋值为 1 和 2，类型为 int。
- 第 24 行，取出 x 和 y 的地址作为参数传给 swap() 函数进行调用。
- 第 27 行，交换完毕时，输出 x 和 y 的值。



### golang router传递多个参数

```go
router.GET("/hello/:first_name/:last_name", Hello)

func Hello(w http.ResponseWriter, r *http.Request, ps httprouter.Params) {
    fmt.Fprintf(w, "hello, %s %s!
", ps.ByName("first_name"), ps.ByName("last_name"))
}
```



### golang 当import依赖同名的时候处理方式(hp 类似别名)

```go
hp "github.com/kirinlabs/HttpRequest"
```



### golang interface类型转string等其他类型

inter 是interface类型，转化为string类型是：

        str := inter .(string)


### golang router传参问题





### golang 发送http请求时设置header

```go
package main
import (
    "fmt"
    "io/ioutil"
    "net/http"                                                                                                                                                     
    "os"
    "encoding/json"
)

func main() { //生成client 参数为默认
    client := &http.Client{}
    //生成要访问的url
    url := "http://somesite/somepath/"
    //提交请求
    reqest, err := http.NewRequest("GET", url, nil)

    //增加header选项
    reqest.Header.Add("Cookie", "xxxxxx")
    reqest.Header.Add("User-Agent", "xxx")
    reqest.Header.Add("X-Requested-With", "xxxx")

    if err != nil {
        panic(err)
    }   
    //处理返回结果
    response, _ := client.Do(reqest)
    defer response.Body.Close()
```



### golang 转换slice/array 变成xxx,yyy,zzz 【带逗号的字符串】

```go
package main
 
import (
	"fmt"
	"strings"
)
 
func main() {
	age := []int{1, 3, 5}
	name := []string{"dongTech"}
 
	fmt.Println(convert(age))
	fmt.Println(convert(name))
}
 
//[a] -> a -> a
//[a b c] -> a b c -> a,b,c
func convert(array interface{}) string {
	return strings.Replace(strings.Trim(fmt.Sprint(array), "[]"), " ", ",", -1)
}
```



### golang   gjson解析json

```go
package main
 
import "github.com/tidwall/gjson"
 
const json = `{"name":{"first":"Janet","last":"Prichard"},"age":47}`
 
func main() {
    value := gjson.Get(json, "name.last")
    println(value.String())
}
```



### golang基础:在Go中打印带有双引号的字符串

```go
package main

import "fmt"

func main() {
  var lang = "Golang"
  fmt.Printf("%q", lang)
}

结果："Golang"
```



### golang 获取get/post请求中的请求头和表单数据

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "这是请求中的路径：", r.URL.Path)
    fmt.Fprintln(w, "这是请求中的路径?后面的参数：", r.URL.RawQuery)
    fmt.Fprintln(w, "这是请求中的User-Agent信息：", r.Header["User-Agent"])
    fmt.Fprintln(w, "这是请求中的User-Agent信息：", r.Header.Get("User-Agent"))

    // 获取请求体内容的长度
    // len := r.ContentLength
    // body := make([]byte, len)
    // r.Body.Read(body)
    // fmt.Fprintln(w, "请求体中的内容是：", string(body))

    // 解析表单，在调用r.Form r.PostForm之前执行
    r.ParseForm()
    // fmt.Fprintln(w, "表单信息：", r.Form)
    fmt.Fprintln(w, "表单信息：", r.PostForm)

    // fmt.Fprintln(w, "用户名：", r.FormValue("username"))
    // fmt.Fprintln(w, "密码：", r.FormValue("password"))
    fmt.Fprintln(w, "密码：", r.PostFormValue("password"))

}

func main() {
    http.HandleFunc("/hello", handler)
    http.ListenAndServe(":8080", nil)

}
```



### golang 参数及返回值

参数一指定数据类型为int
参数二 (...interface{}) 可传任何多个类型的参数
返回值：单个返回值直接指定数据类型可以不使用 ()，多个返回值需使用()。各返回值之间使用逗号分隔

```go
func main() {
    demo.Params(10, 20, "golang", true)
}

func Params(id int, params ...interface{}) (error, error) {
    fmt.Println(id)
    fmt.Println(params[0])
    fmt.Println(params[1])
    fmt.Println(params[2])
    for key, val := range params {
        fmt.Println("key", key)
        fmt.Println("val", val, reflect.TypeOf(val))
    }
    return nil, errors.New("error")
}
```



### golang中的字符串拼接

```go
s1 := "字符串"
s2 := "拼接"
s3 := s1 + s2
fmt.Print(s3) //s3 = "打印字符串"
```



### golang - 数字转字符串

```go
package main

import (
    "strconv"
)

func toString(a interface{}) string {
    if v, p := a.(int); p {
        return strconv.Itoa(v)
    }
    if v, p := a.(int16); p {
        return strconv.Itoa(int(v))
    }
    if v, p := a.(int32); p {
        return strconv.Itoa(int(v))
    }
    if v, p := a.(uint); p {
        return strconv.Itoa(int(v))
    }
    if v, p := a.(float32); p {
        return strconv.FormatFloat(float64(v), 'f', -1, 32)
    }
    if v, p := a.(float64); p {
        return strconv.FormatFloat(v, 'f', -1, 32)
    }
    return "change to String error"
}
```





### golang  func方法名调用不到问题

```go
func函数名首字母小写  private。
func函数名首字母大写  public
```



### golang 关闭http请求

```go
if resp != nil {
		resp.Close()
}
```



### Beego ———— 从浏览器中获取string数据

#### 路由：

```go
beego.Router("/getstring",&controllers.Demo3Controller{},"Get:Getstring")
```

#### 例子：

```go
package controllers
 
import (
	"github.com/astaxie/beego"
	"fmt"
	"strings"
)
 
type Demo3Controller struct {
	beego.Controller
}
 
func (this *Demo3Controller)Getstring(){
 
	username := this.GetString("username")
	nickname := this.GetString("nickname")
	password := this.GetString("password")
	this.Ctx.WriteString(username+nickname+password)
}
```



### golang将go打包成exe

```go
go build -o mygo hello.go
```



## golang获取参数



### golang获取链接中的参数

```go
name := c.GetString("name")
```

### golang获取请求头的参数

```go
request
password := c.Ctx.Input.Header("password")
```

### golang获取body体中的参数

```go
var data map[string]interface{}
json.Unmarshal(c.Ctx.Input.RequestBody, &data)
name     := data["name"].(string)
password := data["password"].(string)
```



## golang类型转换

### Golang  interface{}转换成string

```go
var data map[string]interface{}
json.Unmarshal(c.Ctx.Input.RequestBody, &data)
name     := data["name"].(string)
password := data["password"].(string)
```

### golang interface类型转string等类型

```go
inter 是interface类型，转化为string类型是：
str := inter .(string)

转为其他类型也类似
```



### golang 获取Auth参数值

https://www.cnblogs.com/zdz8207/p/golang-learn-10.html

```go
 authString := base.Ctx.Input.Header("Authorization")
 beego.Debug("AuthString:", authString)
 
 kv := strings.Split(authString, " ")
 if len(kv) != 2 || kv[0] != "Bearer" {
     beego.Error("AuthString invalid:", authString)
     return nil, errInputData
 }
 tokenString := kv[1]
```



## Golang里实现Http服务器并解析header参数和表单参数

```go
package main

import (
	"fmt"
	"net/http"
	"strconv"
)

func main() {
	HttpStart(8088)
}

func HttpStart(port int) {
	http.HandleFunc("/hello", helloFunc)
	err := http.ListenAndServe(":"+strconv.Itoa(port), nil)
	if err != nil {
		fmt.Println("监听失败：", err.Error())
	}
}

func helloFunc(w http.ResponseWriter, r *http.Request) {
	fmt.Println("打印Header参数列表：")
	if len(r.Header) > 0 {
		for k, v := range r.Header {
			fmt.Printf("%s=%s\n", k, v[0])
		}
	}
	fmt.Println("打印Form参数列表：")
	r.ParseForm()
	if len(r.Form) > 0 {
		for k, v := range r.Form {
			fmt.Printf("%s=%s\n", k, v[0])
		}
	}
	//验证用户名密码，如果成功则header里返回session，失败则返回StatusUnauthorized状态码
	w.WriteHeader(http.StatusOK)
	if (r.Form.Get("user") == "admin") && (r.Form.Get("pass") == "888") {
		w.Write([]byte("hello,验证成功！"))
	} else {
		w.Write([]byte("hello,验证失败了！"))
	}
}
```

 ### 输出参数：

```json
运行后，在chrom浏览器里执行请求：http://127.0.0.1:8001/hello?user=admin&pass=888，服务端会打印参数列表如下：

打印Header参数列表：
Accept-Language=zh-CN,zh;q=0.9
Connection=keep-alive
Cache-Control=max-age=0
Upgrade-Insecure-Requests=1
User-Agent=Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.19 Safari/537.36
Accept=text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Accept-Encoding=gzip, deflate, br
打印Form参数列表：
user=admin
pass=888
```

并且会返回成功结果给客户端的，浏览器里运行结果为：

![QQ图片20180228235530.png](http://images.5bug.wang//2018/02/201802281420_5915.png)

如果浏览器里不是请求/hello则会报404，如果参数写其他的也会返回验证失败的结果！



### golang test测试

```go
package utils

import "testing"

func TestDoubleToSingleQuotation(t *testing.T) {
	payload := `{
		"ret": "200",
		"msg": "success",
		"data": [
		    {
			  "type": "UI",
			  "name": "operationalSecurity",
			  "metadata": {
				"resourceType": 1,
				"displayName": "运营防盗",
				"sort": "100",
				"content": "operationalSecurity",
				"contentMd5": "33016394cd1cddeaa33de24fa68035d1"
			  },
			  "client": "web_app",
			  "createdBy": "5e1c271c0c21f80040e5b3b0",
			  "createdAt": "2020-03-20T08:32:43.266Z",
			  "updatedAt": "2020-03-20T08:32:43.266Z",
			  "id": "5e747fabf5d6190039477e55"
		    },
		    {
			  "parent": "5e747fabf5d6190039477e55",
			  "type": "UI",
			  "name": "efencenew",
			  "metadata": {
				"resourceType": 1,
				"displayName": "电子围栏",
				"sort": "101",
				"content": "operationalSecurity:efence",
				"contentMd5": "025ac1a7531a4260e4df979a7f0065b1"
			  },
			  "client": "web_app",
			  "createdBy": "5e1c271c0c21f80040e5b3b0",
			  "createdAt": "2020-03-20T08:46:06.120Z",
			  "updatedAt": "2020-03-20T08:46:06.120Z",
			  "id": "5e7482cef5d6190039477e56"
		    } 
		]
	  }`

	res := DoubleToSingleQuotation(payload, "data.#.metadata.content")
	t.Logf("res: %s", res)
}

```

测试命令：

```shell
KEdeMac-mini:utils datahunter$ go test -v .
```

结果：

```shell
=== RUN   TestDoubleToSingleQuotation
    TestDoubleToSingleQuotation: iroot_context_test.go:47: res: 'operationalSecurity','operationalSecurity:efence'
--- PASS: TestDoubleToSingleQuotation (0.00s)
PASS
ok      common.dh.cn/utils      0.021s
```



### golang 如何判断err

```go
func WriteConfig(w io.Writer, conf *Config) error {
	buf, err := json.Marshal(conf)
	if err != nil {
		return fmt.Errorf("could not marshal config: %v", err)
	}
	if err := WriteAll(w, buf); err != nil {
		return fmt.Errorf("could not write config: %v", err)
	}
	return nil
}
```

