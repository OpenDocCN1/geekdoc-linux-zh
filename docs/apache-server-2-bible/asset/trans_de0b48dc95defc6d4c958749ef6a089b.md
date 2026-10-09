

## 使用 Tripwire 保护您的 Web 内容

作为向开源软件迈出的一大步，Tripwire 在通用公共许可证（GPL）下发布了 Tripwire 开源版 Linux 版本。简而言之，Tripwire 是一个文件和目录完整性检查器，它针对所有文件和目录创建签名数据库，并将它们存储在单个文件中。当再次运行 Tripwire 时，它会计算当前文件和目录的新签名，并将其与数据库中原有的签名进行比较。如果存在差异，该文件或目录的名称将连同差异信息一起被报告。

现在你可以明白，为什么 Tripwire 可以帮助确定入侵期间哪些文件被修改，成为一个非常出色的工具。当然，要做到这一点，你必须确保应用程序所使用的数据库的安全性。在设置新的服务器系统时，许多经验丰富的系统管理员会按照以下顺序执行以下操作：

- 1. 确保新系统未连接到任何网络，以保证尚未有人在其系统安全中安装木马程序、病毒程序或其他威胁。
- 2. 运行 Tripwire 创建所有重要系统文件的签名数据库，包括所有系统二进制文件和配置文件。
- 3. 将数据库写入可重写 CD-ROM。这可以确保高明的恶意攻击者无法修改 Tripwire 数据库来隐藏木马，或阻止程序识别已修改的文件。监控文件数量较少的管理员通常使用软盘来存储数据库。将数据库写入软盘后，软盘将被设置为写保护状态，如果 BIOS 允许，硬盘将被配置为只读设备。
- 4. 设置一个 cron 任务，定期（每日、每周、每月）运行 Tripwire，使应用程序使用 CD-ROM 版本的数据库。

### 获取 Tripwire

Red Hat Linux 附带了 Tripwire 的二进制 RPM 文件。但是，你始终可以从 RPM 镜像站点（如 `http://fr.rpmfind.net`）下载免费的（LGPL）Tripwire 版本。我使用该站点通过 `http://fr.rpmfind.net/linux/rpm2html/search.php?query=Tripwire` 下载了 Tripwire 的源代码和二进制文件。我下载的源代码 RPM 缺少一些安装脚本，因此我从位于 `http://sourceforge.net/projects/tripwire/` 的 Tripwire 开源开发站点再次下载了源代码。我下载的源代码名为 `tripwire-2.3.0-src.tar.gz`。当你阅读本文时，你可能会在那里发现更新的版本。

### 编译 Tripwire

本节向你展示如何从 `tripwire-2.3.0-src.tar.gz` 文件编译、配置和安装 Tripwire。在执行这些步骤时，请确保将你下载的版本替换为 Tripwire 的实际版本号。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_705_0.png)

**注意**

如果你希望从二进制 RPM 包安装 Tripwire，只需从 Tripwire RPM 所在的目录运行 `rpm -ivh tripwire-version.rpm` 命令即可。你仍然需要通过运行 `twininstall.sh` 来配置 Tripwire。请从 `/etc/tripwire` 目录运行此脚本，并跳转到下一节的第 7 步。

要从源码发行版进行编译，请执行以下操作：

- 1. 作为 root 用户，使用 `tar xzvf tripwire-2.3.0-source.tar.gz` 命令解压 tar 包。这将创建一个名为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src` 的子目录。将当前目录更改为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src/src` 目录。
- 2. 运行 `make release` 命令编译所有必要的 Tripwire 二进制文件。这需要一点时间，所以最好在喝咖啡前执行。编译完成 Tripwire 后，你需要安装二进制文件。将目录更改为 `/usr/src/redhat/SOURCES/tripwire-2.3.0-src/install`。使用 `cp install.* ..` 命令将 `install.cfg` 和 `install.sh` 文件复制到父目录。
- 3. 在运行安装脚本之前，可能需要编辑 `install.cfg` 文件，如列表 23-5 所示。例如，如果你不是 vi 编辑器的粉丝，而是支持 emacs，你需要将文件中的 `TWEDITOR` 字段更改为指向 emacs，而不是 `to /usr/bin/vi`。我不建议更改 `CLOBBER`、`TWBIN`、`TWPOLICY`、`TWMAN`、`TWDOC`、`TWDOCSDIR`、`TWSITEKEYDIR` 或 `TWLOCALKEYDIR` 设置的值。但是，你可能需要更改 `TWLATEPROMPTING`、`TWLOOSEDIRCHKS`、`TWMAILNOTIFICATIONS`、`TWMAILREPORTLEVEL`、`TWREPORTLEVEL`、`TWSYSLOG`、`TWMAILMETHOD` 和 `TWMAILPROGRAM` 的值。

**列表 23-5: install.cfg**

```
#
# install.cfg
#
# default install.cfg for:
# Tripwire(R) 2.3 Open Source for Linux
#
# NOTE:  This is a Bourne shell script that stores installation
#  parameters for your installation.  The installer will
#  execute this file to generate your config file and also to
#  locate any special configuration needs for your install.
#  Protect this file, because it is possible for
#  malicious code to be inserted here.
#
# This version of Tripwire has been modified to conform to the FHS
# standard for Unix-like operating systems.
#
# To change the install directory for any tripwire files, modify
# the paths below as necessary.
#
#------------------------------------------------

# If CLOBBER is true, then existing files are overwritten.
# If CLOBBER is false, existing files are not overwritten.
CLOBBER=false

# Tripwire binaries are stored in TWBIN.
TWBIN="/usr/sbin"

# Tripwire policy files are stored in TWPOLICY.
TWPOLICY="/etc/tripwire"

# Tripwire manual pages are stored in TWMAN.
TWMAN="/usr/man"

# Tripwire database files are stored in TWDB.
TWDB="/var/lib/tripwire"

# Tripwire documents directory
TWDOCS="/usr/doc/tripwire"

# The Tripwire site key files are stored in TWSITEKEYDIR.
TWSITEKEYDIR="${TWPOLICY}"

# The Tripwire local key files are stored in TWLOCALKEYDIR.
TWLOCALKEYDIR="${TWPOLICY}"

# Tripwire report files are stored in TWREPORT.
TWREPORT="${TWDB}/report"

# This sets the default text editor for Tripwire.
TWEDITOR="/bin/vi"

# TWLATEPROMPTING controls the point when tripwire asks for a password.
TWLATEPROMPTING=false

# TWLOSEDIRCHK selects whether the directory should be monitored for
# properties that change when files in the directory are monitored.
TWLOOSDIRCHK=false

# TWMAILNOVIOLATIONS determines whether Tripwire sends a no violation
# report when integrity check is run with - email-report but no rule
# violations are found. This lets the admin know that the integrity
# was run, as opposed to having failed for some reason.
TWMAILNOVIOLATIONS=true

# TWEMAILREPORTLEVEL determines the verbosity of e-mail reports.
TWMAILREPORTLEVEL=3

# TWREPORTLEVEL determines the verbosity of report printouts.
TWREPORTLEVEL=3

# TWSYSLOG determines whether Tripwire will log events to the system log
TWSYSLOG=false

######################################################################
# Mail Options - Choose the appropriate
# method and comment the other section
######################################################################
#
#####################
# SENDMAIL options - DEFAULT
#
# Either SENDMAIL or SMTP can be used to send reports via TWMAILMETHOD.
# Specifies which sendmail program to use.
################################################################

TWMAILMETHOD=SENDMAIL
TWMAILPROGRAM="/usr/lib/sendmail -oi -t"

######################################################################
# SMTP options
#
# TWSMTPHOST selects the SMTP host to be used to send reports.
# TWSMTPPORT selects the SMTP port for the SMTP mail program to use.
######################################################################

# TWMAILMETHOD=SMTP
# TWSMTPHOST="mail.domain.com"
# TWSMTPPORT=25

###############################################################################################################################################
# Copyright (C) 1998-2000 Tripwire (R) Security Systems, Inc. Tripwire (R) is a
# registered trademark of the Purdue Research Foundation and is licensed
# exclusively to Tripwire (R) Security Systems, Inc.
###############################################################################################################################################
```

- 4. 运行 `./install.sh` 命令。此命令将引导你完成安装过程。你需要按 Enter 键以接受 GPL 许可协议，并同意文件将复制到的位置。
- 5. 文件复制完成后，系统将提示你输入站点口令短语。此口令短语用于加密 Tripwire 配置和政策文件。请输入一个强口令短语（即不易被猜出且长度至少为 8 个字符的短语），以确保这些文件不会被任何未知方修改。接下来，选择一个本地口令短语。此口令短语用于加密 Tripwire 数据库和报告文件。同样，请在此处选择一个强口令短语。

