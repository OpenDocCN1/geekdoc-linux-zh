

## 12.1.1 使用 rcp 在本地主机与远程主机之间复制文件

使用 rcp 将文件从本地主机复制到远程主机，或从远程主机复制到本地主机时，应先指定要复制的文件，然后指定目标文件，如下面的 rcp 语法语句所示：

```
rcp [option...] localfile hostname:file
```

`localfile` 变量标识要复制的本地文件。`hostname:file` 变量标识远程主机（`hostname`），后跟冒号（`:`）以及本地文件复制到的目标文件名（`file`）。

下面的示例使用 rcp 将本地主机上 `/usr/reports` 目录中的本地文件 YTD_sum 复制到远程主机 moon 上 `/usr/acct` 目录中的文件 `year-end`：

```
% rcp /usr/reports/YTD_sum moon:/usr/acct/year-end
```

您还可以将本地主机上的文件发送给远程主机上的用户。下面的示例演示如何将本地主机 `/usr/reports` 目录中的文件 YTD_sum 复制到远程主机 moon 上用户 jones 的主目录中的文件 `acct_summaries`：

```
% rcp /usr/reports/YTD_sum jones@moon:acct_summaries
```

如前面的示例所示，rcp 命令会为根据原文件创建的新文件指定新的创建日期和时间。它还会根据包含新创建文件的主机或用户目录指定文件的读-写-执行权限。

您可能需要在新建文件中保留被复制文件的原始创建日期和访问权限模式。如下例所示，`-p` 选项使您能够在文件 year-end 中保留 YTD_sum 的原始创建日期和时间以及文件访问权限：

```
% rcp -p /usr/reports/YTD_sum moon:/usr/acct/year-end
```

如果未输入 -p 选项，系统会分配新的日期和时间，文件访问权限将设置为系统管理员为远程主机 moon 分配的默认权限。

在下一个示例中，-p 选项在文件 acct_summaries 中保留了与原始文件 YTD_sum 相同的文件创建和访问权限：

```
% rcp -p /usr/reports/YTD_sum jones@moon:acct_summaries
```

如果未输入 -p 选项，系统会分配新的日期和时间，但与前面的示例不同，文件访问权限将是用户 jones 通过 `.login` 或 `.profile` 文件中的 umask 命令（如果有）设置的默认权限。如果在 `.login` 或 `.profile` 文件中未设置 umask，则由远程主机 moon 的默认值决定文件访问权限模式。有关设置 umask 的详细信息，请参阅 umask(1)。

要将文件从远程主机复制到本地主机，请遵循以下 rcp 语法语句。该命令语法与将本地文件复制到远程主机相同，不同之处在于 localfile 是目标文件，因此它位于命令行末尾：

```
rcp [option...] hostname:file localfile
```

## 12.1.2 使用 ftp 在本地主机与远程主机之间复制文件

ftp 命令是文件传输协议（FTP）的接口，具有大量子命令（见表 12-1、表 12-2 和表 12-3），这些子命令支持复制文件这一主要任务。您可以使用 ftp 命令在支持 ftp 的任何两台主机之间复制文件。

有关 ftp 命令选项的说明，请参阅 ftp(1) 参考手册页，这些选项主要用于网络管理任务。

通过 FTP 复制文件包括以下步骤：

- 1. 在远程主机上建立会话
- 2. 复制文件
- 3. 断开会话

ftp 命令的语法如下：

```
ftp host_name
```

host_name 变量指定您要访问的主机名。如果在命令行中未指定 host_name，则必须使用 ftp 子命令 open（见表 12-1）与远程主机连接。

键入 ftp 后，将显示 `ftp>` 提示符，您便会登录到远程主机。然后您可以使用 ftp 子命令执行以下任务：

- 复制文件（见表 12-1）
- 将本地文件追加到远程文件（见表 12-1）
- 复制多个文件（见表 12-1）
- 列出远程目录的内容（见表 12-2）
- 更改远程主机上的当前目录（见表 12-2）
- 删除远程主机上的文件（见表 12-2）
- 转义到本地 shell 以运行命令（见表 12-3）

