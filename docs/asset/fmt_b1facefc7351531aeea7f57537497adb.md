
`send "character string"` 将字符字符串传输到调制调器

`sleep n` 等待 n 秒

`timeout n n` 限制 expect 的等待时间为 n 秒

`runscript` 的语法并不总是非常直观。一个特别令人烦人的命令是 `expect`：它只有当两个括号都放置在单独的行中，并且 `(` 括号后面跟着空格时才起作用（尽管该行本身不允许有其他命令）。因此，`runscript` 程序主要是耐心的问题（使用经过反复测试的试错法）。

要编写脚本程序，你可以直接用 `runscript` 执行它们，而无需先启动 `minicom`。现在必须通过键盘输入程序从调制调器期望的模式。

下面的示例显示了一个在 Unix 系统上典型登录的脚本。程序等待字符字符串 'ogin'（以便能识别 'Login' 和 'login'），然后发送用户名，等待 'word:'，然后发送密码，以此类推。

```
print "Login trial"

expect

  "ogin"

timeout 20 goto error

# 此处可以输入用户名

send "moser"

expect

  "word"

timeout 5 goto error

# 此处可以输入密码

send "sd4kkbs"

exit

error:

print "Something might have gone wrong!"
```

你应该为脚本文件的存储创建一个单独目录。为了确保 `minicom` 找到这些文件，你必须通过 `Ctrl+A, O, FILE-NAMES AND PATHS, C` 设置该目录。

请检查此目录及其包含的文件的访问权限，确保除了你之外没有其他人可以读取这些文件。毕竟，上述文件包含了你互联网账户的密码！如果你将脚本文件集成到你的电话线路中（它为脚本文件提供了单独的条目），`minicom` 在连接建立后会自动执行该文件。按照上述文件的模式，还可以实现更复杂的任务自动化。

# seyon

`seyon` 本质上执行与 `minicom` 相同的功能但在 X 下运行且稍微更容易处理。该程序通过按钮控制，大部分按钮的标记非常清晰。（某些额外功能可以通过 `MISC` 按钮执行。例如，在那里你会找到 `CAPTURE` 按钮。点击它后，所有的输入和输出都会写入文件 `~/.seyon/capture` ——遗憾的是，里面充满了特殊字符。）

由于其易于处理，本节主要集中在 `seyon` 的正确配置上。关于 `seyon` 的详尽信息可以通过 `man seyon` 或点击 `HELP` 获取。

通常情况下，`seyon` 会立即运行，而无需冗长的配置。你可能需要在调用命令中指定 `-modems /dev/ttySn` 选项，以告诉 `seyon` 它使用哪个接口访问调制调器。

![](img/b30873dd7753687a9253f0b556_0.png)

图 15.16 `seyon` 终端仿真器。

# 配置

`seyon` 通过多个配置文件进行控制。大多数文件位于 `~/.seyon` 目录，例如初始化文件 `startup`、电话列表 `phonelist` 以及各种传输协议的定义 `protocols`。可以在自己的家目录下找到用于复制的示例配置文件。

各种附加设置可以在 `.Xdefaults` 中完成。`.Xdefaults` 中最重要的设置可能是串口接口：

- *.Xdefaults
  `seyon` 的串口接口设置
  ```
  Seyon.modems: /dev/tty5
  ```

在 `phonelist` 中，每行只有两个强制指定：号码和标识该号码的文本。所有后续指示都以 `OPTION=` 的形式输入。两个最重要的选项是 `SCRIPT`（在连接建立后自动执行脚本文件）和 `BPS`（所需的传输速度）。

- *~/.seyon/phonelist
  ```
  123456 tugraz SCRIPT=grazlogin BPS=38400
  234567 mailbox SCRIPT=xylogin BPS=38400
  ```

`startup` 包含一些通用设置，如所需的传输速度、传输比特数等。

# 脚本编程

与 `minicom` 类似，`seyon` 也配备了脚本语言。然而，这种语言具有更强大的语法，类似于 `bash`。与在 `minicom` 中遇到的经验相比，为 `seyon` 编写脚本是一种纯粹的享受。通常，脚本文件存储在 `~/.seyon` 目录中。

所有脚本命令的精确定义在 man 文中提供。下表总结了最重要的命令。

## seyon 脚本命令

| # | 注释 |
| :--- | :--- |
| `echo "character string"` | 在屏幕上显示字符字符串 |
| `exit` | 终止脚本程序 |
| `goto label` | 跳转到标记为: 的行 |
| `pause n` | 等待 n 秒 |
| `transmit "character string"` | 将字符字符串传输到调制调器 |
| `waitfor "character string" [n]` | 等待指定的接收指定的字符字符串；如果未指定 n，超时时间为 30 秒 |

请注意，`transmit` 不传输回车符！必须显式指定换行符字符 `^M`。也可以位于之前的其他控制字符之前。以下最小示例可用于自动化登录 Unix 系统（指定用户名和密码）。

```bash
# "/seyon.ge/script.sample

echo "Login Script"

waitfor "login": 10

transmit "moser^M"

waitfor "word": 3

transmit "asd4JK^M"
```

## 15.7 写入 CD-ROM

本节介绍了 Linux 下的 ISO 镜像创建和 CD-ROM 刻录。重点将是 ISO 9660 格式的单会话数据 CD，而其他变体（音频 CD、多会话 CD）将不被考虑。

首先，是重要步骤的概述：

- 在刻录 CD-ROM 之前，你需要准备数据，即为 CD-ROM 文件系统处理过的数据创建一个 ISO 镜像。通常使用 `mkisofs` 命令来实现这一目的。
- 对于刻录 CD-ROM，你可以在 `cdwrite`（旧版，不再开发）和 `cdrecord` 程序之间进行选择。如果这些程序中都不支持你的 CD-R 驱动器，你也可以在 Windows 或其他操作系统下创建 CD；大多数 CD-R 程序都能写入用 `mkisofs` 创建的 ISO 镜像。
- 取决于内核版本和 SCSI 硬件，在刻录 CD-ROM 之前，可能需要对内核进行补丁并重新编译。
- 最后，你应该检查 CD-ROM。有许多程序可用，可以用于读取所有数据块或所有文件，以便将 CD-ROM 的内容与现有文件系统进行比较。
- 除了面向命令的程序 `mkisofs` 和 `cdrecord`，你也可以使用 X 程序 `xcdrecord`，它允许你在用户友好界面的帮助下完成这两个步骤。

> 本节所讨论的程序的最新版本可以在互联网上找到。
`http://ftp.ge.ucl.ac.uk/pub/mkhfs`
`http://ftp.fokus.gmd.de/pub/unix/cdrecord/`
`http://www.fh-muenchen.de/home/ze/rz/services/projects/xcdrecord`

### 创建和测试 ISO 镜像

创建 ISO 镜像最简单的方法是你想原样复制一张数据 CD（不是音频 CD！）时：

```bash
root# dd if=/dev/cdrom of=/usr/local/iso.img bs=2048
```

```bash
mkisofs [options] -o iso_file directory
```
