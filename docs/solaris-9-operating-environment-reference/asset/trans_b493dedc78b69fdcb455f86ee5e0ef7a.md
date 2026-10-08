

# 取消 (cancel)

# 117

当你将环境变量 `DATEMSK` 设置为日期掩码文件时，日历程序可以识别传统日期，也可以识别扩展格式的日期。

```
castle% setenv DATEMSK datemask
castle% calendar
Chiractic appointment September 16th of the year 1998.
castle%
```

## 环境变量

参见 `environ(5)` 以获取以下影响 `calendar` 执行的环境变量的描述：LC_TYPE、LC_TIME、LC_TYPE、LC_MESSAGES、LC_MESSAGES 和 TZ。

## 退出状态

- 0 成功完成。
- >0 发生错误。

## 文件

- /etc/passwd
系统密码文件。
- /tmp/cal* `calendar` 使用的临时文件。
- /usr/lib/calprogr
用于确定确定今天和明天日期的程序。

## 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SunMesu |

## 相关相关

at(1), crontab(1), mail(1), cron(1M), ypbind(1M), trftime(3C), attributes(5), environ(5)

# cancel — 取消打印请求

## 概要

```
/usr/bin/cancel [request-ID...] [destination...]
/usr/bin/cancel -u username... [destination...]
```

## 描述

`cancel` 命令用于在打印请求尚在队列中或正在打印时取消它们。要取消特定的打印请求，你需要知道打印作业的请求 ID（request ID）。请求 ID 始终包含打印机名称、一个连字符 (-) 和打印请求的数字。当从标准输入提交请求时，会显示请求 ID。要查找请求 ID，输入 `lstat` 并按回车键。只有提交请求的用户或以 root 或 ip 身份登录的用户才能取消打印请求。

你还可以通过以下方式使用 `cancel` 命令：

- 通过指定 `request-ID` 和 `destination` 参数，取消特定打印机上的特定打印作业。
- 通过指定 `destination` 参数取消特定目标上的所有作业。
- 通过指定 `-u username` 选项取消特定用户的所有请求。
- 通过指定 `-u username` 和 `destination` 参数，取消特定打印机上特定用户的所有请求。用户只能取消他们自己的打印请求。默认情况下，用户只能取消来自提交请求所在主机的打印请求。如果超级用户在打印服务器的 `/etc/printers.conf` 中设置了 `set-equivalence=true`，则用户可以取消任何主机上与其用户名关联的打印请求。超级用户（Supers）还可以取消请求提交所在主机上的打印请求。打印客户端命令在打印机数据库名称切换文件中查找目标信息。详情请参见 `nswitch.conf(4)`、`printers(4)` 和 `printers.conf(4)`![](img/185d23104c385df6a62d4cc96b9)

## 选项

- -u username 指定要取消打印请求的用户名。

## 操作数

- destination 指定取消打印请求的目标。`destination` 是打印机名称或打印机类。如果你不指定 `destination`，`cancel` 将使用 POSIX 风格（`server:destination`）或命名（FNS）（`...service/printer/..`）取消请求打印。打印客户端命令按特定顺序查找目标信息。详情请参见 `printers.conf(4)` 和 `printers(4)`。POSIX 风格的目标名称（`server:destination`）如果 `destination` 的格式与 LP 风格的请求-ID 相同，则被视为打印请求。
- request-ID 指定要取消的打印请求 ID，使用 LP 风格的 ID（`destination`）。

## 示例

以下示例列出了打印队列中的作业并使用不同的选项和操作数取消了它们。在第一个示例中，用户尝试取消 `ray` 拥有的打印作业。系统返回了提示符，但作业未从队列中移除。注意，当你没有权限取消某个作业时，`cancel` 命令不会显示错误消息。

```
castle% lpstat
castle-77      castle|winsor  Sep 29 030
castle-78      castle|winsor  Sep 29 032
castle-79      castle|winsor  Sep 29 033
castle-80      castle|ray    Sep 29 036
castle-81      castle|ray    Sep 29 037
castle-82      castle|root   Sep 29 040
castle% whoami
winsor
castle% cancel -u ray
```

在 root 用户身份下，下一个示例从打印机目标删除了 `winsor` 的打印作业。然后，用户尝试通过请求 ID 移除 `root` 拥有的打印作业。

```
castle% cancel -u winsor seild
castle-77: canceled
castle-78: canceled
castle-79: canceled
castle-80      castle|ray  Sep 29 036
castle-81      castle|ray    Sep 29 037
castle-82      castle|root   Sep 29 040
castle% su
Password:
castle cancel-82: canceled
castle childish
```

在接下来的示例中，root 删除了 `root` 拥有的打印作业，然后删除了打印机目标 `seild` 所有作业。注意，当你取消某个目标打印机的所有打印作业时，即使队列中列出了这些作业，也不会显示已取消的列表。

## 退出状态

- 0 成功完成。
- non-zero 发生错误。

## 文件

- /etc/passwd
系统密码文件。
- /tmp/cal* `calendar` 使用的临时文件。
- /usr/lib/calprogr
用于确定今天和明天日期的程序。

## 属性

参见 `attributes(5)` 以获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SunMesu |

## 相关相关

at(1), crontab(1), mail(1), cron(1M), ypbind(1M), trftime(3C), attributes(5), environ(5)

# cat — 合并并显示文件

## 概要

```
/usr/bin/cat [-nbuv] [file...]
```

## 描述

使用 `cat` 命令创建文件、合并两个文件到第三个文件、将一个文件追加到另一个文件的末尾或在标准输出上显示文件内容。

以下语法创建一个新的命名文件。按下回车键后，每行写入文件。如果文件不存在，则会创建它。如果它已经存在，则将被覆盖且无警告。

```
cat > file
```

以下语法在终端上显示文件的内容。

```
cat * file
```

# 合并

以下语法合并 file1 和 file2 并结果写入 file3。如果你没有提供输入文件，`cat` 将从标准输入读取。

```
cat file1 file2 >file3
```

以下语法将 file1 的内容追加到 file2 的末尾。

```
cat file1 >>file2
```

以下语法按顺序在终端显示 file1、file2 和 file3。

> 注意 — 将输出重定向到正在读取的文件之一将覆盖该文件的原始数据。

## 选项

- -n 在每行输出前加上行号。
- -b 类似于 -n 编号，但省略空行的行号。
- -s 对不存在的文件保持沉默。
- -u 不缓冲输出。（默认是缓冲输出。）
- -v 显示非打印字符（制表符、换行符和馈符除外）。ASCII 控制字符（八进制 000–037）打印为 ^n，其中 n 是对应的 ASCII 字符（八进制 100–137 @ A, B, C, ..., X, Y, Z, [, \], ^ 和 _）；DEL 字符（八进制 0177）打印为 ？其他非打印字符打印为 M-x，其中 x 是由低七位指定的 ASCII 字符。你可以将以下选项与 -v 选项结合。

- -e 在每行结束处（换行符之前）打印 $ 字符。
- -t 将表符打印为 ^I，将馈符打印为 ^L

如果你未指定 -v 选项，则忽略 -e 和 -t 选项。

## 操作数

- file 输入文件的路径。如果没有指定文件，使用标准输入。如果文件为 -，则在序列的该点从标准输入读取。`cat` 在这样引用时不会关闭并重新打开标准输入。

## 使用

参见 `largefile(5)` 以获取 `cat` 遇到大于或等于 2GB 文件时的行为描述。

