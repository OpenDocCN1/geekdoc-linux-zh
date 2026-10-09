

## 安全

### root 所有的 setuid 程序极其危险

由于由 root 所有的 setuid 程序允许那些不知道 root 密码且无法使用 sudo 的人获取 root 权限，它们对恶意用户来说是非常诱人的目标。此外，在普通程序中会导致崩溃的编程错误在 setuid 程序中可能变成 root 漏洞。系统中应尽可能少地包含这类程序。您可以通过挂载带有 nosuid 选项的文件系统（第 522 页）在文件系统层面禁用 setuid 程序。您也可以使用 SELinux（第 472 页）来禁用 setuid 程序。有关列出本地系统上所有 setuid 文件的 find 命令，请参见第 458 页。未来版本的 Fedora/RHEL 将移除大多数 setuid 文件；请参见 fedoraproject.org/wiki/Features/RemoveSETUID。

### 不要允许通过互联网进行 root 访问

禁止用户通过网络以 root 身份登录是 Fedora/RHEL 的默认策略。/etc/securetty 文件必须包含您希望用户能够以 root 身份登录的所有设备名称。但是，您可以使用 ssh（第 685 页）通过网络以 root 身份登录。在 Fedora/RHEL 的默认配置中，ssh 的 PAM 配置不会调用使用 securetty 或 access.conf 配置文件的模块。此外，在 /etc/sshd_config 中，Fedora/RHEL 将 PermitRootLogin 设置为 yes（这是默认设置），以允许 root 使用 ssh（第 705 页）登录。为了更安全，请将 PermitRootLogin 更改为 no。

## 真实 UID 与有效 UID

### UID 与用户名

UID（用户 ID）是系统将用户名称关联到的数字。UID 0 通常与用户名 root 关联。为了加快速度，内核通过 UID 而非用户名来跟踪用户。大多数实用程序显示关联的用户名称，而不是 UID。

内核为每个进程关联两个 UID：一个真实 UID 和一个有效 UID。/etc/passwd 文件（或 NIS/LDAP）的第三列指定您的真实 UID。当您登录时，您的真实 UID 与运行登录 shell 的进程相关联。由于您没有执行任何更改操作，运行登录 shell 的进程的有效 UID 与该进程的真实 UID 相同。

### 进程权限

内核根据进程的有效 UID 来确定该进程拥有哪些权限。例如，当进程请求打开文件或执行程序时，内核会查看该进程的有效 UID，以判断是否允许这样做。当用户运行 setuid 程序（第 196 页）时，该程序将以程序所有者的 UID 运行，而不是以运行该程序的用户 UID 运行。

### 术语：root 权限

当本书使用短语“以 root 权限运行”或“获取 root 权限”时，其含义是以有效 UID 为 0（root）的身份运行。

## 使用 su 获取 root 权限

安装 Fedora/RHEL 时，您需要为 root 账户分配一个密码。因此，您可以使用 su 获取 root 权限，而无需进行其他设置。

su（替换用户）实用程序可以启动一个 shell 或以指定用户（包括 root）的身份和权限（有效 UID）执行程序。

- 在命令行中，su 后面跟用户名称；如果您拥有 root 权限或者知道该用户的密码，新启动的 shell 将采用该用户的身份（有效 UID）。
- 当您不带参数执行 su 命令时，su 默认启动一个具有 root 权限的 shell（您需要提供 root 密码）。该 shell 以有效 UID 为 0（root）的身份运行。

### 启动 ROOT SHELL

当您输入 su 命令以获取 root 权限时，su 会启动一个新的 shell，并显示 # 提示符。该 shell 以有效 UID 为 0（root）的身份运行。通过终止此 shell，您可以返回到正常状态（以及您之前的 shell 和提示符）：按 CONTROL-D 或输入 exit 命令。

who 实用程序在带有参数 am i 调用时，会显示调用它的进程的真实 UID（转换为 用户名）。whoami 实用程序显示调用它的进程的有效 UID（转换为 用户名）。如下例所示，su 实用程序（sudo 也是如此）会改变其启动的进程的有效 UID，但保持真实 UID 不变。

```bash
$ who am i
sam  pts/2  2013-06-12 13:43 (192.168.206.1)
$ whoami
sam
$ su
Password:
# who am i
sam  pts/2  2013-06-12 13:43 (192.168.206.1)
# whoami
root
```

不带任何参数执行 su 命令会改变您的有效用户 ID 和组 ID，但对环境的更改最小。例如，PATH 的值与执行 su 命令之前相同。id 实用程序显示调用它的进程的有效 UID 和 GID，以及该进程关联的组。在以下示例中，以 context 开头的信息涉及 SELinux：

```bash
$ pwd
/home/sam
$ echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/sam/.local/bin:/home/sam/bin
$ id
uid=1000(sam) gid=1400(pubs) groups=1400(pubs),10(wheel) context=unconfined_u: ...
$ su
Password:
# pwd
/home/sam
# echo $PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/sam/.local/bin:/home/sam/bin
# id
uid=0(root) gid=0(root) groups=0(root) context=unconfined_u: ...
# exit
exit
$
```

当您执行命令 su -（您可以使用 -l 或 --login 代替连字符）时，su 提供 root 登录 shell：这就像您以 root 身份登录一样。不仅 shell 的有效用户 ID 和组 ID 与 root 匹配，而且环境与以 root 身份登录时相同。登录 shell 在显示提示符之前执行适当的启动文件（第 329 页），并且工作目录设置为如果您以 root 身份登录时的目录（/root）。PATH 也设置为与以 root 身份登录时相同。然而，如 who 所示，新进程的真实 UID 并未从父进程中改变。

```bash
$ su -
Password:
# pwd
/root
# echo $PATH
/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/root/bin
# who am i
sam pts/5 2013-06-12 13:43 (192.168.206.1)
```

### 执行单个命令

您可以使用带 -c 选项的 su 以 root 权限运行命令，并在命令执行完毕后返回到原始 shell。在以下示例中，Sam 试图以非特权用户身份显示 /etc/shadow 文件。cat 实用程序显示一条错误消息。当他使用 su 运行 cat 来显示文件时，su 提示输入密码，他输入了 root 密码，命令成功执行。引号是必需的，因为 su -c 将要执行的命令作为单个参数。

```bash
$ cat /etc/shadow
cat: /etc/shadow: Permission denied

$ su -c 'cat /etc/shadow'
Password:
root: $6$19$GhV$fmvp.m2f$2R1lLZ ... Fyc3wYZFQ/:15861:0:99999:7:::
bin: $:15839:0:99999:7:::
daemon: $:15839:0:99999:7:::
adm: $:15839:0:99999:7:::
```

下一个示例首先显示 Sam 不被允许杀死（第 465 页）某个进程。然而，通过使用 su -c 和 root 密码，Sam 以 root 权限工作，并获准杀死该进程。

```bash
$ kill -15 4982
-bash: kill: (4982) - Operation not permitted
$ su -c "kill -15 4982"
Password:
$
```

最后一个示例结合使用 - 和 -c 选项，展示如何在 root 环境中以 root 权限运行单个命令：

```bash
$ su -c pwd
Password:
/home/sam
$ su - -c pwd
Password:
/root
```

## root 权限、PATH 与安全

- 安全：以 root 权限工作时，PATH 中保留的目录越少，您在以 root 权限工作时执行不可信程序的可能性就越小。如果可能，请仅在 root 的 PATH 中保留默认目录，以及 /usr/bin 和 /usr/sbin。切勿将工作目录包含在 PATH 中（无论是 PATH 中的任何位置作为 : 或 ;，还是作为 PATH 的最后一个元素）。有关更多信息，请参见第 359 页的“PATH：shell 查找程序的位置”。

## 使用 sudo 获取 root 权限

如果 sudo（www.sudo.ws）尚未设置为您可以使用，且存在 root 密码且您知道它是什么，请参见下一页的“管理员和 wheel 组”，了解如何设置 sudo 以使其能够获取 root 权限。

## sudo 的优势

使用 sudo 而不是 root 账户进行系统管理具有许多优势。

- 当您运行 sudo 时，它请求的是您的密码——而不是 root 密码——因此您只需要记住一个密码。
- sudo 实用程序记录其执行的所有命令。此日志对于系统审计以及在您犯错误时追溯步骤非常有用。
- sudo 实用程序记录发出 sudo 命令的用户名。在拥有多个管理员的系统中，此日志告诉您哪些用户发出了 sudo 命令。没有 sudo，您将无法知道哪个用户在以 root 权限工作时发出了命令。
- sudo 实用程序允许实施比使用 su 和 root 账户更细粒度的安全策略。使用 sudo，您可以使特定用户执行特定命令——这是传统的 root 账户设置无法做到的。
- 使用 sudo 使恶意用户更难访问系统。当 root 账户处于解锁状态时，恶意用户在开始前就知道她想要破解的账户的用户名。当 root 账户被锁定时，用户必须确定用户名和密码才能闯入系统。

