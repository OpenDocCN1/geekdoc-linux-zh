

下一个硬件需求是安装 Oracle 所需的磁盘空间。所需的磁盘空间根据所使用的安装类型而有所不同。表 30.2 显示了不同安装类型的所需磁盘空间。

## 表 30.2 Oracle 最小磁盘空间需求

| 安装类型 | 最小所需空间 |
|---|---|
| 最小 | 660MB |
| 典型 | 811MB |
|  | + Oracle8i Client= 306MB |
|  | + Programmer/2000= 276 MB |
| 自定义 | 660MB 至少 |

## 软件需求

就 Oracle 而言，本节与本书中的大多数章节不同。事实上，软件需求根据将要安装的 Oracle 版本以及您运行的 SuSE 版本而有所不同。本章中的 Oracle 安装说明在 SuSE Linux 6.3 或 6.2 上安装 Oracle 8.1.5 EE[STD]。如果您使用的是其他版本的 Oracle 或 SuSE Linux，您可能希望查看 http://www.suse.de/en/support/oracle/，这是一个由 SuSE 开发的网页，旨在让您更轻松地进行 Oracle 安装过程。

用于安装 Oracle 的软件包未随 SuSE Linux 6.3 CD 分发。它们可在以下 ftp 站点获得：ftp://ftp.suse.com/pub/SuSE-Linux/suse_update/Oracle/。

此外，这些文件也包含在本书记述光盘的 /suse_update/Oracle/oracle815-suse62.tar.gz 中。

这些文件包括以下内容：

- Oracle8i-EE.patch.tar.gz—对 Oracle 企业版的补丁，以使安装更容易且无差错（SuSE 版本 6.3 和 6.2）。
- Oracle8i-STD.patch.tar.gz—对 Oracle 标准版的补丁，以使安装更容易且无差错（SuSE 版本 6.3 和 6.2）。
- orarun.rpm—在系统启动时启动 Oracle 服务器的 init 脚本（SuSE 版本 6.3 和 6.2）。
- tcl75lib.rpm—仅在需要 Oracle Intelligent Agent 时需要（SuSE 版本 6.3 和 6.2）。
- javarunt.rpm—Java 运行库。您应该用随原始 SuSE 安装一起提供的软件包替换此软件包（SuSE 版本 6.3 和 6.2）。

## 在 SuSE Linux 6.3/6.2 上预安装 Oracle 8.1.5 EE|STD

如果您不知道发生了什么，安装 Oracle 可能是一项困难的任务。强烈建议您在安装 Oracle 时手边有本章以及 Oracle 手册。

### 提取和安装 SuSE 提供的软件（版本 6.3 和 6.2）

您需要提取从 SuSE ftp 站点下载的文件。事实上，此文件包含在安装 Oracle 之前应应用的软件包和补丁。作为 root 用户，执行以下命令以安装 SuSE 提供的软件：

```
bash#cp oracle815-suse62.tar.gz /tmp
bash#cd /tmp
bash#tar xvfz oracle815-suse62.tar.gz
bash#cd oracle815-suse62
bash#rpm -Uvh orarun.rpm
bash#rpm -Uvh tcl75lib.rpm
bash#rpm -Uvh javarunt.rpm
bash#ln -s /usr/local/jre /usr/lib/jre
```

### 应用补丁（版本 6.3 和 6.2）

如果您拥有安装 CD，此步骤是必要的，尽管令人恼火。您将不得不将 CD 的内容复制到您的硬盘上。之所以此步骤是必须的，是因为您考虑了 SuSE 对 Oracle 所做的补丁。应应用此补丁，以便安装顺利执行。请勿绕过此步骤；Oracle 安装包含错误，这些错误将由此补丁修复：

```
bash#mount /dev/cdrom /cdrom
bash#cp /cdrom /tmp/oracle -R
bash#cd /tmp/oracle
```

对于企业版：

```
bash#tar xzf ../oracle815-suse62/Oracle8i-EE-patch.tar.gz -C /tmp/oracle
bash#cd Oracle8i-EE-patch
bash#./INSTALL.sh
```

对于标准版：

```
bash#tar xzf ../oracle815-suse62/Oracle8i-STD-patch.tar.gz -C /tmp/oracle
bash#cd Oracle8i-STD-patch
bash#./INSTALL.sh
```

## 创建挂载点（版本 6.3 和 6.2）

您必须创建挂载点以供 Oracle 使用。挂载点用于确保不会发生 I/O 瓶颈，并且是 Oracle 安装的重要组成部分。作为 root 用户，创建以下目录以用作 Oracle 的挂载点：

```
bash#mkdir /u02    (Database mount point)
bash#mkdir /u03    (Another Database mount point)
bash#mkdir /u04    (Yet another Database mount point)
```

## 创建组（版本 6.2）

此步骤涉及创建能够管理、操作或使用 Oracle 的相应组。请记住，这些组对于安装过程和使用过程都很重要。

> 注意 数据库管理员以其在 DBA 组中的成员身份而闻名。必须创建此组才能安装或管理 Oracle。

使用 YaST 创建组 dba 和 oinstall。有关创建组的更多信息，请参阅第 4 章“管理用户和组”。

## 创建用户（版本 6.2）

在本部分，我们将讨论默认的 Oracle 用户，该用户能够启动安装过程并为首次使用做好准备。此过程的默认用户名为 oracle。此用户应使用第 4 章中提到的 YaST 创建。在创建此用户后，您应确保她属于组 oinstall，以便此用户可以启动安装过程。不仅此用户将执行安装过程，而且在安装过程完全结束后，她还将拥有 Oracle 软件。

## 设置环境变量（版本 6.2 和 6.3）

在本节中，您将设置在安装期间使用以及只要在系统上使用 Oracle 就会使用的环境变量。本节中应设置的变量从 Oracle 目录到所使用的语言各不相同。应设置以下变量：

- ORACLE_BASE—此变量包含 Oracle 软件安装的根目录。并非必须指定此目录，但强烈建议这样做。
- ORACLE_HOME—此变量包含 Oracle 软件的目录。此变量是必需的。
- NLS_LANG—此变量保存所使用语言的信息。它包含要使用的字符集。默认值是 US7ASCII。您应在安装过程中使用默认值。
- ORA_NLS33—此变量包含存储字符信息。只有在您使用除 US7ASCII 之外的存储字符时才重要，US7ASCII 是默认值。

表 30.3 显示了安装和运行 Oracle 所需的所有环境变量的默认值。

## 表 30.3 默认变量值

| 变量 | 默认值 |
|---|---|
| ORACLE_BASE | /u01/app/oracle (Oracle Standard) /opt/oracle (SuSE Standard) |
| ORACLE_HOME | /u01/app/oracle/product/8.1.5 (Oracle Standard) /opt/oracle/product/8.1.5 (SuSE Standard) |
| NLS_LANG | US7ASCII |
| ORA_NLS33 | $ORACLE_HOME/ocommon/nls/admin/data |

作为 root 用户，编辑您的 /etc/profile 文件并将以下行附加到其中：

```
export ORACLE_BASE=/opt/oracle
export ORACLE_HOME=/opt/oracle/product/8.1.5
export NLS_LANG=US7ASCII
export ORA_NLS33=$ORACLE_HOME/ocommon/nls/admin/data
```

编辑文件后，保存它并执行以下命令使更改生效：

```
bash$ source /etc/profile
```

## 在 SuSE Linux 6.3/6.2 上安装 Oracle 8.1.5 EE|STD

现在，组已就位，安装用户已就位，环境已设置——所有先决条件均已完成。现在，您需要开始安装。输入以下代码片段之一：

如果您使用的是企业版，请输入以下内容：

```
bash$ cd /tmp/Oracle8i-EE-patch
bash$ ./runInstaller
```

或者，如果您使用的是标准版，请输入以下内容：

```
bash$ cd /tmp/Oracle8i-STD-patch
bash$ ./runInstaller
```

Oracle Universal Installer（OUI）启动，显示欢迎消息并提示您按 Next（见图 30.1）。

## 图 30.1

Oracle Universal Installer 的首次启动基于 Java AWT，是图形化安装，而非旧的基于文本的安装。

![](img/659f91d9da7b29976c0625e2e9628511_604_0.png)

## 文件位置

下一个窗口——文件位置窗口——要求安装和清单文件的默认位置（见图 30.2）。这只是源路径和目标路径。如果您已按照本章前面所述设置环境变量，则默认情况下它们将被正确的值填入。

## 图 30.2

OUI 将通过其启动的路径使用源位置。目标文件位置是从您之前导出的环境变量中读取的。

![](img/659f91d9da7b29976c0625e2e9628511_604_1.png)

## UNIX 组

接下来，OUI 会询问可以访问安装和安装更新的 UNIX 用户组。输入组名 oinstall。OUI 将提示您必须使用 root 权限执行某些操作。打开另一个终端，例如 xterm 或 rxvt，然后输入以下命令：

```
bash$su -l
Password:
bash#cd /tmp/OraInstall
bash#./orainstRoot.sh
```
