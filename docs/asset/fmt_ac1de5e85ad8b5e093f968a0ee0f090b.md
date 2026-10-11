
- 1. 使用打印机的 URI，排除开头的 `smb://`。例如，你可能输入 `/host1/myprinter` 或 `/mygroup/host1/myprinter`。

- 2. 选择“需要身份验证时提示用户”或“现在设置身份验证信息”。

- 3. 如果你选择“现在设置身份验证信息”，填写用户名和密码以访问 SMB 打印机；然后点击“验证”检查你是否可以对服务器进行身份验证。

- 4. 点击“下一步”继续。

或者，你可以识别未出现在服务器列表上的服务器。输入创建 SMB URI 所需的信息，包含以下内容：

工作组（Workgroup）：这是分配给 SMB 服务器的组名。在所有情况下并不一定需要使用工作组名。

服务器（Server）：这是计算机的 NetBIOS 名称或 IP 地址，它可能与 TCP/IP 名称相同也可能不同。为了将此转换为访问 SMB 服务器所需的地址，Samba 会检查多个名称可能被分配给 IP 地址的地方。Samba 会按照所示顺序检查以下位置，直到找到匹配项为止：`/etc/hosts` 文件、`/etc/lmhosts` 文件、网络上的 WINS 服务器，以及对每个本地网络接口的广播做出响应以解析名称。

共享（Share）：这是打印机与远程计算机共享的名称。它可能与 SMB 打印机本地用户识别该打印机的名称不同。

用户（User）：SMB 服务器系统需要用户名来让你访问 SMB 打印机。如果你是基于共享级别而非用户级访问控制对打印机进行身份验证，则不需要用户名。在共享级访问下，你可以为每个共享的打印机或文件系统添加密码。

# 第 16 章：配置打印服务器

**密码** 使用与 SMB 用户名和共享资源相关的密码，取决于所使用的访问控制类型。

> **注意**
>
> 当你为 SMB 输入用户名和密码时，这些信息将以未加密的形式存储在 `/etc/cups/printers.conf` 文件中。请确保该文件仅对 root 可读。

以下是一个你可以添加到 `SMB://` 框中的 SMB URI 示例：

`jjones:my9passwdFSTREET/NS1/hp`

此处的 URI 标识了用户名 (`jjones`)、用户密码 (`my9passwd`)、工作组 (`FSTREET`)、服务器 (`NS1`) 以及打印机队列名称 (`hp`)。

按照你处理本地打印机的方式完成剩余操作（请参见本章较早的“添加本地打印机”章节）。

如果所有设置都得当，你可以使用标准的 `lp` 命令将文件打印到打印机。使用此示例，请采用以下格式进行打印：

```
$ cat file1.ps | lp -P NS1-PS
```

> **提示**
>
> 如果你收到失败消息，请确保你打印的目标计算机是可以访问的。对于打印机 NS1 示例，你可以输入 `smclient -L NS1 -U jjones`。然后输入密码（在此情况下为 `my9passwd`）。`-L` 请求有关服务器的信息，`-U jjones` 表示用户 `jjones`。

## 第四部分：成为 Linux 服务器管理员

接受：是

共享：否

作业单：无 无

配额周期：0

页限制：0

限制：0

`<Printer>`

这是一个本地打印机的示例，作为本地系统的默认打印机。设置 `Shared No` 值是因为该打印机目前仅在本地系统可用。最有趣的信息与 `DeviceURI` 有关，它显示打印机连接到并行端口 `/dev/lp0`。状态为空闲（准备好接受打印作业），`Accepting` 值为是（打印机默认接受作业）。

`DeviceURI` 有几种方法可以识别打印机名称，反映了打印机的连接方式。以下是 `printers.conf` 文件中的一些示例：

```
DeviceURI parallel:/dev/lp1
DeviceURI serial:/dev/ttyUSB1?baud=3840+size=8+parity=none+flow=soft
DeviceURI scsi:/dev/scsi/scid60
DeviceURI usb://hostname:port
DeviceURI socket://hostname:Port
DeviceURI tftp://hostname/path
DeviceURI ftp://hostname/path
DeviceURI http://hostname[:port]/path
DeviceURI ipp://hostname/path
DeviceURI smb://hostname/printer
```

前四个显示了本地打印机（并行、串口、scsi 和 usb）的形式。其他示例用于远程主机。在每种情况下，`hostname` 是主机名或 IP 地址。`Port` 或路径定义了每个打印机在主机上的位置。例如，`hostname` 可以是 `myhost.example.com:631`，`path` 可以替换为你喜欢的任何名称，例如 `printers/myprinter`。

## 使用打印命令

为了与旧的 UNIX 和 Linux 打印设施兼容，CUPS 移植了许多用于打印的旧命令。大多数使用 CUPS 的命令行打印可以使用 `lp` 命令完成。LibreOffice、OpenOffice 和 AbiWord 等文字处理应用程序已设置为使用此设施进行打印。

你可以使用“打印设置”窗口为每个打印机定义所需的过滤器，以便文本能够正确格式化。`lp` 命令的选项可以添加过滤器来正确处理文本。管理文档的其他命令包括 `lpq`（查看打印队列内容）、`lprm`（从队列中删除打印作业）和 `lpstat -t`（控制打印机）。

# 第 16 章：配置打印服务器

### 使用 lp 打印

你可以使用 `lp` 命令将文档打印到本地和远程打印机（前提是打印机已本地配置）。文档文件可以添加到 `lp` 命令行的末尾，或者通过管道 (`|`) 重定向到 `lp` 命令。这是一个简单的 `lp` 命令示例：

```
$ lp doc1.ps
```

当你仅用 `lp` 指定文档文件时，输出将重定向到默认打印机。作为个人用户，你可以通过设置 `PRINTER` 变量的值来更改默认打印机。通常，你会将 `PRINTER` 变量添加到你的启动文件之一，例如 `$HOME/.bashrc`。例如，在 `.bashrc` 文件中添加以下行可以将你的默认打印机设置为 `lp3`：

```
export PRINTER=lp3
```

要覆盖默认设置，请在 `lp` 命令上指定特定的打印机。以下示例使用 `-P` 选项来选择不同的打印机：

```
$ lp -P anypons doc1.ps
```

`lp` 命令有多种选项，允许 `lp` 解释并格式化不同类型的文档。`-# num`，其中 `num` 替换为打印的副本数（1 到 100），以及 `-1`（这会导致文档以原始模式发送，假设文档已经格式化）。要 l了解更多选项，请输入 `man lp`。

### 使用 lpstat -t 列出状态

使用 `lpstat -t` 命令列出打印机的状态。这是一个示例：

```
$ /usr/sbin/lpstat -t
printer hp disabled Wed 10 Jul 2019 10:53:34 AM EDT
printer deskjet-555 is idle. enabled Wed 10 Jul 2019
10:53:44 AM EDT
```

此输出显示了两个活动状态打印机。`hp` 打印机目前处于禁用状态（离线）。`deskjet-555` 已启用。

### 使用 lprm 删除作业

用户可以使用 `lprm` 命令从队列中删除自己的作业。在命令行上单独使用 `lprm` 会从默认打印机中删除该用户的所有作业。要从特定打印机删除删除作业，请使用 `-P` 选项，如下：

```
$ lprm -P lp0
```

要删除当前用户的所有作业，请输入以下：

root 用户可以通过在 `lprm` 命令行上指定用户来删除该用户的所有打印作业。例如，要删除名为 mike 的用户的所有打印作业，root 用户输入：

```
# lprm -U mike
```

要从队列中删除单个打印作业，请在 `lprm` 命令行上指定其作业号。要查找作业号，请输入 `lpq` 命令。该命令的输出可能如下：

```
# lpq
```

| Rank | Owner | Job | Files | Total Size |
| :--- | :--- | :--- | :--- | :--- |
| active | root | 133 | /home/jake/pr1 | 467 |
| 2 | root | 197 | /home/jake/mydoc | 23948 |

输出显示有两个可打印作业在等待-（注意：OCR 文本截断或重复）。

## 配置打印服务器

root 用户可以通过在 `lprm` 命令行上指定用户来删除该用户的所有打印作业。例如，要删除名为 mike 的用户的所有打印作业，root 用户输入：

```
# lprm -U mike
```
