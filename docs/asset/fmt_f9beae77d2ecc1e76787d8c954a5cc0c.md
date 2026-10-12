
可以使用`Firefox OS`模拟器在桌面上测试这些作品的第一版本。通过访问`Tools: Web Developer Guide for Firefox OS`即可轻松启动。你也可以在带有`Firefox OS`的手机上进行测试，手机上有一个显示信息和错误的控制台以及硬盘。在浏览器中使用`Firefox`将获得最佳结果。与此同时，`Firefox OS`手机已经上市，这意味着开发者现在可以测试他们的应用了。

# `Go`程序教程

介绍这种最热门的编程语言。在`Go`中，你可以通过返回两个值来赋值两个变量。

```go
// 带返回方式
func timeout(x int, y int) (int, int) {
    return x, y * 2
}

func main() {
    h, i := timeout(2, 6)
    fmt.Println(h, i) // h == 4, i == 12
}

// 另一种命名变量返回方式
func timeout(a, b int) (x, y int) {
    x = a * 2
    y = b * 2
    return
}
```

2007年`Robert Griesemer`、`Rob Pike`和`Ken Thompson`开始编写这种语言。他们觉得`C++`变得太复杂，因此决定从零开始。`Go`获取常量的限制严格得多，原因显而易见

```go
// 常量可以这样设置
const x = 12
```

函数定义在设计和实现上非常友好。

```go
// 示例 4
func example(x int)

// 简写
func example(x int)
```

## 安装`Go`

如果你足够幸运，你可能可以通过以下命令安装`Go`：

```bash
sudo apt-get install go
```

如果一切顺利，现在你的系统上就有了`Go`。欢喜！但是，为了起见，我们假设没有发生这种情况。让我们从源码获取并安装，这样我们可以看到它是如何操作的。`golang.com/go/downloads/`并获取`1.0.2.src.tar.gz`（写作时，这是`Go`的最新版本）。将`tar.gz`解压到任何地方，然后进入找到的`src`文件夹。

# `Go`程序！

`Go`语言 - 教程

假设你的系统中已经安装了`GCC`或其他编译器，我们已经准备好运行它了。像往常一样，`Go`非常友好，它包含了一个`Bash`脚本来安装和测试`Go`。运行它吧：

## 它在哪里？

## 新包不断涌现。什么让`Go`与众不同？

```bash
./all.bash
```

然后去给自己泡杯茶。这个任务可能需要一点时间。在`Bash`脚本退出之前，你应该探索类似以下的内容：

```text
已安装至 [你的架构]
已安装的命令位于 /home/[USERNAME]
在 /home/[USERNAME]:
*** 你需要将 [USERNAME]/go 添加到你的 PATH 中。 *** 
```

`Go`是一门非常令人兴奋的语言：它易学、有趣而且运行速度极快。事实如此，新包不断涌现。任何人都可以像世界各地的软件工程师一样快速学会编写`Go`。在挑战`Python`或`JavaScript`并将其视为竞争对手之前，还有很长的路要走。还记得`Node.js`刚发布时人们是如何看待它的吗？`JavaScript`……运行在服务器上？看看它现在的样子。`Go`已经有了庞大的包库可以使用，并且按项目管理得以前好得多。当`Google`正在用`Go`重写它的整个遗留系统时。这就是承诺。

## 函数

如果你现在能看到这些，那么你好世界（`hello world`）。就像脚本一样，我们需要将`Go`添加到`PATH`中。每个人对设置`PATH`都有自己的偏好。你可以将其放在文件目录中，以便能够访问该站点：

`Go`中的函数可以执行你想要的任何操作。在我们的“你好世界”中，如果我们想使用最基础的实现。如果我们想写一个接受传值的函数，可以这样写：

```bash
PATH="/home/go/bin"
```

```go
func exp(x int, y int) int {
    fmt.Println(x)
    return 0
}
```

注意我们是如何在暴露的名称之后声明声明的。如果类型相同，我们可以这样写：

现在进入你的终端，你将看到帮助对话框，列出了执行`Go`脚本时可以调用的所有命令。

```go
func funcTimes(x int, y int) int {
    return x * y
}
```

## `Hello world`

让我们写一个“`hello world`”。创建一个名为`lets.go`的小文件。如果你执行

```bash
go run lets.go
```

如果我们想返回结果，我们需要类似这样的代码：

```go
func main() {
    h, i := funcTimes(2, 6)
    fmt.Println(h, i) // h = 4, i = 12
}
```

你应该能在终端中看到弹出“`hello world`”。让我们看看我们写了什么。在这里，包（`package`）基本上是`Go`为文件中包含的代码创建名称的方式。如果我们想写一个其他程序使用的模块（`module`），我们可以使用大部分。

注意我们在返回变量之前是如何给它们赋值的。如果我们返回多个值，可以为这些变量命名并这样返回它们：

```go
package main
import ("fmt") // 打印 "Hello, world" // 这只是一个注释
func main() {
    fmt.Println("Hello, world")
}
```

```go
func funcTimes(a, b int) int {
    return a * b
}
```

单语句：

```go
import("fmt", "math", "net")
```

多语句：

```go
import "fmt"
import "math"
import "path"
```

执行时，`go`将运行`main()`函数。

## 变量

`Go`中的声明与其他语言不同。有多种方法可以相同的效果。如果我们想要示例1，你也可以这样包含：

在这些实例中，`a = 1`，`b = 2`。当我们使用`var`关键字时，我们在赋值之前声明了变量。我们也可以在声明的末尾或开头声明变量。如果我们希望变量是常量，我们使用`const`。`Go`也有常量，例如：

```go
const x = 12
```

但你不能像声明变量那样声明它。它是从值中推断出来的。

现在我们有了一个可以工作的环境，可以运行一个小小的“`hello world`”

```go
y = b * 2
return
```

对于数字，我们使用以下代码创建一个子集：

我们像这样声明切片（`slice`）要包含的类型：

```go
numbers = []int{1, 2, 4, 8, 16, 32, 64, 128}
lessNumbers = numbers[:3]
```

```go
var places = [3]Coordinates
```

`Go`中的函数也可以返回闭包（`closures`）。但我们必须小心意识到我们返回的是一个函数——我们返回的是函数被调用时执行的结果。这有点让人困惑。

```go
func aDecoder(x, y int) int {
	randomNumber := 5
	return func(x, y int) int {
		return x + randomNumber
	}
}
```

然后我们可以这样将切片传递给切片：

```go
places[0] = Coordinates(1.1, 2.2)
```

注意在`aDecoder()`中我们指定返回的是一个整数，而不是函数。如果是`JavaScript`的话。

# 教程

# 通过网页控制树莓派机器人

`LinuxDeveloper`

![](img/4c82285250803e975d41cda3a51d081f_53_0.png)

![](img/4c82285250803e975d41cda3a51d081f_53_1.png)

# 从连接网络的设备控制树莓派机器人

# 顾问

`Linus Fraser`是一位程序员和系统管理员，`RaspberryTutorials` `YouTube`系列的创建者，并担任树莓派基金会的`Linux`管理员志愿者。

在上一期节目中，我们制作了一个树莓派机器人。在本期节目中，我们将创建一个`Python` `Web`应用程序，让你能够通过第一称视角控制你的机器人。

在上一期构建了我们的树莓派后，我们一直在思考各种教程，以扩展`Jonny Pi`的技能和能力。我们的主意之一是从网页浏览器控制机器人。为了让它变得更有趣，我们决定整合树莓派摄像头模块，这样我们就可以展示`Jonny Pi`所看到的第一人称视角。只要你处于机器人的`Wi-Fi`范围内，就可以通过观察应用本身的反馈来到处行驶。
