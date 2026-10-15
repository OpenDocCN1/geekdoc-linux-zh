
# 创建用户

```bash
root@kemal:~# adduser zeynep
Adding new group `zeynep` (1001) ...
Adding new user `zeynep` (1000) with group `zeynep` ...
Creating home directory `/home/zeynep` ...
Copying files from `/etc/skel` ...
Yeni parolayı girin: 
Yeni parolayı tekrar girin:
password: şifre başarıyla güncellendi
zeynep için kullanıcı bilgileri değiştiriliyor
Yeni değeri girin, veya varsayılan değer için ENTER'a basın
Tam Isim []:
Oda Numarası []:
İş Telefonu []:
Ev Telefonu []:
Diğer []:
Is the information correct? [Y/n] y
root@kemal:~# _
```

如你所见，用户的家目录已创建，且用户已被包含在 `zeynep` 组中。

```bash
root@kemal:~# cd /home
root@kemal:/home# ls
zeynep
root@kemal:/home# groups zeynep
zeynep : zeynep
root@kemal:/home# _
```

在这里，我们来讨论 `uid`（用户 ID）和 `gid`（组 ID）。在 Linux 系统中，为用户发放一个标识数字。这些数字如下：

- root 用户：`UID=0`, `GID=0`
- 系统用户：`UID-499`, `GID-499`
- 普通用户：`UID-500`, `GID-500`

让我们通过 `id` 检查这些数字。

```bash
root@kemal:~# id
uid=0(root) gid=0(root)
root@kemal:~# id zeynep
uid=1000(zeynep) gid=1001(zeynep) groups=zeynep
root@kemal:~#
```

关于用户的信息会自动写入 `/etc/passwd` 和 `/etc/shadow`。

```bash
root@kemal:~# cat /etc/passwd | grep zeynep
zeynep:x:1000:1001:/home/zeynep:/bin/bash
root@kemal:~# cat /etc/shadow | grep zeynep
zeynep:!YSTKDDla.Ifdak0QNONQ7Y1Oc:99999:::
root@kemal:~#
```

可以使用 `useradd` 创建用户账户。创建一个名为 `zeynep` 的用户可以使用 `useradd -m zeynep`。使用 `-m` 参数会自动生成用户对应的家目录。如果不使用该参数，我们可以手动创建此目录。之后我们可以使用 `passwd zeynep` 为该用户设置密码。

## 删除用户

可以使用两个命令从系统中删除用户。如果你使用 `adduser` 创建用户，删除用户及其家目录（例如 'zeynep'）可以使用 `deluser --remove-home zeynep`。如果你使用 `useradd -m` 创建用户，删除其家目录必须使用 `userdel -r zeynep`。

## 手动添加新用户

手动向系统添加用户需要在 `passwd`、`shadow` 和 `group` 文件进行设置。使用 `vim` 等控制命令可以方便地编辑 `passwd` 和 `group` 文件。记住这一点。例如，我们想向系统添加一个名为 `deneme` 的用户。为了实验，我们在 `passwd` 文件中添加 `deneme:x:2000:2000::/home/deneme:/bin/false`，创建一个名为 `deneme` 的用户，其数字为 2000，属于 2000 组。在完全创建用户后，我们将 `/bin/false` 改为 `/bin/bash` 以赋予他们 bash 壳。我们将 `/home/deneme` 设置为主目录。现在需要在 `shadow` 文件中进行设置。为此，我们将该行复制到底部，然后将用户名改为 `deneme`。然后我们从终端使用 `passwd deneme` 为新用户设置新密码。最后，在 `/etc/group` 文件中添加 `deneme:x:2000` 并保存。在完成这些设置后，我们在 `/home` 下创建 `deneme` 文件夹并安排权限：

```bash
- cd /home
- mkdir deneme
- chown deneme:deneme deneme
- chmod 700 deneme
```

通过在 `/bin/false` 开头写入 `/bin/bash`，我们创建了新用户。

## 修改用户信息

在系统中更改用户的个人信息可以使用 `chfn` 命令。例如，要更改 `zeynep` 的资料，输入 `chfn zeynep` 并按顺序输入所需信息即可完成所需的更改。

![](img/aa6ce54dbb8ffe59d7befb8c6764064_128_0.png)

## 列出用户信息

要查看用户信息可以使用 `chage` 命令。例如，通过 `chage -l zeynep` 命令将列出用户 `zeynep` 的信息。

![](img/aa6ce54dbb8ffe59d7befb8c6764064_128_1.png)

此命令不仅用于显示用户信息。例如，`chage` 命令用于更改用户的密码过期日期。如果我们想让 `zeynep` 的密码在 2015 年 11 月 16 日失效，必须使用 `chage -E 2015/11/16 zeynep`。

## 使用户激活或非激活

锁定用户账户或重新激活已锁账户我们基本上使用 `usermod [-L|-U] <user>` 命令。例如，锁定名为 `deneme` 的用户账户使用 `usermod -L deneme`；要重新激活账户必须使用 `usermod -U deneme`。要禁用用户账户，在 `/etc/shadow` 文件的加密密码区域，我们在密码开头添加一个感叹号 `!`。

额外信息，如果你想删除属于 `/etc/shadow` 文件的密码区域，必须使用 `passwd -d <user>` 命令。此过程不会禁用用户。用户可以在不需要密码的情况下远程连接到系统。因此，这种方法被称为快速禁用用户方法。或者如果你倾向于使用列表账户，可以使用此方法。

## 修改用户密码

如你所知，`root` 用户有权对系统进行任何更改，包括所有关于用户的应用程序。`root` 用户可以随时更改系统中的任何用户。要执行此操作，`root` 用户必须使用相应的命令，例如对于 `zeynep` 用户，需要使用 `passwd zeynep` 命令。如果 `root` 用户想更改自己的密码，他/她只能使用 `passwd` 命令。

```
root@kemal:-# passwd zeynep
Yeni parolayı girin:
Yeni parolayı tekrar girin:
passwd: şifre başarıyla güncellendi
root@kemal:-#
```

## 冒充另一个用户的配置

用户可以冒充其他用户的身份，这意味着以其他用户的权限工作并执行某些进程。首先，他/她应该知道该用户的密码。如果你是 `root` 用户，你可以以任何用户的配置进行工作。

在继续之前，让我们回一下之前提到的 `w` 和 `whoami` 命令。通过这些命令，我们可以看到一些信息，例如我们正在以什么身份工作，我们是以什么身份身份连接到系统的。你可以在下表中看到示例用法和区别：

```
root@kemal:-# w
10:50 up 11 min, 2 users,  load average: 0.27, 0.52, 0.46
USR     TTY             FROM             LOGIN   JCPU    PCPU    WHAT
root     0                               10:15  ?xd7   1:12  0.14s gdm-session-wor
pts/0    :0                               10:19  2.00s  0.14s 0.01s w
root@kemal:-# who
root     0                               2015-08-19 10:19 (:0)
pts/0
root@kemal:-# whoami
root     0                               2015-08-19 10:19 (:0)
pts/0
root@kemal:-# who am i
root     0                               2015-08-19 10:19 (:0)
pts/0
```
