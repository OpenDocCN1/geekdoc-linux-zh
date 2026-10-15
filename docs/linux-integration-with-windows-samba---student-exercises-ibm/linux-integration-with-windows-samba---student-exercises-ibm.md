
# Linux 与 Windows 集成 (Samba) - 学生练习 (IBM Learning, 2003, 课程代码 QLX26)

## 学生练习题

### 练习说明

课程中的每个练习都分为下所示的部分。请选择最适合你实验室工作方法的部分。你可以根据情况选择使用这些部分的组合。

**练习说明** — 本部分包含你要求完成的任务。关于如何执行任务没有确定的细节。你将有机会完成指定的练习，利用你在单元演示中学到的知识、该单元的学生笔记本、你过去的经验以及可能还有一点点直觉。

**带提示的练习说明** — 此部分与练习说明完全相同，但额外提供了提示来帮助你完成练习。练习说明部分结合带提示的说明部分，可以在你需要时为你提供提示。

## 练习 1. 安装 Samba

### 本练习关于什么

在本次练习中，你将从源码和随发行版的 RPM 文件安装 Samba。

### 你应该能够

在练习结束时，你应该能够：

- 编译并安装源码包
- 安装二进制 RPM

### 所需材料

- `http://www.samba.org`: 源码包
- `http://www.redhat.com`: RPM

### 练习说明

#### 从源码安装 Samba

在练习的第一部分，你将遵循从 Samba 网站获取的原始源码包安装 Samba 的步骤。之后你将对其进行测试并卸载。这样做是因为我们希望教室里的每个人都使用相同的配置，而只有通过安装操作系统提供的二进制 RPM 才能确保这一点。

1. 以 root 身份登录 Linux 机器。除非教师另有说明，密码为 inx。
2. 启动图形用户环境并启动浏览器（Konqueror、Netscape、Mozilla 或 Galeon）。教师可能会指示你需要配置代理或 socks 服务器，因为教室可能位于防火墙之后。一旦可以上网，访问 Samba 网站 (`http://www.samba.org`)。浏览网站。进入下载部分并下载最新的 Samba 版本。存储在 `/root`
3. 进入 `/usr/src` 并解压源码包。
4. 进入 Samba 目录查看“Manifest”文件，直到看到安装说明。仔细阅读这些说明。
5. 进入源码目录运行 `./configure --help`。仔细查看不同的配置选项；这些选项决定了启用哪些 Samba 文件和功能。
6. 不带任何选项运行 `./configure` 脚本这将确保我们以后可以轻松安装。缺点是所有的二进制文件都不会位于 `$PATH` 中。该脚本将运行大约分钟。
7. 运行 `make` 命令构建所有二进制文件。取决于系统的速度，需要 5-20 分钟。在系统编译时，你可能想去买咖啡。
8. 运行 `make install` 命令安装所有内容。注意所有文件都相对于目录 `/usr/local/samba` 进行安装。
9. 在配置文件应该所在的目录（对于常规安装，为 `/usr/local/samba/lib`）中创建一个基本的 `smb.conf` 文件。如果不知道配置字段的位置

> 注意：为了节省时间，你的教师可能已经下载了此版本并将其存储在本地。如果是这种情况，请咨询教师。

现在，运行 `testparm` 命令，该命令是作为 `make install` 的一部分安装。你可以从 `testparm` 命令的输出中读取目录。

`smb.conf` 文件应包含一个 `netbios name`（netbios 名称）和一个 `workgroup`（工作组）语句。

10. 再次运行 `testparm` 命令。
11. 启动 `smbd` 和 `nmbd` 守护进程，均使用 `-D` 选项使其作为守护进程启动。
12. 使用 `smclient` 命令验证你的守护进程确实在运行。
13. 杀死所有 Samba 守护进程。
14. 使用 `make uninstall` 卸载所有 Samba 程序。验证 `/usr/local/samba` 目录确实为空，除了我们自己创建的 `smb.conf` 文件、一些文档以及几个锁文件和日志文件外。然后完全删除 `/usr/local/samba` 目录。

#### 从 RPM 安装 Samba

15. 根据实验设置，发行版附带的 Samba RPM 位于 `/root` 或存储在网络服务器上。或者，你的老师可能会有 CD 分发给你。无论如何，安装所有 Samba RPM 并列出这些 RPM 的信息以及它们包含的文件。
16. 浏览在你的系统上配置的默认 `smb.conf` 文件的内容。
17. 使用发行版的启动脚本启动 Samba。
18. 再次使用 `smclient` 命令测试你的本地配置。
19. 使用发行版的脚本停止 Samba 守护进程。

### 实验结束

### 带有提示的练习说明

#### 从源码安装 Samba

在练习的第一部分，你将遵循使用从 Samba 网站获取的原始源码 tar 包安装 Samba 所需的所有步骤。之后，你将简要地测试此安装并卸载它。这样做的原因是，我们希望教室里的每个人都使用相同的配置，而只有当每个人都从操作系统提供的二进制 RPM 安装时，才能确保这一点这一点。

1. 以 root 身份登录你的 Linux 机器。除非老师另有说明，密码为 ibminx。

   > 以 root 身份登录并提供 ibminx 作为 root 密码。

2. 启动图形用户环境并启动浏览器（Konqueror, Netscape, Mozilla 或 Galeon）。

   你的老师可能会指示你可能为代理服务器或 socks 服务器配置浏览器，因为教室可能位于防火墙后面。

   一旦你能够访问网络，访问 Samba 网站（`http://www.samba.org`）。浏览该网站。进入下载部分并下载最新的稳定 Samba 版本。将其存储在 `/root`。

   注意：为了保存下载，你的老师可能已经下载了该版本并将其存储在本地。如果是这种情况，请询问老师。

3. 进入 `/usr/src` 目录并解压 samba tar 包。

   ```
   # cd /usr/src
   # tar -zxvf /root/samba-version.tar.gz
   ```

4. 进入 samba 目录并浏览 "Manifest" 文件，直到你看到安装说明。仔细阅读这些内容。

   ```
   # cd samba-version
   # less Manifest
   ```

5. 进入 "source" 目录并运行 `./configure --help`。仔细查看不同的配置：这些选项决定了所有文件将放在何处以及启用 Samba 的哪些功能（包括实验性功能）。

   ```
   # cd source
   ./configure --help | less
   ```

6. 在不带任何选项的情况下运行 `./configure`。不提供选项将确保我们以后可以方便地重新安装 Samba。缺点是并不是所有的二进制文件都位于包含在 `$PATH` 中的位置。

   此脚本将花费大约分钟。

   ```
   # ./configure
   ```

7. 运行 `make` 命令以构建你所有的二进制文件。（这将花费 5-20 分钟，取决于系统的速度。你可能想在系统编译时去喝杯咖啡。）

   ```
   # make
   ```

8. 运行 `make install` 命令以安装所有内容。注意，所有文件都是相对于目录 `/usr/local/samba` 安装的。

   ```
   # make install
   ```

9. 在配置文件应该所在的目录中创建一个基础的 `smb.conf` 文件（对于常规安装，路径为 `/usr/local/samba/lib`）。如果你不知道配置文件应该放在哪里，运行作为 `make install` 的一部分安装的 `testparm` 命令。你可以从 `testparm` 命令的输出中读取目录。

   `smb.conf` 文件应包含一个 `netbios name` 和一个 `workgroup` 语句。

   ```
   cd /usr/local/samba/bin
   # /testparm
   cd /usr/local/samba/lib
   vi smb.conf
   ```

   编辑文件使其如下：

   ```
   [global]
   netbios name = system1
   workgroup = 1x26
   ```

10. 再次运行 `testparm` 命令。

    ```
    # /usr/local/samba/bin/testparm
    ```

11. 启动 `smbd` 和 `nmbd` 守护进程，均使用 `-D` 选项使其成为守护进程。

    ```
    /usr/local/samba/bin/smbd -D
    /usr/local/samba/bin/nmbd -D
    ```

12. 使用 `smclient` 命令验证你的守护进程确实在运行。

    ```
    /usr/local/samba/bin/smclient -L system1 -N
    ```

13. 杀死所有 Samba 守护进程。

    ```
    killall smbd
    killall nmbd
    ```

14. 使用 `make uninstall` 命令卸载所有 Samba 程序。验证 `/usr/local/samba` 目录确实为空，除了我们自己创建的 `smb.conf` 文件、一些文档以及几个锁文件和日志文件外。然后完全删除 `/usr/local/samba` 目录。

    ```
    cd /usr/src/samba-version/source
    # make uninstall
    cd /usr/local/samba
    ls -IR | less
    cd /root
    rm -fr /usr/local/samba
    ```

#### 从 RPM 安装 Samba

15. 根据实验设置，发行版附带的 Samba RPM 位于 `/root` 或存储在网络服务器上。或者，你的老师可能会有 CD 分发给你。无论如何，安装所有 Samba RPM 并列出这些 RPM 的信息以及它们包含的文件。

    ```
    # Is samba*.rpm
    # rpm -qip samba*.rpm | less
    # rpm -qlp samba*.rpm | less
    # rpm -ivh samba*.rpm
    ```

16. 浏览在你的系统上配置的默认 `smb.conf` 文件的内容。

    ```
    # less /etc/samba/smb.conf
    ```

17. 使用你的发行版的启动脚本启动 Samba。

    ```
    redhat# service smb start
    suse# rcnmb start; rcnmb start
    ```

18. 使用 `smclient` 命令测试你的本地配置。

    ```
    # smclient -L localhost -N
    ```

19. 使用你的发行版的脚本停止 Samba 守护进程。

    ```
    redhat# service smb stop
    suse# rcnmb stop; rcnmb stop
    ```

### 实验结束

## 练习 2. 网络浏览

### 本练习关于什么

在此练习中，你将配置 Samba 进行网络浏览。

### 你应该能够做到

在实验结束时，你应该：

- 配置 Samba 进行网络浏览

### 练习说明

#### 配置主服务器

在练习的这一部分，你需要与一个或两个伙伴小组合作，并配置你的系统。你将尝试不同的浏览设置，让不同的机器意料之外地成为本地和域主。

1. 寻找一个或两个伙伴小组一起工作，如有必要，互相介绍。
2. 将发行版自带的默认 `smb.conf` 文件移动到安全位置，以便你可以从空白 `smb.conf` 文件开始。在这个新文件中，配置一个 `netbios name`（你的主机名）和一个 `workgroup`（你与小组确定的名称）。还要包含一个 `log level = 2` 语句，并确保日志输出到 `/var/log/samba`
3. 启动图形用户环境（如果尚未启动）。打开至少两个终端窗口。在一个窗口中启动 `tail -f /var/log/samba/nmbd`，在另一个窗口中连续运行 `smclient -L localhost -N`。
4. 使用 `uptime` 命令确定哪个系统运行时间最长。启动 Samba 进程。等待大约分钟观察浏览选举过程。为你的工作组选出主服务器需要多长时间？为什么这么久？哪个系统被选中了？为什么？
5. 停止所有系统上的 Samba 守护进程。在某个系统中，配置 Samba 为本地主服务器（LMB），`os level` 为 32。重新启动所有 Samba 进程。哪一个变成了 LMB？为什么？这次花了多久？
6. 保持成为 LMB 的系统运行。在非 LMB 系统上，停止 Samba 守护进程，并将该系统配置为首选主，`os level` 为 33。启动此进程。该系统会成为 LMB 吗？
7. 在你进行这些练习时，你是否在 `smclient` 命令的输出中看到了其他主服务器出现？这花了多久？

#### WINS 服务

8. 你的老师将指定教室中的一个系统（或他的她的服务器）作为 WINS 服务器。配置你的所有系统使用此 WINS 服务器，然后运行相同的模拟。这对花费的时间有影响吗？

#### 清理

9. 修改你的 `smb.conf` 文件，使其成为一个 OS 级别为零的简单系统，并作为 lx26 工作组的一部分。不要尝试成为主浏览器。

### 实验结束

### 带有提示的练习说明

#### 配置主浏览器

在练习的这部分，你需要与一或两个伙伴小组合作，并将你的两个或三个系统配置在同一个工作组中。你将尝试不同的浏览设置，让不同的机器（意料之中）成为本地和域域主浏览器。

1. 寻找一或两个伙伴小组合作，并在必要时互相介绍自己。
2. 将发行版自带的默认 `smb.conf` 文件移动到安全位置，以便从一个空白 `smb.conf` 文件开始。在这个新的空白文件中，配置 netbios 名字（你的主机名）和一个工作组（你与伙伴小组共同确定的名称）。还要包含 `log level = 2` 语句，并确保日志输出到 `/var/log/samba/log.%m`

   > `mv /etc/samba/smb.conf /etc/samba/smb.conf`
   >
   > `vi /etc/samba/smb.conf`

   文件的内容应如下：

   ```
   [global]
   netbios name = systemgroup
   workgroup = oursgroup
   log level = 2
   log file = /var/log/samba/log.%m
   ```

   > `# testparam`

3. 如果图形用户环境尚未启动，请启动它。打开至少两个终端窗口。在一个窗口中，对文件 `/var/log/samba/log.mbnd` 启动 `tail -f`，在另一个窗口中，每隔一秒连续运行一次 `smbclient -L localhost -N`。

   > `# startx`
   >
   > 在一个 xterm/nxterm/rxvt/Konsole/gnome-terminal 窗口中：
   >
   > `# tail -f /var/log/samba/log.mbnd`
   >
   > 在另一个 xterm/nxterm/rxvt/Konsole/gnome-terminal 窗口中：
   >
   > `# while true`
   >
   > `do`
   >
   > `clear`
   >
   > `smbclient -L localhost -N`
   >
   > `sleep 1`
   >
   > `done`

4. 运行 `uptime` 命令确定哪个系统运行时间最长。启动 Samba 守护进程。等待一分钟左右查看浏览器选举的情况。为你的工作组选出一个主浏览器需要多长时间？为什么这么久？哪个系统被选中了？为什么？

   ```
   >> # uptime
   >> redhat# service smb restart
   suse: rcmb start; rsmb start
   ```

5. 停止所有系统上的所有 Samba 守护进程。在某个系统上，将 Samba 配置为本地主浏览器（LMB），OS 级别为 32。重新启动所有 Samba 守护进程。哪个系统变成了 LMB？为什么？这次花了多长时间？

   ```
   >> redhat# service smb stop
   suse# rcmb stop; rcmb stop
   >> # vi /etc/samba/smb.conf
   ```

   添加以下行：

   ```
   local master = yes
   os level = 32
   ```

   ```
   >> redhat# service smb start
   suse: rcmb start; rsmb start
   ```

6. 保持变为 LMB 的系统运行。在非 LMB 系统上，停止 Samba 守护进程，并将该系统配置为首选主浏览器，OS 级别为 33。启动此守护进程。该系统会变成 LMB 吗？

   ```
   >> redhat# service smb stop
   suse: rsmb stop; rcmb stop
   >> # vi /etc/samba/smb.conf
   ```

   添加以下行：

   ```
   local master = yes
   os level = 33
   preferred master = yes
   ```

   ```
   >> # testparam
   >> redhat# service smb start
   suse# rcmb start; rsmb start
   ```

7. 在你进行这些练习时，是否在 `smclient` 命令的输出中看到了其他主浏览器的出现？这花了多久？

#### WINS 服务

8. 老师将指定教室中的一个系统（他/她自己的服务器）作为 WINS 服务器。配置你的所有系统使用此 WINS 服务器，然后再次运行模拟。这对耗时有影响吗？

   ```
   >> redhat# service smb stop
   suse: rcmb stop; rcmb stop
   >> # vi /etc/samba/smb.conf
   ```

   如果你是 WINS 服务器，添加以下行：

   ```
   wins support = yes
   ```

   如果你是 WINS 客户端，添加以下行：

   ```
   wins server = <WINS 服务器的 IP 地址>
   ```

   ```
   >> # testparam
   >> redhat# service smb start
   suse# rcmb start; rsmb start
   ```

#### 清理



## 练习 2 配置 Samba 服务器

### 基础配置

- 9. 修改你的`smb.conf`文件，使其成为一个 OS 级别为零的简单系统，并作为`lx26`工作组的一部分。不要尝试成为主浏览器。

```
# vi /etc/samba/smb.conf
```

修改文件使其如下：

```
[global]
netbios name = system1
workgroup = lx26
```

```
# testparam
redhat# service smb restart
suse# rcmb restart; rsmb restart
```

## 实验结束

## 练习 3 身份验证

### 本练习内容

本单元将用于学生熟悉 Windows 身份验证及其在 Samba 中的实现。

### 你应该能够做到

实验结束时，你应该能够：

- 配置基础身份验证
- 配置加密密码
- 配置客账户

### 练习说明

#### 基础身份验证

- 1. 验证你的系统中已添加了两个用户账户`samba1`和`samba2`，并且这些账户的密码分别为`samba1`和`samba2`。

- 2. 配置你的`smb.conf`文件使 Samba 处于`security = user`模式。使用`smbclient`以用户`samba1`的身份访问 Samba。使用密码 "samba1"。这可行吗？

- 3. 现在尝试使用密码 "SAMBA1"（全大写）登录。这可行吗？为什么？

- 4. 将`samba1`的 UNIX 密码更改为 "Samba1"（大写字母 S）。然后尝试用密码 "samba1"、"Samba1" 和 "SAMBA1" 登录。这可行吗？将密码级别更改为 1 并再次尝试这些密码。现在可行吗？

- 5. 为`samba1`尝试不同的 UNIX 密码（包含多个大写字母）以及各种密码设置，直到你理解它是如何运作的。

- 6. 将`samba1`的密码改回`samba1`。

- 7. 编辑`/etc/samba/smusers`文件并为`samba1`添加一个别名，使其使用 Windows 用户名 "Samba User 1"。修改`smb.conf`文件以使用`/etc/smamba`文件。然后尝试用 Windows 用户名 "Samba User 1" 登录 Samba。

#### 加密密码

- 8. 配置 Samba 使用加密密码。使用`smadduser`将`samba1`和`samba2`添加到 Samba 密码文件中。查看结果`/etc/samba/smbpasswd`文件。

- 9. 尝试以`samba1`登录 Samba。这可行吗？现在将`samba1`的 UNIX 密码更改为完全不同的内容。再次尝试登录。

- 10. 将`samba1`的密码改回`samba1`。

#### 客账户

- 11. 尝试用无效用户名登录 Samba。发生了什么？

- 12. 为你的系统添加一个 UNIX 账户 "pcguest"。**不要**给该账户设置密码。修改`smb.conf`文件，当用户提供无效用户名时使用该账户。再次尝试用无效用户名登录 Samba。现在发生了什么？

#### 从 Windows 95/98/ME 机器登录 Samba

根据当地情况，教室里有一台或两台机器被设置成了 Windows 95/98/ME 机器，或者你的系统上有一个预配置了 Windows 95/98/ME 的 VMware 镜像。老师可以告诉你教室里使用的是什么。

- 13. 启动 Windows 95/98/ME 机器。当需要登录时，使用 "samba1" 和密码 "samba1" 登录。启动 Windows 资源管理器并浏览你的网络邻。（注意：启动后可能需要几分钟才能实际访问网络邻：Windows 机器也会进行浏览器选举……）浏览自己的 Samba 服务器。你获得访问权限了吗？

- 14. 注销（开始；关机；关闭所有程序）并以不存在的用户登录。浏览网络邻并尝试访问你的系统。这可行吗？为什么？

- 15. 如果还有时间，禁用服务器上的客账户，从 Windows 机器访问 Samba。这可行吗？

实验结束

## 带有提示的练习说明

### 基础身份验证

- 1. 验证你的系统中已添加了两个用户账户`samba1`和`samba2`，这些账户的密码分别为`samba1`和`samba2`。

```
# id samba1
# id samba2
```

使用`<Alt-F6>`或`<Ctrl-Alt-F6>`切换到空闲终端，并用`samba1`登录`samba1`。对`samba2`执行同样的操作。

- 2. 配置你的`smb.conf`文件使 Samba 处于`security = user`模式。使用`smbclient`以用户1 的身份访问。使用密码 "samba1"。这可行吗？

```
redhat# service smb stop
suse: rcmb stop; rcmb stop
# vi /etc/samba/smb.conf
```

添加以下行：

```
security = user
```

```
# testparam
redhat# service smb start
suse# rcmb start; rsmb start
# smclient -L localhost -U samba1
Password: samba1
```

- 3. 现在尝试使用密码 "SAMBA1"（全大写）登录。这可行吗？

- 4. 将`samba1`的 UNIX 密码更改为 "Samba1"（大写字母 S）。然后尝试用密码 "samba1"、"Samba1" 和 "SAMBA1" 登录。这可行吗？将密码级别更改为 1 并再次尝试这些密码。现在可行吗？

```
# passwd samba1
New password: Samba1
Retype new password: Samba1
# smclient -L localhost -U samba1
```

Log on with password`samba1`,`Samba1`and`SAMBA1`.

```
# vi /etc/samba/smb.conf
```

添加以下行：

```
password level = 1
```

```
# testparam
redhat# service smb restart
suse# rcmb restart; rsmb restart
# smclient -L localhost -U samba1
```

使用密码`samba1`登录`SAMBA1`。

- 5. 尝试不同的 UNIX 密码（包含多个大写字母）和各种密码级别设置，直到你理解其原理。

- 6. 将`samba1`的密码改回`samba1`。

```
# passwd samba1
新密码：samba1
重新输入新密码：samba1
```

- 7. 编辑`/etc/samba/smbsusers`文件并为`samba1`添加一个别名，使其使用 Windows 用户名 "Samba User 1"。更改`smb.conf`文件以使用`/etc/samba/smbsusers`文件。然后尝试使用 Windows 用户名 "Samba User 1" 登录 Samba。

```
# vi /etc/samba/smbsusers
```

添加以下行：

```
sambal = "Samba User 1"
```

```
# vi /etc/samba/smb.conf
```

添加以下行：

```
username map = /etc/samba/smbsusers
```

```
# testparam
redhat# service smb restart
suse# rcmb restart; rcsmb restart
# smclient -L localhost -U "Samba User 1"
```

### 加密密码

- 8. 配置 Samba 使用加密密码。使用`smadduser`将`samba1`和`samba2`添加到 Samba 密码文件中。查看生成的`/etc/samba/smbpasswd`文件。

```
# vi /etc/samba/smb.conf
```

添加以下行：

```
crypt passwords = yes
smbpasswd file = /etc/samba/smbpasswd
```

```
# testparam
redhat# service smb restart
suse: rcmb restart; rcsmb restart
# smadduser samba1:samba1
新 SMB 密码：samba1
重新输入新 SMB 密码：samba1
# smbadduser samba2:samba2
新 SMB 密码：samba2
重新输入新 SMB 密码：samba2
# less /etc/samba/smbpasswd
```

- 9. 尝试以`samba1`身份登录 Samba。有效吗？现在将`samba1`的 UNIX 密码改为完全不同的内容。再次尝试登录。有效吗？

```
# smclient -L localhost -U samba1
# passwd samba1
新密码：something completely different
重新输入新密码：something completely different
# smclient -L localhost -U samba1
```

- 10. 将`samba1`的密码改回`samba1`。

```
# passwd samba1
新密码：samba1
重新输入新密码：samba1
```

### 宾客账户

- 11. 尝试使用无效用户名登录 Samba。发生了什么？

```
# smclient -L localhost -U "An invalid username"
密码：bla
```

- 12. 在你的系统中添加一个 UNIX 账户 "pcguest"。切勿给该账户设置密码。然后更改`smb.conf`文件，当用户提供无效用户名时使用该账户。再次尝试使用无效用户名登录 Samba。发生了什么？

```
# useradd pcguest
# vi /etc/samba/smb.conf
```

添加以下行：

```
guest account = pcguest
map to guest = bad user
```

```
# testpart
redhat# service smb restart
suse# rcsm restart; rcsmb restart
# smclient -L localhost -U "An invalid username"
```

### 从 Windows 95/98/ME 登录 Samba

根据本地情况，教室里的一两台机器被设置为 Windows 95/98/ME 机器，或者你的系统中有一个预配置的带有 Windows 95/98/ME 的 VMware 镜像。老师可以告诉你教室里使用的是什么。

- 13. 启动 Windows 95/98/ME 机器。当需要登录时，使用用户名 "samba1" 和密码 "samba1"。启动 Windows 资源管理器并浏览网络邻域。（注意：启动后可能需要几分钟才能访问网络邻域：Windows 机器也会进行浏览器选举……）浏览自己的 Samba 服务器。你能访问吗？

- 14. 注销（开始；关闭；关闭所有程序并以其他用户登录）并使用 Samba 服务器上不存在的用户名登录。再次浏览网络邻域并尝试访问你的系统。有效吗？为什么？

- 15. 如果时间允许，禁用 Samba 服务器上的宾客账户，并再次从 Windows 机器访问你的 Samba 服务器。有效吗？

实验结束

## 练习 4 文件共享

### 本次练习内容

在练习中，你将练习讲座中提供的技术，配置 Samba 以在 Linux 主机上共享目录。你将尝试动态主目录、权限问题以及磁盘共享的其他特性。

### 你应该能够做到的

实验结束时，你应该能够：

- 正确设置动态主目录
- 配置只读、公共等磁盘共享

### 练习说明

#### [homes] 模板

如讲座所示，`[homes]`实际上是一个用于共享特定用户主目录的模板。

- 1. 修改`smb.conf`文件添加`[homes]`共享。

- 2. 使用`smclient`命令在匿名、`samba1`、`samba2`以及错误用户名的情况下获取服务器上的共享列表。

- 3. 使用`smclient`命令登录`samba1`的主目录。上传`/etc/passwd`文件到`/home/samba1/passwd`。这些权限符合你的预期吗？

- 4. 使用`smb`命令访问`samba2`的主目录。上传`/etc/passwd`。断开连接并查看`/home/samba2/passwd`的权限。

- 5. 在 Windows 95/98/ME 系统上，浏览网络邻域。该命令的作用是什么？

- 6. 使用`smb.conf`文件添加`[homes]`共享。你还需要做其他操作吗？

- 7. 使用`smb.conf`文件添加`[tmp]`共享。有效吗？

- 8. 创建一个新组 "samba"。将`samba1`加入该组。谁可以访问？

- 9. 为光驱器配置共享。当光驱被移除时，Samba 应该自动挂载。

注意：这仅适用于 Linux（而非其他 UNIX），且仅在你的 Linux 内核支持`smbfs`文件系统时有效。

### 学生练习

由于未知原因，`smount`命令似乎无法工作。

```
# umount /mnt/samba
# ls -l /home/samba2/passwd
```

- 5. 在 Windows 95/98/ME 系统上，使用密码`samba1`登录`samba1`。浏览你的网络邻域并进入你自己的服务器。你看到了哪些共享？访问`samba1`共享查看里面有什么文件。你可以读取和写入文件吗？

- 6. 在 Windows 95/98/ME 系统上，启动 MS-DOS 提示符。运行命令`net use h: \servername\homes`。这个命令的作用是什么什么？它起作用吗？为什么要使用"homes"而不是你自己的用户名？

### 其他共享

- 7. 编辑`smb.conf`文件，并如课程所示添加一个`[tmp]`共享。使用`smclient`或`smbmount`或者从 Windows 95/98/ME 系统访问此共享。你可以添加和删除自己的文件吗？

```
# vi /etc/samba/smb.conf
```

添加以下共享：

```
[tmp]
comment = Free disk space here
writable = yes
browsable = yes
public = yes
path = /tmp
```

```
# testparm
redhat# service restart
suse# rcnmb restart; rscmb restart
```

- 8. 创建一个新的 UNIX 组 "samba"。仅将`samba1`添加到该组作为其次要组。为该组创建一个`/groups/samba`目录，并设置正确的组所有权权限。然后为`smb.conf`文件中的该目录添加一个共享。以`samba1`和`samba2`的身份浏览你的服务器。哪些用户可以看到并访问该共享？现在也将`samba2`添加到该组。你是否还需要进行其他操作来允许`samba2`访问该组？

```
# groupadd samba
# usermod -G group samba1
# mkdir -p /groups/samba
# chmod 2770 /groups/samba
# chgrp samba /groups/samba
# vi /etc/samba/smb.conf
```

添加以下共享：

```
[samba]
comment = samba group share
writable = yes
browsable = yes
public = no
path = /groups/samba
valid users = @samba
```

```
# testparm
redhat# service smb restart
suse# rerun restart; rscmb restart
# smclient -L localhost -N
# smclient //localhost/samba -U samba1%samba1
# smclient //localhost/samba -U samba2%samba1
# smclient //localhost/samba -U samba2%samba2
# smclient //localhost/samba -U samba2%samba2
# usermod -G samba samba2
# smclient -L localhost -U samba2%samba2
# smclient //localhost/samba -U samba2%samba2
```

- 9. 配置一个导出你的 CD-ROM 驱动器的共享。当有人连接时，Samba 应该自动关闭 CD 箱并挂载 CD；当共享断开时卸载并弹出 CD。尝试从 Windows 95/98/ME 系统查看这是否有效。

### 注意事项

由于未知原因，`root postexec`命令似乎无法正常工作。正在调查中。

```
# vi /etc/samba/smb.conf
```

添加以下共享：

```
[CD]
comment = CD-ROM
writable = no
browsable = yes
public = no
path = /mnt/cdrom
root postexec = eject -t ; mount /mnt/cdrom
root postexec = umount /mnt/cdrom ; eject
```

```
# testparm
redhat# service smb restart
suse# rerun restart; rscmb restart
```

## 实验结束

## 练习 5 打印机共享

### 练习目标

在本次练习中，你将配置 Linux Samba 服务器以支持主机 Linux 操作系统当前支持的所有打印机。此外，你将学习如何限制哪些打印机实际上被共享。

### 你应该能够学会

在实验结束，你应该能够：



- 配置基础的 Samba 设置，将所有 Linux 配置的打印机暴露给 SMB 网络客户端
- 将上述配置限制为仅选定的打印机

### 练习说明

### 配置 UNIX 打印机

考虑到本课程教学的教室种类多样，无法在此处包含如何配置系统以使用 UNIX 打印机（可以使用常规 UNIX 命令访问的打印机）的说明。你的导师将告诉你如何配置你的 UNIX 打印机。

Red Hat Linux 使用 `redhat-config-printer` 实用，而 SUSE 通过 YaST2 控制中心配置打印机。

作为替代方案，如果教室中完全没有打印机，你可以打印到虚拟终端（实例 `/dev/tty9` 或 `xterm /dev/pts/n`，通过 `tty` 命令查明）。如果是这种情况，请确保打印子系统用户（"lp"）有访问该设备的权限（`chown lp /dev/tty9`）。

1. 使用导师提供的说明配置你的打印机。
2. 创建测试文件 `/root/testfile` 并在其中写入内容（例如诗歌），以便你能识别该文件属于自己。
3. 使用常规 UNIX 命令将测试文件发送到打印机，以验证你的打印子系统工作正常。

### 配置 [printers] 模板共享

4. 修改你的 `smb.conf` 文件，使你的 printcap 文件中的所有打印机都自动共享。然后重启 Samba。

```
printable = true
guest ok = true
# testparam
redhat# service smb restart
suse# smsm restart; rcsmb restart
```

5. 使用 `smclient` 命令浏览你的 Samba 服务器。你看到打印机共享了吗？打印机共享名称是什么？为什么？

```
# smclient -L localhost -N
```

6. 使用 `smclient` 命令打印测试文件。以 `samba1` 登录。验证文件是否已打印。

```
# smclient //localhost/ip -U samba%samba1
smb: \> print /root/testfile
smb: \> exit
```

7. 切换到 Windows 95/98/ME 系统并再次浏览邻域。安装在 Samba 服务器上共享的打印机并尝试打印文件。

### 配置单个打印机

8. 编辑你的 `samba.conf` 文件，使打印机不再自动加载。然后配置两个打印机，一个是 "nolinenumber"，另一个是 "linenumbers"。对于两者都添加一个打印命令语句，让它们打印到同一台打印机，第二个应该在打印作业中添加行号。然后使用 `smprint` 命令将你的测试文件打印到打印机。

```
# vi /etc/samba/samba.conf
```

将 `load printers` 语句更改为：

```
load printers = no
```

添加以下两个共享：

```
[nolinenumbers]
path = /var/spool/samba
writable = no
guest ok = yes
printable = yes
print command = lpr -r -P lp %s

[linenumbers]
path = /var/spool/samba
writable = no
guest ok = yes
```

# 学生练习题

```
printable = yes
print command = nl % | lpr -r -P lp
# testparam
redhat# service smb restart
suse# rcsmb restart; rcsmb restart
# smclient //localhost/ninenumbers -U samba1%samba
smb: \> print /root/testfile
smb: \> exit
# smclient //localhost/ninenumbers -U samba1%samba
smb: \> print /root/testfile
smb: \> exit
```

### 使用伪打印机（可选）

通过修改单个打印机的打印命令，我们可以做很多奇特的事情。一个典型的例子是将打印作业发送到传真机而不是打印机。我们在教室里没有传真机，所以我们将做其他事情，只需理解这个概念。

9. 配置一个名为 "mailoroot" 的打印机共享。如果作业提交到此打印机，它们需要邮件给 root。

```
# vi /etc/samba/smb.conf
```

添加以下共享：

```
[mailoroot]
path = /var/spool/samba
writable = no
guest ok = yes
printable = yes
print command = cat %s | mail -s "Print file from %U" root
# testparam
redhat# service smb restart
suse# rcsmb restart; rcsmb restart
```

10. 在 Windows 系统上，将此附加打印机安装为通用文本打印机，并向此打印机打印一个小型文本文件（如有必要，用 Word 或记事本创建一个）。然后，以 root 身份使用 `mail` 命令检查你的邮箱。成功了吗？
11. 列出 `/var/spool/samba` 中的文件。你在这里看到任何文件吗？为什么？你会如何解决这个问题？

```
# ls -l /var/spool/samba
```

## 实验结束

# 练习 6. Windows 域支持

### 本次练习的目的是

本次工作坊将让你获得配置 Samba 软件的经验，使其在中等复杂的网络中充当域控制器。

### 你应该能够做到的

实验结束时，你应该能够：

- 配置 Samba 作为主域控制器（Primary Domain Controller, PDC）
- 配置登录脚本
- 配置漫游配置文件

### 练习说明

### 配置 Samba PDC

在本节中，你将把你的 Samba 服务器配置为主域控制器。由于一个域中只能有一个 PDC，你将把你的工作组（workgroup）从 LX26 更改为唯一的名称。

1. 配置你的 `smb.conf` 文件，使你处于唯一的工作组中，并且你的系统能够接受域登录。
2. 切换到 Windows 95/98/ME 系统并配置此域登录。删除 C:\Windows 下所有的 `*.PWL` 文件。重启机器并使用无效密码以 `samba1` 身份登录你的域。这有效吗？然后使用有效密码以 `samba1` 身份登录域。

### 登录脚本

3. 修改你的 `smb.conf` 文件，使客户端登录域使用登录脚本 `/home/netlogon/login.bat`。创建登录脚本，使其包含 MS-DOS 命令 `net h: \server\homes`。
4. 在你的 Windows 95/98/ME 系统上，注销并重新登录。登录后，启动 Windows 资源管理器。你看到 H:- 盘了吗？你可以修改和添加文件吗？

### 漫游配置文件

5. 修改你的 `smb.conf` 文件以支持漫游配置文件，同时支持 Windows 95/98/ME 客户端和 Windows NT/2000 客户端。
6. 进入你的 Windows 95/98/ME 系统并配置漫游配置文件。重启系统，然后以 `samba1` 登录。在询问是否使用漫游配置文件时回答 "yes"。更改你环境中的某些内容（例如背景图案）并注销。

### 将 Samba 服务器加入域

对于练习的这部分，你必须与伙伴小组协作。

7. 与你的伙伴小组讨论谁将作为域的 PDC，谁的服务器将加入域。交换关于 netbios 名称、域名称、根密码等信息。
8. 配置 PDC 以允许系统自动加入域。
9. 在 PDC 上为另一台服务器创建一个机器信任账户（machine trust account）。
10. 配置另一台服务器以支持域登录，并将其加入域。
11. 从任何 Samba 服务器，使用 `smclient` 命令查看 Samba 服务器（不是 PDC）的信息。以 `samba1` 登录。你需要什么密码？在 PDC 上，将用户 `samba1` 的密码更改为其他内容。然后尝试登录另一台服务器。密码真的会在 PDC 上检查吗？

## 实验结束

## 带有提示的练习说明

### 配置 Samba 为 PDC

在本节中，你将把你的 Samba 服务器配置为主域控制器。由于一个域中只能有一个 PDC，你将把你的工作组从 LX26 更改为唯一的名称。

1. 配置你的 `smb.conf` 文件，使你处于唯一的工作组中，并且你的系统能够接受域登录。

```
# vi /etc/samba/smb.conf
```

将文件使其看起来如下：

```
[global]
netbios name = system1
workgroup = workgroup
security = user
os level = 64
domain master = yes
local master = yes
domain logins = yes

[netlogon]
writable = no
public = no
path = /home/netlogon
```

你之前配置的任何打印选项可以保留保留。

```
# mkdir /home/netlogon
# testparam
redhat# service smb restart; rcsmb restart; rcsmb restart
```

2. 切换到 Windows 95/98/ME 系统并登录域。删除 C:\Windows 下所有的 `*.PWL` 文件。重启机器并使用无效密码以 `samba1` 身份登录你的域。这有效吗？然后：
   - 进入你的网络属性。选择“Microsoft 网络客户端”并点击属性。启用“登录到 Windows 域”。
   - 使用 Windows 资源管理器删除 C:\Windows 下所有的 `*.PWL` 文件。
   - 重启系统。
   - 使用有效密码以 `samba1` 登录。

### 登录脚本

3. 修改你的 `smb.conf` 文件，使客户端登录域使用登录脚本 `/home/netlogon/login.bat`。创建登录脚本，使其包含 MS-DOS 命令 `net h: \server\homes`。

```
vi /etc/samba/smb.conf
```

在 `[global]` 部分添加以下行：

```
logon script = logon.bat
```

```
testpam
redhat# service smb restart; smb restart; smb restart
suse# vi /home/netlogon/logon.bat
```

文件应包含：

```
@echo off
net use h: \servername\homes
```

4. 在你的 Windows 95/98/ME 系统上，注销并重新登录。登录后，启动 Windows 资源管理器。你看到 H:- 盘了吗？你可以修改和添加文件吗？

### 漫游配置文件

5. 修改你的 `smb.conf` 文件以支持漫游配置文件，同时支持 Windows 95/98/ME 客户端和 Windows NT/2000 客户端。

```
# mkdir /home/profile
# mkdir /home/profile/samba1
# chown samba1:samba1 /home/profile/samba1
# mkdir /home/profile/samba2
# chown samba2:samba2 /home/profile/samba2
# vi /etc/samba/smb.conf
```

删除 logon script 行，因为我们当前的脚本会干扰驱动驱动参数。
在 `[global]` 部分添加以下行：

```
logon path = \server1\profile\%U
logon drive = H:
logon home = \server1\%U
preserve case = yes
short preserve case = yes
```

区分大小写 = 无

添加以下共享：

```
[profile]
path = /home/profile
create mode = 0600
directory mode = 0770
browsable = yes
writable = yes
```

```
testparam
redhat# service smb restart; smb restart
suse# rcmnb restart; smb restart
```

6. 转到你的 Windows 95/98/ME 并配置漫游配置文件。重启系统，然后以 samba1 的身份登录。在询问是否要使用漫游配置文件时，回答“是”。在你的环境中更改某些内容（例如背景图案）并注销。
   - 点击开始；设置：控制面板。点击密码。转到“用户配置文件”选项卡并选择你想要的漫游配置级别。点击确定，但先不要重启计算机。
   - 在控制面板中，点击“网络”。验证主登录（Primary Logon）已设置为“Microsoft 网络的客户端”。
   - 重启你的系统。
   - 使用密码 samba1 登录 samba1。当出现消息询问是否要启用漫游配置文件时，点击是。
   - 更改环境中的某些内容，例如背景图案，并注销。
   - 在 PDC（主域控制器）上：

```
# Is -l /home/samba1
```

   - 再次在你的 Windows 机器上登录 samba1。一切运行正常吗？
   - 在教室里另一台也配置了漫游配置文件的 Windows 机器上登录 samba1（不要忘记指定你自己的域名）。这可行吗？

### 在域中加入 Samba 服务器

对于练习的这部分，你需要与伙伴小组合作。

7. 与你的伙伴小组讨论谁将作为域的 PDC，谁的服务器将加入域。交换关于 netbios 名称、域名、根密码等信息。
8. 配置 PDC 以便允许系统自动加入域。

```
# vi /etc/samba/smb.conf
```

在 [global] 部分添加以下脚本（单单行）：

```
add user script = /usr/sbin/useradd -g 100 -d /dev/null -c "%U" -s /bin/false -M %u
```

```
testparam
redhat# service smb restart
suse# rcmnb restart; rcmnb restart
# smbadduser root:root
```

新的 SMB 密码: ibmlinx
重输新的 SMB 密码: ibmlinx

9. 在 PDC 上为另一服务器创建一个机器信任账户。

```
useradd -g 100 -d /dev/null -c "System 2" -s /bin/false -M system2$
password -l system2
# smbpasswd -a -m system2
```

10. 配置另一服务器以支持域登录，并将其加入域。

```
redhat# service smb stop
suse# rcmnb stop; rcmnb stop
mv /etc/samba/smb.conf /etc/samba/smb.conf.pdc
vi /etc/samba/smb.conf
```

创建此文件使其看起来如下：

```
[global]
netbios name = system2
workgroup = workgroup1
security = domain
password server = *
encrypt passwords = yes
```



```
>> testparam
>> # smbpasswd -j workgroup1 -r system1 -U root
>> redhat# service smb start
suse# rcmnb start; rcmnb start
```

- 11. 从任何 Samba 服务器，使用`smclient`命令查看 Samba 服务器（不是 PDC）上的信息。以`samba1`身份登录。你需要什么密码？在 PDC 上，将用户`samba1`的密码更改为其他。然后尝试登录另一个服务器。密码真的会在 PDC 上检查吗？

```
>> smclient -L server2 -U samba1%samba1

（在 PDC 上）
>> # smbpasswd samba1
新的 SMB 密码: somethingelse

重输新的 SMB 密码: somethingelse
（在任何系统上）

>> # smclient -L server2 -U samba1%samba1

>> # smclient -L server2 -U samba1%somethingelse
```

实验结束

# 练习 7. 使用 SWAT 配置 Samba

### 本练习内容

本练习将使用图形界面 SWAT 环境配置 Samba 服务器。

### 你应该能够做什么

在实验结束时，你应该能够：

- 安装 SWAT 并配置`xinetd.conf`
- 使用 SWAT 配置文件共享
- 使用 SWAT 配置打印机共享

### 练习说明

### 安装和配置 SWAT

Red Hat Linux 将 SWAT 包含在独立于 Samba 服务器和客户端软件的 RPM 中，而 SuSE 将 SWAT 包含在主 Samba 服务器 RPM 中。

- 1. **仅限 Red Hat Linux**：验证 SWAT RPM 是否安装。如果没有安装，现在安装它。
- 2. 启用 SWAT。

### 运行 SWAT

你在实验中的目标是使用 SWAT 重建你到为止生成的`smb.conf`文件。你将从一个空白配置文件开始，逐步通过 SWAT 屏幕，填写参数以创建磁盘共享打印打印共享。

在这些实验的答案中，我们列出了你可能更改过的参数，但它们可能不完整，或者你可能某处使用了同义词（例如，`writable = yes`和`read only = no`是同义词）。因此，答案可能不包含创建与你过去几天构建的完全相同的配置文件所需的设置。

- 3. 将`smb.conf`文件重命名为`smb.conf.org`以保存你的原始设置。然后为 SWAT 创建一个新的`/etc/smb.conf`。
- 4. 启动网络浏览器（Netscape, Conqueror 或 Lynx）并访问`http://localhost:901`。使用 root 密码登录。浏览不同的屏幕直到你对设置感到熟悉。

注意：如果你的浏览器之前使用了代理服务器，你现在可能需要禁用该代理服务器。

- 5. 访问全局参数部分，并用你到目前为止使用的值填充字段。最好通过记忆或通过回顾之前的实验来完成，但如果你卡住了，可以参考你的`/etc/samba/smb.conf.org`文件。你随时可以访问 **View**（查看）链接查看目前的配置文件样式。
- 6. 现在进入磁盘共享部分并创建共享。
- 7. 现在进入打印机共享部分。
- 8. 现在添加打印机共享。

### 比较文件

- 9. 比较文件查看差异。
- 10. 尝试保存结果。

实验结束

依赖。你可以随时访问“查看”（View）链接来查看目前配置文件的样貌。

- 6. 现在前往磁盘共享部分，创建你在课程中一直使用的共享。
- 7. 此时，你应该能够重启服务器并使用客户端来验证你目前所完成的工作。尝试一下看看它是如何运行的！
- 8. 现在添加所有的打印机共享。根据你的`printcap`文件的内容，最后一步可能非常简单，因为 Samba 会读取该文件并动态创建打印机共享。如果你愿意，可以返回全局部分（global section）并像在之前的实验中中做的那样关闭“加载打印机”（load printers），然后由你自己创建这些共享。

### 比较文件

- 9. 尝试比较`/etc/smb.org`和`/etc/smb.conf`文件，查看哪些参数不同。你打算如何处理这些注释？

```bash
diff /etc/samba/smb.conf /etc/samba/smb.conf.org
```

- 10. 是否有一个程序可以打印出所有的配置参数，但忽略任何注释？如果有，你可以对`smb.org`文件运行该程序并保存结果。然后对`smb.conf`文件再次运行它并保存这些结果。当你比较这两组结果时，将是准确的，因为注释已经了。执行这一操作。

```bash
testParm /etc/samba/smb.conf.org > /tmp/smb.conf.org

testParm /etc/samba/smb.conf > /tmp/smb.conf

diff /tmp/smb.conf /tmp/smb.conf
```

上一个命令的输出是仍需要检查的配置参数。

## 实验结束

![](img/02c5567fb834f88299ec1da6031f7afb_55_0.png)
