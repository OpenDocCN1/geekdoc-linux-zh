

## 表 6.2 PC-BSD 和 Solaris 中都可用的打印相关命令列表

| System V 兼容 UNIX | BSD 兼容 UNIX | 用途 |
| lp | lpr | 提交文件进行打印 |
| lpstat | lpq | 显示一个或多个打印机的打印作业状态 |
| cancel | lprm | 从打印队列中移除/清除一个或多个作业 |
|  | lpc | 启动打印机控制程序 |
|  | lptest | 生成波纹图案以测试打印机 |

必须非常注意的是，你绝不要尝试用 lp 或 lpr 命令打印非文本文件，尤其是包含控制字符的文件（例如可执行文件如 a.out）。这样做不会打印出你想要的内容并会浪费大量打印纸。甚至不要尝试测试。如果不小心发送了非文本文件的打印请求，请立即关闭打印机并通知你的系统管理员你需要帮助。

下面是对 lp 命令的简要描述。

## 语法

```
lp [options] file-list
```

用途：提交打印 file-list 中文件的请求

## 常用选项/功能：

- -P page-list  打印 page-list 中指定的页
- -d ptr  将打印请求发送到 ptr 打印机
- -m  打印完成后发送电子邮件
- -n N  打印 file-list 中文件(s)的 N 份；默认是一份
- -t title  在横幅页上打印标题
- -w  打印完成后向用户终端写入信息

下面的会话展示了如何使用带选项和不带选项的 lp 命令。第一个命令在默认打印机上打印示例文件。系统管理员为系统上的用户设置默认打印机。第一个打印请求的作业 ID 为 cpr-981，这告诉你打印机名称为 cpr。第二个命令使用 -d 选项指定示例文件应打印在 spr 打印机上。第三个命令用于在 qpr 打印机上打印 sample 和 phones 文件各三份。

```
% lp sample
request id is cpr-981 (1 file(s))
% lp -d spr sample
request id is spr-983 (1 file(s))
% lp -d qpr -n 3 sample phones
request id is qpr-984 (2 file(s))
%
```

如前所述，lp 命令的 BSD 对应命令是 lpr 命令。下面是对该命令的简要描述。

## 语法

```
lpr [options] file-list
```

用途：提交打印 file-list 中文件的请求

## 常用选项/功能：

- -# -N N  打印 file-list 中文件(s)的 N 份；默认是一份
- -P ptr  将打印请求发送到 ptr 打印机
- -T title  在横幅页上打印标题
- -m  打印完成后发送电子邮件
- -p  使用 pr 命令格式化输出

下面的会话展示了 BSD 版本的命令，它们执行与 lp 命令相同的打印任务。因此，第一个 lpr 命令发送打印示例文件到默认打印机的打印请求。第二个命令发送打印示例文件到 spr 打印机的请求。第三个命令在 qpr 打印机上打印 sample 和 phones 文件各三份。

```
% lpr sample
% lpr -P spr sample
% lpr -P qpr -# 3 sample
%
```

你可以使用以下命令打印 sample 文件，并在 pr 命令生成的每页上加上页眉信息。竖线符号（|）称为管道符号，我们将在第 9 章详细讨论。

```
% pr sample | lpr
%
```

你也可以使用 lpr -p sample 命令执行相同的任务。你可以使用以下命令打印带有行号和每页 pr 页眉的 sample 文件。你也可以使用 nl sample | lpr -p 命令执行相同的任务。

```
$ nl sample | pr | lpr
$
```

你可以通过指定适当的标志使 lpr 命令打印非标准文本文件，例如 TEX 文件。例如，你可以使用 -t 选项打印 troff 文件，使用 -n 选项打印 nroff 文件。

## 6.8.3 查找你的打印请求状态

在 System V 兼容系统中，lpstat 命令可用于显示打印机上打印作业的状态。下面是对 lpstat 命令的简要描述。

## 语法

```
lpstat [options]
```

用途：显示打印机上打印作业的状态

## 常用选项/功能：

- -d 显示使用 lp 命令发送到默认打印机的打印作业状态
- -o job-ID-list 显示 job-ID-list 中的打印作业状态；用空格分隔作业 ID，多个作业时将请求用双引号括起来
- -p printer-list 显示 printer-list 中指定的打印机上的打印作业状态
- -u user-list 显示 user-list 中用户的打印作业状态

不带任何选项时，lpstat 命令会显示所有正在打印或等待在默认打印机打印队列中的你的打印作业状态。下面的会话中的命令展示了该命令的一些典型用法。lpstat -p 命令显示网络上所有打印机的状态。lpstat -p qpr 显示 qpr 打印机上的打印作业状态。lpstat -u sarwar 显示用户 sarwar 的所有打印作业。命令的输出显示 sarwar 提交了三个打印作业：两个到 qpr（作业 ID 为 qpr-3998 和 qpr-3999）和一个到 tpr（作业 ID 为 tpr-203）。最后，lpstat -a 命令显示所有处于活动状态并接受打印作业的打印机。

```
$ lpstat -p
printer cpr is idle. enabled since Tue Sep 2 10:43:48 GMT 2014. available. printer mpr faulted. enabled since Mon Sep 1 10:48:29 GMT 2014. available. printer qpr now printing qpr-53. enabled since Mon Sep 1 10:48:29 GMT 2014. available. printer spr is idle. enabled since Mon Sep 1 10:48:29 GMT 2003. available.
$ lpstat -p qpr
printer qpr now printing qpr-53. enabled since Mon Sep 1 10:48:29 GMT 2014. available.
$ lpstat -u sarwar
qpr-3998 sarwar 93874 Sep 2 22:05 on qpr
qpr-3999 sarwar 93874 Sep 2 22:05
tpr-203 sarwar 93874 Sep 2 22:05 on tpr
$ lpstat -a
cpr accepting requests since Tue Sep 2 10:43:48 GMT 2014
spr accepting requests since Mon Sep 1 10:48:29 GMT 2014
$
```
