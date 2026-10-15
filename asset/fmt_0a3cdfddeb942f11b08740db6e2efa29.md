
在此示例中，我们使用 `systemd-run` 命令执行一个非特权用户的 Bash Shell 脚本，并说明该守护进程可以作为 systemd 服务被控制和监控。按照演示顺序执行以下步骤，以理解这些点：

1. 在你的家目录下创建一个可执行的 Bash Shell 脚本，命名为 `test-daemon.bash`，使用 `nano` 或你的文本编辑器：

```bash
#!/bin/bash
i=0
while sleep 10
do
  echo "<$i>This message is coming from a new-style daemon"
  i=$((i+1))%8
done
```

2. 执行以下命令，某些细节我们在第 17 节中提到过：

```
systemd-run --user --unit=test-daemon ./test-daemon.sh
```

Running as unit test-daemon.service.

3. 使用以下命令检查用户状态：

```
systemctl --user status test-daemon
```

```
test-daemon.service - /home/bob/.test-daemon.sh
Loaded: loaded
Transient: yes
Drop-In: /run/user/1000/system/test-daemon.service.d
L50-Description.conf, L50-ExecStart.conf
Active: (running) since Sat 2016-06-06 09:04:09 PDT; 20 ago
Main PID: 2252 (test-daemon.sh)
CGroup: /slice/user-1000.slice/user1000/test-daemon.service
-2252 /bin/sh /home/bob/.test-daemon.sh
-2252 sleep 10
Aug 06 09:04:09 bob[1152]: Started /home/bob/.test-daemon.sh.
Aug 06 09:04:19 bob test-daemon.sh[2252]: This message is coming from a new-style daemon
Aug 06 09:04:29 bob test-daemon.sh[2252]: This message is coming from a new-style daemon
Output truncated.
```

4. 最后，使用命令停止守护进程运行：

```
systemctl --user stop test-daemon
```

# 练习 18.1

使用 18.5.1.1 节中的四个步骤，将你选择的另一个具有个人意义且实用的 Bash 脚本转换为 systemd 控制的服务。然后根据你的用例，临时或永久地使用该服务。

## 18.5.1.2 与无关的守护进程

这里是同一个 Bash 脚本，但我们使用“永久”和特权用户技术将其转换为服务。按照所示顺序执行以下步骤，以理解这些点：

1. 在 `/usr/local/bin` 创建以下 Bash 脚本。命名为 `style.bash`，使用你喜欢的编辑器。执行此操作时请确保你有 root 权限，以便你可以在第 2 步中使用 `sudo` 命令保存并执行此文件：

```bash
#!/bin/bash
i=0
while sleep 10
do
    echo "<$i>This message is coming from a new-style daemon" > /dev/null
    i=$((i+1))%8
done
```

2. 当工作目录为 `/usr/local/bin` 时，以 root 身份执行脚本：

```
sudo ./style.bash
```

3. 编辑 `style.bash` 并在 `/etc/systemd/system` 中使用你喜欢的编辑器创建以下服务文件，命名为 `style.service`：

```ini
[Service]
ExecStart=/usr/local/bin/style.bash
```

4. 使用以下命令启动服务：

```
systemctl start style
```

5. 使用以下命令显示运行中守护进程的状态：

```
systemctl status style
```

6. 执行以下命令停止服务：

```
systemctl stop style
```

# 练习 18.14

使用 `journalctl -r` 查看 systemd 日志中的最新条目。输出中有任何显示新式的内容？

# 练习 18.15

使用 `journalctl -r` 查看 systemd 日志中的最新条目。输出中有任何显示新式的内容？

# 练习 18.16

使用 18.5.1.1 节中的步骤，将你选择的另一个 Bash 脚本转换为 systemd 控制的服务。然后根据你的用例，临时或永久地使用该服务。

## 18.5.2.1 如何在将其服务之前运行 webserver2

你必须在运行 `webserver2` 的目录下包含一个 `index.html` 文件。我们不会为你提供或阐述如何创建 `index.html` 文件，这部分留由你自行完成。

一旦你正确编译了 `webserver2`，就可以通过输入以下命令来运行它：

```
./webserver2 port_number /pathname_to_web_directory
```

其中

- `port_number` 是你想要监听的端口，例如 8083，
- `/pathname_to_web_directory` 是可执行二进制映像文件以及 `index.html` 文件所在的路径，例如 `/home/bob`

在 Linux Mint 系统上运行它的命令是：

```
./webserver2 8083 /home/bob/index.html
```

请注意，`webserver2` 是一个缓存服务器——它会向请求代理返回任何以 `.html`、`.jpg`、`.gif`、`.png`、`.ico` 和 `zip` 结尾的页面。它不支持运行通用网关接口 (CGI) 脚本、Perl 或超文本预处理器 (PHP) 扩展。

要测试 `webserver2`，请将浏览器设置为机器的 IP 地址（或 `localhost` `127.0.0.1`）以及你选择的端口 `port_number`。例如，通过打开你的 `index.html` 文件，我们将看到 URL 符合：

```
192.168.0.6:8083
```

你在 `index.html` 中定义的任何内容现在都会出现在你的 Web 浏览器中。

当你从 `webserver2` 提供 `index.html` 时，可以使用 `kill` 命令停止它，例如：

```
sudo kill -9 13325
```

其中

13325 是 `webserver2` 进程的 PID，如 `ps -C webserver2` 命令所示。

在进入下一节之前，你应该杀死 `webserver2` 守护进程。

## 18.5.2.2 Web服务器示例程序逻辑模型

遵循书籍网站上书中第 W21 章第 3–13 节所示的各种守护进程程序的基本设计和实现，我们的示例 `webserver2` 包含了与经典 Linux 守护进程模型非常相似的系统调用和程序结构。关于“旧式”Linux 守护进程模型的基本描述请参考图 W21.3。

## 练习 18.17

从程序结构的通用层面来看，`webserver2.c` 程序的代码与图 W21.3 所示的内容之间有什么区别？

我们的 `webserver2` 代码与图 W21.3 之间的主要区别之一是对程序健壮性的维护。这意味着在图中所示的 11 个步骤中的许多步骤，包含了错误检查与处理以及系统日志记录。

特殊的是，我们的示例 `webserver2` 守护进程中未设置为 0 的模型异常是：有一个独立的模块负责将所有的消息日志（包括错误）记录到系统日志中。例如，每当向 webserver 的传入请求产生异常时，这些错误将使用 `sd_print_journal` 系统调用记录在 systemd journal 中。此外，网页请求和发送也会记录在 systemd journal 中，允许系统管理员作为服务监控 `webserver2` 的运行情况，并通过超文本传输协议 (HTTP) 的 `get` 和 `post` 以及发布到日志的错误消息检查可能的入侵警报。

我们在本章最后提出了一个问题，让你将书籍网站第 W21 章第 3–13 节以及图 W21.3 中总结的系统调用与示例 `webserver2` 的系统调用进行对比。

## 18.5.2.3 在 webserver2 中使用日志应用程序接口 (API)

在本小节中，我们将展示 systemd journal 为日志记录提供的原生 API 系统调用。我们还阐述了在 `webserver2` 示例程序中使用这些原生 API 系统调用。
