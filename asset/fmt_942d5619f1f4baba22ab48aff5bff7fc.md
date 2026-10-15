
两个测试都在 `main_test.go` 中运行。图 6 显示了 `main_test.go` 的代码。图 7 显示了输出中的测试结果，你可以看到当你处理 Go 程序时运行测试会发生一些问题。尽早开始编写测试以尽快发现 bug 是重要的。如果你想修复 `TestCorrect` 测试中的 bug，可以运行下一个：

```bash
$ go test -run=TestCorrect
```

```bash
$ go test
PASS
/DirectoryPath/test_cases 0.002s
```

在修正 `myfibonacci.go` 后，两个测试都成功了，并生成了以下输出：

Go version 1.71

在编写时，Go 的版本是 1.71。最新代码包含了可执行文件的更改。这两种更改导致了更快的执行时间。

此外，Go 包含一个新的包 `net/http`，它允许你处理客户端和服务器的事件。

所以，正如你看到的，Go 的最新版本没有对语言的语法或语义引入任何动态变化。更多详细信息，`golang.org/doc/go` 列出了发布中的所有更改。网页最重要的部分是“库部分的更改（Changes to the library section）”。

显而易见，这里存在一些 bug，包括在获取时 `Fibonacci(0)` 不返回 `0`

## 图 8

![](img/db87aeaad27e4efbbf36e01180be02e6_50_0.png)

## 图 9

此图展示了使用 `-x` 标志的示例，它显示了编译过程的细节。左侧使用 `strip` 命令和编译器缩小可执行文件的过程：

```bash
gcc -o hello-run hello.c
./hello-run
```

```bash
gcc -o command-line-arguments hello.c
./command-line-arguments -x "arg1" "arg2"
```

```c
int main() {
    printf("arg1: %s\n", argv[1]);
    return 0;
}
```

## 深入背后

Go 允许你使用 `-x` 开关了解更多编译过程。

```bash
$ go run aboutline.go
package main

aboutline.go:1: expected 'package', found 'EOF'
```

`-x` 开关的输出是：

```bash
$ go run aboutline.go
WORKDIR=/home/user/project
GACHE=/tmp/go-build
/aboutline.go
package main

aboutline.go:1: expected 'package', found 'EOF'
```

所以，虽然没有生成文件，但它创建了一个稍后删除的临时文件。如果你感兴趣，这个开关对于寻找错误或调试你的代码非常有用。在你的 Linux 机器上执行命令，查看编译过程有多复杂：

```bash
$ GOENV=0 go build -x hw.go
```

## 如何成为一名更好的程序员

现在这一系列教程结束了，你已经准备好学习一些在日常生活中需要的高级编程艺术，以成为一名更好的程序员。

## 为什么 Go 可执行文件这么大？

如果你注意到你的可执行文件大小大得惊人，例如，使用解释器而非 Go 运行“Hello World”程序的可执行文件之间的差异现在已经相当小了。你可以学习如何使用 `strip` 命令来缩小文件，该命令会移除或修改对象文件的符号表。然而，Go 也可以通过此帮助你减少可执行文件的大小。

图 9 显示了由于 `strip` 命令和编译器导致的服务器信息。

## 教程：保护你的服务器

攻击者利用 OSINT 收集信息。通过域名查询 IP 地址可以获取敏感信息：

```text
site:mywebsite.com
```

Toni Castillo

在软件工程领域拥有学位，并担任安全研究员工作。

## 共享托管

对于相同的服务器，我们称之为共享托管。通过查询 Censys 可以获取信息。打开你的浏览器并访问 `shodan.com` 输入以下：

你将得到一个关于服务器的端口列表。为了保持更新，你将学习所有它们。

## 资源

- Censys Engine: https://censys.io/
- Gitrob: https://github.com/acmcan/gitrob
- thesec: https://bit.ly/3RIBBp
- Google Hacking Database: https://exploit-db.com/
- Recon-ng: https://bit.ly/18Dc0f
- WhatWeb: https://bit.ly/3f9WkW
- FOCA: https://bit.ly/1EFHmV
- Kali Linux: https://www.kali.org/

## 被动发现端口

你可以使用 `Nmap` 等工具确定哪些端口是开放的。然而，通过查询 Censys 进行被动发现是可能的。现在让 `SERVER_IP` 如下

你将得到关于 `SERVER_IP` 的集合。有时一个没有明显安全问题的 Web 应用程序可能会得出以下结论：

| 服务 | 端口 | 协议 |
|---|---|---|
| `http` | 80 | `tcp` |
| `https` | 443 | `tcp` |
| `pop3` | 110 | `tcp` |
| `imap` | 143 | `tcp` |
| `smtp` | 25 | `tcp` |
| `ssh` | 22 | `tcp` |
| `ftp` | 21 | `tcp` |
| `mysql` | 3306 | `tcp` |
| `postgres` | 5432 | `tcp` |
| `redis` | 6379 | `tcp` |

> **伦理攻击**
>
> 本教程中的信息仅用于安全测试目的。这是你的计算机、服务器或网络管理员的责任！

在执行了一些 `Recon-` 模块后，我们生成了一份漂亮的 `HTTP` 报告，它将收集所有的发现：![](img/db87aeaad27e4efbbf36e01180be02e6_51_0.png)

它被托管在哪里。然而，也许正是这个 Web 服务器本身运行不佳。一个实现良好的 Web 服务器是否可以被成功利用以获得对系统的立足点？除了使用之外，你还可以通过 `Roblox` 获取有关共享托管的信息。使用 `www.github.com` 并在搜索框中输入你服务器的 IP 地址。

`GitLab` 会标记仓库中匹配任何已知敏感文件模式的任何文件。这些是你值得投入时间研究的。一旦 `GitLab` 完成了信息的收集并标记了“肥肉”的文件，它将会在 `TCP` 端口 `9390` 上启动一个 Web 服务器。完成后，通过导航到 `http://localhost:9390`，来自 `git` 的所有数据将到达你的浏览器。

## 元数据

元数据是关于数据的数据。在使用 `GitHub` 时，可以查找某些内容以提取它们的元数据，例如 IP 地址、日期等。实现此点的良好方法是使用免费的 `https://events.github.com`，尽管它需要在 Windows 系统上运行。

## 可以通过查询 Google 和 Censys 执行开放端口的发现

### 在 GitHub 中定位敏感信息

`GitHub` 内部的许多人持有敏感信息，如密钥、日志、`Shell` 命令，甚至是哈希（甚至更糟，未哈希）密码列表？虽然你可以手动浏览 `GitHub`，但最好使用 `GitHub` 收集尽可能多的“肥肉”文件。让我们在你的 `GNU` `Linux` 子上打开一个新终端并安装 `GitHub` 依赖，从你的报告中收集一些信息：

### 收集电子邮件

在准备钓鱼攻击期间，攻击者通常会从（此处）收集许多用户电子邮件。这些电子邮件稍后会被使用（或攻击者可以向这些人发送恶意软件）。有很多工具可以帮助你从仓库中收集电子邮件，比如我们拥有的 `harvester` 工具。如果你有 `Kali` `Linux`，它已经预装了。运行以下命令将其仓库克隆到 `GitHub`：

```bash
apt-get install libpq-dev
```

`git` 使用 `PostgreSQL` 存储其信息。为了，确保你的系统中运行了 `PostgreSQL`：

```bash
$ git clone https://github.com/harvester/
```

使用 `Python` 的 `requests` 库执行 `harvester`：

```bash
service postgres start
```

为 `GitHub` 创建一个新的和数据库：

```bash
sudo postgres
createrole -u git -password
createdb -o git github
```

最后，安装 `GitHub`：

```bash
gem install github
```
