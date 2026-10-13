
## 表 5.1 继续

| 属性名称 | 说明 |
|---|---|
| uid | 用户的用户 ID |
| gid | 用户的默认组 ID |
| realname | 用户的真实姓名 |
| home | 用户的主目录 |
| shell | 用户的登录 shell |

要在实际中看到这一点，以下是我如何提取一份列出账户名称和密码字符串的报告：

```
$ nireport . /users name passwd
nobody *
root c8bklkt6E1th9
daemon *
unknown *
www *
taylor fse2jv5k6jIA
```

你可以看到，其中四个账户（正如前面所报告的那样，使用 /dev/null 登录 shell 的账户）已禁用登录功能，而另外两个账户具有显式的加密密码。

4. 为了让事情更有趣，我创建了一个 UID 为 0 且没有密码的账户，名为 badguy，恰如其名。不过这次我不能直接将信息追加到 /etc/passwd 文件中；我需要使用一个名为 niadduser 的脚本将信息添加到 NetInfo 数据库中。（我们稍后在本小时内会开发这个脚本。）

在有了这个新账户之后，让我们看看如何将 nireport 与一些常规 Unix 工具结合起来创建一些有用的分析过滤器：

```
$ nireport . /users name uid | awk '$2 == 0 { print $0 }'
root 0
badguy 0
```

这表明有两个账户的 UID=0。

缺失密码的测试稍微复杂一些：

```
$ nireport . /users name passwd | awk 'NF==1 { print $0 }'
badguy
```

在这种情况下，变量 NF 是字段数，因此 awk 测试本质上是“如果输出行中只有一个字段。”

5. 最后，在离开之前，让我们更改 badguy 账户的密码，以确保不会留下这个巨大的安全漏洞！

```
$ passwd badguy
Changing password for badguy.
New password:
Retype new password:
$ ni report . /users name passwd | grep badguy
badguy Hk4IS.3eeh69.
```

看起来一切再次安全了！

从某种意义上说，NetInfo 是一个很棒的应用程序，管理着构成 Unix 系统世界的各种数据库，包括打印机、Internet 服务、用户账户和网络连接。它也有着悠久的血统，源自 Sun Microsystems 最初开发的网络信息服务（NIS）和 Yellow Pages（YP）服务。（一分钟后我们会谈谈这些服务。）

然而，NetInfo 在 Unix 世界中也有些另类。不仅它不是流行 Linux 发行版的一部分，它也没有包含在任何主要商业 Unix 发行版中（除了 Mac OS X）。因此 NetInfo 非常不兼容，且特定于平台和版本。

通常，我会建议你仅出于这个原因而避免使用该实用程序，但如果你运行的是 Darwin 或其他启用了 NIS/YP（NetInfo）的 Unix 系统，你必须通过 NetInfo 设施进行操作，否则你的更改将被忽略。例如，测试 Darwin 平台上的 /etc/passwd 文件在末尾包含以下几行：

```
$ tail -3 /etc/passwd
www::70:70:World Wide Web Server:/Library/WebServer:/noshell
unknown::*99:99:Unknown User:/nohome:/noshell
testme::0:0:Unknown Root User:/var/root:/bin/tcsh
```

然而你会注意到，如果你翻回去查看，testme 账户从未出现在 NetInfo 列表中。这是因为它被添加到密码文件中，但未添加到 NetInfo 数据库中。

## 添加用户和 adduser 脚本

先把 Darwin、BSD 和 NetInfo 的怪异之处放在一边，让我们呼吸一下新鲜空气，回到“常规 Unix”（无论那意味着什么）吧，好吗？

创建新用户账户需要几个步骤，而不仅仅是创建 /etc/passwd 文件中的新条目。这些步骤如下：

- 1. 将用户添加到 /etc/passwd 文件。
- 2. 将用户添加到 /etc/group 文件。
- 3. 创建其主目录。
- 4. 可选地复制默认 .profile/.login 文件。
- 5. 确保该目录及其内容都归新用户所有。
- 6. 将其初始密码设置为已知值。

这些步骤不少，都可以手工完成，但为什么要那样做呢？相反，让我们构建一个脚本来自动化所有操作，并一步将用户添加到系统中。

![](img/5ced0c78d748bd190e9027e5549a3622_111_0.png)

> Solaris 和 Red Hat Linux 7.2 中都已内置了 adduser 命令，但当你使用多种 Unix 变体时，你会发现 adduser 并不是广泛可用，而且语法因系统而异。更明智的解决方案是了解该命令的作用，然后为自己的需求复制它。有了自己的脚本，你可以为首选配置进行微调，然后随着管理职责的扩展将其从系统移动到系统。许多顶级系统管理员都有自己随身携带的完整工具包。

## 任务 5.3：在常规 Unix 世界中添加用户

如果你使用的是标准 Unix 系统，添加用户就是将他们添加到密码文件和组文件，然后创建主目录并设置初始密码的直接序列。

- 1. 开始时，我们需要在开始构建账户之前从系统管理员收集信息。这最容易使用 shell 内置的 read 函数完成。以下是它如何工作的演示：

```
echo "Add new user account to ${hostname}"
echo -n "login: " ; read login
echo -n "uid: " ; read uid
echo -n "gid: " ; read gid
echo -n "full name: " ; read fullname
echo -n "home dir: " ; read homedir
echo -n "shell: " ; read shell

echo "Setting up account:"
echo "${login}:x:${uid}:${gid}:${fullname}:${homedir}:${shell}"
```

作为练习，如果你运行此脚本，你可以看到它如何简化收集必要数据并输出 /etc/passwd 格式行的过程：
Add new user account to staging.intuitive.com
login: astaire
uid: 211
gid: 211
full name: Fred Astaire
home dir: /home/astaire
shell: /bin/bash
Setting up account:
astaire:x:211:211:Fred Astaire:/home/astaire:/bin/bash

这是脚本的核心功能。现在是时候改进了……

2. 开始时，让我们认识到主目录总是在系统上的同一文件夹中，并且其名称始终与账户名称相同：

```
$homedir=$defaulthome/$account
```

此外，没有进一步信息很难提示管理员输入 UID。同时，按惯例，UID 在 /etc/passwd 文件中按升序排列，因此如果你自动提取最后一个 UID 并递增它，你就可以将其用作默认的新 UID：

```
currentUID=`tail -1 /etc/passwd | cut -d: -f3`
newUID=`expr $currentUID + 1`
```

这种方法的问题在于，如果由于某种原因密码文件没有将最高 UID 作为最后一行，你可能会遇到严重问题。相反，更明智的方法是使用 awk 提取最高 UID（加一）：

```
uid=`awk -F: '{ if (big < $3) big=$3 } END { print big + 1 }' /etc/passwd`
```

这是一个非常优雅且相当典型的 Unix 解决方案。

![](img/5ced0c78d748bd190e9027e5549a3622_112_0.png)

> 许多 Unix 系统管理员更喜欢使用 Perl 而不是 awk，但我仍然倾向于使用 awk，因为我可以 100% 确定它会包含在所有 Unix 的标准发行版中，而有些系统会排除 Perl，让用户事后自行安装。

3. 分配默认组有两种方法，正如我们已经看到的。有些站点默认给每个用户自己的个人组，这始终与 UID 相同。其他站点则有所有用户默认加入的标准组。这些可以在代码中很容易地建模：

```
# if your site policy is for all users to get their own group
gid=$uid
# otherwise, add them to the default group
gid=$defaultgid
```

当我们自动修改 /etc/group 文件以包含新账户时，还需要进行额外的调整，但我们已经超前了！

4. 以下是脚本的第一个完整版本，其中包含一个额外的测试以确保只有用户 root 可以运行它：

```bash
$ cat adduser.sh
#!/bin/sh

# ADDUSER - add a new user to the system, including building their
# home directory, copying in default config data, etc.

progname=`basename $0`
pwfile="/etc/passwd"
gfile="/etc/group"
hdir="/home"

if [ "`whoami`" != "root" ] ; then
  echo "$progname: Error: You must be root to run this command."
  exit 0
fi

echo "Add new user account to `hostname`"
echo -n "login: "  ; read login

uid=`awk -F: '{ if (big < $3) big=$3 } END { print big + 1 }' /etc/passwd`
homedir=$hdir/$login

# we are giving each user their own group, so gid=uid
gid=$uid

echo -n "full name: "  ; read fullname
echo -n "shell: "      ; read shell

echo "Ready to set up account:"
echo "$login:x:$uid:$gid:$fullname:$homedir:$shell"
exit 0
```

运行它时，只需要三个字段：

```
$ sh adduser.sh
Add new user account to staging.intuitive.com
login: testdude
full name: The Test Dude
shell: /bin/csh
Ready to set up account:
testdude:x:503:503:The Test Dude:/home/testdude:/bin/csh
```

下一步显然是让脚本开始执行操作，而不是仅仅演示如何提示输入！这可以通过添加以下行来完成：

```bash
echo ${login}:x:${uid}:${gid}:${fullname}:${homedir}:${shell} >> /etc/passwd
mkdir $homedir
```
