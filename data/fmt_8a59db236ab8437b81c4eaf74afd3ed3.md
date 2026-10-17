
这两个类型都被定义为接口，这意味着它们不能被直接实例化。每个类型都包含一个单一导出函数的定义：`Read` 或 `Write`。正如第 1 章所解释，你可以将这些函数视为抽象方法，必须在类型上实现它们，该类型才能被视为 `Reader` 或 `Writer`。例如，以下的人造类型符合合同并可以使用任何接受 `Reader` 的地方：

```go
type FooReader struct {
    func (fooReader *FooReader) Read(p []byte) (int, error) {
        // 从某任何地方读取数据。
        return len(dataReadFromSomewhere), nil
    }
}
```

同样的想法也适用于 `Writer` 接口：

```go
type FooWriter struct {
    func (fooWriter *FooWriter) Write(p []byte) (int, error) {
        // 将数据写入某处。
        return len(dataWrittenSomewhere), nil
    }
}
```

让我们利用这些知识创建一些半可用的东西：一个封装 `stdin` 和 `stdout` 的自定义 `Reader` 和 `Writer`。这段代码有点生造，因为 Go 的 `os.Stdin` 和 `os.Stdout` 类型已经充当了 `Reader` 和 `Writer`，但如果你不偶尔重新发明一下轮子，你就学不到任何东西，不是吗？

列表 2-9 显示了完整的实现，并在随后提供了解释。

```go
package main

import (
  "fmt"
  "log"
  "os"
)

// FooReader 定义 io.Reader 以从 stdin 读取。
type FooReader struct {}

// Read 从 stdin 读取。
func (fooReader *FooReader) Read(b []byte) (int, error) {
  fmt.Print("in > ")
  return os.Stdin.Read(b)
}

// FooWriter 定义 io.Writer 以写入 stdout。
type FooWriter struct {}

// Write 写入 stdout。
func (fooWriter *FooWriter) Write(b []byte) (int, error) {
    fmt.Print("out>")
    return os.Stdout.Write(b)
}

func main() {
    // 实例化 reader
    var (
        reader FooReader
        writer FooWriter
    )

    // 创建缓冲区来持有输入/输出。
    input := make([]byte, 4096)

    // 使用 reader 读取。
    s, err := reader.Read(input)
    if err != nil {
        log.Fatalf("无法读取数据")
    }
    fmt.Printf("%d bytes from stdin\n", s)

    // 使用 writer 写入。
    s, err = writer.Write(input)
    if err != nil {
        log.Fatalf("无法写入数据")
    }
    fmt.Printf("%d bytes to stdout\n", s)
}
```

Listing 2-9: reader 和 writer 演示 (ch-2/io-example/main.go)

代码定义了两个类型：`FooReader` ① `FooWriter` ④。在每个类型上，你为 `FooReader` 定义了 `Read([]byte)` 函数 ②，为 `FooWriter` 定义了 `Write([]byte)` 函数 ⑤。在这种情况下，这两个函数从 `stdin` 读取 ③ 并写入 `stdout` ⑥。

注意 `FooReader` 和 `os.Stdin` 的 `Read` 函数都返回长度和任何错误。数据本身被复制到传递的字节切片中。这与节之前提供的 `Reader` 接口定义一致。`main()` 函数创建一个切片（命名为 `input` 7），然后在调用 `FooReader.Read([]byte)` 8 和 `FooWriter.Write([]byte)` 9 时使用它。

程序的示例输出如下：

```
$ go run main.go
in > hello world!!!
Read 15 bytes from stdin
out> hello world!!!
Write 4096 bytes to stdout
```

从 `Reader` 将数据拷贝到 `Writer` 是一个相当常见的模式——以至于 Go 的 `io` 包包含一个 `Copy()` 函数，可以用来简化 `main()` 函数。该函数的原型如下：

```go
func Copy(io.Writer, src io.Reader) (written int64, error error)
```

这个便利函数允许你实现与之前相同的程序行为，用列表 2-10 中的代码替换你的 `main()`。

```go
func main() {
    var (
        reader FooReader
        writer FooWriter
    )
    if _, err := io.Copy(&writer, &reader); err != nil {
        log.Fatalf("无法读取/写入数据")
    }
}
```

```
}
```

列表 2-10：使用 io.Copy (/ch-2/copy-example/main.go)

注意，对 `reader.Read([byte])` 和 `writer.Write([byte])` 的显式调用已被替换为对 `io.Copy(writer, reader)` 的单个调用。底层，`io.Copy(writer, reader)` 调用提供的 reader 的 `Read([byte])` 函数，从而触发来自 stdin 的 `FooReader`。随后，`io.Copy(writer, reader)` 调用提供的 writer 的 `Write([byte])` 函数，导致调用 writer 并将数据写入 stdout。本质上，`io.Copy(writer, reader)` 处理了顺序的“先读后写”过程，无需处理所有琐碎的细节。

这一介绍性章节绝非对 Go I/O 和接口的全面回顾。Go 标准包中存在许多便利函数以及自定义的读取器和写入器。在大多数情况下，Go 的标准包包含了实现最常见任务的基础实现。在下一节中，让我们探索如何将这些基础知识应用于 TCP 通信，最终利用赋予你的力量来开发现实生活中可用的工具。

## 创建 Echo 服务器

按照大多数语言的惯例，你将从构建一个 echo 服务器开始，以学习如何从套字读写数据。为了实现这一点，你将使用 `net.Conn`，这是 Go 的面向流的网络连接，我们在构建端口扫描器时曾介绍过它。根据 Go 对该数据类型的文档，`Conn` 实现了 `Reader` 和 `Writer` 接口定义的 `Read([byte])` 和 `Write([byte])` 函数。因此，`Conn` 既是 Reader也是 Writer（是的，这是可能的）。这逻辑上是合理的，因为 TCP 连接是双向的，可以用于发送（写）或接收（读）数据。

创建 `Conn` 实例后，你将能够通过 TCP 套字发送接收数据。然而，TCP 服务器不能直接制造连接；必须由客户端建立。在 Go 中，你可以使用 `net.Listen(network, address string)` 先在特定端口上开启 TCP 监听器。一旦客户端连接，`Accept()` 方法就会创建并返回一个 `Conn` 对象，你可以用它接收和发送数据。

列表 2-11 展示了服务器实现的完整示例。为了清晰起见，我们包含了内联注释。不用担心理解整个代码，我们稍后会进行拆解。

```go
package main

import (
	"io"
	"log"
	"net"
)

// echo 是一个处理函数，简单地回显接收到的数据。
func echo(conn net.Conn) {
	defer conn.Close()

	// 创建缓冲区缓冲区存储接收到的数据。
	b := make([]byte, 512)
	for {
		size, err := conn.Read(b[:])
		if err == io.EOF {
			log.Println("Client disconnected")
			break
		}
		if err != nil {
			log.Println("Unexpected error")
			continue
		}
		log.Printf("Received %d bytes: %s\n", size, string(b))

		// 通过 conn.Write 发送数据。
		log.Println("Writing data")
		if _, err := conn.Write(b[0:size]); err != nil {
			log.Fatalf("Unable to write data")
		}
	}
}

func main() {
	// 绑定到所有接口上的 TCP 端口 20080。
	listener, err := net.Listen("tcp", "20080")
	if err != nil {
		log.Fatalf("Unable to bind to port")
	}
	log.Println("Listening on 0.0.0.0:20080")
	// 等待连接。连接建立时创建 net.Conn。
	conn, err := listener.Accept()
	if err != nil {
		log.Fatalf("Unable to accept connection")
	}
	// 处理连接。使用 goroutine 实现并发。
	go echo(conn)
}
```

列表 2-11：基础 echo 服务器 (/ch-2/echo-server/main.go)

**列表 2-11** 从定义一个名为 `echo(net.Conn)` 的函数开始，它接受一个 `Conn` 实例作为参数。它作为一个连接处理程序来执行必要的 I/O。该函数无限循环，使用缓冲区从连接中读写数据。数据被读取到一个名为 `b` 的变量中，随后被写回连接。

现在，你需要设置一个会调用你的处理程序的监听器。如之前所述，服务器不能制造连接，而是必须等待客户端连接。因此，使用 `net.Listen(network, address string)` 函数在所有接口上启动一个定义为绑定到端口 20080 的 `listener`。

接下来，通过一个无限循环确保服务器在接收到一个连接后将继续监听连接。在循环内部，你调用了 `listener.Accept()`，该函数在等待客户端连接时会阻塞执行。当客户端连接时，此函数返回一个 `Conn` 实例。回本节早前的讨论，`Conn` 既是 Reader 也是 Writer（它实现了 `Read([]byte)` 和 `Write([]byte)` 接口方法）。

随后，`Conn` 实例被传递给 `echo(net.Conn)` 处理函数。该调用之前带有 `go` 关键字，使其成为并发调用，这样其他连接在等待处理程序时就不会被阻塞。

```go
func echo(conn net.Conn) {
	defer conn.Close()
	// Copy data from io.Reader to io.Writer via io.Copy().
	if _, err := io.Copy(conn, conn); err != nil {
		log.Fatalf("Unable to read/write data")
	}
}
```

你已经探索了 I/O 的基础知识，并将其应用于 TCP 服务器。现在，是时候转向更具实用性和更具相关性的示例了。

## 代理 TCP 连接

既然你已经有了坚实的基础，就可以利用目前为止所学的知识，创建一个简单的端口转发器，通过中间服务或主机来代理连接。正如本章早些提到的，这对于尝试绕过限制性的出站控制，或者利用某个系统来绕过网络隔离非常有用。

在列出代码之前，考虑这样一个想象的现实问题：Joe 是 ACME 公司的一名表现不佳的员工，担任业务分析师。由于他在简历中加入了一些轻微的夸大，他拿着丰厚的薪水。（他真的读过常春藤高校吗？Joe，这可不符合道德。）Joe 缺乏动力，但他对猫的热爱却与其相反——以至于他在家里安装了摄像头，并托管了一个网站 joescat.website，通过该网站可以远程监控那些落满皮屑的毛茸茸球体。但有一个问题：ACME 发现了 Joe。他们不喜欢他 24 小时用用 4K 超高清直播他的猫，这浪费了宝贵的 ACME 网络带宽。ACME 甚至阻止了员工访问 Joe 的猫咪摄像头网站。

Joe 有了一个主意。“如果我在我控制的互联网系统上设置一个端口转发器呢，”Joe 说，“并强制将从该主机发送的所有流量重定向到 joescatcam.website 会怎样？” Joe 在第二天检查，并确认他可以访问托管在 jooproxy.com 域名上的个人网站。Joe 错过了下午的会议，来到一家咖啡馆，并迅速为他的问题编写了一个解决方案。他将把接收到 http://jooproxy.com 的所有流量转发到 http://joescatcam.website。

以下是 Joe 的代码，他在 joescatcam.com 服务器上运行它：

```go
func handle(src net.Conn) {
	dst, err := net.Dial("tcp", "joescatcam.website:80")
	if err != nil {
		log.Fatal("Unable to connect to our unreachable host")
	}
	defer dst.Close()

	// Run in goroutine to prevent io.Copy from blocking
	go func() {
		// Copy our source's output to the destination
		if _, err := io.Copy(dst, src); err != nil {
			log.Fatal(err)
		}
	}()

	// Copy our destination's output back to our source
	if _, err := io.Copy(src, dst); err != nil {
		log.Fatal(err)
	}
}

func main() {
	// Listen on local port 80
	listener, err := net.Listen("tcp", ":80")
	if err != nil {
		log.Fatalln("Unable to bind to port")
	}

	for {
		conn, err := listener.Accept()
		if err != nil {
			log.Fatalln("Unable to accept connection")
		}
		go handle(conn)
	}
}
```

首先查看 Joe 的 `handle(net.Conn)` 函数。Joe 连接到 joescatcam.website（记住，这个无法访问的主机无法 Joe 的公司工作站直接访问）。Joe 随后使用了两次 `Copy(Writer, Reader)`。第一次调用确保来自入站连接的数据被复制到 joescatcam.website 连接。第二次调用确保从 joescatcam.website 读取的数据被写回连接客户端的连接。`Copy(Writer, Reader)` 是一个阻塞函数，它将继续阻塞执行直到网络连接关闭。Joe 明智地将他的第一次调用 `Copy(Writer, Reader)` 封装在一个新的 goroutine 中。这确保了 `handle(net.Conn)` 函数内部的执行继续，并且可以进行第二次 `Copy(Writer, Reader)` 调用。

Joe 的代理监听 80 端口，并中继从到 80 端口 joescatcam.website 的连接收到的任何流量。Joe 那个疯狂又浪费的男人，通过 `curl` 连接到 joesproxy.com，确认他可以连接到 joescatcam.website：

```bash
$ curl -i -X GET http://joseproxy.com
HTTP/1.1 200 OK
Date: Wed, 25 Nov 2020 19:51:54 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Thu, 27 Jun 2019 15:30:43 GMT
ETag: "6d-519594e7f2d25"
Accept-Ranges: bytes
Content-Length: 109
Vary: Accept-Encoding
Content-Type: text/html
--snip--
```

此时，Joe 做到了。他正在过着梦想，一边浪费 ACME 赞助的时间和网络带宽一边看他的猫。今天，会有猫看！

## 复现用于命令执行的cat

在这一部分，让我们复现 Netcat 一些更有趣的功能——特别是它巨大的安全漏洞。
