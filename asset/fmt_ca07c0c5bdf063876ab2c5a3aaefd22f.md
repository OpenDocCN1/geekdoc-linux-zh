
### RSA 密钥指纹

RSA 密钥指纹是 `b5:fb3c:53:50:b4:ab:81:f3:cd:e2:bb:ba:44:d3:75`。

确认是否继续连接（是/否）？`yes`

警告：已永久将 `192.168.1.30` 添加到已知主机列表。

`admin42@ubuserserver`：`$ password:`

欢迎使用 `Ubuntu 12.04 LTS` (`GNU/Linux 3.2.0-26-generic-pae i686`)

* 文档：`https://help.ubuntu/`

有 1 个软件包可以更新。

更新均为安全更新。

上次登录：2012年6月6日 星期三 19:25:57 来源 `172.28.0.131`

`admin42@ubuserserver`：`-`

```
用户可通过输入 `exit` 或使用 `Ctrl-d` 退出远程服务器。
```

```
admin42@ubuserserver:-$ exit

logout

Connection to 192.168.1.30 closed.

paul@ub204:-$
```

### 在远程机器上执行命令

此截图显示了如何在远程服务器上执行 `pwd` 命令。不需要手动退出服务器。

```
paul@ubul204:-$ ssh admin42@192.168.1.30 pwd

admin42@192.168.1.30 password:

/home/admin42

paul@ubul204:-$
```

## 25.4. `scp`

`scp` 命令的工作原理与 `cp` 类似，但它允许复制的源和目的地位于 `ssh` 之后。这里是一个示例，我们从远程服务器将 `/etc/hosts` 文件复制到用户 `paul` 的家目录。

```
paul@ubuntu204:~~$ scp admin42@192.168.1.30:/etc/hosts /home/paul/serverhosts

admin42@192.168.1.30's password:

hosts                     100%   809      0.8KB/s  00:00
```

这是一个反向操作的示例，将本地文件复制到远程服务器。

```
paul@ubuntu204:~$ ~/serverhosts admin42@192.168.1.30:/etc/hosts.new

admin42@192.168.1.30's password:

serverhosts             100%   809      0.8KB/s  00:00
```

## 25.5. 设置无密码 `ssh`

要通过公钥/私钥设置无密码 `ssh` 身份验证，请使用 `ssh-keygen` 生成一个没有密码短的密钥对，然后将你的公钥复制到目标服务器。让我们分步进行。

在接下来的示例中，我们将在 `Alice` 和 `Bob` 之间建立无密码的 `ssh`。`Alice` 在红帽企业级 `Linux` 上有一个账户，`Bob` 在笔记本电脑上运行的是 `Ubuntu`。`Bob` 想要通过 `ssh` 和私钥系统允许 `Alice` 访问。这意味着即使 `Bob` 更改了他在笔记本电脑上的密码，`Alice` 仍然拥有访问权限。

### 25.5.1. `ssh-keygen`

下面的示例显示 `Alice` 使用 `ssh-keygen` 生成了一个密钥对。`Alice` 没有输入密码短语。

```
alice@RHEL5 ~]$ ssh-keygen -t rsa

Generating public/private rsa key pair.

Enter file to save the key (/home/alice/.ssh/id_rsa):

Created directory '/home/alice/.ssh'.

Enter empty passphrase (enter for no passphrase):

Enter same passphrase again:

Your identification has been saved in /home/alice/.ssh/id_rsa.

Your public key has been saved in /home/alice/.ssh/id_rsa.pub.

The key fingerprint is:

9bacac56:c9e8:d18c:4a25:72:bb:45:eb alice@RHEL5

[alice@RHEL5 ~$]
```

你可以同样的方式使用 `ssh-keygen -t dsa`。

### 25.5.2. `~/.ssh`

当 `ssh-keygen` 生成公钥和私钥时，它还会创建一个具有正确权限的隐藏 `.ssh` 目录。如果你需要，则需要执行 `chmod 700 ~`。否则，`ssh` 将拒绝使用这些密钥（全局可读的私钥是不安全的）。

如你所见，`Alice` 家目录下的 `.ssh` 目录是安全的。

```
alice@RHEL5 ~]$ ls -ld .ssh

drwxr-xr-x 2 alice alice 4096 1 07:38 .ssh

[alice@RHEL5 ~$]
```

`Bob` 在家里使用 `Ubuntu`。他需要创建 `.ssh` 目录并手动对其进行安全设置。

```
bob@laika:~$ mkdir .ssh

bob@laika:~$ ls -ld .ssh

drwxr-xr-x 2 bob bob 4096 2008-05-14 16:53 .ssh/

bob@laika:~$ chmod 700 .ssh/

bob@laika:~$
```

### 25.5.3. `id_rsa` 和 `id_rsa_pub`

`ssh-keygen` 命令在 `.ssh` 中生成两个密钥。公钥名为 `~/.ssh/id_rsa.pub`。私钥名为 `~/.ssh/id_rsa`。

#### `ssh` 客户端和服务器

```
[alice@RHEL 5 ~]$ ls -l .ssh/

total 16

--rw-r-- 1 alice 1671 May 07:38 id_rsa

--rw-r-- 1 alice 393 May 07:38 id_rsa.pub
```

当使用 `dsa` 代替 `rsa` 时，文件将名为 `id_dsa` 和 `id_dsa.pub`。

### 25.5.4. 从 Alice 的服务器将公钥复制到另一台电脑

为了将公钥从 `Alice` 的服务器复制到 `Bob` 的笔记本电脑，`Alice` 决定使用 `scp`。

```
[alice@RHEL 5~]$ scp id_rsa.pub bob@192.168.48.92:~/.ssh/authorized_keys

bob@192.168.48.92's password:

100 393 0.4KB/s 00:00
```

在复制第二个密钥时要小心！不要覆盖第一个密钥，而是将密钥追加到 `~/.ssh/authorized_keys` 文件中！

```
cat id_rsa.pub >> ~/.ssh/authorized_keys
```

`Alice` 也可以像示例这样使用 `ssh-copy-id`。

```
ssh-copy-id -i ~/.ssh/id_rsa.pub bob@192.168.48.92
```

### 25.5.5. `authorized_keys`

在 `~/.ssh` 目录中，你可以创建一个 `authorized_keys` 文件。该文件可以包含你信任的多个或多个密钥。信任的人可以使用他们的密钥证明自己的身份并通过 `ssh` 访问你的账户。示例显示 `authorized_keys` 文件包含了 `Alice` 的公钥。

```
bob@alice:~$ cat ~/.ssh/authorized_keys

ssh-rsa AAAAB3NzaC1yc2EAAAADAABABQyZ6y+HpqW2z1T4DtkqMnMW8bWU/OPG33fUv1/NHouilmpe20df/u2u4mljfde/0/tTMGSBenYCR8CT9Yta+y/scuhchaII2JVCggktuu41WFDLcum08/mKFrWfrc/UpN5XkT14l2mNp9c6
```

### 25.5.6. 使用 `ssh` 进行 `X` 转发

`Alice` 可以使用 `ssh` 连接到 `Bob` 的笔记本电脑。通过 `ssh` 结合，可以在远程主机上执行命令。`ssh` 的另一个流行功能是 `X11` 转发。以下是一个 `X` 转发的示例：在远程客端运行应用程序，将其附加到本地计算机。

```
paul@debian5:~$ ssh -X greet@dyns.org -p 5555
```
