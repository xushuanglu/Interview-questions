# golang教程

[![img](https://upload.jianshu.io/users/upload_avatars/8852308/93d0d400-d6bd-4a17-bff7-1ece0bb99334.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96)](https://www.jianshu.com/u/a02b655e1b7b)

[陨石坠灭](https://www.jianshu.com/u/a02b655e1b7b)

0.0962018.06.28 10:48:07字数 8,280阅读 4,241

## 环境搭建

[Golang在Mac OS上的环境配置](https://www.jianshu.com/p/358cbc939569)

[使用Visual Studio Code辅助Go源码编写](https://studygolang.com/articles/9290)

[VS Code折腾记 - (2) 快捷键大全，没有更全](http://blog.csdn.net/crper/article/details/54099319)

## 语法

1. public的变量必须以大写字母开头,private变量则以小写字母开头
2. Go语言对{ }应该怎么写进行了强制

```golang
if express{
    ...   
}
```

1. Go 语言首创的错误处理规范:

```golang
f, err := os.Open(filename) if err != nil {
        log.Println("Open file failed:", err)
return }
defer f.Close()
... // 操作已经打开的f文件
```

这里有两个关键点。

- 其一是defer关键字。defer语句的含义是不管程序是否出现异常,均 在函数退出时自动执行相关代码。
- 其二是Go语言的函数允许返回多个值。

大多数函数 的最后一个返回值会为error类型,以在错误情况下返回详细信息。error类型只是一个系统内 置的interface,如下:

```golang
type error interface {
    Error() string
}
```

1. Go语言支持类、类成员方法、类的组合,但反对继承,反对虚函数(virtual function) 和虚函数重载。确切地说,Go也提供了继承,只不过是采用了组合的文法来提供:

```golang
type Foo struct { 
    Base
    ... 
}
func (foo *Foo) Bar() { 
    ...
}
```

1. Go语言也放弃了构造函数(constructor)和析构函数(destructor)。
2. Go语言送上了一份非常棒的礼物:接口(interface)。

Go语言中的接口与其他语言最大的一点区别是它的非侵入性。在Go语言中,实现类的时候无需从接口派生,具体代码如下:

```golang
type Foo struct { // Go 文法 
    ...
}
var foo IFoo = new(Foo)
```

只要Foo实现了接口IFoo要求的所有方法,就实现了该接口,可以进行赋值。

特点:

- 其一,Go语言的标准库再也不需要绘制类库的继承树图。
- 其二,不用再纠结接口需要拆得多细才合理。
- 其三,不用为了实现一个接口而专门导入一个包,而目的仅仅是引用其中的某个接口的定义。

在Go语言中,只要两个接口拥有相同的方法列表,那么它们就是等同的,可以相互赋值,如对 于以下两个接口,第一个接口:

```golang
package one
type ReadWriter interface {
    Read(buf [] byte) (n int, err error) 
    Write(buf [] byte) (n int, err error)
}
//第二个接口:
package two
type IStream interface {
    Write(buf [] byte) (n int, err error) 
    Read(buf [] byte) (n int, err error)
}
```

在Go语言中,这两个接口实际上并无区别,因为:

- 任何实现了one.ReadWriter接口的类,均实现了two.IStream;
- 任何one.ReadWriter接口对象可赋值给two.IStream,反之亦然;
- 在任何地方使用one.ReadWriter接口,与使用two.IStream并无差异。

1. 函数多返回值

```golang
//返回多个参数
func getName() (firstName, middleName, lastName, nickName string) {
    return "May", "M", "Chen", "Babe"
}

//灵活赋值
func getName2() (firstName, middleName, lastName, nickName string) {
    firstName = "May"
    middleName = "M"
    lastName = "Chen"
    nickName = "Babe"
    return
}

//赋值
firstName, middleName, lastName, nickName := getName()
```

并不是每一个返回值都必须赋值,没有被明确赋值的返回值将保持默认的空值。

如果开发者只对该函数其中的某几个返回值感兴趣的话,也可以直接用下划线作为占位符来 忽略其他不关心的返回值。

```golang
 _, _, lastName, _ := getName()
```

1. Go语言引入了3个关键字用于标准的错误处理流程,这3个关键字分别为defer、panic和 recover。
2. 匿名函数和闭包。

在Go语言中,所有的函数也是值类型,可以作为参数传递。Go语言支持常规的匿名函数和 闭包,比如下列代码就定义了一个名为f的匿名函数,开发者可以随意对该匿名函数变量进行传 递和调用:

```golang
f := func(x, y int) int { 
    return x + y
}
```

1. 类型和接口。Go语言的类型定义非常接近于C语言中的结构(struct),甚至直接沿用了struct关键字。

```golang
type Bird struct { 
    ...
}

func (b *Bird) Fly() { 
    // 以鸟的方式飞行
}


type IFly interface { 
    Fly()
}

func main() {
    var fly IFly = new(Bird) fly.Fly()
}
```

11.并发编程。 Go语言引入了goroutine概念,它使得并发编程变得非常简单。

通过在函数调用前使用关键字go,我们即可让该函数以goroutine方式执行。

Go语言通过系统的线程来多路派遣这些函数的执行,使得 每个用go关键字执行的函数可以运行成为一个单位协程。当一个协程阻塞的时候,调度器就会自 动把其他协程安排到另外的线程中去执行,从而实现了程序无等待并行化运行。

Go语言实现了CSP(通信顺序进程,Communicating Sequential Process)模型来作为goroutine 间的推荐通信方式。

在CSP模型中,一个并发系统由若干并行运行的顺序进程组成,每个进程不 能对其他进程的变量赋值。进程之间只能通过一对通信原语实现协作。Go语言用channel(通道) 这个概念来轻巧地实现了CSP模型。

另外,由于一个进程内创建的所有goroutine运行在同一个内存地址空间中,因此如果不同的 goroutine不得不去访问共享的内存变量,访问前应该先获取相应的读写锁。Go语言标准库中的 sync包提供了完备的读写锁功能。

```golang
package main

import "fmt"

func sum(values [] int, resultChan chan int) { 
    sum := 0
    for _, value := range values { 
        sum += value
    }
    resultChan <- sum // 将计算结果发送到channel中 
}

func main() {
    values := [] int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
    resultChan := make(chan int, 2)
    go sum(values[:len(values)/2], resultChan)
    go sum(values[len(values)/2:], resultChan)
    sum1, sum2 := <-resultChan, <-resultChan // 接收结果
    fmt.Println("Result:", sum1, sum2, sum1 + sum2)
}
```

12.反射。

Go语言的反射实现了反射的大部分功能,但没有像Java语言那样内置类型工厂,故而无法做 到像Java那样通过类型字符串创建对象实例。

反射最常见的使用场景是做对象的序列化(serialization,有时候也叫Marshal & Unmarshal)。

```golang
package main
import (
    "fmt"
    "reflect"
)
type Bird struct {
    Name string
    LifeExpectance int
}

func (b *Bird) Fly() { 
    fmt.Println("I am flying...")
}

func main() {
    sparrow := &Bird{"Sparrow", 3}
    s := reflect.ValueOf(sparrow).Elem() typeOfT := s.Type()
    for i := 0; i < s.NumField(); i++ {
        f := s.Field(i)
        fmt.Printf("%d: %s %s = %v\n", i, typeOfT.Field(i).Name,f.Type(),f.Interface())
    }
}
```

1. 语言的交互性。

由于Go语言与C语言之间的天生联系,Go语言的设计者们自然不会忽略如何重用现有C模块 的这个问题,这个功能直接被命名为Cgo。Cgo既是语言特性,同时也是一个工具的名称

Cgo的用法非常简单,比如下面例子就可以实现在Go中调用C语言标准库的puts函数。

```golang
package main
/*
#include <stdio.h> 
#include <stdlib.h>
*/
import "C"
import "unsafe"
func main() {
    cstr := C.CString("Hello, world")
    C.puts(cstr) 
    C.free(unsafe.Pointer(cstr))
}
```

注意:使用C.puts,C.free需要include stdlib.h

### 开始

1.第一个 Go 程序

- 每个Go源代码文件的开头都是一个package声明,表示该Go代码所属的包。包是Go语言里 最基本的分发单位,也是工程管理中依赖关系的体现。
- 要生成Go可执行程序,必须建立一个名 字为main的包,并且在该包中包含一个叫main()的函数(该函数是Go可执行程序的执行起点)。
- Go语言的main()函数不能带参数,也不能定义返回值。命令行传入的参数在os.Args变量 中保存。如果需要支持命令行开关,可使用flag包。
- 不得包含在源代码文件中没有用到的包,否则Go编译器会报编译错误。
- 所有Go函数(包括在对象编程中会提到的类型成员函数)以关键字func开头。

一个常规的 函数定义包含以下部分:

```golang
func 函数名(参数列表)(返回值列表) { 
    // 函数体
}
```

- Go支持多个返回值。

并不是所有返回值都必须赋值。在函数返回时没有被明确赋值的返回值都会被设置为默认 值,比如result会被设为0.0,err会被设为nil。

- Go程序的代码注释与C++保持一致,即同时支持以下两种用法:

```golang
/*
块注释
*/
// 行注释
```

- Go代码里没有出现分号。Go 程序并不要求开发者在每个语句后面加上分号表示语句结束

```golang
package main
import "fmt"// 我们需要使用fmt包中的Println()函数
func main() {
    fmt.Println("Hello, world. 你好,世界!")
}
```

1. 编译环境准备

安装包的下载地址为http://code.google.com/p/go/downloads/list

在*nix环境中,Go默认会被安装到/usr/local/go目录中。安装包在安装完成后会自动添加执行文件目录到系统路径中。

安装完成后,请重新启动命令行程序,然后运行以下命令以验证Go是否已经正确安装:

```shell
$ go version
go version go1
```

如果提 示找不到go命令,可以通过手动添加/usr/local/go/bin到PATH环境变量来解决。

1. 编译程序

假设之前介绍的Hello, world代码被保存为了hello.go,并位于~/goyard目录下,那么可以用以 下命令行编译并直接运行该程序:

```shell
$ cd ~/goyard
$ go run hello.go # 直接运行 
Hello, world. 你好,世界!
```

使用这个命令,会将编译、链接和运行3个步骤合并为一步,运行完后在当前目录下也看不 到任何中间文件和最终的可执行文件。如果要只生成编译结果而不自动运行,我们也可以使用 Go 命令行工具的build命令:

```shell
$ cd ~/goyard
$ go build hello.go
$ ./hello
Hello, world. 你好,世界!
```

1. 工程管理

例子:带尖括号的名字表示其为目录。xxx_test.go表示的是一个对于xxx.go的单元 测试,这也是Go工程里的命名规则。

```xml
<calcproj> ├─<src>
├─<calc> ├─calc.go
├─<simplemath> ├─add.go
├─add_test.go ├─sqrt.go ├─sqrt_test.go
├─<bin> ├─<pkg>#包将被安装到此处
```

- 为了能够构建这个工程,需要先把这个工程的根目录加入到环境变量GOPATH中。假设calcproj 目录位于/goyard下,则应编辑/.bashrc文件,并添加下面这行代码:

```jsx
export GOPATH=~/goyard/calcproj
```

然后执行以下命令应用该设置:

```bash
$ source ~/.bashrc
```

GOPATH和PATH环境变量一样,也可以接受多个路径,并且路径和路径之间用冒号分割。

- 设置完GOPATH后,现在我们开始构建工程。假设我们希望把生成的可执行文件放到
   calcproj/bin目录中,需要执行的一系列指令如下:

```ruby
$ cd ~/goyard/calcproj
$ mkdir bin
$ cd bin
$ go build calc
```

1. 么我们到底怎么运行这些单元测试呢?这也非常简单。因为 已经设置了GOPATH,所以可以在任意目录下执行以下命令:

```bash
$ go test simplemath
ok  simplemath  0.014s
```

1. 打印日志

Go语言包中包含一个fmt包,其中提供了大量易用的打印函数,我们会接触到的主要是 Printf()和Println()。

```golang
fval := 110.48
ival := 200
sval := "This is a string. "
fmt.Println("The value of fval is", fval)
fmt.Printf("fval=%f, ival=%d, sval=%s\n", fval, ival, sval)
fmt.Printf("fval=%v, ival=%v, sval=%v\n", fval, ival, sval)
```

输出结果:

```text
The value of fval is 100.48
fval=100.48, ival=200, sval=This is a string.
fval=100.48, ival=200, sval=This is a string.
```

1. GDB调试

不用设置什么编译选项,Go语言编译的二进制程序直接支持GDB调试,比如之前用go build
 calc编译出来的可执行文件calc,就可以直接用以下命令以调试模式运行:

```ruby
$ gdb calc
```

1. 变量

- 变量声明

Go语言的变量声明方式与C和C++语言有明显的不同。对于纯粹的变量声明,Go语言引入了 关键字var,而类型信息放在变量名之后

```golang
var v1 int
var v2 string 
var v3 [10]int // 数组
var v4 []int // 数组切片
var v5 struct {
    f int 
}
var v6 *int // 指针
var v7 map[string] int // map,key为string类型,value为int类型
var v8 func(a int) int

// var关键字的另一种用法是可以将若干个需要声明的变量放置在一起,免得程序员需要重复 写var关键字

var (
    v1 int
    v2 string
)
```

- 变量初始化

对于声明变量时需要进行初始化的场景,var关键字可以保留,但不再是必要的元素

```golang
var v1 int = 10 // 正确的使用方式1
var v2 = 10 // 正确的使用方式2,编译器可以自动推导出v2的类型 
v3 := 10 // 正确的使用方式3,编译器可以自动推导出v3的类型
```

这里Go语言也引入了另一个C和C++中没有的符号(冒号和等号的组合:=),用于明确表达同时进行变量声明和初始化的工作。出现在:=左侧的变量不应该是已经被声明过的,否则会导致编译错误

- 变量赋值

在Go语法中,变量初始化和变量赋值是两个不同的概念。下面为声明一个变量之后的赋值过程:

```golang
var v10 int
v10 = 123

fmt.Println("Go语言的变量赋值与多数语言一致,但Go语言中提供了C/C++程序员期盼多年的多重赋值功 能,比如下面这个交换i和j变量的语句:")

i, j = j, i
```

- 匿名变量

```golang
func GetName() (firstName, lastName, nickName string) { 
    return "May", "Chan", "Chibi Maruko"
}

//若只想获得nickName,则函数调用语句可以用如下方式编写:
_, _, nickName := GetName()
```

1. 常量

在Go语言中,常量是指编译期间就已知且不可改变的值。常量可以是数值类型(包括整型、
 浮点型和复数类型)、布尔类型、字符串类型等。

- 字面常量

所谓字面常量(literal),是指程序中硬编码的常量,如:

```go
-12
3.14159265358979323846 // 浮点类型的常量 
3.2+12i // 复数类型的常量 
true // 布尔类型的常量 
"foo" // 字符串常量
```

- 常量定义

通过const关键字,你可以给字面常量指定一个友好的名字

```golang
const Pi float64 = 3.14159265358979323846
const zero = 0.0 // 无类型浮点常量
const (
    size int64 = 1024
    eof = -1 // 无类型整型常量
)
const u, v float32 = 0, 3  // u = 0.0, v = 3.0,常量的多重赋值
const a, b, c = 3, 4, "foo" //a=3,b=4,c="foo", 无类型整型和字符串常量
```

Go的常量定义可以限定常量类型,但不是必需的。如果定义常量时没有指定类型,那么它 与字面常量一样,是无类型常量。
 常量定义的右值也可以是一个在编译期运算的常量表达式,比如

```golang
const mask = 1 << 3
```

由于常量的赋值是一个编译期行为,所以右值不能出现任何需要运行期才能得出结果的表达
 式

- 预定义常量

Go语言预定义了这些常量:true、false和iota

iota比较特殊,可以被认为是一个可被编译器修改的常量,在每一个const关键字出现时被重置为0,然后在下一个const出现之前,每出现一次iota,其所代表的数字会自动增1

```golang
const (         // iota被重设为0
    c0 = iota   // c0 == 0
    c1 = iota   // c0 == 1
    c2 = iota   // c0 == 2
)

const (
    a = 1 << iota //a == 1 (iota在每个const开头被重设为0)
    b = 1 << iota //a == 2 (iota在每个const开头被重设为0)
    c = 1 << iota //a == 4 (iota在每个const开头被重设为0)
)
const ( 
    u = iota * 42   //u == 0
    v = iota * 42   //v==42.0
    w = iota * 42   //v==84.0
)

const x = iota // x == 0 (因为iota又被重设为0了)
const y = iota // y == 0 (同上)
```

如果两个const的赋值语句的表达式是一样的,那么可以省略后一个赋值表达式。因此,上面的前两个const语句可简写为:

```golang
const (         // iota被重设为0
    c0 = iota   // c0 == 0
    c1          // c0 == 1
    c2          // c0 == 2
)

const (
    a = 1 << iota //a == 1 (iota在每个const开头被重设为0)
    b             //a == 2 (iota在每个const开头被重设为0)
    c             //a == 4 (iota在每个const开头被重设为0)
)
const ( 
    u = iota * 42   //u == 0
    v               //v==42.0
    w               //v==84.0
)
```

- 枚举

枚举指一系列相关的常量,比如下面关于一个星期中每天的定义。

```go
const (
    Sunday = iota
    Monday
    Tuesday
    Wednesday
    Thursday
    Friday
    Saturday
    numberOfDays    // 这个常量没有导出
)
```

同Go语言的其他符号(symbol)一样,以大写字母开头的常量在包外可见。
 )
 以上例子中numberOfDays为包内私有,其他符号则可被其他包访问。

1. 类型

基础类型

- 布尔类型:bool。

Go语言中的布尔类型与其他语言基本一致,关键字也为bool,可赋值为预定义的true和false示例代码如下:

```golang
var v1 bool
v1 = true
v2 := (1 == 2) // v2也会被推导为bool类型
```

布尔类型不能接受其他类型的赋值,不支持自动或强制的类型转换。

- 整型:int8、byte、int16、int、uint、uintptr等。 

整型是所有编程语言里最基础的数据类型。

| 类型          | 长度(字节) | 值范围                                    |
| ------------- | ---------- | ----------------------------------------- |
| int8          | 1          | -128 ~ 127                               |
| uint8(即byte) | 1          | 0~255                                     |
| int16         | 2          | -32768~32767                              |
| uint16        | 2          | 0~65535                                   |
| int32         | 4          | -2147483648~2147483647                   |
| uint32        | 4          | 0~4294967295                              |
| int64         | 8          | -9223372036854775808~9223372036854775807 |
| uint64        | 8          | 0~18446744073709551615                    |
| int           | 平台相关   | 平台相关                                  |
| uint          | 平台相关   | 平台相关                                  |
| uintptr       | 同指针     | 在32位平台下为4字节,64位平台下为8字节     |

int和int32在Go语言里被认为是两种不同的类型,编译器也不会帮你自动 做类型转换

```golang
var value2 int32
value1 := 64 // value1将会被自动推导为int类型
value2 = int32(value1) // 编译通过
```

当然,开发者在做强制类型转换时,需要注意数据长度被截短而发生的数据精度损失(比如
 将浮点数强制转为整数)和值溢出(值超过转换的目标类型的值范围时)问题。

两个不同类型的整型数不能直接比较,比如int8类型的数和int类型的数不能直接比较,但各种类型的整型变量都可以直接与字面常量(literal)进行比较

```golang
var i int32
var j int64
i, j = 1, 2
if i==j{ // 编译错误 
    fmt.Println("i and j are equal.")
}
if i==1 || j==2{// 编译通过 
    fmt.Println("i and j are equal.")
}
```

位运算

| 运算   | 含义 |
| ------ | ---- |
| x << y | 左移 |
| x >> y | 右移 |
| x^y    | 异或 |
| x&y    | 与   |
| x\|y   | 或   |
| ^x     | 取反 |

- 浮点类型:float32、float64。

float32等价于C语言的float类型, float64等价于C语言的double类型。

```golang
var fvalue1 float32
fvalue1 = 12
fvalue2 := 12.0 // 如果不加小数点,fvalue2会被推导为整型而不是浮点型
```

以上例子中类型被自动推导的fvalue2,需要注意的是其类型将被自动设为float64, 而不管赋给它的数字是否是用32位长度表示的。

因为浮点数不是一种精确的表达方式,所以像整型那样直接用==来判断两个浮点数是否相等 是不可行的,这可能会导致不稳定的结果。

```golang
import "math"

// p为用户自定义的比较精度,比如0.00001 

func IsEqual(f1, f2, p float64) bool {
    return math.Fdim(f1, f2) < p 
}
```

- 复数类型:complex64、complex128。 

复数实际上由两个实数(在计算机中用浮点数表示)构成,一个表示实部(real),一个表示 虚部(imag)。

```golang
var value1 complex64
value1 = 3.2 + 12i
value2 := 3.2 + 12i
value3 := complex(3.2, 12)
```

对于一个复数z = complex(x,y),就可以通过Go语言内置函数real(z)获得该复数的实部,也就是x,通过imag(z)获得该复数的虚部,也就是y。

- 字符串:string。

```golang
var str string // 声明一个字符串变量
str = "Hello world" // 字符串赋值
ch := str[0] // 取字符串的第一个字符
fmt.Printf("The length of \"%s\" is %d \n", str, len(str)) fmt.Printf("The first character of \"%s\" is %c.\n", str, ch)
```

字符串的内容可以用类似于数组下标的方式获取,但与数组不同,字符串的内容不能在初始 化后被修改

Go语言仅支持UTF-8和Unicode编码。对于其他编码,Go语言标准库并没有内置的编码转换支持。

字符串遍历

```golang
//方式一
str := "Hello,世界"
n := len(str)
for i := 0; i < n; i++ {
ch := str[i] // 依据下标取字符串中的字符,类型为byte
    fmt.Println(i, ch)
}

//方式二
str := "Hello,世界"
for i, ch := range str {
    fmt.Println(i, ch)//ch的类型为rune 
}
```

- 字符类型:rune。

在Go语言中支持两个字符类型,一个是byte(实际上是uint8的别名),代表UTF-8字符串的单个字节的值;另一个是rune,代表单个Unicode字符。

- 错误类型:error。

复合类型:

- 指针(pointer)
- 数组(array)

一些常规的数组声明方法:

```golang
[32]byte // 长度为32的数组,每个元素为一个字节 
[2*N] struct { x, y int32 } // 复杂类型数组
[1000]*float64  // 指针数组
[3][5]int  // 二维数组
[2][2][2]float64 // 等同于[2]([2]([2]float64))

arrLength := len(arr)

for i, v := range array {
    fmt.Println("Array element[", i, "]=", v)
}
```

数组长度在定义后就不可更改,在声明时长度可以为一个常量或者一个常量 表达式(常量表达式是指在编译期即可计算结果的表达式)。

需要特别注意的是,在Go语言中数组是一个值类型(value type)。所有的值类型变量在赋值和作为参数传递时都将产生一次复制动作。

```golang
package main

import "fmt"

func modify(array [10]int) {
    array[0] = 10 // 试图修改数组的第一个元素 fmt.Println("In modify(), array values:", array)
}
func main() {
    array := [5]int{1,2,3,4,5} // 定义并初始化一个数组
    modify(array) // 传递给一个函数,并试图在函数体内修改这个数组内容
    fmt.Println("In main(), array values:", array)
}
```

结果

```text
In modify(), array values: [10 2 3 4 5]
In main(), array values: [1 2 3 4 5]
```

- 切片(slice)

数组切片就像一个指向数组的指针,实际上它拥有自己的数据结构,而不仅仅是 个指针。数组切片的数据结构可以抽象为以下3个变量: 一个指向原生数组的指针;数组切片中的元素个数;数组切片已分配的存储空间。

```golang
package main
import "fmt"
func main() {
    // 先定义一个数组
    var myArray [10]int = [10]int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10} // 基于数组创建一个数组切片
    var mySlice []int = myArray[:5]
    fmt.Println("Elements of myArray: ") 
    for _, v := range myArray {
        fmt.Print(v, " ")
    }
    fmt.Println("\nElements of mySlice: ")
    for _, v := range mySlice {
        fmt.Print(v, " ")
    }
    fmt.Println()
}
```

Go语言支持用myArray[first:last]这样的方式来基于数组生成一 个数组切片,而且这个用法还很灵活

```golang
//创建一个初始元素个数为5的数组切片,元素初始值为0:
mySlice1 := make([]int, 5) 
//创建一个初始元素个数为5的数组切片,元素初始值为0,并预留10个元素的存储空间:
mySlice2 := make([]int, 5, 10) 
//直接创建并初始化包含5个元素的数组切片:
mySlice3 := []int{1, 2, 3, 4, 5}
```

可动态增减元素是数组切片比数组更为强大的功能。与数组相比,数组切片多了一个存储能 力(capacity)的概念,即元素个数和分配的空间可以是两个不同的值。

```golang
package main
import "fmt" func main() {
mySlice := make([]int, 5, 10)
fmt.Println("len(mySlice):", len(mySlice))
fmt.Println("cap(mySlice):", cap(mySlice)) }
```

结果

```text
len(mySlice): 5
cap(mySlice): 10
```

函数:

append:在末尾添加元素或者切片

cap:切片空间

len:切片长度

copy:复制。加入的两个数组切片不一样大,就会按其中较小的那个数组切片的元素个数进行 复制。

```go
mySlice = append(mySlice, 1, 2, 3)

mySlice2 := []int{8, 9, 10}
// 给mySlice后面添加另一个数组切片
mySlice = append(mySlice, mySlice2...)


slice1 := []int{1, 2, 3, 4, 5} slice2 := []int{5, 4, 3}
copy(slice2, slice1) // 只会复制slice1的前3个元素到slice2中 copy(slice1, slice2) // 只会复制slice2的3个元素到slice1的前3个位置
```

- 字典(map)

```golang
package main
import "fmt"
// PersonInfo是一个包含个人详细信息的类型 
type PersonInfo struct {
    ID string
    Name string Address string
}
func main() {
    var personDB map[string] PersonInfo
    personDB = make(map[string] PersonInfo)
    // 往这个map里插入几条数据
    personDB["12345"] = PersonInfo{"12345", "Tom", "Room 203,..."} personDB["1"] = PersonInfo{"1", "Jack", "Room 101,..."}
    // 从这个map查找键为"1234"的信息 
    person, ok := personDB["1234"]
    // ok是一个返回的bool型,返回true表示找到了对应的数据 
    if ok {
        fmt.Println("Found person", person.Name, "with ID 1234.")
    } else {
        fmt.Println("Did not find person with ID 1234.")
    }
}
//声明
var myMap map[string] PersonInfo
//创建
myMap = make(map[string] PersonInfo)
//创建了一个初始存储能力为100的map
myMap = make(map[string] PersonInfo, 100)
myMap = map[string] PersonInfo{
    "1234": PersonInfo{"1", "Jack", "Room 101,..."},
}
//赋值
myMap["1234"] = PersonInfo{"1", "Jack", "Room 101,..."}
//删除
delete(myMap, "1234")
//元素查找
value, ok := myMap["1234"] 
if ok{// 找到了
    // 处理找到的value 
}
```

- 通道(chan)
- 结构体(struct)
- 接口(interface)

1. 流程控制

- 条件 if,else,else if

条件语句不需要使用括号将条件包含起来();

无论语句体内有几条语句,花括号{}都是必须存在的;

左花括号{必须与if或者else处于同一行;

有返回值的函数中,不允许将“最终的”return语句包含在if...else...结构中

- 选择 switch,case,select

```golang
switch i { 
    case 0:
        fmt.Printf("0") 
    case 1:
        fmt.Printf("1") 
    case 2:
        fallthrough 
    case 3:
        fmt.Printf("3") 
    case 4, 5, 6:
        fmt.Printf("4, 5, 6") 
    default:
        fmt.Printf("Default")
}


switch {
    case 0 <= Num && Num <= 3:
        fmt.Printf("0-3")
    case 4 <= Num && Num <= 6:
        fmt.Printf("4-6")
    case 7 <= Num && Num <= 9:
        fmt.Printf("7-9")
}
```

结果

```text
i = 0时,输出0;
i = 1时,输出1;
i = 2时,输出3;
i = 3时,输出3;
i = 4时,输出4, 5, 6;
i = 5时,输出4, 5, 6;
i = 6时,输出4, 5, 6;
i = 其他任意值时,输出Default。
```

只有在case中明确添加fallthrough关键字,才会继续执行紧跟的下一个case;

条件表达式不限制为常量或者整数;

单个case中,可以出现多个结果选项;

与C语言等规则相反,Go语言不需要用break来明确退出一个case;

- 循环 for,range

与多数语言不同的是,Go语言中的循环语句只支持for关键字,而不支持while和do-while 结构。

```golang
sum := 0 
for {
    sum++
    if sum > 100 {
       break 
    }
}
```

Go语言的for循环同样支持continue和break来控制循环,但是它提供了一个更高级的break,可以选择中断哪一个循环

```golang
for j := 0; j < 5; j++ {
    for i := 0; i < 10; i++ {
        if i > 5 { 
            break JLoop
        
        fmt.Println(i)
    } 
}
JLoop: // break语句终止的是JLoop标签处的外层循环。
//
```

- 跳转 goto
- break,continue,fallthrough

1. 函数

```golang
package mymath 
import "errors"
func Add(a int, b int) (ret int, err error) {
    if a < 0 || b < 0 { // 假设这个函数只支持两个非负数字的加法
        err= errors.New("Should be non-negative numbers!")
    return
}
return a + b, nil // 支持多重返回值 }
```

如果参数列表中若干个相邻的参数类型的相同,比如上面例子中的a和b,则可以在参数列表 中省略前面变量的类型声明

如果返回值列表中多个返回值的类型相同,也可以用同样的方式合并

小写字母开头的函数只在本包内可见,大写字母开头的函数才能被其他包使用。

- 不定参数类型:...type本质上是一个数组切片,也就是[]type

```golang
func myfunc(args ...int) {
    for _, arg := range args {
        fmt.Println(arg)
    }
}
```

- 定参数的传递

```golang
func myfunc(args ...int) { 
    // 按原样传递
    myfunc3(args...)
    // 传递片段,实际上任意的int slice都可以传进去
    myfunc3(args[1:]...)
}
```

- 任意类型的不定参数

如果你希望传任意类型,可以指定类型为 interface{}

```golang
func Printf(format string, args ...interface{}) { 
    // ...
}

package main
import "fmt"
func MyPrintf(args ...interface{}) { 
    for _, arg := range args {
        switch arg.(type) { 
            case int:
                fmt.Println(arg, "is an int value.") 
            case string:
                fmt.Println(arg, "is a string value.") 
            case int64:
                fmt.Println(arg, "is an int64 value.") 
            default:
                fmt.Println(arg, "is an unknown type.")
        }
    }
}
```

- 匿名函数

匿名函数可以直接赋值给一个变量或者直接执行

```golang
f := func(x, y int) int { 
    return x + y
}
func(ch chan int) { 
    ch <- ACK
} (reply_chan) // 花括号后直接跟参数列表表示函数调用
```

- defer 相当于c++的析构函数和java中的finally

```golang
defer func() {
    // 做你复杂的清理工作
} ()
```

- panic()和recover()

Go语言引入了两个内置函数panic()和recover()以报告和处理运行时错误和程序中的错误场景:

```golang
func panic(interface{}) 
func recover() interface{}

panic(404)
panic("network broken") 
panic(Error("file not exists"))
```

当在一个函数执行过程中调用panic()函数时,正常的函数执行流程将立即终止,但函数中  之前使用defer关键字延迟执行的语句将正常展开执行,之后该函数将返回到调用函数,并导致  逐层向上执行panic流程,直至所属的goroutine中所有正在执行的函数被终止。

recover()函数用于终止错误处理流程。一般情况下,recover()应该在一个使用defer 关键字的函数中执行以有效截取错误处理流程。

```golang
defer func() {
    if r := recover(); r != nil {
        log.Printf("Runtime error caught: %v", r)
    }
}()
```

- 快迅解析命令行参数的flag包。

```golang
package main
import "flag"

import "fmt"
var infile *string = flag.String("i", "infile", "File contains values for sorting") 
var outfile *string = flag.String("o", "outfile", "File to receive sorted values") 
var algorithm *string = flag.String("a", "qsort", "Sort algorithm")
func main() { 
    flag.Parse()
    if infile != nil {
        fmt.Println("infile =", *infile, "outfile =", *outfile,"algorithm =",*algorithm)
    } 
}
```

调用:

```shell
$ go build sorter.go
$ ./sorter -i unsorted.dat -o sorted.dat -a bubblesort
#结果
#infile = unsorted.dat outfile = sorted.dat algorithm = bubblesort
```

1. 面向对象

- 引用类型

channel和map类似,本质上是一个指针。将它们设计为引用类型而不是统一的值类型的原因 是,完整复制一个channel或map并不是常规需求。同样,接口具备引用语义,是因为内部维持了两个指针

```golang
type interface struct { 
    data *void
    itab *Itab 
}
```

- 所有的Go语言类型(指针类型除外)都可以有自己的方法。
- 初始化

```golang
type Rect struct { 
    x, y float64
    width, height float64 
}

rect1 := new(Rect)
rect2 := &Rect{}
rect3 := &Rect{0, 0, 100, 200}
rect4 := &Rect{width: 100, height: 200}
```

在Go语言中,未进行显式初始化的变量都会被初始化为该类型的零值,例如bool类型的零 值为false,int类型的零值为0,string类型的零值为空字符串。

在Go语言中没有构造函数的概念,对象的创建通常交由一个全局的创建函数来完成,以 NewXXX来命名,表示“构造函数”:

```golang
func NewRect(x, y, width, height float64) *Rect { 
    return &Rect{x, y, width, height}
}
```

- 可访问性

需要注意的一点是,Go语言中符号的可访问性是包一级的而不是类型一级的。在上面的例 子中,尽管area()是Rect的内部方法,但同一个包中的其他类型也都可以访问到它。

1. 接口

接口赋值并不要求两个接口必须等价。如果接口A的方法列表是接口B的方法列表的子集, 那么接口B可以赋值给接口A

- 接口查询,让Writer接口转换为two.IStream

```golang
type Reader interface {
    Read(buf []byte) (n int, err error)
}
type Writer interface {
    Write(buf []byte) (n int, err error)
}

type IStream interface {
    Write(buf []byte) (n int, err error) 
    Read(buf []byte) (n int, err error)
}

var file1 Writer = ...
if file5, ok := file1.(two.IStream); ok {
    ... 
}
```

- 类型查询

```golang
var v1 interface{} = ... 
switch v := v1.(type) {
    case int: // 现在v的类型是int 
    case string: // 现在v的类型是string 
    ...
}
```

- 接口组合

```golang
// ReadWriter接口将基本的Read和Write方法组合起来 
type ReadWriter interface {
    Reader
    Writer 
}
```

- Any类型

由于Go语言中任何对象实例都满足空接口interface{},所以interface{}看起来像是可以指向任何对象的Any类型

1. 并发

- go

goroutine是Go语言中的轻量级线程实现,由Go运行时(runtime)管理。

```golang
func Add(x, y int) { z := x + y
    fmt.Println(z)
}
go Add(1, 1)
package main
import "fmt" 
import "sync" 
import "runtime"

var counter int = 0


func Count(lock *sync.Mutex) { 
    lock.Lock()
    counter++
    fmt.Println(z)
    lock.Unlock()
}

func main() {
    lock := &sync.Mutex{}
    for i := 0; i < 10; i++ { 
        go Count(lock)
    }
    
    for {
        lock.Lock()
        
        c := counter
        
        lock.Unlock()
        runtime.Gosched()//让出CPU时间
        if c >= 10 {
            break
        }
    }
}
```

- chan

Go语言提供的是另一种通信模型,即以消息机制而非共享内存作为通信方式。

channel是Go语言在语言级别提供的goroutine间的通信方式。我们可以使用channel在两个或 多个goroutine之间传递消息。

```golang
package main
import "fmt"
func Count(ch chan int) { 
    ch <- 1
    fmt.Println("Counting")
}
func main() {
    chs := make([]chan int, 10) 
    for i := 0; i < 10; i++ {
        chs[i] = make(chan int)
        go Count(chs[i]) 
    }
    for _, ch := range(chs) { 
        <-ch
    }
}
```

- select

Go语言直接在语言级别支持select关键字,用于处理异步IO 问题。select有比较多的限制,其中最大的一条限制就是每个case语句里必须是一个IO操作

```golang
select {
    case <-chan1:
        // 如果chan1成功读到数据,则进行该case处理语句 
    case chan2 <- 1:
        // 如果成功向chan2写入数据,则进行该case处理语句 
    default:
        // 如果上面都没有成功,则进入default处理流程 
}
```

- 缓冲

之前我们示范创建的都是不带缓冲的channel,这种做法对于传递单个数据的场景可以接受,但对于需要持续传输大量数据的场景就有些不合适了。

要创建一个带缓冲的channel,其实也非常容易:

```golang
c := make(chan int, 1024)
```

从带缓冲的channel中读取数据可以使用与常规非缓冲channel完全一致的方法,但我们也可 以使用range关键来实现更为简便的循环读取:

```golang
for i := range c { 
    fmt.Println("Received:", i)
}
```

- 超时处理
   虽然select机制不是专为超时而设计的,却能很方便地解决超时问题。因为select的特点是只要其中一个case已经 完成,程序就会继续往下执行,而不会考虑其他case的情况。

```golang
// 首先,我们实现并执行一个匿名的超时等待函数 
timeout := make(chan bool, 1)

go func() {
    time.Sleep(1e9) // 等待1秒钟
    timeout <- true 
}()

// 然后我们把timeout这个channel利用起来 
select {
    case <-ch:
        // 从ch中读取到数据
    case <-timeout:
        // 一直没有从ch中读取到数据,但从timeout中读取到了数据
}
```

- 单向channel

```golang
var ch1 chan int // ch1是一个正常的channel,不是单向的
var ch2 chan<- float64// ch2是单向channel,只用于写float64数据
var ch3 <-chan int // ch3是单向channel,只用于读取int数据

ch4 := make(chan int)
ch5 := <-chan int(ch4) // ch5就是一个单向的读取channel 
ch6 := chan<- int(ch4) // ch6 是一个单向的写入channel

//单向channel的用法
func Parse(ch <-chan int) { 
    for value := range ch {
        fmt.Println("Parsing value", value)
    }
}
```

- 关闭channel

```golang
//判断channel是否被关闭
x, ok := <-ch

//关闭channel
close(ch)
```

- 同步锁

sync包提供了两种锁类型:sync.Mutex和sync.RWMutex。

```golang
var l sync.Mutex func foo() {
    l.Lock()
    defer l.Unlock()
    //...
}
```

- 全局唯一性操作

```go
var a string
var once sync.Once
func setup() {
    a = "hello, world"
}
func doprint() { 
    once.Do(setup)
    print(a) 
}
func twoprint() { 
    go doprint() 
    go doprint()
}
```

1. 网络编程

Go语言标准库对此过程进行了抽象和封装。无论我们期望使用什么协议建立什么形式的连接,都只需要调用net.Dial()即可。

```golang
func Dial(net, addr string) (Conn, error)

//TCP链接:
conn, err := net.Dial("tcp", "192.168.0.10:2100")

//UDP链接:
conn, err := net.Dial("udp", "192.168.0.12:975")

//ICMP链接(使用协议名称):
conn, err := net.Dial("ip4:icmp", "www.baidu.com")

//ICMP链接(使用协议编号):
conn, err := net.Dial("ip4:1", "10.0.0.3")
```

目前,Dial()函数支持如下几种网络协议:"tcp"、"tcp4"(仅限IPv4)、"tcp6"(仅限 IPv6)、"udp"、"udp4"(仅限IPv4)、"udp6"(仅限IPv6)、"ip"、"ip4"(仅限IPv4)和"ip6"(仅限IPv6)。

实际上,Dial()函数是对DialTCP()、DialUDP()、DialIP()和DialUnix()的封装。我们也可以直接调用这些函数,它们的功能是一致的。

```golong
func DialTCP(net string, laddr, raddr *TCPAddr) (c *TCPConn, err error) 
func DialUDP(net string, laddr, raddr *UDPAddr) (c *UDPConn, err error) 
func DialIP(netProto string, laddr, raddr *IPAddr) (*IPConn, error)
func DialUnix(net string, laddr, raddr *UnixAddr) (c *UnixConn, err error
```

- 工具包

net.ResolveTCPAddr(),用于解析地址和端口号;

net.DialTCP(),用于建立链接。

func net.ParseIP(),验证IP地址有效性

func IPv4Mask(a, b, c, d byte) IPMask,创建子网掩码

func (ip IP) DefaultMask() IPMask,获取默认子网掩码

根据域名查找IP:

```golang
func ResolveIPAddr(net, addr string) (*IPAddr, error){}
func LookupHost(name string) (cname string, addrs []string, err error){}
```

- HTTP客户端

```golang
func (c *Client) Get(url string) (r *Response, err error){}
func (c *Client) Post(url string, bodyType string, body io.Reader) (r *Response, err error){}
func (c *Client) PostForm(url string, data url.Values) (r *Response, err error) {}
func (c *Client) Head(url string) (r *Response, err error){}
func (c *Client) Do(req *Request) (resp *Response, err error){}
```

http.Get() 等价于http.DefaultClient.Get()

```golang
resp, err := http.Get("http://example.com/") 
if err != nil {
    // 处理错误 ...
    return
}
defer resp.Body.close() 
io.Copy(os.Stdout, resp.Body)
```

添加cookie

```golang
req, err := http.NewRequest("GET", "http://example.com", nil) 
// ...
req.Header.Add("User-Agent", "Gobook Custom User-Agent")
// ...
client := &http.Client{ //... }
resp, err := client.Do(req)
// ...
```

DisableKeepAlives bool：是否取消长连接,默认值为 false,即启用长连接。

DisableCompression bool 是否取消压缩(GZip),默认值为 false,即启用压缩。

MaxIdleConnsPerHost int 指定与每个请求的目标主机之间的最大非活跃连接(keep-alive)数量。如果不指定,默认使
 用 DefaultMaxIdleConnsPerHost 的常量值。

func(t *Transport) CloseIdleConnections()。该方法用于关闭所有非活跃的
 连接

func(t *Transport) RegisterProtocol(scheme string, rt RoundTripper)。
 该方法可用于注册并启用一个新的传输协议

func(t *Transport) RoundTrip(req *Request) (resp *Response, err error)。
 用于实现 http.RoundTripper 接口

```golong
tr := &http.Transport{
    TLSClientConfig: &tls.Config{RootCAs:  pool}, 
    DisableCompression: true,
}
client := &http.Client{Transport: tr}
resp, err := client.Get("https://example.com")
```

通常,我们可以在默认的 http.Transport 之上包一层 Transport 并实现 RoundTrip() 方法

```golang
package main
import( 
    "net/http"
)
type OurCustomTransport struct { 
    Transport http.RoundTripper
}
func (t *OurCustomTransport) transport() http.RoundTripper { 
    if t.Transport != nil {
        return t.Transport 
    }
    return http.DefaultTransport
}

func (t *OurCustomTransport) RoundTrip(req *http.Request) (*http.Response, error) { 
    // 处理一些事情 ...
    // 发起HTTP请求
    // 添加一些域到req.Header中
    return t.transport().RoundTrip(req)
}

func (t *OurCustomTransport) Client() *http.Client { 
    return &http.Client{Transport: t}
}

func main() {
    t := &OurCustomTransport{ 
        //...
    }
    c := t.Client()
    resp, err := c.Get("http://example.com")
    // ...
}
```

- HTTP服务端

使用 net/http 包提供的http.ListenAndServe()方法,可以在指定的地址进行监听, 开启一个HTTP,服务端该方法的原型如下:

```golang
func ListenAndServe(addr string, handler Handler) error
```

该方法有两个参数:第一个参数 addr 即监听地址;第二个参数表示服务端处理程序, 通常为空,这意味着服务端调用  http.DefaultServeMux 进行处理,而服务端编写的业务逻 辑处理程序 http.Handle() 或  http.HandleFunc() 默认注入 http.DefaultServeMux 中

```golang
http.Handle("/foo", fooHandler)
http.HandleFunc("/bar", func(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, %q", html.EscapeString(r.URL.Path))
})
log.Fatal(http.ListenAndServe(":8080", nil))
```

如果想更多地控制服务端的行为,可以自定义 http.Server

```golang
s := &http.Server{
    Addr:"8080",
    Handler:myHander,
    ReadTimeout:10*time.Second,
    WriteTimeout:10*time.Second,
    MaxHeaderBytes: 1 << 20,   
}
log.Fatal(s.ListenAndServe())
```

1. JSON 处理

使用json.Marshal()函数可以对一组数据进行JSON格式的编码。

```golang
func Marshal(v interface{}) ([]byte, error)
```

Go语言的大多数数据类型都可以转化为有效的JSON文本,但channel、complex和函数这几种 类型除外。

如果转化前的数据结构中出现指针,那么将会转化指针所指向的值,如果指针指向的是零值, 那么null将作为转化后的结果输出。

数组和切片会转化为JSON里边的数组,但[]byte类型的值将会被转化为 Base64编码后的字符串,slice类型的零值会被转化为 null。

字符串将以UTF-8编码转化输出为Unicode字符集的字符串,特殊字符比如<将会被转义为\u003c。

结构体会转化为JSON对象,并且只有结构体里边以大写字母开头的可被导出的字段才会被转化输出,而这些可导出的字段会作为JSON对象的字符串索引。

转化一个map类型的数据结构时,该数据的类型必须是 map[string]T(T可以是
 encoding/json 包支持的任意数据类型)。

- 解码JSON数据

```golang
func Unmarshal(data []byte, v interface{}) error
```

如果JSON中的字段在Go目标类型中不存在,json.Unmarshal()函数在解码过程中会丢弃 该字段。

- 解码未知结构的JSON数据

如果要解码一段未知结构的JSON,只需将这段JSON数据解码输出到一个空接口即可。

JSON中的布尔值将会转换为Go中的bool类型; 

数值会被转换为Go中的float64类型;

字符串转换后还是string类型;

JSON数组会转换为[]interface{}类型;

JSON对象会转换为map[string]interface{}类型;  null值会转换为nil。

```golang
var r interface{} err := json.Unmarshal(b, &r)
gobook, ok := r.(map[string]interface{})
if ok {
for k, v := range gobook {
    switch v2 := v.(type) { 
        case string:
            fmt.Println(k, "is string", v2) 
        case int:
            fmt.Println(k, "is int", v2) 
        case bool:
            fmt.Println(k, "is bool", v2) 
        case []interface{}:
            fmt.Println(k, "is an array:") 
            for i, iv := range v2 {
                fmt.Println(i, iv)
            }
        default:
            fmt.Println(k, "is another type not handle yet")
      } 
    }
}
```

- JSON的流式读写

```golang
func NewDecoder(r io.Reader) *Decoder{}
func NewEncoder(w io.Writer) *Encoder{}

package main import (
        "encoding/json"
        "log"
        "os"
)
func main() {
    dec := json.NewDecoder(os.Stdin) 
    enc := json.NewEncoder(os.Stdout) 
    for {
        var v map[string]interface{}
        if err := dec.Decode(&v); err != nil {
            log.Println(err)
            return
        }
        for k := range v {
            if k != "Title" { 
                v[k] = nil, false
            }
        }
        if err := enc.Encode(&v); err != nil { 
            log.Println(err)
        }
    }
}
```

1. 网站程序

```golang
package main

import ( 
    "io"
    "log"
    "net/http" 
)

func helloHandler(w http.ResponseWriter, r *http.Request) {               io.WriteString(w, "Hello, world!")
}
func main() {
    http.HandleFunc("/hello", helloHandler) 
    err := http.ListenAndServe(":8080", nil) 
    if err != nil {
        log.Fatal("ListenAndServe: ", err.Error())
    }
}
```

- 渲染网页模板

使用Go标准库提供的html/template包,可以让我们将HTML从业务逻辑程序中抽离出来 形成独立的模板文件,这样业务逻辑程序只负责处理业务逻辑部分和提供模板需要的数据,模板 文件负责数据要表现的具体形式。

双大括号{{}}是区分模板代码和HTML的分隔符,括号里边可以是要显示输 出的数据,或者是控制语句,比如if判断式或者range循环体等。

在使用range语句遍 历的过程中,.即表示该循环体中的当前元素,.|formatter表示对当前这个元素的值以 formatter 方式进行格式化输出

.|urlquery}即表示对当前元素的值进行转换以适合作为URL一部 分,而{{.|html 表示对当前元素的值进行适合用于HTML 显示的字符转化

```html
<!doctype html>
<html>
    <head>
        <meta charset="utf-8">
        <title>List</title>
    </head>
    <body>
        <ol>
            {{range $.images}}
            <li><a href="/view?id={{.|urlquery}}">{{.|html}}</a></li>
            {{end}}
        </ol>
    </body>
</html>
```

如果要更改模板中默认的分隔符,可以使用template包提供的Delims()方法。

```golang
package main
import ( 
    "io"
    "log"
    "net/http"
    "io/ioutil"
    "html/template"
)
func uploadHandler(w http.ResponseWriter, r *http.Request) { 
    if r.Method == "GET" {
        t, err := template.ParseFiles("upload.html") 
        if err != nil {
            http.Error(w, err.Error(),http.StatusInternalServerError)
            return
        }
        t.Execute(w, nil) return
    }
    if r.Method == "POST" {
        // ... 
    }
}
func listHandler(w http.ResponseWriter, r *http.Request) {          
    fileInfoArr, err := ioutil.ReadDir("./uploads")
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError) 
        return
    }
    locals := make(map[string]interface{}) 
    images := []string{}
    for _, fileInfo := range fileInfoArr {
        images = append(images, fileInfo.Name) 
    }
    locals["images"] = images 
    t, err := template.ParseFiles("list.html") 
    if err != nil {
        http.Error(w, err.Error(), http.StatusInternalServerError) 
        return
    }
    t.Execute(w, locals)
}
```

- 模板缓存

```golang
templates := make(map[string]*template.Template)
func init() {
    for _, tmpl := range []string{"upload", "list"} {
        t := template.Must(template.ParseFiles(tmpl + ".html"))
        templates[tmpl] = t
    }
}
```

- 巧用闭包避免程序运行时出错崩溃

我们定义了一个名为 safeHandler() 的函数,该函数有一个参数并且返回一个值,传入的参数和返回值都是一个函数,且都是http.  HandlerFunc类型,这种类型的函数有两个参数:http.ResponseWriter和 *http.Request。函  数规格同photoweb 的业务逻辑处理函数完全一致。

```golang
func safeHandler(fn http.HandlerFunc) http.HandlerFunc { 
    return func(w http.ResponseWriter, r *http.Request) {
        defer func() {
            if e, ok := recover().(error); ok {
                http.Error(w, err.Error(),http.StatusInternalServerError) // 或者输出自定义的 50x 错误页面
                // w.WriteHeader(http.StatusInternalServerError)
                // renderHtml(w, "error", e)
                // logging
                log.Println("WARN: panic in %v - %v", fn, e)
                log.Println(string(debug.Stack()))
            }
        }()
        fn(w,r)
    }
}
```

要应用safeHandler()函数,只需在main()中对各个业务逻辑处理函数做一次包装,如下 面的代码所示:

```golang
func main() {
    http.HandleFunc("/", safeHandler(listHandler))
    http.HandleFunc("/view", safeHandler(viewHandler))
    http.HandleFunc("/upload", safeHandler(uploadHandler)) 
    err := http.ListenAndServe(":8080", nil)
    if err != nil {
        log.Fatal("ListenAndServe: ", err.Error())
    }
}
```

- 动态请求和静态资源分离

```golang
const (
    ListDir = 0x0001
)

func staticDirHandler(mux *http.ServeMux, prefix string, staticDir string, flags int) {
    mux.HandleFunc(prefix, func(w http.ResponseWriter, r *http.Request) { 
        file := staticDir + r.URL.Path[len(prefix)-1:]
        if (flags & ListDir) == 0 {
            if exists := isExists(file); !exists { 
                http.NotFound(w, r)
                return
            }
        }
        http.ServeFile(w, r, file)
    })
}

func main() {
    mux := http.NewServeMux()
    staticDirHandler(mux, "/assets/", "./public", 0) mux.HandleFunc("/", safeHandler(listHandler)) mux.HandleFunc("/view", safeHandler(viewHandler)) mux.HandleFunc("/upload", safeHandler(uploadHandler)) err := http.ListenAndServe(":8080", mux)
    if err != nil {
        log.Fatal("ListenAndServe: ", err.Error())
    }
}
```

1. 加密

```golang
package main import(
    "fmt"
    "crypto/sha1"
    "crypto/md5"
)
func main(){ TestString:="Hi,pandaman!"
    Md5Inst:=md5.New()
    Md5Inst.Write([]byte(TestString))
    Result:=Md5Inst.Sum([]byte(""))
    fmt.Printf("%x\n\n",Result)
    Sha1Inst:=sha1.New()
    Sha1Inst.Write([]byte(TestString))
    Result=Sha1Inst.Sum([]byte(""))
    fmt.Printf("%x\n\n",Result)
}
```

1. 单元测试

单元测试源文件的命名规则如下:在需要测试的包下面创建以“_test”结尾的go文件,形 如[^.]*_test.go。

Go的单元测试函数分为两类:功能测试函数和性能测试函数,分别为以Test和Benchmark 6 为函数名前缀并以*testing.T为单一参数的函数。下面是测试函数声明的例子:

```golang
func TestAdd1(t *testing.T){}
func BenchmarkAdd1(t *testing.T){}

func TestAdd1(t *testing.T) { 
    r := Add(1, 2)
    if r != 2 { // 这里本该是3,故意改成2测试错误场景 
        t.Errorf("Add(1, 2) failed. Got %d, expected 3.", r)
    }
}

func BenchmarkAdd1(b *testing.B) { 
    for i := 0; i < b.N; i++ {
        Add(1, 2) 
    }
}
```

如果测试代码中一些准备工作的时间太长,我们也可以这样处理以明确排除这些准备工作所花费 时间对于性能测试的时间影响:

```golang
func BenchmarkAdd1(b *testing.B) {
    b.StopTimer() // 暂停计时器
    DoPreparation() // 一个耗时较长的准备工作,比如读文件 b.StartTimer() // 开启计时器,之前的准备时间未计入总花费时间内
    for i := 0; i < b.N; i++ { 
        Add(1, 2)
    }
}
```

性能单元测试的执行与功能测试一样简单,只不过调用时需要增加-test.bench参数

```shell
 $ go test–test.bench add.go
```

1. 反射

Type主要表达的是被反射的这个变量本身的类型信息,而Value则为该变量实例本身 的信息。

```golang
package main
import ( 
    "fmt"
    "reflect" 
)

func main() {
    var x float64 = 3.4
    fmt.Println("type:", reflect.TypeOf(x), " ;value:", reflect.ValueOf(x))
    v := reflect.ValueOf(x)
    fmt.Println("type:", v.Type(), " ;value:", v.Float(), "; kind:", v.Kind())//v.Kind() == reflect.Float64
    if v.CanSet(){
        v.Set(4.1)
    }else{
        p := reflect.ValueOf(&x) // 注意:得到X的地址
        fmt.Println("settability of p:" , p.CanSet())
        w := p.Elem()
        w.SetFloat(7.1)
        fmt.Println(w.Interface())
        fmt.Println(x)
    }
    
    
}
```

在 调用ValueOf()的地方,需要注意到x将会产生一个副本,因此ValueOf()内部对x的操作其实 都是对着x的一个副本。假如v允许调用Set(),那么我们也可以想象出,被修改的将是这个x的 副本,而不是x本身。

- 对结构的反射操作

```golang
type T struct { 
    A int
    B string
}
t := T{203, "mh203"}
s := reflect.ValueOf(&t).Elem() typeOfT := s.Type()
for i := 0; i < s.NumField(); i++ {
    f := s.Field(i)
    fmt.Printf("%d: %s %s = %v\n", i,typeOfT.Field(i).Name, f.Type(), f.Interface())
}
```

以上例子的输出为:

```text
0: A int = 203
1: B string = mh203
```

在试图修改成员的值时,也需要注意可赋值属性。

1. 语言的交互性

```golang
package hello
/*
#include <stdio.h> void hello() {
    printf("Hello, Cgo! -- From C world.\n");
}
*/
import "C"
func Hello() int { 
    return int(C.hello())
}
```

那就是如果这里的C代码需要依赖一个非C标准库的第三方库。Cgo提供了#cgo这样的 C文法,让开发者有机会定依赖的第三方库和编译选。

# cgo的第一种用法:

```golang
// #cgo CFLAGS: -DPNG_DEBUG=1 
// #cgo linux CFLAGS: -DLINUX=1 
// #cgo LDFLAGS: -lpng
// #include <png.h>
import "C"
```

# cgo还有另 外一种更简 一些的用法

```golang
// #cgo pkg-config: png cairo 
// #include <png.h>
import "C"
```

调用者可以用以下 的方式  得到错误码,在传递数组类型的参数时需要 意,在Go语言中将第一个元 的地 作为整个数组的起 始地 传入:

```golang
n, err := C.f(&array[0]) // 需要显示指定第一个元素的地址  
```

- 链接符号

接符号关心的是如何将语言文法使用的符号 化为 接期使用的符号

由于 Go 语言并无重载, 此语言的“ 接符号”由如下信息构成。

- [x] Package。Package 名可以是多层,例如A/B/C。
- [x] ClassType。 很特别的是,Go 语言中 ClassType 可以是  ,也可以不是。
- [x] Method。

其“ 接符号”的组成规则如下:

- [x] Package.Method 或 Package.ClassType·Method

```text
func New(cfg Config) *MockFS
func (fs *MockFS) Mkdir(dir string) (code int, err error) 
func (fs MockFS) Foo(bar Bar)
它们的 接符号分别为:
qbox.us/mockfs.New
qbox.us/mockfs.*MockFS·Mkdir
qbox.us/mockfs.MockFS·Foo
```

1. 常用包介绍

- fmt。它实现了格式化的输入输出操作,其中的fmt.Printf()和fmt.Println()是开发者使用最为频繁的函数。
- io。它实现了一系列非平台相关的IO相关接口和实现,比如提供了对os中系统相关的IO功能的封装。我们在进行流式读写(比如读写文件)时,通常会用到该包。
- bufio。它在io的基础上提供了缓存功能。在具备了缓存功能后,bufio可以比较方便地提供ReadLine之类的操作。
- strconv。本包提供字符串与基本数据类型互转的能力。
- os。本包提供了对操作系统功能的非平台相关访问接口。接口为Unix风格。提供的功能 包括文件操作、进程管理、信号和用户帐号等。
- sync。它提供了基本的同步原语。在多个goroutine访问共享资源的时候,需要使用sync中提供的锁机制。
- flag。它提供命令行参数的规则定义和传入参数解析的功能。绝大部分的命令行程序都需要用到这个包。
- encoding/json。JSON目前  用做网络程序中的通信格式。本包提供了对JSON的基本支持,比如从一个对象序列化为JSON字符 ,或者从JSON字符 反序列化出一个具体的对象等。
- http。它是一个强大而易用的包,也是Golang语言是一门“互联网语言”的最好 证。通过http包,只需要数行代码,可实现一个爬虫或者一个Web务器,这在传统语言中 是无法想象的。

![img](https://upload-images.jianshu.io/upload_images/8852308-e94e4ee405c26818.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

golang思维导图.png