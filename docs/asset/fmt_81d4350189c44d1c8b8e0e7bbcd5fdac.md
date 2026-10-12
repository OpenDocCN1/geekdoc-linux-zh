
一个命令的输出可以作为另一个命令的输入，这被称为管道（pipeline）。这意味着一个命令的标准输出可以重定向到另一个命令的标准输入，并由该命令再重定向到下一个命令，依此类推。这两个命令是并行执行的；第二个命令将等待第一个命令完成标准输出的发送。管道使用的字符是竖线（在 Linux 中称为 pipe）：`command1 | command2` 或多于两个 `command1 | command2 | command3 | commandN`。接下面的插图显示了进程之间如何使用管道进行标准输入输出流的通信。请参考下图：

## 文本终端

![](img/bcd1b6709d1a6bc46b09b8587284794e_97_0.png)

图 3.22：管道图示例。来源：Wikimedia

在接下来的图中，一个命令（`cat`）的输出将作为另一个命令（`head`）的输入，而另一个命令（`nl`）将从第二个命令的标准输出中接收标准输入数据。

这种组合将显示来自 `/etc/services` 文件（`cat` 命令）输出的前 10 行（`head` 命令），并对其进行编号（`nl` 命令）。

```bash
root@ubuntu:-# cat /etc/services | head | nl
1 # Network services, Internet style
2 #
3 # Updated from https://www.iana.org/assignments/service-names-port-number/service-names-port-numbers.xhtml
4 #
5 # New ports will be added on request if they have been officially added ed
6 # by IANA and used in the real-world or are needed by a debian package.
7 # If you need a huge list of used numbers install the nmap package.

8 tcppmum 1/tcp # TCP port service multiplexer
9 echo 7/tcp
```

图 3.23：使用三个命令的管道示例

## 数据流的 CLI 命令

有三个简单的标准命令可以操作标准流：`echo`、`read` 和 `tee`。

### echo 命令

这个简单的命令显示一行文本。它用于显示变量的值、创建带有内容的文件，或向现有文件添加数据。最常用的选项是 `-n`，表示不在行尾添加换行符。在下面的内容中，展示了该命令的不同用法：

```bash
agonzalez@ubuntu:-$ echo "Some text and value of variable $HOME"
Show some text and value of variable /home/agonzalez
agonzalez@ubuntu:-$ echo "Create a file" > example.txt
agonzalez@ubuntu:-$ echo "Append content to file" >> example.txt
agonzalez@ubuntu:-$ cat example.txt
```

创建文件

向文件添加内容

图 3.24：`echo` 命令示例以及使用 `cat` 命令显示文件内容

### read 命令

如前所示，此命令请求用户从标准输入引入一个值并保存到变量中。一些常用选项有 `-p` 添加提示文本，以及 `-t` 指定用户提供输入的超时时间。在接下来的截图中，展示了 `read` 命令的使用：

```bash
agonzalez@ubuntu:~$ read -p "Introduce username: " USERNAME
Introduce username: testuser
agonzalez@ubuntu:~$ echo $USERNAME
testuser
```

图 3.25：`read` 命令允许询问用户输入数据

### tee 命令

重定向标准输出的一个局限性是标准输出被保存到变量中。一些常用选项有 `-p` 添加提示文本，以及 `-t` 指定用户提供输入的超时时间。在接下来的截图中，展示了 `read` 命令的使用：

```bash
agonzalez@ubuntu:~$ read -p "Introduce username: " USERNAME
Introduce username: testuser
agonzalez@ubuntu:~$ echo $USERNAME
testuser
```

在安装 Linux 发行版期间，会创建一个名为 `root` 的管理员用户。出于安全考虑，还建议使用 `sudo` 创建一个新用户，以便登录并执行管理任务。

针对不同发行版的 Linux 的云镜像也包含一个默认用户。该用户没有设置密码，连接它的唯一方法是使用私 SSH 密钥。这将在网络和安全章节中介绍。云镜像的典型登录用户名为 `cloud-user`（适用于大多数基于 RPM 的发行版）、`ec2-user`（适用于 Amazon Web Services 中的 Linux 系统），或特定发行版的名称（`CentOS` 系统使用 `centos`，`Ubuntu Server` 使用 `ubuntu`）。

Linux 中的用户不仅保留给人类登录，还包括服务或应用程序相关的系统用户。Linux 用户通过数字 ID（`uid`）进行标识：安装期间创建的预定义用户将使用 0 到 99 之间的范围，而通过安装服务应用创建的系统用户将使用 100 到 999 之间的范围。普通用户拥有更大的范围，从 1,000 到 6,000。`uid` 0 留给 `root` 用户。

Linux 拥有一个组列表，用户是这些组的成员。一个用户始终关联一个主组，并可选地关联多个辅助组。这些组有助于将文件和程序的权限关联多个用户。与用户一样，在安装 Linux 发行版期间或安装新服务应用程序时会创建系统组。组也通过数字 ID（`gid`）标识，范围与用户相同：安装期间创建的预定义组为 0-99，安装服务应用期间的系统组为 100-999，普通组为 1,000–6,000。`root` 用户拥有自己的 `gid` 为 0 的 `root` 组。

管理员可以使用可用的系统工具创建、修改以及删除用户和组。Linux 将用户、密码、组以及组密码存储在文件中。用于保存信息的四个主要文件如下：

- `/etc/passwd`：系统中本地可用用户列表。该文件包含用冒号（":"）分隔的字段，字段如下：

    - `username`: 用户登录名，最大长度为 32 个字符。

    - `password`: 它将包含字母“x”，表示它存储在 `/etc/shadow` 中。也可以在此文件中存储加密后的密码，尽管不建议这样做。

    - `user id (uid)`: 与用户关联的唯一数字 ID。

    - `group id(gid)`: 数字 ID，作为主组引用 `/etc/group` 文件中的某个组。

    - `User information`: 如今，此字段包含用户的全名。在历史上，这些字段包含姓名、位置、电话号码和办公室电话，并用逗号分隔。

    - `Home directory`：用户存放数据主目录的完整路径。

    - `Shell`: 要使用的 shell 的完整路径。系统用户将使用 `/bin/nologin`、`/usr/bin/nologin` 或 `/bin/false` 以避免他们作为普通用户登录。普通用户使用 `/bin/bash`、`/bin/sh` 或其他的流行替代，如 `/bin/zsh`。

- `/etc/shadow`：此文件包含系统中本地用户的密码信息和过期日期。此文件应受到保护，使非管理员用户无法读取。它包含用冒号（":"）分隔的九个字段：

    - `username`: `/etc/passwd` 中存在的的用户。

    - `encrypted password`: 通常由 `passwd` 命令自动填充的密码。

    - `date of last password change`: 此字段有三个可能的值：

        - 空值：用户没有过期日期。

        - 0 值：意味着用户在登录后必须更改密码。

        - 整数：表示自 1970 年 1 月 1 日 00:00 UTC 以来经过的天数，表示最后一次更改密码的时间。

    - `minimum password age`: 用户再次允许更改密码之前必须等待的最少天数。空字段和值 0 表示没有最小密码更改时间限制。

    - `maximum password age`: 用户下次登录时必须更改密码的最大天数。空字段意味着没有最大密码有效期，没有密码警告期，也没有密码闲置期。

    - `password warning period`: 密码过期前应警告用户的天数。在此天数内用户应会收到警告。空字段和值 0 表示没有密码警告期。
