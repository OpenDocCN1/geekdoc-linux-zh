
```
Apache -f "path_to_httpd.conf"
```

例如，你可以创建两个主 Apache 服务，一个响应端口 80，另一个响应端口 8080，方法是创建两个 `httpd.conf` 文件。你可以使用上述命令运行这些服务中的每一个。但是，在 Windows 2000 或 NT 系统中，已经安装了一个默认的 Apache 服务，因此你只需修改 `C:\Program Files\Apache Group\Apache\conf\httpd.conf` 以反映端口更改，并将其另存为另一个文件。然后，你只需使用上述命令运行一个 Apache 实例即可。默认的 Apache 配置仍然可以在端口 80 上运行。

要创建一个新的 Apache 服务，请从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令：

```apache
Apache -n new_service_name -f "path_to_httpd.conf" -k install
```

运行此命令将安装一个新服务，名为 `new_service_name`，它将使用 `path_to_httpd.conf` 路径。

你也可以使用 `Apache -n existing_service_name -k uninstall` 命令移除现有的 Apache 服务。

## 配置 Windows 下的 Apache

前面章节中找到的大多数信息也适用于 Windows 上的 Apache。然而，由于 Unix 系统和 Windows 系统在底层工作方式上的差异，Windows 版 Apache 和 Unix 版 Apache 之间存在某些区别。本章将讨论这些区别。

### Windows `httpd.conf` 语法

Unix 系统和 Windows 系统的 `httpd.conf` 文件之所以不同，是因为 Windows 处理路径名的方式不同。区别如下：

- 在 Windows 系统中，路径中的目录和文件名使用反斜杠分隔。例如，`c:\temp` 是一个有效的目录路径。但是，Apache 内部仍然使用前斜杠作为路径分隔符，因此你仍然必须使用前斜杠。例如，在 `httpd.conf` 文件中 `c:/temp` 是正确的，但 `c:\temp` 是错误的。

- Windows 路径通常包含空格。例如，`c:\Program Files\Apache Group\Apache\htdocs` 在 Windows 环境中是一个可接受的路径。在 `httpd.conf` 文件中使用此类路径名时，请用双引号将整个路径括起来。例如：

```apache
ServerRoot "C:/Program Files/Apache Group/Apache"
```

这里，`ServerRoot` 指令被设置为指向 `C:/Program Files/Apache Group/Apache` 目录。

# 第 21 章：配置 Windows 下的 Apache

- Windows 上的 `httpd.conf` 与 Unix 上的 `httpd.conf` 有何不同
- 调整 Apache 以优化性能
- 测试 Apache 配置
- 使用 Comanche 管理 Apache
- 为基于 Perl 的 CGI 脚本配置 Apache
- 如何在 Windows 上使用 `mod_perl`
- 如何在 Windows 上使用 PHP
- 如何在 Apache 中使用 ISAPI 扩展
- 如何在 Windows 上使用 `UserDir`

## 调整 Apache 性能

早在 Apache 2.0 之前，Windows 上的 Apache 就已经是多线程的。这是因为像 Windows 2000 和 Windows NT 这样的 Windows 系统在使用线程时比使用由多个子进程组成的服务表现更好。

在 Windows 系统中，Apache 仅使用两个进程运行。父进程监控子进程，后者负责使用多个线程处理所有请求。

为了控制在 Windows 下 Apache 可以同时处理多少个请求，你需要调整 `ThreadsPerChild` 指令。有关此指令的详细信息，请参见第 4 章。此指令控制负责所有请求的唯一 Apache 子进程可以创建的线程数。默认值 50 对于大多数网站来说应该足够了。

如果你需要更高的响应率，请确保你有适当的系统资源，例如足够的 RAM 和快速的 CPU 来支持你的速率需求。根据 `winnt_MPM` 模块的源代码，你应该可以将此值设置为最大 4096 个线程。对于大多数 Web 网站，低于 256 的数值可能更合适。

`MaxRequestsPerChild` 指令限制了子进程可以处理的请求数（有关此指令的详细信息，请参见第 4 章）。由于在 Windows 下单个子进程通过线程处理所有请求，因此此指令应设置为非常高的数值或 0，这意味着子进程将永不退出。

## 测试 Apache 配置

每次修改 `httpd.conf` 文件时，你都可以从 Apache 二进制目录（默认为 `C:\Program Files\Apache Group\Apache`）运行以下命令，以确定是否创建了任何语法错误。

```apache
Apache -t
```
