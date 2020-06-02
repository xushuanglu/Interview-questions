# Go编码规范指南

## 序言

看过很多方面的编码规范，可能每一家公司都有不同的规范，这份编码规范是写给我自己的，同时希望我们公司内部同事也能遵循这个规范来写Go代码。

如果你的代码没有办法找到下面的规范，那么就遵循标准库的规范，多阅读标准库的源码，标准库的代码可以说是我们写代码参考的标杆。

## 格式化规范

go默认已经有了gofmt工具，但是我们强烈建议使用goimport工具，这个在gofmt的基础上增加了自动删除和引入包.

```
go get golang.org/x/tools/cmd/goimports
```

不同的编辑器有不同的配置, sublime的配置教程：http://michaelwhatcott.com/gosublime-goimports/

LiteIDE默认已经支持了goimports，如果你的不支持请点击属性配置->golangfmt->勾选goimports

保存之前自动fmt你的代码。

## 行长约定

一行最长不超过80个字符，超过的请使用换行展示，尽量保持格式优雅。

## go vet

vet工具可以帮我们静态分析我们的源码存在的各种问题，例如多余的代码，提前return的逻辑，struct的tag是否符合标准等。

```
go get golang.org/x/tools/cmd/vet
```

使用如下：

```
go vet .
```

## package名字

保持package的名字和目录保持一致，尽量采取有意义的包名，简短，有意义，尽量和标准库不要冲突。

## import 规范

import在多行的情况下，goimports会自动帮你格式化，但是我们这里还是规范一下import的一些规范，如果你在一个文件里面引入了一个package，还是建议采用如下格式：

```
import (
    "fmt"
)
```

如果你的包引入了三种类型的包，**标准库包**，**程序内部包**，**第三方包**，建议采用如下方式进行组织你的包：

```
import (
    "encoding/json"
    "strings"

    "myproject/models"
    "myproject/controller"
    "myproject/utils"

    "github.com/astaxie/beego"
    "github.com/go-sql-driver/mysql"
)   
```

有顺序的引入包，不同的类型采用空格分离，第一种实标准库，第二是项目包，第三是第三方包。

在项目中不要使用相对路径引入包：

```
// 这是不好的导入
import “../net”

// 这是正确的做法
import “github.com/repo/proj/src/net”
```

## 变量申明

变量名采用驼峰标准，不要使用`_`来命名变量名，多个变量申明放在一起

```
var (
    Found bool
    count int
)
```

**在函数外部申明必须使用var,不要采用`:=`，容易踩到变量的作用域的问题。**

## 自定义类型的string循环问题

如果自定义的类型定义了String方法，那么在打印的时候会产生隐藏的一些bug

```
type MyInt int
func (m MyInt) String() string { 
    return fmt.Sprint(m)   //BUG:死循环
}

func(m MyInt) String() string { 
    return fmt.Sprint(int(m))   //这是安全的,因为我们内部进行了类型转换
}
```

## 避免返回命名的参数

如果你的函数很短小，少于10行代码，那么可以使用，不然请直接使用类型，因为如果使用命名变量很
容易引起隐藏的bug

```
func Foo(a int, b int) (string, ok){

}
```

当然如果是有多个相同类型的参数返回，那么命名参数可能更清晰：

```
func (f *Foo) Location() (float64, float64, error)
```

**下面的代码就更清晰了：**

```
// Location returns f's latitude and longitude.
// Negative values mean south and west, respectively.
func (f *Foo) Location() (lat, long float64, err error)
```

## 错误处理

错误处理的原则就是不能丢弃任何有返回err的调用，不要采用`_`丢弃，必须全部处理。接收到错误，要么返回err，要么实在不行就panic，或者使用log记录下来

### error 信息

error的信息不要采用大写字母，尽量保持你的错误简短，但是要足够表达你的错误的意思。

## 长句子打印或者调用，使用参数进行格式化分行

我们在调用`fmt.Sprint`或者`log.Sprint`之类的函数时，有时候会遇到很长的句子，我们需要在参数调用处进行多行分割：

下面是错误的方式：

```
log.Printf(“A long format string: %s %d %d %s”, myStringParameter, len(a),
    expected.Size, defrobnicate(“Anotherlongstringparameter”,
        expected.Growth.Nanoseconds() /1e6))
```

应该是如下的方式：

```
log.Printf( 
    “A long format string: %s %d %d %s”, 
    myStringParameter,
    len(a),
    expected.Size,
    defrobnicate(
        “Anotherlongstringparameter”,
        expected.Growth.Nanoseconds()/1e6, 
    ),
）   
```

## 注意闭包的调用

在循环中调用函数或者goroutine方法，一定要采用显示的变量调用，不要再闭包函数里面调用循环的参数

```
fori:=0;i<limit;i++{
    go func(){ DoSomething(i) }() //错误的做法
    go func(i int){ DoSomething(i) }(i)//正确的做法
￼}
```

http://golang.org/doc/articles/race_detector.html#Race_on_loop_counter

## 在逻辑处理中禁用panic

在main包中只有当实在不可运行的情况采用panic，例如文件无法打开，数据库无法连接导致程序无法
正常运行，但是对于其他的package对外的接口不能有panic，只能在包内采用。

强烈建议在main包中使用log.Fatal来记录错误，这样就可以由log来结束程序。

## 注释规范

注释可以帮我们很好的完成文档的工作，写得好的注释可以方便我们以后的维护。详细的如何写注释可以
参考：http://golang.org/doc/effective_go.html#commentary

### bug注释

针对代码中出现的bug，可以采用如下教程使用特殊的注释，在godocs可以做到注释高亮：

```
// BUG(astaxie):This divides by zero. 
var i float = 1/0
```

http://blog.golang.org/2011/03/godoc­documenting­go­code.html

## struct规范

### struct申明和初始化格式采用多行：

定义如下：

```
type User struct{
    Username  string
    Email     string
}
```

初始化如下：

```
u := User{
    Username: "astaxie",
    Email:    "astaxie@gmail.com",
}
```

### recieved是值类型还是指针类型

到底是采用值类型还是指针类型主要参考如下原则：

```
func(w Win) Tally(playerPlayer)int    //w不会有任何改变 
func(w *Win) Tally(playerPlayer)int    //w会改变数据
```

更多的请参考：https://code.google.com/p/go-wiki/wiki/CodeReviewComments#Receiver_Type

### 带mutex的struct必须是指针receivers

如果你定义的struct中带有mutex,那么你的receivers必须是指针

## ----------------------------------------------------------------



## Golang编码规范

### - gofmt

大部分的格式问题可以通过gofmt解决，gofmt自动格式化代码，保证所有的go代码与官方推荐的格式保持一致，于是所有格式有关问题，都以gofmt的结果为准。

### - 行长

一行最长不超过80个字符，超过的使用换行展示，尽量保持格式优雅。

### - 注释

在编码阶段应该同步写好变量、函数、包的注释，最后可以利用godoc导出文档。注释必须是完整的句子，句子的结尾应该用句号作为结尾（英文句号）。注释推荐用英文，可以在写代码过程中锻炼英文的阅读和书写能力。而且用英文不会出现各种编码的问题。
**每个包都应该有一个包注释，一个位于package子句之前的块注释或行注释。**包如果有多个go文件，只需要出现在一个go文件中即可。

```go
// ping包实现了常用的ping相关的函数
package ping
```

导出函数注释，第一条语句应该为一条概括语句，并且使用被声明的名字作为开头。

```go
// 求a和b的和，返回sum。
func Myfunction(sum int) (a, b int) {
```

### - 命名
  - 需要注释来补充的命名就不算是好命名。
  - 使用可搜索的名称：单字母名称和数字常量很难从一大堆文字中搜索出来。单字母名称仅适用于短方法中的本地变量，名称长短应与其作用域相对应。若变量或常量可能在代码中多处使用，则应赋其以便于搜索的名称。
  - 做有意义的区分：Product和ProductInfo和ProductData没有区别，NameString和Name没有区别，要区分名称，就要以读者能鉴别不同之处的方式来区分 。
  - 函数命名规则：驼峰式命名，名字可以长但是得把功能，必要的参数描述清楚，**函数名名应当是动词或动词短语，如postPayment、deletePage、save。**并依Javabean标准加上get、set、is前缀。例如：xxx + With + 需要的参数名 + And + 需要的参数名 + .....
  - 结构体命名规则：结构体名应该是名词或名词短语，如Custome、WikiPage、Account、AddressParser，避免使用Manager、Processor、Data、Info、这样的类名，类名不应当是动词。
  - 包名命名规则：包名应该为小写单词，不要使用下划线或者混合大小写。
  - 接口命名规则：单个函数的接口名以"er"作为后缀，如Reader,Writer。接口的实现则去掉“er”。



```csharp
type Reader interface {
        Read(p []byte) (n int, err error)
}
```

**两个函数的接口名综合两个函数名**

```csharp
type WriteFlusher interface {
    Write([]byte) (int, error)
    Flush() error
}
```

**三个以上函数的接口名，抽象这个接口的功能，类似于结构体名**

```csharp
type Car interface {
    Start([]byte)
    Stop() error
    Recover()
}
```

### - 常量

**常量均需使用全部大写字母组成，并使用下划线分词：**

```cpp
const APP_VER = "1.0"
```

***如果是枚举类型的常量，需要先创建相应类型：***

```go
type Scheme string

const (
    HTTP  Scheme = "http"
    HTTPS Scheme = "https"
)
```

**如果模块的功能较为复杂、常量名称容易混淆的情况下，为了更好地区分枚举类型，可以使用完整的前缀：**

```go
type PullRequestStatus int

const (
    PULL_REQUEST_STATUS_CONFLICT PullRequestStatus = iota
    PULL_REQUEST_STATUS_CHECKING
    PULL_REQUEST_STATUS_MERGEABLE
)
```

### - 变量

变量命名基本上遵循相应的英文表达或简写,在相对简单的环境（对象数量少、针对性强）中，可以将一些名称由完整单词简写为单个字母，例如：
\* user 可以简写为 u
\* userID 可以简写 uid
若变量类型为 bool 类型，则名称应以 Has, Is, Can 或 Allow 开头：

```csharp
var isExist bool
var hasConflict bool
var canManage bool
var allowGitHook bool
```

### - 变量命名惯例

**变量名称一般遵循驼峰法，但遇到特有名词时，需要遵循以下规则：**

```undefined
* 如果变量为私有，且特有名词为首个单词，则使用小写，如 apiClient
* 其它情况都应当使用该名词原有的写法，如 APIClient、repoID、UserID
* 错误示例：UrlArray，应该写成urlArray或者URLArray
```

下面列举了一些常见的特有名词：

```php
// A GonicMapper that contains a list of common initialisms taken from golang/lint
var LintGonicMapper = GonicMapper{
    "API":   true,
    "ASCII": true,
    "CPU":   true,
    "CSS":   true,
    "DNS":   true,
    "EOF":   true,
    "GUID":  true,
    "HTML":  true,
    "HTTP":  true,
    "HTTPS": true,
    "ID":    true,
    "IP":    true,
    "JSON":  true,
    "LHS":   true,
    "QPS":   true,
    "RAM":   true,
    "RHS":   true,
    "RPC":   true,
    "SLA":   true,
    "SMTP":  true,
    "SSH":   true,
    "TLS":   true,
    "TTL":   true,
    "UI":    true,
    "UID":   true,
    "UUID":  true,
    "URI":   true,
    "URL":   true,
    "UTF8":  true,
    "VM":    true,
    "XML":   true,
    "XSRF":  true,
    "XSS":   true,
}
```

### - struct规范

struct申明和初始化格式采用多行：

定义如下：

```cpp
type User struct{
    Username  string
    Email     string
}
```

初始化如下：

```go
u := User{
    Username: "test",
    Email:    "test@gmail.com",
}
```

- 控制结构

if
if接受初始化语句，约定如下方式建立局部变量

```go
if err := file.Chmod(0664); err != nil {
    return err
}
```

for
采用短声明建立局部变量

```go
sum := 0
for i := 0; i < 10; i++ {
    sum += i
}
```

return
**尽早return：一旦有错误发生，马上返回**

```go
f, err := os.Open(name)
if err != nil {
    return err
}
d, err := f.Stat()
if err != nil {
    f.Close()
    return err
}
codeUsing(f, d)
```

### - 错误处理
  - error作为函数的值返回,必须对error进行处理
  - 错误描述如果是英文必须为小写，不需要标点结尾
  - 采用独立的错误流进行处理

不要采用下面的处理错误写法

```go
    if err != nil {
        // error handling
    } else {
        // normal code
    }
```

采用下面的写法

```go
    if err != nil {
        // error handling
        return // or continue, etc.
    }
    // normal code
```

**使用函数的返回值时，则采用下面的方式**

```go
x, err := f()
if err != nil {
    // error handling
    return
}
// use x
```

### - panic

尽量不要使用panic，除非你知道你在做什么

### - import

对import的包进行分组管理，用换行符分割，而且标准库作为分组的第一组。如果你的包引入了三种类型的包，标准库包，程序内部包，第三方包，建议采用如下方式进行组织你的包

```go
package main

import (
    "fmt"
    "os"

    "kmg/a"
    "kmg/b"

    "code.google.com/a"
    "github.com/b"
)
```

**在项目中不要使用相对路径引入包：**

```swift
// 错误示例
import “../net”

// 正确的做法
import “github.com/repo/proj/src/net”
```

goimports会自动帮你格式化

### - 参数传递
  - 对于少量数据，不要传递指针
  - 对于大量数据的struct可以考虑使用指针
  - 传入参数是map，slice，chan不要传递指针，因为map，slice，chan是引用类型，不需要传递指针的指针
- 单元测试

单元测试文件名命名规范为 example_test.go
测试用例的函数名称必须以 Test 开头，例如：TestExample



## 如何写出优雅的 Golang 代码

链接：https://www.jianshu.com/p/596eaebd6e54



代码规范：使用辅助工具帮助我们在每次提交 PR 时自动化地对代码进行检查，减少工程师人工审查的工作量；

最佳实践

- 目录结构：遵循 Go 语言社区中被广泛达成共识的 [目录结构](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fgolang-standards%2Fproject-layout)，减少项目的沟通成本；
- 模块拆分：按照职责对不同的模块进行拆分，Go 语言的项目中也不应该出现 `model`、`controller` 这种违反语言顶层设计思路的包名；
- 显示与隐式：尽可能地消灭项目中的 `init` 函数，保证显式地进行方法的调用以及错误的处理；
- 面向接口：面向接口是 Go 语言鼓励的开发方式，也能够为我们写单元测试提供方便，我们应该遵循固定的模式对外提供功能；
  1. 使用大写的 `Service` 对外暴露方法；
  2. 使用小写的 `service` 实现接口中定义的方法；
  3. 通过 `func NewService(...) (Service, error)` 函数初始化 `Service` 接口；

单元测试：保证项目工程质量的最有效办法；

- 可测试：意味着面向接口编程以及减少单个函数中包含的逻辑，使用『小方法』；
- 组织方式：使用 Go 语言默认的 Test 框架、开源的 `suite` 或者 BDD 的风格对单元测试进行合理组织；
- Mock 方法：四种不同的单元测试 Mock 方法；
  - [gomock](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fgolang%2Fmock)：最标准的也是最被鼓励的方式；
  - [sqlmock](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2FDATA-DOG%2Fgo-sqlmock)：处理依赖的数据库；
  - [httpmock](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fjarcoal%2Fhttpmock)：处理依赖的 HTTP 请求；
  - [monkey](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fbouk%2Fmonkey)：万能的方法，但是只在万不得已时使用，类似的代码写起来非常冗长而且不直观；
- 断言：使用社区的 [testify](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fstretchr%2Ftestify) 快速验证方法的返回值；



### go代码规范链接：

[https://blog.csdn.net/winter_wu_1998/article/details/102926479](https://blog.csdn.net/winter_wu_1998/article/details/102926479)



## 无需任何代码即可学习Git和GitHub！



## 内容

- [谚语](https://github.com/cristaloleg/go-advice#go-proverbs)
- [围棋禅](https://github.com/cristaloleg/go-advice#the-zen-of-go)
- [码](https://github.com/cristaloleg/go-advice#code)
- [并发](https://github.com/cristaloleg/go-advice#concurrency)
- [性能](https://github.com/cristaloleg/go-advice#performance)
- [模组](https://github.com/cristaloleg/go-advice#modules)
- [建立](https://github.com/cristaloleg/go-advice#build)
- [测试中](https://github.com/cristaloleg/go-advice#testing)
- [工具类](https://github.com/cristaloleg/go-advice#tools)
- [杂项](https://github.com/cristaloleg/go-advice#misc)

### 谚语

- 不要通过共享内存进行通信，而要通过通信共享内存。
- 并发不是并行性。
- 渠道编排；互斥锁序列化。
- 接口越大，抽象性越弱。
- 使零值有用。
- `interface{}` 什么也没说。
- Gofmt的风格不是每个人的最爱，但gofmt是每个人的最爱。
- 稍微复制胜于一点依赖。
- Syscall必须始终使用构建标记来保护。
- Cgo必须始终使用build标签来保护。
- Cgo不是Go。
- 对于不安全的包装，无法保证。
- 清晰胜于聪明。
- 反思从未明确。
- 错误是价值。
- 不要仅仅检查错误，而要优雅地处理它们。
- 设计架构，命名组件，记录细节。
- 文档供用户使用。
- 不要惊慌

作者：Rob Pike查看更多：[https](https://go-proverbs.github.io/) : [//go-proverbs.github.io/](https://go-proverbs.github.io/)

### 围棋禅

- 每个包装实现一个目的
- 明确处理错误
- 早日返回，而不是深入巢穴
- 并发给调用者
- 在启动goroutine之前，请知道它何时会停止
- 避免包装级别状态
- 简单很重要
- 编写测试以锁定包API的行为
- 如果您认为速度缓慢，请先通过基准测试进行验证
- 节制是一种美德
- 可维护性计数

作者：Dave Cheney查看更多：[https](https://the-zen-of-go.netlify.com/) : [//the-zen-of-go.netlify.com/](https://the-zen-of-go.netlify.com/)

### 

#### 始终是`go fmt`您的代码。

社区使用官方的Go格式，不要重新发明轮子。

尝试减少代码熵。这将帮助所有人使代码易于阅读。

#### 多个if-else语句可以折叠到一个开关中

```
//不差，
if foo（）{
     // ... 
} 否则， 如果 bar  ==  baz {
     // ... 
} else {
     // ... 
} //

更好地切换 {
 case foo（）：
     // .. 。情况吧== 巴兹：
     // ... 默认：
     // ... 
}
```

#### 传递信号`chan struct{}`而不是`chan bool`。

当您看到`chan bool`结构中的定义时，有时不容易理解如何使用该值，例如：

```
输入 Service  struct {
     deleteCh  chan  bool  //这是什么意思？
}
```

但是，我们可以通过将其更改为`chan struct{}`明确表示的内容来使其更加清晰：我们不在乎值（始终为`struct{}`），我们在乎可能发生的事件，例如：

```
键入 Service  struct {
     deleteCh  chan  struct {} //好的，如果事件比删除一些东西的话。
}
```

#### 更喜欢`30 * time.Second`而不是`time.Duration(30) * time.Second`

您不需要将无类型的const包装在类型中，编译器会找出来。还喜欢将const移到第一位：

```
// BAD
delay := time.Second * 60 * 24 * 60

// VERY BAD
delay := 60 * time.Second * 60 * 24

// GOOD
delay := 24 * 60 * 60 * time.Second
```

#### Use `time.Duration` instead of `int64` + variable name

```
// BAD
var delayMillis int64 = 15000

// GOOD
var delay time.Duration = 15 * time.Second
```

#### Group `const` declarations by type and `var` by logic and/or type

```
// BAD
const (
    foo = 1
    bar = 2
    message = "warn message"
)

// MOSTLY BAD                                             
const foo = 1
const bar = 2
const message = "warn message"

// GOOD
const (
    foo = 1
    bar = 2
)

const message = "warn message"
```

This pattern works for `var` too.

-  every blocking or IO function call should be cancelable or at least timeoutable

-  

  implement

  ```
Stringer
  ```
  
  interface for integers const values

  - https://godoc.org/golang.org/x/tools/cmd/stringer

-  check your defer's error

```
  defer func() {
      err := ocp.Close()
      if err != nil {
          rerr = err
      }
  }()
```

-  don't use `checkErr` function which panics or does `os.Exit`

-  use panic only in very specific situations, you have to handle error

-  

  don't use alias for enums 'cause this breaks type safety

  - https://play.golang.org/p/MGbeDwtXN3

```
  package main
  type Status = int
  type Format = int // remove `=` to have type safety

  const A Status = 1
  const B Format = 1

  func main() {
	println(A == B)
  }
```

-  

  if you're going to omit returning params, do it explicitly

  - so prefer this `_ = f()` to this `f()`

-  the short form for slice initialization is `a := []T{}`

-  

  iterate over array or slice using range loop

  - instead of `for i := 3; i < 7; i++ {...}` prefer `for _, c := range a[3:7] {...}`

-  use backquote(`) for multiline strings

-  skip unused param with _

```
  func f(a int, _ string) {}
```

-  If you are comparing timestamps, use `time.Before` or `time.After`. Don't use `time.Sub` to get a duration and then check its value.
-  always pass context as a first param to a func with a `ctx` name
-  few params of the same type can be defined in a short way

```
  func f(a int, b int, s string, p string)
  func f(a, b int, s, p string)
```

-  

  the zero value of a slice is nil

  - https://play.golang.org/p/pNT0d_Bunq

  ```
    var s []int
    fmt.Println(s, len(s), cap(s))
    if s == nil {
      fmt.Println("nil!")
    }
    // Output:
    // [] 0 0
    // nil!
  ```

  - https://play.golang.org/p/meTInNyxtk

```
  var a []string
  b := []string{}

  fmt.Println(reflect.DeepEqual(a, []string{}))
  fmt.Println(reflect.DeepEqual(b, []string{}))
  // Output:
  // false
  // true
```

-  

  do not compare enum types with

  ```
<
  ```
  
  ,

  ```
>
  ```

  ,
  
  ```
<=
  ```

  and

  ```
  >=
  ```

  - use explicit values, don't do this:

```
  value := reflect.ValueOf(object)
  kind := value.Kind()
  if kind >= reflect.Chan && kind <= reflect.Slice {
    // ...
  }
```

-  use `%+v` to print data with sufficient details

-  

  be careful with empty struct

  ```
struct{}
  ```
  
  , see issue:

  https://github.com/golang/go/issues/23440

  - more: https://play.golang.org/p/9C0puRUstrP

```
  func f1() {
    var a, b struct{}
    print(&a, "\n", &b, "\n") // Prints same address
    fmt.Println(&a == &b)     // Comparison returns false
  }

  func f2() {
    var a, b struct{}
    fmt.Printf("%p\n%p\n", &a, &b) // Again, same address
    fmt.Println(&a == &b)          // ...but the comparison returns true
  }
```

-  

  wrap errors with

  http://github.com/pkg/errors

  - so: `errors.Wrap(err, "additional message to a given error")`

-  

  be careful with

  ```
range
  ```
  
  in Go:

  - `for i := range a` and `for i, v := range &a` doesn't make a copy of `a`
- but `for i, v := range a` does
  - more: https://play.golang.org/p/4b181zkB1O

-  

  reading nonexistent key from map will not panic

  - `value := map["no_key"]` will be zero value
  - `value, ok := map["no_key"]` is much better

-  

  do not use raw params for file operation

  - instead of an octal parameter like `os.MkdirAll(root, 0700)`
  - use predefined constants of this type `os.FileMode`

-  

  don't forget to specify a type for

  ```
iota
  ```
  
  - https://play.golang.org/p/mZZdMaI92cI

```
  const (
    _ = iota
    testvar         // will be int
  )
```

vs

```
  type myType int
  const (
    _ myType = iota
    testvar         // will be myType
  )
```

#### Don’t use `encoding/gob` on structs you don’t own.

At some point structure may change and you might miss this. As a result this might cause a hard to find bug.

#### Don't depend on the evaluation order, especially in a return statement.

```
// BAD
return res, json.Unmarshal(b, &res)

// GOOD
err := json.Unmarshal(b, &res)
return res, err
```

#### To prevent unkeyed literals add `_ struct{}` field:

```
type Point struct {
	X, Y float64
	_    struct{} // to prevent unkeyed literals
}
```

For `Point{X: 1, Y: 1}` everything will be fine, but for `Point{1,1}` you will get a compile error:

```
./file.go:1:11: too few values in Point literal
```

There is a check in `go vet` command for this, there is no enough arguments to add `_ struct{}` in all your structs.

#### To prevent structs comparison add an empty field of `func` type

```
type Point struct {
	_ [0]func()	// unexported, zero-width non-comparable field
	X, Y float64
}
```

#### Prefer `http.HandlerFunc` over `http.Handler`

To use the 1st one you just need a func, for the 2nd you need a type.

#### Move `defer` to the top

This improves code readability and makes clear what will be invoked at the end of a function.

#### JavaScript parses integers as floats and your int64 might overflow.

Use `json:"id,string"` instead.

```
type Request struct {
	ID int64 `json:"id,string"`
}
```

### Concurrency

-  

  best candidate to make something once in a thread-safe way is

  ```
sync.Once
  ```
  
  - don't use flags, mutexes, channels or atomics

-  to block forever use `select{}`, omit channels, waiting for a signal

-  

  don't close in-channel, this is a responsibility of it's creator

  - writing to a closed channel will cause a panic

-  

  ```
  func NewSource(seed int64) Source
  ```

  in

  ```
math/rand
  ```

  is not concurrency-safe. The default
  
  ```
lockedSource
  ```

  is concurrency-safe, see issue:

  https://github.com/golang/go/issues/3611

  - more: https://golang.org/pkg/math/rand/
  
-  when you need an atomic value of a custom type use [atomic.Value](https://godoc.org/sync/atomic#Value)

### Performance

-  

  do not omit

  ```
defer
  ```
  
  - 200ns speedup is negligible in most cases

-  

  always close http body aka

  ```
defer r.Body.Close()
  ```
  
  - unless you need leaked goroutine

-  filtering without allocating

```
    b := a[:0]
    for _, x := range a {
    	if f(x) {
		    b = append(b, x)
    	}
    }
```

#### To help compiler to remove bound checks see this pattern `_ = b[7]`

-  

  ```
  time.Time
  ```

  has pointer field

  ```
time.Location
  ```

  and this is bad for go GC
  
  - it's relevant only for big number of `time.Time`, use timestamp instead

-  

  prefer

  ```
regexp.MustCompile
  ```
  
  instead of

  ```
regexp.Compile
  ```

  - in most cases your regex is immutable, so init it in `func init`

-  

  do not overuse

  ```
fmt.Sprintf
  ```
  
  in your hot path. It is costly due to maintaining the buffer pool and dynamic dispatches for interfaces.

  - if you are doing `fmt.Sprintf("%s%s", var1, var2)`, consider simple string concatenation.
- if you are doing `fmt.Sprintf("%x", var)`, consider using `hex.EncodeToString` or `strconv.FormatInt(var, 16)`
  
-  

  always discard body e.g.

  ```
io.Copy(ioutil.Discard, resp.Body)
  ```
  
  if you don't use it

  - HTTP client's Transport will not reuse connections unless the body is read to completion and closed

```
    res, _ := client.Do(req)
    io.Copy(ioutil.Discard, res.Body)
    defer res.Body.Close()
```

-  

  don't use defer in a loop or you'll get a small memory leak

  - 'cause defers will grow your stack without the reason

-  don't forget to stop ticker, unless you need a leaked channel

```
  ticker := time.NewTicker(1 * time.Second)
  defer ticker.Stop()
```

-  

  use custom marshaler to speed up marshaling

  - but before using it - profile! ex: https://play.golang.org/p/SEm9Hvsi0r

```
  func (entry Entry) MarshalJSON() ([]byte, error) {
	buffer := bytes.NewBufferString("{")
	first := true
	for key, value := range entry {
		jsonValue, err := json.Marshal(value)
		if err != nil {
			return nil, err
		}
		if !first {
			buffer.WriteString(",")
		}
		first = false
		buffer.WriteString(key + ":" + string(jsonValue))
	}
	buffer.WriteString("}")
	return buffer.Bytes(), nil
  }
```

-  `sync.Map` isn't a silver bullet, do not use it without a strong reasons
  - more: https://github.com/golang/go/blob/master/src/sync/map.go#L12
-  storing non-pointer values in `sync.Pool` allocates memory
  - more: https://github.com/dominikh/go-tools/blob/master/cmd/staticcheck/docs/checks/SA6002
-  to hide a pointer from escape analysis you might carefully(!!!) use this func:
  - source: https://go-review.googlesource.com/c/go/+/86976

```
  // noescape hides a pointer from escape analysis.  noescape is
  // the identity function but escape analysis doesn't think the
  // output depends on the input. noescape is inlined and currently
  // compiles down to zero instructions.
  func noescape(p unsafe.Pointer) unsafe.Pointer {
  	x := uintptr(p)
  	return unsafe.Pointer(x ^ 0)
  }
```

-  for fastest atomic swap you might use this `m := (*map[int]int)(atomic.LoadPointer(&ptr))`

-  

  use buffered I/O if you do many sequential reads or writes

  - to reduce number of syscalls

-  

  there are 2 ways to clear a map:

  - reuse map memory

```
	for k := range m {
		delete(m, k)
	}
```

- allocate new

```
	m = make(map[int]int)
```

### Modules

-  if you want to test that `go.mod` (and `go.sum`) is up to date in CI https://blog.urth.org/2019/08/13/testing-go-mod-tidiness-in-ci/

### Build

-  strip your binaries with this command `go build -ldflags="-s -w" ...`

-  

  easy way to split test into different builds

  - use `// +build integration` and run them with `go test -v --tags integration .`

-  

  tiniest Go docker image

  - https://twitter.com/bbrodriges/status/873414658178396160
  - `CGO_ENABLED=0 go build -ldflags="-s -w" app.go && tar C app | docker import - myimage:latest`

-  

  run

  ```
go format
  ```
  
  on CI and compare diff

  - this will ensure that everything was generated and committed

-  

  to run Travis-CI with the latest Go use

  ```
travis 1
  ```
  
  - see more: https://github.com/travis-ci/travis-build/blob/master/public/version-aliases/go.json

-  check if there are mistakes in code formatting `diff -u <(echo -n) <(gofmt -d .)`

### Testing

-  prefer `package_test` name for tests, rather than `package`
-  `go test -short` allows to reduce set of tests to be runned

```
  func TestSomething(t *testing.T) {
    if testing.Short() {
      t.Skip("skipping test in short mode.")
    }
  }
```

-  skip test depending on architecture

```
  if runtime.GOARM == "arm" {
    t.Skip("this doesn't work under ARM")
  }
```

-  

  track your allocations with

  ```
testing.AllocsPerRun
  ```
  
  - https://godoc.org/testing#AllocsPerRun

-  

  run your benchmarks multiple times, to get rid of noise

  - `go test -test.bench=. -count=20`

### Tools

-  quick replace `gofmt -w -l -r "panic(err) -> log.Error(err)" .`

-  

  ```
  go list
  ```

  allows to find all direct and transitive dependencies

  - `go list -f '{{ .Imports }}' package`
- `go list -f '{{ .Deps }}' package`
  
-  

  for fast benchmark comparison we've a

  ```
benchstat
  ```
  
  tool

  - https://godoc.org/golang.org/x/perf/cmd/benchstat

-  [go-critic](https://github.com/go-critic/go-critic) linter enforces several advices from this document

-  `go mod why -m ` tells us why a particular module is in the `go.mod` file

-  `GOGC=off go build ...` should speed up your builds [source](https://twitter.com/mvdan_/status/1107579946501853191)

-  

  The memory profiler records one allocation every 512Kbytes. You can increase the rate via the

  ```
GODEBUG
  ```
  
  environment variable to see more details in your profile.

  - by https://twitter.com/bboreham/status/1105036740253937664

### Misc

-  dump goroutines https://stackoverflow.com/a/27398062/433041

```
  go func() {
    sigs := make(chan os.Signal, 1)
    signal.Notify(sigs, syscall.SIGQUIT)
    buf := make([]byte, 1<<20)
    for {
      <-sigs
      stacklen := runtime.Stack(buf, true)
      log.Printf("=== received SIGQUIT ===\n*** goroutine dump...\n%s\n*** end\n", buf[:stacklen])
    }
  }()
```

-  

  check interface implementation during compilation

  ```
  var _ io.Reader = (*MyFastReader)(nil)
  ```

-  

  if a param of len is nil then it's zero

  - https://golang.org/pkg/builtin/#len

-  anonymous structs are cool

```
  var  hits  struct { 
    sync。Mutex 
    n  int 
  } 命中。Lock（）
   命中。n ++ 命中。解锁（）
```

-  

  ```
  httputil.DumpRequest
  ```

   是非常有用的东西，不要创建自己的东西

  - https://godoc.org/net/http/httputil#DumpRequest

- 要获取调用堆栈，我们已经`runtime.Caller` https://golang.org/pkg/runtime/#Caller

-  封送任意JSON，您可以封送 `map[string]interface{}{}`

- 配置您的位置，

  ```
  CDPATH
  ```

  以便您可以

  ```
  cd github.com/golang/go
  ```

  从任何董事那里进行

  - 将此行添加到您的`bashrc`（或类似的）`export CDPATH=$CDPATH:$GOPATH/src`

-  切片中的简单随机元素

  - `[]string{"one", "two", "three"}[rand.Intn(3)]`




### 避免包重命名导入，防止名称冲突；

好的包名称不需要重命名。如果发生命名冲突，则更倾向于重命名最接近本地的包或特定于项目的包。

包导入按组进行组织，组与组之间有空行。标准库包始终位于第一组中。

```go
package main
import (
    "fmt"
    "hash/adler32"
    "os"
    "appengine/foo"
    "appengine/user"
    "github.com/foo/bar"
    "rsc.io/goversion/version"
)
```

[goimports](https://godoc.org/golang.org/x/tools/cmd/goimports) 会为你做这件事。



## mport Dot

**部分包由于循环依赖，不能作为测试包的一部分进行测试时，以`.`形式导入它们可能很有用：**

```go
package foo_test
import (
    "bar/testutil" // also imports "foo"
    . "foo"
)
```

​      在这种情况下，测试文件不能位于 foo 包中，因为它使用的 bar/testutil 依赖于 foo 包。所以我们使用`import .`形式使得测试文件伪装成 foo 包的一部分，即使它不是。除了这种情况，不要在程序中使用 `import .`。它将使程序更难阅读——因为不清楚如 Quux 这样的名称是否是当前包中或导入包中的顶级标识符。

### Go 对多返回值的支持提供了一种更好的解决方案。

函数应返回一个附加值以指示其他返回值是否有效，而不是要求客户端检查 in-band 错误值。此附加值可能是一个 error，或者在不需要解释时可以是布尔值。它应该是最终的返回值。

```
// Lookup returns the value for key or ok=false if there is no mapping for key.
func Lookup(key string) (value string, ok bool)
```

这可以防止调用者错误地使用返回结果：

```
Parse(Lookup(key))  // compile-time error
```

并鼓励更健壮和可读性强的代码：

```
value, ok := Lookup(key)if !ok  {    return fmt.Errorf("no value for %q", key)}return Parse(value)
```

此规则适用于公共导出函数，但对于未导出函数也很有用。

返回值如 nil，“”，0 和 -1 在他们是函数的有效返回结果时是可接收的，即调用者不需要将它们与其他值做分别处理。

某些标准库函数（如 “strings” 包中的函数）会返回 in-band 错误值。这大大简化了字符串操作，代价是需要程序员做更多事。通常，Go 代码应返回表示错误的附加值。



## Indent Error Flow

Try to keep the normal code path at a minimal indentation, and indent the error handling, dealing with it first. This improves the readability of the code by permitting visually scanning the normal path quickly. For instance, don't write:

尝试将正常的代码路径保持在最小的缩进处，优先处理错误并缩进。通过允许快速可视化扫描正常路径来提高代码的可读性。例如，不要写：

```go
if err != nil {
    // error handling
} else {
    // normal code
}
```

相反，书写以下代码：

```go
if err != nil {
    // error handling
    return // or continue, etc.
}
// normal code
```

如果 if 语句具有初始化语句，例如：

```go
if x, err := f(); err != nil {
    // error handling
    return
} else {
    // use x
}
```

那么这可能需要将短变量声明移动到新行：

```go
x, err := f()
if err != nil {
    // error handling
    return
}
// use x
```



## Initialisms

名称中的单词是首字母或首字母缩略词（例如 “URL” 或 “NATO” ）需要具有相同的大小写规则。例如，“URL” 应显示为 “URL” 或 “url” （如 “urlPony” 或 “URLPony” ），而不是 “Url”。举个例子：ServeHTTP 不是 ServeHttp。对于具有多个初始化 “单词” 的标识符，也应当显示为 “xmlHTTPRequest” 或 “XMLHTTPRequest”。

**当 “ID” 是 “identifier” 的缩写时，此规则也适用于 “ID” ，因此请写 “appID” 而不是“appId”。**

由协议缓冲区编译器生成的代码不受此规则的约束。人工编写的代码比机器编写的代码要保持更高的标准。



## Useful Test Failures

失败的测试也应该提供有用的消息，说明错误，展示输入内容，实际内容以及预期结果。编写一堆 assertFoo 帮助程序可能很吸引人，但请确保您的帮助程序能产生有用的错误消息。假设调试失败测试的人不是你，也不是你的团队。典型的 Go 失败测试如：

```go
if got != tt.want {
    t.Errorf("Foo(%q) = %d; want %d", tt.in, got, tt.want) // or Fatalf, if test can't test anything more past this point
}
```

请注意，此处的命令是 实际结果!=预期结果，并且错误消息也使用该命令格式。然而一些测试框架鼓励倒写输出格式，如 预期结果 != 实际结果，“预期结果为 0，实际结果为 x”，等等。但是 Go 没有这样做。

如果这看起来像是打了很多字，你可能想写一个表驱动的测试。

在使用具有不同输入的测试帮助程序时以消除失败测试歧义的另一种常见技术是使用不同的 TestFoo 函数包装每个调用者，而测试名称也根据对应的输入命名：

```go
func TestSingleValue(t *testing.T) { testHelper(t, []int{80}) }
func TestNoValues(t *testing.T)    { testHelper(t, []int{}) }
```

In any case, the onus is on you to fail with a helpful message to whoever's debugging your code in the future.

在任何情况下，你都有责任向可能会在将来调试你的代码的开发者提供有用的消息。



### 不错链接：

https://www.zybuluo.com/wddpct/note/1264988



#### Multiple if-else statements can be collapsed into a switch

```go
// NOT BAD
if foo() {
    // ...
} else if bar == baz {
    // ...
} else {
    // ...
}

// BETTER
switch {
case foo():
    // ...
case bar == baz:
    // ...
default:
    // ...
}
```



#### Prefer `30 * time.Second` instead of `time.Duration(30) * time.Second`

You don't need to wrap untyped const in a type, compiler will figure it out. Also prefer to move const to the first place:

```go
// BAD
delay := time.Second * 60 * 24 * 60

// VERY BAD
delay := 60 * time.Second * 60 * 24

// GOOD
delay := 24 * 60 * 60 * time.Second
```



#### Use `time.Duration` instead of `int64` + variable name

```go
// BAD
var delayMillis int64 = 15000

// GOOD
var delay time.Duration = 15 * time.Second
```

#### Group `const` declarations by type and `var` by logic and/or type

```go
// BAD
const (
    foo = 1
    bar = 2
    message = "warn message"
)

// MOSTLY BAD
const foo = 1
const bar = 2
const message = "warn message"

// GOOD
const (
    foo = 1
    bar = 2
)

const message = "warn message"
```



#### Don't depend on the evaluation order, especially in a return statement.

```go
// BAD
return res, json.Unmarshal(b, &res)

// GOOD
err := json.Unmarshal(b, &res)
return res, err
```



### Testing

-  prefer `package_test` name for tests, rather than `package`
-  `go test -short` allows to reduce set of tests to be runned

```go
  func TestSomething(t *testing.T) {
    if testing.Short() {
      t.Skip("skipping test in short mode.")
    }
  }
```



### 零值Mutexes是有效的

零值的 `sync.Mutex` 和 `sync.RWMutex` 是有效的，所以基本是不需要一个指向 `Mutex` 的指针的。

| Bad                                 | Good                            |
| ----------------------------------- | ------------------------------- |
| mu := new(sync.Mutex)<br/>mu.Lock() | var mu sync.Mutex<br/>mu.Lock() |



#### 返回 Slices 和 Maps

同理，谨慎提防用户修改暴露内部状态的 slices 和 maps 。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| type Stats struct {<br/>  sync.Mutex<br/><br/>  counters map[string]int<br/>}<br/><br/>// Snapshot 返回当前状态<br/>func (s *Stats) Snapshot() map[string]int {<br/>  s.Lock()<br/>  defer s.Unlock()<br/><br/>  return s.counters<br/>}<br/><br/>// snapshot 不再受锁保护了！<br/>snapshot := stats.Snapshot() | type Stats struct {<br/>  sync.Mutex<br/><br/>  counters map[string]int<br/>}<br/><br/>func (s *Stats) Snapshot() map[string]int {<br/>  s.Lock()<br/>  defer s.Unlock()<br/><br/>  **result := make(map[string]int, len(s.counters))<br/>  for k, v := range s.counters {<br/>    result[k] = v<br/>  }<br/>  return result<br/>}**<br/><br/>// snapshot 是一分拷贝的内容了<br/>snapshot := stats.Snapshot() |

### 

### 使用 defer 来做清理工作

使用 defer 来做资源的清理工作，例如文件的关闭和锁的释放。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| p.Lock()<br/>if p.count < 10 {<br/>  p.Unlock()<br/>  return p.count<br/>}<br/><br/>p.count++<br/>newCount := p.count<br/>p.Unlock()<br/><br/>return newCount<br/><br/>// 当有多处 return 时容易忘记释放锁 | p.Lock()<br/>defer p.Unlock()<br/><br/>if p.count < 10 {<br/>  return p.count<br/>}<br/><br/>p.count++<br/>return p.count<br/><br/>// 可读性更高 |

defer 只有非常小的性能开销，只有当你能证明你的函数执行时间在纳秒级别时才可以不使用它。使用 defer 对代码可读性的提高是非常值得的，因为使用 defer 的成本真的非常小。特别是在一些主要是做内存操作的长函数中，函数中的其他计算操作远比 `defer` 重要。



### Channel 的大小设为 1 还是 None

通道的大小通常应该设为 1 或者设为无缓冲类型。默认情况下，通道是无缓冲类型的，大小为 0 。将通道大小设为其他任何数值都应该经过深思熟虑。认真考虑如何确定其大小，是什么阻止了工作中的通道被填满并阻塞了写入操作，以及何种情况会发生这样的现象。

| Bad                                             | Good                                                         |
| ----------------------------------------------- | ------------------------------------------------------------ |
| // 足以满足任何人！<br/>c := make(chan int, 64) | // 大小 为 1<br/>c := make(chan int, 1) // or<br/>// 无缓冲 channel, 大小为 0<br/>c := make(chan int) |

### 错误类型

**有很多种方法来声明 errors:**

- `errors.New` 声明简单的静态字符串错误信息
- `fmt.Errorf` 声明格式化的字符串错误信息
- 为自定义类型实现 `Error()` 方法
- 通过 `"pkg/errors".Wrap` 包装错误类型

返回错误时，请考虑以下因素来作出最佳选择：

- 这是一个不需要其他额外信息的简单错误吗？如果是，使用`error.New`。

- 客户需要检测并处理此错误吗？如果是，那应该自定义类型，并实现 `Error()` 方法。

- 是否是在传递一个下游函数返回的错误？如果是，请查看[error 封装](https://note.mogutou.xyz/articles/2019/10/13/1570978862812.html#error-wrapping)部分。

- 其他，使用 `fmt.Errorf` 。

  

如果客户需要检测错误，并且是通过 `errors.New` 创建的一个简单的错误，请使用var 声明这个错误类型。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| // package foo<br/><br/>func Open() error {<br/>  return errors.New("could not open")<br/>}<br/><br/>// package bar<br/><br/>func use() {<br/>  if err := foo.Open(); err != nil {<br/>    if err.Error() == "could not open" {<br/>      // handle<br/>    } else {<br/>      panic("unknown error")<br/>    }<br/>  }<br/>} | // package foo<br/><br/>var ErrCouldNotOpen = errors.New("could not open")<br/><br/>func Open() error {<br/>  return ErrCouldNotOpen<br/>}<br/><br/>// package bar<br/><br/>if err := foo.Open(); err != nil {<br/>  if err == foo.ErrCouldNotOpen {<br/>    // handle<br/>  } else {<br/>    panic("unknown error")<br/>  }<br/>} |



### Error 封装

**下面提供三种主要的方法来传递函数调用失败返回的错误：**

- 如果想要维护原始错误类型并且不需要添加额外的上下文信息，就直接返回原始错误。
- 使用 `"pkg/errors".Wrap` 来增加上下文信息，这样返回的错误信息中就会包含更多的上下文信息，并且通过 `"pkg/errors".Cause` 可以提取出原始错误信息。
- 如果调用方不需要检测或处理特定的错误情况，就直接使用 `fmt.Errorf` 。

情况允许的话建议增加更多的上下文信息来代替诸如 `"connection refused"` 之类模糊的错误信息。返回 `"failed to call service foo: connection refused"` 用户可以知道更多有用的错误信息。

**在将上下文信息添加到返回的错误时，请避免使用 "failed to" 之类的短语以保持信息简洁，**这些短语描述的状态是显而易见的，并且会随着错误在堆栈中的传递而逐渐堆积：

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| s, err := store.New()<br/>if err != nil {<br/>    return fmt.Errorf(<br/>        "failed to create new store: %s", err)<br/>} | s, err := store.New()<br/>if err != nil {<br/>    return fmt.Errorf(<br/>        "new store: %s", err)<br/>} |
| `failed to x: failed to y: failed to create new store: the error ` | `x: y: new store: the error `                                |

但是，如果这个错误信息是会被发送到另一个系统时，必须清楚的表明这是一个错误（例如，日志中 `err` 标签或者 `Failed` 前缀）。



### 处理类型断言失败

**[类型断言](https://golang.org/ref/spec#Type_assertions)的单返回值形式在遇到类型错误时会直接 panic 。因此，请始终使用 "comma ok" 惯用方法。**

| Bad                | Good                                                         |
| ------------------ | ------------------------------------------------------------ |
| `t := i.(string) ` | t, ok := i.(string)<br/>if !ok {<br/>  // handle the error gracefully<br/>} |



### strconv 性能优于 fmt

将原语转换为字符串或从字符串转换时，`strconv` 速度比 `fmt` 更快。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| for i := 0; i < b.N; i++ {<br/>  s := fmt.Sprint(rand.Int())<br/>} | for i := 0; i < b.N; i++ {<br/>  s := strconv.Itoa(rand.Int())<br/>} |
| `BenchmarkFmtSprint-4    143 ns/op    2 allocs/op `          | `BenchmarkStrconv-4    64.2 ns/op    1 allocs/op`            |



## 代码风格

### 声明分组

Go 支持将相似的声明分组：

| Bad                       | Good                               |
| ------------------------- | ---------------------------------- |
| import "a"<br/>import "b" | import (<br/>  "a"<br/>  "b"<br/>) |

分组同样适用于常量、变量和类型的声明：

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| const a = 1<br/>const b = 2<br/><br/>var a = 1<br/>var b = 2<br/><br/>type Area float64<br/>type Volume float64 | const (<br/>  a = 1<br/>  b = 2<br/>)<br/><br/>var (<br/>  a = 1<br/>  b = 2<br/>)<br/><br/>type (<br/>  Area float64<br/>  Volume float64<br/>) |

仅将相似的声明放在同一组。不相关的声明不要放在同一个组内。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| type Operation int<br/><br/>const (<br/>  Add Operation = iota + 1<br/>  Subtract<br/>  Multiply<br/>  ENV_VAR = "MY_ENV"<br/>) | type Operation int<br/><br/>const (<br/>  Add Operation = iota + 1<br/>  Subtract<br/>  Multiply<br/>)<br/><br/>const ENV_VAR = "MY_ENV" |

**声明分组可以在任意位置使用。例如，可以在函数内部使用。**

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| func f() string {<br/>  var red = color.New(0xff0000)<br/>  var green = color.New(0x00ff00)<br/>  var blue = color.New(0x0000ff)<br/><br/>  ...<br/>} | func f() string {<br/>  var (<br/>    red   = color.New(0xff0000)<br/>    green = color.New(0x00ff00)<br/>    blue  = color.New(0x0000ff)<br/>  )<br/><br/>  ...<br/>} |



### Import 组内顺序

import 有两类导入组：

- 标准库
- 其他

goimports 默认的分组如下：

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| import (<br/>  "fmt"<br/>  "os"<br/>  "go.uber.org/atomic"<br/>  "golang.org/x/sync/errgroup"<br/>) | import (<br/>  "fmt"<br/>  "os"<br/><br/>  "go.uber.org/atomic"<br/>  "golang.org/x/sync/errgroup"<br/>) |

### 包名

当为包命名时，请注意如下事项：

- 字符全部小写，没有大写或者下划线
- 在大多数情况下引入包不需要去重命名
- 简单明了，命名需要能够在被导入的地方准确识别
- 不要使用复数。例如，`net/url`, 而不是 `net/urls`
- 不要使用“common”，“util”，“shared”或“lib”之类的。这些都是不好的，表达信息不明的名称



### 包导入别名

如果包的名称与导入路径的最后一个元素不匹配，那必须使用导入别名。

```go
import (
  "net/http"

  client "example.com/client-go"
  trace "example.com/trace/v2"
)
```

在其他情况下，除非导入的包名之间有直接冲突，否则应避免使用导入别名。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| import (<br/>  "fmt"<br/>  "os"<br/><br/><br/>  nettrace "golang.net/x/trace"<br/>) | import (<br/>  "fmt"<br/>  "os"<br/>  "runtime/trace"<br/><br/>  nettrace "golang.net/x/trace"<br/>) |

### 

### 函数分组与排布顺序

- 函数应该粗略的按照调用顺序来排布
- 同一文件中的函数应该按照接收器的类型来分组排布

**所以，公开的函数应排布在文件首，并在 struct、const 和 var 定义之后。**

newXYZ()/ NewXYZ() 之类的函数应该排布在声明类型之后，具有接收器的其余方法之前。

因为函数是按接收器类别分组的，所以普通工具函数应排布在文件末尾。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| func (s *something) Cost() {<br/>  return calcCost(s.weights)<br/>}<br/><br/>type something struct{ ... }<br/><br/>func calcCost(n int[]) int {...}<br/><br/>func (s *something) Stop() {...}<br/><br/>func newSomething() *something {<br/>    return &something{}<br/>} | type something struct{ ... }<br/><br/>func newSomething() *something {<br/>    return &something{}<br/>}<br/><br/>func (s *something) Cost() {<br/>  return calcCost(s.weights)<br/>}<br/><br/>func (s *something) Stop() {...}<br/><br/>func calcCost(n int[]) int {...} |



### 减少嵌套

**代码应该通过尽可能地先处理错误情况/特殊情况，并且及早返回或继续下一循环来减少嵌套。尽量减少嵌套于多个级别的代码数量。**

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| for _, v := range data {<br/>  if v.F1 == 1 {<br/>    v = process(v)<br/>    if err := v.Call(); err == nil {<br/>      v.Send()<br/>    } else {<br/>      return err<br/>    }<br/>  } else {<br/>    log.Printf("Invalid v: %v", v)<br/>  }<br/>} | for _, v := range data {<br/>  if v.F1 != 1 {<br/>    log.Printf("Invalid v: %v", v)<br/>    continue<br/>  }<br/><br/>  v = process(v)<br/>  if err := v.Call(); err != nil {<br/>    return err<br/>  }<br/>  v.Send()<br/>} |



### 不必要的 else

**如果一个变量在 if 的两个分支中都设置了，那应该使用单个 if 。**

| Bad                                                          | Good                                   |
| ------------------------------------------------------------ | -------------------------------------- |
| var a int<br/>if b {<br/>  a = 100<br/>} else {<br/>  a = 10<br/>} | a := 10<br/>if b {<br/>  a = 100<br/>} |



### 全局变量声明

***在顶层使用标准 var 关键字声明变量时，不要显式指定类型，除非它与表达式的返回类型不同。***

| Bad                                                         | Good                                                         |
| ----------------------------------------------------------- | ------------------------------------------------------------ |
| var _s string = F()<br/><br/>func F() string { return "A" } | var _s = F()<br/>// F 已经明确声明返回一个字符串类型，我们没有必要显式指定 _s 的类型<br/><br/>func F() string { return "A" } |

**如果表达式的返回类型与所需的类型不完全匹配，请显示指定类型。**

```go
type myError struct{}

func (myError) Error() string { return "error" }

func F() myError { return myError{} }

var _e error = F()
// F 返回一个 myError 类型的实例，但是我们要 error 类型
```

### 

### 结构体中的嵌入类型

**嵌入式类型（例如 mutex ）应该放置在结构体字段列表的顶部，并且必须以空行与常规字段隔开。**

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| type Client struct {<br/>  version int<br/>  http.Client<br/>} | type Client struct {<br/>  http.Client<br/><br/>  version int<br/>} |



### 使用字段名来初始化结构

初始化结构体时，必须指定字段名称。`go vet` 强制执行。

| Bad                            | Good                                                         |
| ------------------------------ | ------------------------------------------------------------ |
| k := User{"John", "Doe", true} | k := User{<br/>    FirstName: "John",<br/>    LastName: "Doe",<br/>    Admin: true,<br/>} |



### 局部变量声明

如果声明局部变量时需要明确设值，应使用短变量声明形式（:=）。

| Bad              | Good          |
| ---------------- | ------------- |
| `var s = "foo" ` | `s := "foo" ` |

但是，在某些情况下，使用 var 关键字声明变量，默认的初始化值会更清晰。例如，声明空切片。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| func f(list []int) {<br/>  filtered := []int{}<br/>  for _, v := range list {<br/>    if v > 10 {<br/>      filtered = append(filtered, v)<br/>    }<br/>  }<br/>} | func f(list []int) {<br/>  var filtered []int<br/>  for _, v := range list {<br/>    if v > 10 {<br/>      filtered = append(filtered, v)<br/>    }<br/>  }<br/>} |



### nil是一个有效的slice

nil 是一个有效的长度为 0 的 slice，这意味着：

- **不应明确返回长度为零的切片，而应该直接返回 nil 。**

  | Bad                                     | Good                                |
  | --------------------------------------- | ----------------------------------- |
  | if x == "" {<br/>  return []int{}<br/>} | if x == "" {<br/>  return nil<br/>} |

- **若要检查切片是否为空，始终使用 `len(s) == 0` ，不要与 nil 比较来检查。**

  | Bad                                                         | Good                                                         |
  | ----------------------------------------------------------- | ------------------------------------------------------------ |
  | func isEmpty(s []string) bool {<br/>  return s == nil<br/>} | func isEmpty(s []string) bool {<br/>  return len(s) == 0<br/>} |

- **零值切片（通过 var 声明的切片）可直接使用，无需调用 make 创建。**

  | Bad                                                          | Good                                                         |
  | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | nums := []int{}<br/>// or, nums := make([]int)<br/><br/>if add1 {<br/>  nums = append(nums, 1)<br/>}<br/><br/>if add2 {<br/>  nums = append(nums, 2)<br/>} | var nums []int<br/><br/>if add1 {<br/>  nums = append(nums, 1)<br/>}<br/><br/>if add2 {<br/>  nums = append(nums, 2)<br/>} |

### 

### 缩小变量作用域

**如果有可能，尽量缩小变量作用范围，除非这样与减少嵌套的规则冲突。**

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| err := ioutil.WriteFile(name, data, 0644)<br/>if err != nil {<br/> return err<br/>} | if err := ioutil.WriteFile(name, data, 0644); err != nil {<br/> return err<br/>} |



### 初始化结构体引用

**在初始化结构引用时，使用 `&T{}` 而非 `new(T)`，以使其与结构体初始化方式保持一致。**

| Bad                                                          | Good                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| sval := T{Name: "foo"}<br/><br/>// 定义方式不一致<br/>sptr := new(T)<br/>sptr.Name = "bar" | sval := T{Name: "foo"}<br/><br/>sptr := &T{Name: "bar"} |



### 格式化字符串放在 Printf 外部

如果为 Printf-style 函数声明格式化字符串，将格式化字符串放在函数外面 ，并将其设置为 const 常量。

这有助于 `go vet` 对格式字符串进行静态分析。

| Bad                                                          | Good                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `msg := "unexpected values %v, %v\n" fmt.Printf(msg, 1, 2) ` | `const msg = "unexpected values %v, %v\n" fmt.Printf(msg, 1, 2) ` |

### 为 Printf 样式函数命名