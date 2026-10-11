

## 示例 13-9 运行 run_crack 脚本。（续）

```text
rmi -f dswlib.o debug.o rules.o stringlib.o *
make[1]: Leaving directory `/usr/local/src/crack/c50a/src/lib'
make[1]: Entering directory `/usr/local/src/crack/c50a/src/libdes'
/bin/rm -f *.O gasp core rpw destest des speed libdes.a nf5 *.old \*.bak destest rpw des speed
make[1]: Leaving directory `/usr/local/src/crack/c50a/src/libdes'
make[1]: Entering directory `/usr/local/src/crack/c50a/src/util'
rm -f *.O
make[1]: Leaving directory `/usr/local/src/crack/c50a/src/util'
make[1]: Entering directory `/usr/local/src/crack/c50a/src/lib'
make[1]: `/usr/local/src/crack/c50a/run/linux-2-unknown/lib05.a' is up to date.
make[1]: Leaving directory `/usr/local/src/crack/c50a/src/lib'
make[1]: Entering directory `/usr/local/src/crack/c50a/src/util'
all made in util
make[1]: Leaving directory `/usr/local/src/crack/c50a/src/util'
Crack: The dictionaries seem up to date...
Crack: Sorting out and merging feedback, please be patient...
Crack: Merging password files...
Crack: Creating gecos-derived dictionaries
mkgecosd: making non-permuted words dictionary
mkgecosd: making permuted words dictionary
Crack: Launching: cracker -kill run/Ktopcat.8746
Done
----passwords cracked as of Sat Jun 5 13:26:45 CDT 1999----
Guessed bob [password] [ /usr/local/src/crack/c50a/run/tp/pass /bin/tcsh ]
----done----
<remainder of output snipped>
```

**find_files** 脚本。该脚本搜索 SUID 或 SGID 文件中的漏洞，并报告不寻常的设备文件、所有用户可写的目录、不寻常的文件名以及您可能需要知道的符号链接。

系统中随意存放的异常设备文件应当引起怀疑。**find_files** tiger 脚本将报告在非标准位置找到的设备文件。如果由于某种原因，您需要在非标准位置（也许是用于 FTP）保留合法的设备文件，您可以更新 `tiger.rc` 文件中的 `FS_DEVDIRS` 变量，以反映系统中的额外设备文件位置。

根据操作系统在处理符号链接时的行为不同，涉及符号链接的命令结果可能会令人惊讶。例如，在某些系统上，链接的所有权可能会改变，而在其他系统上，链接的*目标*的所有权可能会改变。**find_files** 报告会报告那些指向系统文件的符号链接。

**find_files** 脚本还会查找 `tiger.rc` 文件中由 `Tiger_Files_of_Note` 变量定义的不寻常文件名（参见第 352 页的表 13.6）。默认情况下，它检查 FSP 服务器控制文件（常被破解者用于文件传输），并报告没有有效所有者或组的文件。请检查这些文件并核实是否由您安装。您可能还需要设置有效的所有者和组。

1. 脚本 **find_files** 中的注释引用了变量 `FS_FILES`，但实际上使用的是 `Tiger_Files_of_Note`。

当发现 SUID 或 SGID 脚本时，tiger 试图确定这些文件是否属于原始操作系统发行版的一部分。由于竞态条件（race conditions）的利用，编写安全的 SUID 和 SGID 程序非常困难。为此检查，tiger 需要拥有系统目录中 SGID 和 SUID 文件的列表。如果您的特定发行版中没有 SUID 文件列表，tiger 将报告系统中存在的所有 SUID 文件。

SUID 脚本中存在相对路径可能导致系统被入侵，如果用户可以精心构造包含被引用名称压缩版本的目录层次结构；因此，所有此类文件都会被报告。此外，find_files 还将报告在系统中找到的常规二进制文件的任何 SUID 副本。

最后，find_files 将报告所有用户可写的目录。所有用户可写的目录可以为入侵者提供存储或可能删除文件的地方。

## tigexp 脚本

tigexp 脚本用于解释单个消息 ID、在现有安全报告中插入解释，或生成一个包含安全报告中引用的所有消息 ID 完整解释的单独列表。该实用程序在第 373 页的“解码 tiger 输出”中作了更详细的说明。

## check_symlink 脚本

check_symlink 脚本位于 tiger 主目录的 scripts/misc 子目录中（我们一直使用的是 /usr/src/tiger）。该脚本测试您的系统在执行 chown 或 chmod 时是否跟随符号链接。如果是，那么在更改用户目录或 /tmp 中文件的所有权或权限时，您可能无意中更改了与安全相关的文件的权限。这是一个独立脚本；您可以单独运行它来测试系统的行为。

# 安装 tiger 以通过 cron 运行

如果您选择安装 tiger 使其可以通过 cron 运行，请从编辑 /usr/src/tiger/Makefile 开始。验证安装目录的配置是否反映了您的选择。示例 13-10 显示了您根据安装目录选择可能需要编辑的 Makefile 中的行。

## 示例 13-10 编辑 tiger Makefile

```text
TIGERHOME=/usr/local/tiger
...
TIGERWORK=/var/spool/tiger/work
...
TIGERLOGS=/var/spool/tiger/logs
...
TIGERBIN=/var/spool/tiger/bin
...
```

## 顺便提一下……

> 如果您正在安全服务器上设置 `tiger`，可以在安装完成后将 `TIGERHOME` 目录设置为只读。`TIGERROOT` 和 `TIGERLOGS` 目录在 `tiger` 执行时需要可写，但在其他时间应受保护以防篡改。建议选择仅属于 `tiger` 的私有目录。不要使用 `/tmp` 目录。

现在按示例 13-11 所示执行 `make`。

## 示例 13-11 使用 make 安装 tiger

```text
make
#
#if [ ! -d /usr/local/tiger ]; then \
# mkdir -p /usr/local/tiger; \
# chmod 755 /usr/local/tiger; \
# fi; \
#if [ ! -d /usr/local/tiger/scripts ]; then \
# mkdir /usr/local/tiger/scripts; \
# chmod 755 /usr/local/tiger/scripts; \
#fi; \
...
<lots of output snipped>
...
#chmod 644 /usr/local/tiger/conf/g;
```

根据您的处理器、用户数量和内存量，某些检查将比其他的耗时更长。您会希望更频繁地运行某些脚本。例如，您可能不希望每天运行 `crack`（不过话说回来，您是 root---如果您想这样做也可以）。

既然您已经安装了 `tiger`，您可以设置 `cron` 时间表以定期在您的自定义时间表中运行 `tiger` 的各个部分。这包括添加一个 `cron` 任务，例如每小时运行一次 `tiger/cron`。`tiger/cron` 将检查 `crontab` 文件，并仅运行您计划的任务，从而使 root 的 `crontab` 稍微整洁一些。

`tiger` 首次通过 `tiger/cron` 运行时，您（或通过 `tiger.conf` 文件中的 `Tiger_Mail_RCPT` 变量配置的用户）将通过电子邮件收到完整报告。在后续运行中，仅报告自上次运行以来的更改。

示例 13-12 展示了一个示例 `crontab` 文件。

## 示例 13-12 示例 crontab 文件

```text
# Sample 'tiger/cron' crontab file...
# By running 'tiger/cron' from `cron` say, once an hour:
# 0 * * * * .../tiger/cron >/dev/null 2>&1
# You can run the different checks in stages, without having to
# clutter up the crontab for root.
#-------------------------------------------------------------
```

## 示例 13-12 示例 cronce 文件（续）

```text
#
# Field 1: Comma separated list of hours (0-23) or `*` when this should be run.
#
# Field 2: Comma separated list of days of month or `*` when this should be run.
#
# Field 3: Comma separated list of days of week or `*` when this should be run. Days of week must be exactly as `date' prints.
#
# Remaining fields: Scripts to execute
#
0,8,16 * * * check_known
2 * * check_accounts check_roots check_netro check_anonftp
1 * * check_perms check_signatures check_group check_passed
3 * Mon check_inetd check_exports check_aliases check_path check_cron
2 * Sun find_files
2 1 * crack_run
```

示例 13-13 展示了 root 的 crontab 中的两行示例。可以在命令行中指定特定的 tigercron 文件。

## 示例 13-13 tigercron 的示例 crontab 条目

```text
0 * * * * /usr/local/tiger/tigercron >/dev/null 2>&1
0 * * * * /usr/local/tiger/tigercron alternate.cronc >/dev/null 2>&1
```

tigercron 按照表 13.8 中指定的顺序使用变量来定位 tiger 主目录。

## 我应该运行哪些脚本？

在继续之前，让我们花点时间讨论您可能想运行哪些脚本，以及运行的频率。如果您有多台机器，您可以为每种类型的系统设置不同的 cronrc 文件。您可能有用于用户开发的机器（至少他们这么说）。

| 选项 | 值 |
|:-|:-|
| -B | 指定 tiger 的 Basedir。如果使用此选项，它将优先于其他两种方法。 |
| TIGERHOMEDIR | tiger 将检查您的 UNIX shell 是否有 TIGERHOMEDIR 环境变量；如果存在，该值优先于 TigerInstallDir。 |
| TigerInstallDir | 如果未设置其他两个选项，则使用此值。TigerInstallDir 是安装前在 Makefile 中分配给 TIGERHOME 的值。在通过 make 安装 tiger 时，此值会被复制到所有脚本中。 |

