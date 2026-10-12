
### 使用 su 获取 root 权限

在安装 Fedora/RHEL 时，你为 root 账户分配了一个密码。因此，你可以直接使用 `su` 获取 root 权限，而无需任何额外设置。

`su`（替换用户）实用程序可以使用指定用户的身份和权限生成 shell 或执行程序，包括 root：

- 在命令行中在 `su` 后跟随用户名称；如果你正在以 root 权限工作或知道该用户的密码，你将获得该用户的身份。
- 当你不带任何参数给出 `su` 命令时，`su` 默认生成一个具有 root 权限的 shell（你必须提供 root 密码）。

## 启动 root shell

当你输入 `su` 命令以 root 权限工作时，`su` 会启动一个新的 shell，显示 `#` 提示符。你可以通过终止此 shell 来返回正常状态（以及之前的 shell 和 提示符）：按下 CTRL-D 或输入 `exit` 命令。不带任何参数的 `su` 命令会更改你的用户 ID 和组 ID，但对环境的更改极小。例如，`PATH` 的值与你输入 `su` 命令之前相同。`id` 显示你关联的用户 ID 和组 ID。在以下示例中，以 `context` 开头的信息属于 SELinux：

```
$ pw
/home/sam
$ echo PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/bin:/sbin:/home/sam/bin
$ id
uid=500(sam) gid=500(sam) groups=500(sam) context=unconfined:u: ...
$ su
Password:
# pw
/home/sam
# echo PATH
/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/bin:/sbin:/home/sam/bin
# id
uid=0(root) gid=0(root) groups=0(root),1(bin),2(daemon),3(sys),4(adm)
# exit
```

当你输入 `su` 命令（可以使用 `-l` 或 `--` 代替连字符）时，`su` 提供一个 root 登录 shell：就像是你以 root 身份登录一样。不仅 shell 的用户 ID 和组 ID 与 root 匹配，环境也与你以 root 登录时相同。登录 shell 在显示提示符之前会执行相应的启动文件（第 282 页），并且工作目录被设置为以 root 登录时的目录（`/`）。`PATH` 的设置也如同你登录 root 一，通常在 `/bin` 之前包含 `/sbin` 和 `/usr/sbin`。

```
$ su
Password:
# pwd
/root
# echo PATH
/usr/local/sbin:/usr/local/bin:/bin:/usr/sbin:/root
```

## 执行单个命令

你可以使用 `-c` 选项以 root 权限运行命令，命令执行完成后会返回原始 shell。在示例中，Sam 以自己的非特权用户身份尝试设置系统时钟。`date` 显示错误信息，随后是所输入的日期的扩展版本。当他使用 root 设置系统时钟时，系统会提示他输入密码，他响应 root 命令，而引号是必要的，因为 `-c` 将要执行的命令视为单个参数。

```
$ date 1281448
date: not set
$ su -c "date 1281448"
Password:
Wed Dec 28 14:48 UTC 2023
```

## root 权限、PATH 和安全

root 拥有的 setuid 程序极其危险。由于 root 拥有的 setuid 程序允许任何不知道 root 密码且无法使用 setuid 获取 root 权限的人获取权限，它们是恶意用户的青睐目标。此外，导致普通程序崩溃的编程错误可能会变成 setuid 程序。系统应尽可能减少此类程序。你可以通过挂载带有 `nousid` 选项的文件系统（第 522 页）通过文件系统禁用 setuid 程序。你还可以使用 SELinux（第 459 页）来禁用 setuid 程序。参见第 459 页列出本地系统中所有 setuid 文件的命令。在未来的发布中，Fedora/RHEL 将移除所有 setuid 文件；见 `aproject.org/wiki/Features/RemoveSETUID`。

`/etc/security` 文件控制哪些终端（ttys）可以以 root 身份登录。通过 `/etc/security/access.conf` 文件，PAM 控制了登录的身份和方式。最初，该文件仅包含注释。详情请见第 463 页、文件中的注释以及 `access.conf` 页面。不允许通过互联网访问 root

禁止用户通过网络以 root 身份登录是 Fedora/RHEL 的默认策略。`/etc/security` 文件必须包含你希望能够以 root 身份登录的所有设备名称。

然而，你可以使用 `ssh`（第 673 页）通过网络以 root 身份登录。Fedora/RHEL 自带的 `ssh` 并不遵循 `security` 或 `access.conf` 中的指令。此外，在 `/etc/ssh/sshd_config` 中，Fedora/RHEL 将 `PermitRootLogin` 设置为 `yes`（默认设置），以允许 root 使用 `ssh` 登录（第 694 页）。为了更安全的系统，请将 `PermitRootLogin` 改为 `no`。
