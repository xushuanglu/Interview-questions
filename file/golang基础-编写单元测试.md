# golang基础-编写单元测试



# 1. Go测试

Go有一个内建的测试指令`go test`以及`testing`包，联合给出一个最小但完整的测试体验。
 标准工具链同时包含性能测试和基于语句的测试，代码覆盖率类似于NCover（`.NET`）或Istanbul（`Node.js`）.

## 1.1 编写单元测试

Go中单元测试与语言中的其他特性例如格式化或命名一样，遵循固有的语法。语法故意避免使用断言，开发人员需对值和行为进行检查。
 下面有个在`main`包中的待测试的示例方法。我们定义了一个名为`Sum`的导出函数，它接收两个整数，并将它们相加。

```go
package main

func Sum(x int, y int) int {
    return x + y
}

func main() {
    Sum(5, 5)
}
```

然后我们在一个独立的文件中编写测试用例。测试文件可以在一个不同的package(文件夹)或在同一个(`main`)。下面是加法运算的一个单元测试用例：

```css
package main

import "testing"

func TestSum(t *testing.T) {
    total := Sum(5, 5)
    if total != 10 {
       t.Errorf("Sum was incorrect, got: %d, want: %d.", total, 10)
    }
}
```

### Golang测试函数的特性：

- 第一个也是唯一的参数必须是`t *testing.T`
- 函数名称以`Test`开头,紧接着以大写字母开头的单词或短语
- 通常被测试的方法会长这样 i.e.`TestValidateClient`
- 调用`t.Error`或者`t.Fail`来表示错误（例子中调用`t.Errorf`来提供更多细节）
- `t.Log`可以用来提供无失败的调试信息
- 测试代码必须保持在一个命名为`something_test.go`的文件中，例如：`addition_test.go`

> 如果你的代码和测试用例在用一个文件夹，那么你可以使用`go run *.go`语句来执行测试用例。我倾向于使用`go build`创建一个二进制文件，然后再运行。

也许你更习惯于使用`Assert`关键字来执行检查，但是`The Go Programming Language`的作者对于超越断言的风格提出了一些好的论点。
 使用断言：

- 用例会感觉是用不同的语言在编写(RSpec/Mocha用于实例化)
- 错误被隐藏在 "assert: 0 == 1"
- 生成好几页的堆栈跟踪信息
- 测试执行会在出现第一个断言后退出-掩盖了大量的错误

> 有其他第三方库赋值了RSpec或Assert的感受。可以查看[stretchr/testify](https://links.jianshu.com/go?to=https%3A%2F%2Fgithub.com%2Fstretchr%2Ftestify)

## 测试表

"test tables"的概念是一系列测试输入和输出数值（切片数组）。这有一个`Sum`函数的示例。

```go
package main

import "testing"

func TestSum(t *testing.T) {
    tables := []struct {
        x int
        y int
        n int
    }{
        {1, 1, 2},
        {1, 2, 3},
        {2, 2, 4},
        {5, 2, 7},
    }

    for _, table := range tables {
        total := Sum(table.x, table.y)
        if total != table.n {
            t.Errorf("Sum of (%d+%d) was incorrect, got: %d, want: %d.", table.x, table.y, total, table.n)
        }
    }
}
```

如果你想要触发错误跳出测试，可以将`Sum`函数修改为返回`x*y`

```go
$ go test -v
=== RUN   TestSum
--- FAIL: TestSum (0.00s)
    table_test.go:19: Sum of (1+1) was incorrect, got: 1, want: 2.
    table_test.go:19: Sum of (1+2) was incorrect, got: 2, want: 3.
    table_test.go:19: Sum of (5+2) was incorrect, got: 10, want: 7.
FAIL
exit status 1
FAIL    github.com/alexellis/t6 0.013s
```

### 启动测试

有两种方法启动一个package的测试。单元测试和整体测试的方法很类似。

#### 1.同目录的测试：

`go test`
 这个命令适配所有符合`packagename_test.go`的文件

#### 2.完全限定包名

`go test github.com/alexellis/golangbasics1`
 现在在Go里运行了单元测试，`go test -v`获取更加冗长的输出，并且你将看到每个测试用例的PASS/FAIL结果包括任何由`t.Log`产生的日志信息。

> 单元测试和整体测试的区别是单元测试通常隔离与网络、磁盘等通信的依赖关系。单元测试通常仅仅测试一件事情，例如一个函数的功能。

## 1.2 更多有关`go test`

**语句覆盖**
 `go test`工具内建了语句的代码覆盖率。若要使用上述示例进行尝试，请输入：

```bash
$ go test -cover
PASS
coverage: 50.0% of statements
ok      github.com/alexellis/golangbasics1  0.009s
```

高语句覆盖率优于低语句覆盖率或无覆盖，但是，衡量标准可能会误导人。我们希望确保不仅是在执行语句，而且还要验证行为和输出值，并针对差异提出错误。如果您从上面的测试中删除`“if”`语句，它将保留50%的测试覆盖率，但在验证`“Sum”`方法的行为时失去了它的有用性。

#### 生成HTML格式的覆盖率报告

如果您使用以下两个命令，您可以可视化您的程序的哪些部分已被测试覆盖，以及哪些语句依然缺失 ：

```csharp
go test -cover -coverprofile=c.out
go tool cover -html=c.out -o coverage.html 
```

然后用浏览器打开coverage.html

#### Go不会传送你的测试用例

此外，将命名为`addition_test.go`的文件遗留在你的package也许会让人觉得不自然。REST确保GO编译器和链接器不会将您的测试文件存储在它所产生的任何二进制文件中 。
 下面是在前面的Golang基础教程中使用的net/http包中找到生产和测试代码的示例。

```go
$ go list -f={{.GoFiles}} net/http
[client.go cookie.go doc.go filetransport.go fs.go h2_bundle.go header.go http.go jar.go method.go request.go response.go server.go sniff.go status.go transfer.go transport.go]

$ go list -f={{.TestGoFiles}} net/http
[cookie_test.go export_test.go filetransport_test.go header_test.go http_test.go proxy_test.go range_test.go readrequest_test.go requestwrite_test.go response_test.go responsewrite_test.go transfer_test.go transport_internal_test.go]
```

更多信息请参考 [Golang testing docs](https://links.jianshu.com/go?to=https%3A%2F%2Fgolang.org%2Fpkg%2Ftesting%2F)

## 1.3 隔离依赖关系

定义单元测试的关键因素是与运行时依赖项或协作者隔离。
 Golang中通过interface实现，如果你具有C#或Java背景，它们看起来有点不同。Golang中接口是隐含的而不是强制接口，这意味着具体类不需要提前知道接口。
 这意味着我们可以拥有非常小的接口，例如 [io.ReadCloser](https://links.jianshu.com/go?to=https%3A%2F%2Fgolang.org%2Fsrc%2Fio%2Fio.go%3Fs%3D4977%3A5022%23L116)，它仅仅由Reader和Closer两个方法组成：
 `Read(p []byte) (n int, err error)`
 **Reader接口**
 `Close() error`
 **Closer接口**
 如果您正在设计一个供第三方使用的软件包，那么设计接口是有意义的，这样其他人就可以编写单元测试来在需要时隔离您的软件包。
 接口可以在函数调用中替换。因此，如果我们想测试这个方法，我们只需要提供一个实现Reader接口的假/测试双重类。

```go
package main

import (
    "fmt"
    "io"
)

type FakeReader struct {
}

func (FakeReader) Read(p []byte) (n int, err error) {
    // return an integer and error or nil
}

func ReadAllTheBytes(reader io.Reader) []byte {
    // read from the reader..
}

func main() {
    fakeReader := FakeReader{}
    // You could create a method called SetFakeBytes which initialises canned data.
    fakeReader.SetFakeBytes([]byte("when called, return this data"))
    bytes := ReadAllTheBytes(fakeReader)
    fmt.Printf("%d bytes read.\n", len(bytes))
}
```

在实现自己的抽象（如上所述）之前，最好搜索Golang文档以查看是否已经有可以使用的东西。在上面的例子中，我们也可以在bytes包中使用标准库
 `func NewReader(b []byte) *Reader`
 Golang testing/ iotest包提供了一些读取器实现，这些实现很慢或导致错误在读取中途被抛出。这些是弹性测试的理想选择

## 1.4 有用的示例

我将重构前一篇文章中的代码示例，其中我们发现有多少宇航员在太空中。
 我们将从测试文件开始：

```go
package main

import "testing"

type testWebRequest struct {
}

func (testWebRequest) FetchBytes(url string) []byte {
    return []byte(`{"number": 2}`)
}

func TestGetAstronauts(t *testing.T) {
    amount := GetAstronauts(testWebRequest{})
    if amount != 1 {
        t.Errorf("People in space, got: %d, want: %d.", amount, 1)
    }
}
```

我有一个名为GetAstronauts的导出方法，它调用HTTP端点，从结果中读取字节，然后将其解析为结构并返回“number”属性中的整数
 我在测试中的假/测试双重只返回满足测试所需的最小JSON，并且首先我让它返回一个不同的数字，以便我知道测试有在工作。很难确定第一次通过的测试是否有效。
 这是我们运行主要功能的应用程序代码。 GetAstronauts函数将接口作为其第一个参数，允许我们从该文件及其导入列表中隔离和抽象出任何HTTP逻辑。

```go
package main

import (
    "encoding/json"
    "fmt"
    "log"
)

func GetAstronauts(getWebRequest GetWebRequest) int {
    url := "http://api.open-notify.org/astros.json"
    bodyBytes := getWebRequest.FetchBytes(url)
    peopleResult := people{}
    jsonErr := json.Unmarshal(bodyBytes, &peopleResult)
    if jsonErr != nil {
        log.Fatal(jsonErr)
    }
    return peopleResult.Number
}

func main() {
    liveClient := LiveGetWebRequest{}
    number := GetAstronauts(liveClient)

    fmt.Println(number)
}
```

GetWebRequest接口指定如下函数：

```csharp
type GetWebRequest interface {
    FetchBytes(url string) []byte
}
```

> 接口是推断而不是显式修饰到结构上。这与C＃或Java等语言不同。

名为types.go的完整文件看起来像这样，并从之前的博客文章中提取:

```go
package main

import (
    "io/ioutil"
    "log"
    "net/http"
    "time"
)

type people struct {
    Number int `json:"number"`
}

type GetWebRequest interface {
    FetchBytes(url string) []byte
}

type LiveGetWebRequest struct {
}

func (LiveGetWebRequest) FetchBytes(url string) []byte {
    spaceClient := http.Client{
        Timeout: time.Second * 2, // Maximum of 2 secs
    }

    req, err := http.NewRequest(http.MethodGet, url, nil)
    if err != nil {
        log.Fatal(err)
    }

    req.Header.Set("User-Agent", "spacecount-tutorial")

    res, getErr := spaceClient.Do(req)
    if getErr != nil {
        log.Fatal(getErr)
    }

    body, readErr := ioutil.ReadAll(res.Body)
    if readErr != nil {
        log.Fatal(readErr)
    }
    return body
}
```

#### 选择抽象的内容

上面的单元测试实际上只测试了json.Unmarshal函数以及我们对有效HTTP响应体的外观的假设。对于我们的示例，这种抽象可能没问题，但我们的代码覆盖率得分会很低。
 也可以进行较低级别的测试，以确保正确执行HTTP获取超时2秒，或者我们创建了GET请求而不是POST
 幸运的是，Go有一组用于创建虚假HTTP服务器和客户端的辅助函数







# go单元测试和基准测试

在*_test.go文件中，有三种类型的函数：测试函数、基准测试(benchmark)函数、示例函数。一个测试函数是以Test为函数名前缀的函数，用于测试程序的一些逻辑行为是否正确；go  test命令会调用这些测试函数并报告测试结果是PASS或FAIL。基准测试函数是以Benchmark为函数名前缀的函数，它们用于衡量一些函数的性能；go  test命令会多次运行基准测试函数以计算一个平均的执行时间。示例函数是以Example为函数名前缀的函数，提供一个由编译器保证正确性的示例文档。

### 测试函数

- 测试文件必须以“_test.go”结尾
- 导入testing包
- 测试函数名必须以Test开头，且签名必须接收一个指向testing.T类型的指针，并无返回值，如TestDownload(t *testing.T)
- t.Log用来输出测试消息，t.Logf可格式化消息；t.Fatal（t.Fatalf）测试失败，只退出该测试函数；t.Error（t.Errorf）测试失败，但不会退出该测试函数，可继续向下执行

### 基准测试函数

- 测试文件必须以“_test.go”结尾
- 导入testing包
- 测试函数名必须以Benchmark开头，且签名必须接收一个指向testing.B类型的指针，并无返回值，如BenchmarkDownload(b *testing.B)
- 循环上限为b.N

### 特殊用法

- t.SkipNow()写在测试函数内容第一行，可以跳过此测试函数
- 可以使用t.Run来执行subtest，做到控制test输出以及顺序
- 使用TestMain作为初始化test，做一些初始化的操作，如数据库连接，文件打开等，然后使用m.Run()来调用tests，如果没有在TestMain里调用m.Run()，则除了TestMain外其余tests（包括Benchmark）都不会被执行

```go
func TestP(t *testing.T) {
    t.SkipNow() // 跳过此测试
    res := Print1to20()
    fmt.Println(res)
    if res != 200 {
        t.Error("Wrong result")
    }
}
func testPrint(t *testing.T) {
    res := Print1to20()
    fmt.Println(res)
    if res != 190 {
        t.Error("Wrong result")
    }
}

func testPrint2(t *testing.T) {
    res := Print1to20()
    fmt.Println(res)
    if res != 190 {
        t.Error("Wrong result")
    }
}

func TestAll(t *testing.T) {
    t.Run("TestPrint", testPrint)
    t.Run("TestPrint2", testPrint2)
}
func TestMain(m *testing.M) {
    fmt.Println("some init")
    m.Run()
}
```

### 命令行

- go test [-v]   目录下全部文件内的全部单元测试函数[-v显示详情]
- go test xxx_test.go [-v]  目录下指定文件内的全部单元测试函数
- go test -run TestXXX [-v]  目录下指定单元测试函数
- go test -bench=".*" [-v]   目录下全部单元测试和基准测试
- go test -run="none" -bench=".*"   目录下全部基准测试函数（不跑单元测试）（参数-run对应一个正则表达式）
- go test -run="none" -bench="BenchmarkXXX" 目录下指定基准测试函数
- -benchtime="3s"，指定运行时间，默认不小于1s；-benchmem可显示每次操作分配内存的次数（allocs/op），字节数（B/op）
- go tool cover查看测试覆盖率的使用

### 测试分类

一种测试分类的方法是基于测试者是否需要了解被测试对象的内部工作原理。黑盒测试只需要测试包公开的文档和API行为，内部实现对测试代码是透明的。相反，白盒测试有访问包内部函数和数据结构的权限，因此可以做到一些普通客户端无法实现的测试。例如，一个白盒测试可以在每个操作之后检测不变量的数据类型。（白盒测试只是一个传统的名称，其实称为clear box测试会更准确。）

黑盒和白盒这两种测试方法是互补的。黑盒测试一般更健壮，随着软件实现的完善测试代码很少需要更新。它们可以帮助测试者了解真实客户的需求，也可以帮助发现API设计的一些不足之处。相反，白盒测试则可以对内部一些棘手的实现提供更多的测试覆盖。

### 基准测试剖析

Go语言支持多种类型的剖析性能分析，每一种关注不同的方面，但它们都涉及到每个采样记录的感兴趣的一系列事件消息，每个事件都包含函数调用时函数调用堆栈的信息。内建的go test工具对几种分析方式都提供了支持。

CPU剖析数据标识了最耗CPU时间的函数。在每个CPU上运行的线程在每隔几毫秒都会遇到操作系统的中断事件，每次中断时都会记录一个剖析数据然后恢复正常的运行。

堆剖析则标识了最耗内存的语句。剖析库会记录调用内部内存分配的操作，平均每512KB的内存申请会触发一个剖析数据。

阻塞剖析则记录阻塞goroutine最久的操作，例如系统调用、管道发送和接收，还有获取锁等。每当goroutine被这些操作阻塞时，剖析库都会记录相应的事件。

只需要开启下面其中一个标志参数就可以生成各种分析文件。当同时使用多个标志参数时需要当心，因为一项分析操作可能会影响其他项的分析结果。

```bash
go test -cpuprofile=cpu.out
go test -blockprofile=block.out
go test -memprofile=mem.out
```

一旦我们已经收集到了用于分析的采样数据，我们就可以使用pprof来分析这些数据。这是Go工具箱自带的一个工具，但并不是一个日常工具，它对应go tool pprof命令。该命令有许多特性和选项，但是最基本的是两个参数：生成这个概要文件的可执行程序和对应的剖析数据。

为了提高分析效率和减少空间，分析日志本身并不包含函数的名字；它只包含函数对应的地址。也就是说pprof需要对应的可执行程序来解读剖析数据。虽然go test通常在测试完成后就丢弃临时用的测试程序，但是在启用分析的时候会将测试程序保存为foo.test文件，其中foo部分对应待测包的名字。

下面的命令演示了如何收集并展示一个CPU分析文件。我们选择net/http包的一个基准测试为例。通常最好是对业务关键代码的部分设计专门的基准测试。因为简单的基准测试几乎没法代表业务场景，因此我们用-run=NONE参数禁止那些简单测试。

```cpp
$ go test -run=NONE -bench=ClientServerParallelTLS64 \
    -cpuprofile=cpu.log net/http
 PASS
 BenchmarkClientServerParallelTLS64-8  1000
    3141325 ns/op  143010 B/op  1747 allocs/op
ok       net/http       3.395s

$ go tool pprof -text -nodecount=10 ./http.test cpu.log
2570ms of 3590ms total (71.59%)
Dropped 129 nodes (cum <= 17.95ms)
Showing top 10 nodes out of 166 (cum >= 60ms)
    flat  flat%   sum%     cum   cum%
  1730ms 48.19% 48.19%  1750ms 48.75%  crypto/elliptic.p256ReduceDegree
   230ms  6.41% 54.60%   250ms  6.96%  crypto/elliptic.p256Diff
   120ms  3.34% 57.94%   120ms  3.34%  math/big.addMulVVW
   110ms  3.06% 61.00%   110ms  3.06%  syscall.Syscall
    90ms  2.51% 63.51%  1130ms 31.48%  crypto/elliptic.p256Square
    70ms  1.95% 65.46%   120ms  3.34%  runtime.scanobject
    60ms  1.67% 67.13%   830ms 23.12%  crypto/elliptic.p256Mul
    60ms  1.67% 68.80%   190ms  5.29%  math/big.nat.montgomery
    50ms  1.39% 70.19%    50ms  1.39%  crypto/elliptic.p256ReduceCarry
    50ms  1.39% 71.59%    60ms  1.67%  crypto/elliptic.p256Sum
```

参数-text用于指定输出格式，在这里每行是一个函数，根据使用CPU的时间长短来排序。其中-nodecount=10参数限制了只输出前10行的结果。对于严重的性能问题，这个文本格式基本可以帮助查明原因了。

这个概要文件告诉我们，HTTPS基准测试中crypto/elliptic.p256ReduceDegree函数占用了将近一半的CPU资源，对性能占很大比重。相比之下，如果一个概要文件中主要是runtime包的内存分配的函数，那么减少内存消耗可能是一个值得尝试的优化策略。

对于一些更微妙的问题，你可能需要使用pprof的图形显示功能。这个需要安装GraphViz工具，可以从 http://www.graphviz.org 下载。参数-web用于生成函数的有向图，标注有CPU的使用和最热点的函数等信息。

如果想了解更多，可以阅读Go官方博客的“Profiling Go Programs”一文。

### 示例函数

以Example为函数名开头。示例函数没有函数参数和返回值。下面是IsPalindrome函数对应的示例函数：

```go
func ExampleIsPalindrome() {
    fmt.Println(IsPalindrome("A man, a plan, a canal: Panama"))
    fmt.Println(IsPalindrome("palindrome"))
    // Output:
    // true
    // false
}
```

示例函数有三个用处。最主要的一个是作为文档：一个包的例子可以更简洁直观的方式来演示函数的用法，比文字描述更直接易懂，特别是作为一个提醒或快速参考时。一个示例函数也可以方便展示属于同一个接口的几种类型或函数之间的关系，所有的文档都必须关联到一个地方，就像一个类型或函数声明都统一到包一样。同时，示例函数和注释并不一样，示例函数是真实的Go代码，需要接受编译器的编译时检查，这样可以保证源代码更新时，示例代码不会脱节。

根据示例函数的后缀名部分，godoc这个web文档服务器会将示例函数关联到某个具体函数或包本身，因此ExampleIsPalindrome示例函数将是IsPalindrome函数文档的一部分，Example示例函数将是包文档的一部分。

示例函数的第二个用处是，在go test执行测试的时候也会运行示例函数测试。如果示例函数内含有类似上面例子中的// Output:格式的注释，那么测试工具会执行这个示例函数，然后检查示例函数的标准输出与注释是否匹配。



