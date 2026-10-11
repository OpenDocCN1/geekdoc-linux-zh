
## 通过 FTP 连接 IBM i5/OS

本章讨论了从 Linux 操作系统访问存储在 IBM i5/OS 系统上的数据的文件传输协议（FTP）方法。涵盖的方法包括：

- FTP 操作技巧
- 在交互模式下运行 FTP 命令
- 在批处理模式下运行 FTP 命令

### 7.1 FTP 操作

FTP 是传输控制协议/网协议（TCP/IP）的标准。FTP 包含客户端和服务器应用程序。大多数操作系统都包含客户端应用程序，并且通常在交互模式下运行。大多数操作系统也包含服务器应用程序。然而，服务器应用程序在后台或批处理模式下运行，必须显式启动。

#### 7.1.1 常用 FTP 命令

FTP 中有两种传输数据的方式。这是二进制模式和美国标准信息交换代码（ASCII）模式。在二进制模式下，文件的位将按原样复制。对对数据进行任何转换。二进制模式用于传输实际程序、图像、文件对象和其他。在非二进制模式下，数据可以在两个系统之间进行转换。非二进制模式（或 ASCII 模式）用于文本文件、程序源代码和其他人类可的文件。默认情况下，你的 FTP 会话为非二进制模式。要切换到二进制模式，输入 FTP 命令 `bin`。

要启动 FTP 会话，输入 `ftp [server]`，其中 `server` 是你想要传输文件的系统的主机名或 IP 地址。启动 FTP 会话后，你可以使用 `get` 命令从远程系统获取文件到本地系统，并使用 `put` 命令将文件从本地系统上传到远程系统。你可以在单个 FTP 会话中执行多次 `get` 和 `put` 命令。

当初始化 IBM/OS 的 FTP 时，你处于 `QSYS` 文件系统。对于文件内的对象通过 `library/file/member` 访问，对于非文件对象通过 `library/object` 访问。你也可以访问集成文件系统（IFS）中的文件。要切换到 IFS 模式，输入 FTP 命令 `quote site namefmt 1`, `cd /`。访问 QSYS 文件可以使用 `/qsys.lib/library.lib/file/member.mbr` 或 `/qsys.lib/library/object.type`。访问 IFS 中的文件可以使用 `/directory/directory2/file.name`，其中 `file.name` 是你想要的文件名。

其他 FTP 命令是 `cd` 和 `lcd`，它们分别更改远程和本地系统的目录位置。`prompt` 命令与 `mget` 或 `mput` 配合使用非常有用。

#### 7.1.2 管理 FTP

配置 i/OS 使用命令 `CHGPTBL *`。启动和停止 FTP 使用 `ENDTCPSVR *`。

或者，对于 i/OS 使用命令 `STRTCPSVR`

### 7.2 使用 Linux 作为客户端

从 IBM i/OS 传输数据与从 Linux 传输数据相同，不同在于 i/OS 拥有不同的文件系统。FTP 命令从 IBM i/OS 命令行发布，并登录到 Linux 服务器需要 Linux 系统上的 FTP 服务器正在运行。通常你使用 `QSYS` 文件系统。如果你需要更改本地目录到 IFS，则使用 FTP 命令 `quote namefmt 1`。

`cd` 命令用于更改本地系统的目录，在本例中，即 IBM i/OS 系统。`cd` 命令用于更改远程或 Linux 系统的目录。如果不使用 `prompt` 命令，在传输每个文件之前，系统会提示你是否传输该文件。

### 7.4 在批模式下运行 FTP 命令

到目前为止，我们展示了交互式运行的 FTP 命令。虽然这是常用的用法，但也可以以批处理或程序模式执行 FTP 命令。在 IBM i/OS 的控制语言 (CL) 程序或 Linux 系统的上的脚本文件中，你可以输入 FTP 命令，提供或被提示输入用户名和密码，然后运行若干 FTP 命令。你可以使用 FTP 的 `run` 命令来运行远程命令。

示例-2 是一个简单的脚本文件，它以 `ITUSER` 身份创建，提示输入密码，创建一个 IBM i/OS 库，创建多个源物理文件，放入多个源文件，创建一个刚刚下载的 CL 程序之一，并运行新创建的程序。

示例-7-2 示例 FTP 脚本文件：`download.txt`

```
quote rcmd crtlib sysymgt text('Systems Management Tools')
```

```
quote rcmd crcrcf sysymgt/qclsrc text('CL Programs')
```

```
put "iso/sysymgt/chgcmdft.cl sysymgt/qclsrc.chgcmdft
put "iso/sysymgt/startmpg.cl sysymgt/qclsrc.startmpg
put "iso/sysymgt/starttys.cl sysymgt/qclsrc.starttys
put "iso/sysymgt/startup.cl sysymgt/qclsrc.startup
put "iso/sysymgt/mapkeys.cl sysymgt/qclsrc.mapkeys
put "iso/sysymgt/create.cl sysymgt/qclsrc.create
put "iso/sysymgt/snads.cl sysymgt/qclsrc.snads
put "iso/sysymgt/ctl.cl sysymgt/qclsrc.ctl
put "iso/sysymgt/dev.cl sysymgt/qclsrc.dev
put "iso/sysymgt/lin.cl sysymgt/qclsrc.lin
put "iso/sysymgt/pt.cl sysymgt/qclsrc.pt
put "iso/sysymgt/tn.cl sysymgt/qclsrc.tn
```

```
quote rcmd crtlpg sysymgt/create sysymgt/qclsrc
```

```
quit
```

要在 Linux 上使用此 FTP 脚本文件，请使用以下命令：

```
ftp system < download.txt
```
