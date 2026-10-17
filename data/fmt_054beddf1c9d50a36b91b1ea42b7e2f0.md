
```bash
bash# pwconv
bash# more /etc/shadow
/etc/shadow: No such file or directory
bash# more /etc/passwd

halt:\*:7:0:halt:/sbin:/sbin/halt
operator:\*:11:0:operator:/root:/bin/bash
root:fjFHWL5BVUg2:0:0:/root:/bin/bash
shutdown:\*:6:0:shutdown:/sbin:/sbin/shutdown
sync:\*:5:0:sync:/sbin:/bin/sync
bin:\*:1:1:bin:/bin:
ftp:\*:404:1::/home/ftp:/bin/bash
daemon:\*:2:2:daemon:/sbin:
adm:\*:3:4:adm:/var/adm:
lp:\*:4:7:lp:/var/spool/lpd:
mail:\*:8:12:mail:/var/spool/mail:
postmaster:\*:14:12:postmaster:/var/spool/mail:/bin/bash
news:\*:9:13:news:/usr/lib/news:
uucp:\*:10:14:uucp:/var/spool/uucppublic:
man:\*:13:15:man:/usr/man:
games:\*:12:100:games:/usr/games:
nobody:\*:65534:100:nobody:/dev/null:
veritech:jHgLDoQc0lJpY:1001:100:Rick Hunter,...:/home/veritech:/bin/bash
```

## 如何让影子文件变得无用？

简短的回答是：你最好知道这一点。我是在请一位同事协助我处理 UNIX 安全事务时发现的。我们走进教室，开始检查文件权限。我们首先检查的是 `/etc/passwd` 文件，发现密码字段中全是 `x`。这表明密码文件已启用影子保护。

记得可靠的 UNIX 系统也使用影子密码，尽管比 `/etc/shadow` 文件更复杂，所以我们决定接下来查找 `/etc/shadow` 文件。当我们找到它时，不仅可以看到它，还可以编辑它（文件权限设置为 666）。

不仅 `root` 账户很容易遭到入侵，这也让我意识到良好主机安全的重要性。（幸好这是教室环境，如果在生产服务器上，那将是一场灾难。）

教训：如果你确实使用了密码影子保护，`切勿更改影子文件的权限`。

## 禁用或删除未使用的账户

如果你决定不再希望某个特定用户存在于你的系统上（例如，另一位程序员写代码更好，或者有人更换了办公室同事），你应该禁用或删除该账户。禁用账户有多种方法，但如果你要删除账户，最好不要手动操作；必须先正确清理所有文件。

### 禁用账户

要锁定账户，请在 `passwd` 命令中使用 `-l` 选项。

```bash
bash# passwd -l veritech
Password changed.
```

你可以使用 `-S` 选项查看账户信息。注意其中的 `L` 表示已锁定。

```bash
bash# passwd -S veritech
veritech L 07/19/98 0 99999 7 -1
```

请注意，`/etc/passwd` 中没有任何内容被更改，但 `/etc/shadow` 的密码字段出现了明显差异。

```bash
bash# cat /etc/shadow
halt:*:10426:0:99999:7:::
operator:*:10426:0:99999:7:::
root:zDv78WL5BVg2:10426:0:99999:7:::
shutdown:*:10426:0:99999:7:::
sync:*:10426:0:99999:7:::
bin:*:10426:0:99999:7:::
ftp:*:10426:0:99999:7:::
daemon:*:10426:0:99999:7:::
adm:*:10426:0:99999:7:::
lp:*:10426:0:99999:7:::
mail:*:10426:0:99999:7:::
postmaster:*:10426:0:99999:7:::
news:*:10426:0:99999:7:::
uucp:*:10426:0:99999:7:::
man:*:10426:0:99999:7:::
games:*:10426:0:99999:7:::
nobody:*:10426:0:99999:7:::
bob:TH54ciu/THDu.:10426:0:99999:7:::
veritech:!jHg1DqoCj1pIy:10426:0:99999:7:::
```

`!` 字符不属于加密密码文件所使用的字符集，因此这使账户处于禁用状态。要移除 `!` 并重新启用账户，请使用 `-u` 选项。你可以看到账户已恢复。

```bash
bash$ passwd -u veritech
Password changed.
```

禁用账户的另一种方法是在 `/etc/passwd` 或 `/etc/shadow`（取决于你是否使用影子密码）的密码字段中放入 `*`。这是系统默认用于创建那些不需要登录但用于管理目的账户的方式。因此，对于退役账户，这是一种很好的做法。以下代码展示了该方法的应用。

```bash
bash$ cat /etc/shadow
halt::*:10426:0:99999:7:::
operator::*:10426:0:99999:7:::
root:1f829W79sL5BVug2:10426:0:99999:7:::
shutdown::*:10426:0:99999:7:::
sync::*:10426:0:99999:7:::
bin::*:10426:0:99999:7:::
ftp::*:10426:0:99999:7:::
daemon::*:10426:0:99999:7:::
adm::*:10426:0:99999:7:::
lp::*:10426:0:99999:7:::
mail::*:10426:0:99999:7:::
postmaster::*:10426:0:99999:7:::
news::*:10426:0:99999:7:::
uucp::*:10426:0:99999:7:::
man::*:10426:0:99999:7:::
games::*:10426:0:99999:7:::
nobody::*:10426:0:99999:7:::
veritech:jJHgIJoQcJpIy:10426:0:99999:7:::
```

> 不要使用这两种方法中的任何一种来禁用 `root` 账户！它们可能会给未来带来重大麻烦。想象一下，如果 `root` 无法登录会引发怎样的惊奇和喜悦——例如，无法正常关机、挂载驱动器或进行编辑。如果你将 `root` 的 shell 更改为不可用的 shell（如 `/bin/sh`，这是一个不存在的 shell，除非是拼写错误，本意应为 `/bin/csh`），甚至无法通过 FTP 进入 `root` 账户。

## 删除账户

当你决定不再需要某个用户账户时，`userdel` 命令可以为你删除该账户——前提是你必须小心且正确地使用它。该命令会遍历 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件，并移除用户信息。如果账户不存在，该命令无法工作（这不出所料）；如果账户存在但有任何类型的进程正在运行，它也无法工作（很容易忘记登录本身就是一个进程）。该命令的格式如下：

```bash
# userdel username
```

如果你想要删除目录和文件，请使用 `-r` 选项。我建议你在删除用户主目录之前先对其进行备份。

你也可以手动从文件中移除该条目，尽管 `userdel` 效率更高。

## 用户和组

当你设置好用户账户后，你可以指定某些特性或将它们归类为一组。例如，如果你在家里运行 Slackware 系统，你可以按家庭或朋友将人们分组。你可能有一些信息不希望家人看到，但希望朋友看到。在企业环境中，你可以拥有 `execut`、`infosys`、`market` 和 `accting` 等组。

## 设置用户环境

在定义系统用户时，你还可以定义每个用户可以使用的环境类型。你可以定义他们的 shell、磁盘空间和个人信息。

### SHELL

你的 shell 是你的用户环境。在 UNIX 的早期，可用的 shell 包括 Bourne Shell（第一个 shell）、C shell（来自 Berkeley）和 Korn Shell。如今，我们有相当多的 shell 可供选择，包括 Bourne-Again Shell (`bash`)、增强 C shell (`tcsh`) 以及 Z Shell (`zsh`，Korn Shell 的增强版)。

当前 Slackware 中可用的 shell 包括：

- `/bin/ash`
- `/bin/bash`
- `/bin/csh`
- `/bin/sh`
- `/bin/tcsh`
- `/bin/zsh`
