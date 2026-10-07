
Wine 是最古老的程序之一（至少就 Linux 而言是这样），并且拥有一个庞大的用户群为其提供支持。

从这里你可以探索相关章节：
- 在第 23 章 “Wabi” 中，使用 Wabi（Windows 应用程序二进制接口），它允许你在 X 窗口系统下运行 Windows 应用程序。
- 在第 26 章 “C 编程” 和第 27 章 “C++ 编程” 中，学习在 Linux 下编写 C 和 C++ 程序。
- 在第 56 章 “源代码控制” 中，学习使用源代码控制系统同时控制多个文件版本。

## 第 60 章 HylaFAX
*作者：Tim Parker*

### 本章内容
- 安装 HylaFAX 956
- 发送传真 961
- 接收传真 962

计算机更实用的方面之一是，它能够处理你用最喜欢的文字处理软件编写的文档，并将其传真给某人。与打印一份副本、将其放入传真机并手动发送的传统流程相比，这节省了时间、纸张和精力。计算机上的传真程序允许你从任何具有打印输出功能的应用程序发送传真，并接收来自他人的传入传真。

虽然为 PC 设计的最有效的传真程序是为 Windows 设计的，但 UNIX 和 Linux 也存在几种传真实用程序。你可以从众多供应商处为你的 Linux 系统购买商业传真软件包，但幸运的是，有些是免费的。如果你计划经常使用你的 Linux 系统，你可能需要考虑安装这些传真工具之一。

最常用的 Linux 传真实用程序称为 HylaFAX。HylaFAX 由 Sam Leffer 编写，免费提供。HylaFAX 并非对商业传真软件的劣质模仿，而是一个集传真接收和发送于一体的完整系统，在功能和实用性上与商业软件包不相上下。HylaFAX 依赖于 Ghostscript 系统来处理传真图像，因此如果你之前没有读过，可能需要阅读一下第 27 章 “C++ 编程” 中关于 Ghostscript 的内容。

### 安装 HylaFAX

大多数 Linux 发行版都包含 HylaFAX，作为 CD-ROM 套件的一部分。如果你没有获取到 HylaFAX 的副本，你可以从许多 FTP 和网站下载它。你可能会发现一个名为 FlexFAX 的程序，它是 HylaFAX 基于的早期实用程序。如果有选择，请选择 HylaFAX。对于大多数版本的 HylaFax，你还需要一个 C++ 编译器，因为只提供源代码。随大多数 Linux 系统附带的 GNU C++ 编译器就足够了。

**提示**
HylaFAX 可从大多数 FTP 站点获取，但该工具的“主页”是 ftp.sgi.com。请检查目录列表以获取 HylaFAX 信息。HylaFAX 的文档可通过 FTP 站点或万维网上的 http://www.sgi.com 获取。有关 HylaFAX 的更多描述和历史，请访问站点 http://www.vix.com/hylaFAX。

如果你有一个压缩、tar 打包的文件需要解压，HylaFAX 会将其内容转储到临时目录。例如，如果你有 HylaFAX 归档文件 HylaFax-v4.0-tar.gz，你可以使用以下命令解压并将其放入传真目录：

```bash
mkdir /usr/fax
cd /usr/fax
cp /tmp/HylaFax-v4.0-tar.gz .
gunzip HylaFax-v4.0-tar.gz
tar -xf HylaFax-v4.0-tar
```

以 root 身份执行所有这些步骤。当然，你必须将放置 HylaFAX 归档文件的目录替换为上述命令中的 /tmp。如果你不想使用 /usr/fax 作为 HylaFAX 目录，请同时更改这些命令到你的目标目录。

### 编译 HylaFAX

当传真目录中的所有文件都提取完成后，你需要调用 C++ 编译器以生成可执行文件。在子目录 /port/linux 中的某个文件中可能包含一些重要信息，通常是一个名为 README 的文件。要编译 HylaFAX，请发出以下命令（请记住，你必须以 root 身份登录）：

```bash
configure
make clean
make install
```

configure 和 make 命令会显示一系列步骤，我们稍后会查看这些步骤。当你发出 configure 命令时，你会看到一系列关于 HylaFAX 应使用哪些目录的消息：

HylaFAX 配置参数如下：
应用程序目录: /usr/local/bin
库数据文件目录: /usr/local/lib/fax
库可执行文件目录: /usr/local/lib/fax
服务器目录: /usr/local/etc
手册页目录: /usr/local/man
文档目录: /usr/local/doc/HylaFAX
暂存目录: /usr/spool/fax
uucp 锁文件类型: ascii
uucp 锁文件目录: /usr/spool/uucp
uucp 锁文件模式: 0444
PostScript 图像类型: gs
PostScript 图像程序: /usr/local/bin/gs
默认页面大小: 北美 Letter

默认垂直分辨率 (lpi): 98
字体度量目录: /usr/local/lib/afm
sendmail 程序位置: /usr/lib/sendmail
这些设置是否合适 [yes]?

不要更改任何这些默认目录位置，因为 Linux 中的许多其他应用程序都使用它们。当你发出 `make` 命令时，你需要等待几分钟让编译器完成其任务，因为它必须通过几个阶段并从你系统上的许多位置获取文件。

安装例程完成后，请检查目录 /usr/local/bin/fax 是否存在并包含文件。如果是，你就可以使用 HylaFAX 了。

### 添加调制解调器

下一步是将调制解调器添加到 HylaFAX。这通过 faxaddmodem 脚本添加，该脚本引导你完成配置调制解调器的每个步骤。HylaFAX 可与大多数 1 类和 2 类传真调制解调器一起工作，这意味着它可以支持当今大多数具有传真功能的调制解调器。当你运行 `faxaddmodem` 时，你会被问到一系列问题，其中大多数应保持默认设置（同样，此例程应以 root 身份运行）：

```bash
# faxaddmodem
Verifying your system is set up properly for fax service...

There is no entry for the fax user in the password file.
The fax software needs a name to work properly; add it [yes]?

    Added user "fax" to /etc/passwd.
    Added fax user to "/etc/passwd.sgi".

There does not appear to be an entry for the fax service in
either the yellow pages database or the /etc/services file;
should an entry be added to /etc/services [yes]?

There is no entry for the fax service in "/usr/etc/inetd.conf";
should one be added [yes]?

Poking inetd so that it rereads the configuration file.

There does not appear to be an entry for the FaxMaster in
either the yellow pages database or the /usr/lib/aliases file;
should an entry be added to /usr/lib/aliases [yes]?
Users to receive fax-related mail [root]?

Rebuilding /usr/lib/aliases database.
46 aliases, longest 81 bytes, 923 bytes total
```

完成系统设置验证。

调制解调器连接的串行端口 [/? cua0]

好的，是时候为调制解调器设置一个配置文件了。手册页 config(4F) 在此过程中可能很有用。另外请注意，你可以随时安全地中断此过程。

没有现有的配置。让我们从头开始。

传真调制解调器的电话号码 [/? +1.613.838.1234]

这是与正在配置的调制解调器关联的电话号码。它作为“身份”传递给对端传真机，也可能出现在传真服务器创建的标签行上。电话号码应使用完整的国际拨号规范，格式为 +<国家代码>. <区号>; <本地部分>。如果可能引起问题，为了可读性而包含的其他字符会自动移除。

- 区号 [/? 613]
- 国家代码 [1]?
- 长途拨号前缀 [1]?
- 国际拨号前缀 [011]?
- 正常服务器操作期间的跟踪 [1]?
- 发送和接收会话期间的跟踪 [11]?
- 接收传真的保护模式 [0600]?
- 接听前等待的振铃次数 [1]?
- 调制解调器扬声器音量 [off]?

服务器配置参数如下

FAXNumber:            +1.613.838.1234
AreaCode              613
CountryCode            1
LongDistancePrefix:    1
InternationalPrefix:   011
ServerTracing:         1
SessionTracing:        11
RecvFileMode:          0600
RingsBeforeAnswer:     1
SpeakerVolume:         off

这些设置是否合适 [yes]?

现在我们要探测 tty 端口，以确定连接的调制解调器类型。这需要几秒钟，请耐心等待。注意，如果你没有将调制解调器连接到端口，或者调制解调器未打开，这可能会导致挂起（只需去连接调制解调器或将其打开即可）。

