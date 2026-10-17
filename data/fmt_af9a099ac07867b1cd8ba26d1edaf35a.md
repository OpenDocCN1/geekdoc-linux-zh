
```
3108 bytes transferred

lftp@localhost:~/status/ put /etc/hosts

lftp@localhost:~/status/ ls

-rw-r--r-- 1 13597 13594 Oct 23 2009 enrolled-20091012

-rw-r--r-- 1 13597 514 Oct 23 2009 enrolled-20091013

-rw-r--r-- 1 0 0 201 May 23 20:22 hosts

lftp@localhost:~/status/-> ls

anaconda-ks.cfg bin install.log

dog Pictures sent

Downloads Public survey-200910223.txt

lftp@localhost:~/status/-> quit
```

在提供用户名（`-u chris`）后，`lftp`会提示输入`chris`的Linux密码。输入`pwd`显示`chris`已登录到本地主机，且`/home/chris`是当前目录。就像使用普通的Linux命令行shell一样，您可以使用`cd`切换到另一个目录并使用`ls`列出该目录的内容。

要让客户端解释您的命令，只需在命令前加上感叹号（`!`）。例如，`!pwd`显示启动`lftp`的会话当前目录为`/root`。了解这一点很好，因为如果您在未指定目标地的情况下从服务器获取文件，它将存到客户端的目录（在本例中为`/root`）。您可能运行的其他可由客户端系统解释的命令包括`cd`（切换目录）或`ls`（列出文件）。

假设您拥有服务器的读取权限以及发起系统上当前目录的权限，您可以使用`get`命令从服务器下载文件（`get survey-200910223.txt`）。如果您拥有服务器上当前目录的写入和上传权限，则可以使用`put`将文件复制到服务器（`/etc/hosts`）。

运行`ls`命令显示`/etc/hosts`已上传到服务器。运行`ls`可以让您看到`survey-200910223.txt`文件已从服务器下载到发起系统。

# 第四部分：成为 Linux 服务器管理员

## 使用 gFTPTP 客户端

Linux下还有许多其他FTP客户端可用。您可以尝试的另一个FTP客户端是gFTPTP。`gFTP`客户端提供了一个界面，让您同时看到FTP服务器的本地和远程站点。要在Fedora和Red Hat企业级Linux中安装gFTPTP，请运行以下命令安装`gfttp`包：

```
# yum install gfttp
```
