
- 环境变量：标准操作所需的 shell 环境变量。包括 `USER`、`LOGNAME`、`MAIL`、`HOSTNAME` 和 `HISTSIZE`。

- `INPUTRC`：根据输入文件设置键盘映射。

`/etc/profile` 文件最后查看的是 `/etc/profile.d` 目录并引入其中找到的文件。每个文件都包含用户的设置。例如，`lang.sh` 和 `lang.csh` 文件识别外语言的位置。`vim` 文件创建了别名，使得在使用 `vi` 时会使用 `vim`。

## 创建便携桌面

Linux 是一个诞生于互联网的操作系统，因此它拥有强大的网络能力并不意外。这使得 Linux 成为优秀的服务器，但也让 Linux 成为优秀的桌面工作站，特别是在高度网络环境中。Fedora 和 RHEL 允许你轻松为用户设置随他们移动的便携桌面。在其他领先操作系统上并不容易。

通常，Linux 用户的家目录位于 `/home` 目录下。作为替代方案，你可以在 `/home` 目录下创建一个以系统主机命名的目录。在该目录内创建用户的家目录。因此，在名为 `dexter` 的 Linux 系统上，用户 `mary` 的家目录将是 `/home/dexter/mary` 而不是 `/home/mary`。这样做有一个很好的理由。

如果你登录到 Linux 系统 `rattert` 并希望像访问本地存储一样访问 `dexter` 上的家目录，最好的方法是使用网络文件系统 `NFS` 将 `dexter` 的 `/home` 挂载到 `rattert` 的 `/home` 上。这使得无论你登录到哪台机器，都可以获得相同的家目录内容。

要如描述所示挂载 `dexter` 的 `/home` 目录，你需要在 `rattert` 的 `/etc/fstab` 文件中添加类似下行的内容：

```
dexter:/home /nfs defaults 0 0
```

你还可以在 `dexter` 的 `/etc/exports` 目录中添加如下的条目：

```
/home rattert
```

# 第 11 章：设置与支持用户 459

现在，当 `ratbert` 启动时，它会自动通过网络挂载 `dexterter` 的家目录。这使得你能够处理 `dexterter` 的 `/home` 上的远程文件和目录，就像它们存储在 `ratbert` 本地一样。遗憾的是，这产生了一个副作用，即“覆盖”了 `ratbert` 真实的 `/home` 目录。

这时基于系统名的额外目录层级派上用场了。由于 `dexterter` 的所有家目录都位于 `/home/dexter`，而 `ratbert` 的所有家目录都位于 `/home/ratbert`，我们可以消除了覆盖另一个用户家目录的危险。事实上，让我们把这个例子再推进一步：假设有这样一个场景，在该场景中，`dexter`、`ratbert` 和 `daffy` 系统都拥有可以与其他系统共享的桌面。如指示所示，每个系统的 `/etc/fstab` 和 `/etc/exports` 文件都应该添加以下行。

`dexter` 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

```
/etc/exports file
/home/dexter ratbert, daffy
/etc/fstab file
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

`ratbert` 的 `/etc/exports` 和 `/etc/fstab` 文件为：

```
/etc/exports
/home/ratbert dexter, daffy
/etc/fstab
dexter:/home/dexter /home/dexter nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

`daffy` 的 `/etc/exports` 和 `/etc/fstab` 文件为：

```
/etc/exports
/home/daffy ratbert, dexter
/etc/fstab
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
dexter:/home/dexter /home/dexter nfs defaults 0 0
```

如你所示，每个系统都使用 `NFS` 挂载另外两个系统的家目录。用户可以在不同的服务器之间穿梭，并在每个系统上看到完全相同的桌面。

## 为用户提供支持

创建新用户账户只是众多管理任务中的微小之一。没有哪一个章节能够充分讨论持续支持用户所涉及的所有任务。但我与你分享一些提示和步骤，以减轻这种负担。

### 创建技术支持邮箱

电子邮件是一项极佳的通信工具，特别是对于工作过度的系统管理员而言。人们通常在电子邮件上花费的精力和努力比他们留下的语音消息多。文本消息在发送前可以进行编辑以确保清晰，而且重要的细节可以从其他源复制粘贴。这使得电子邮件成为 Linux 用户与系统管理员通信的绝佳方法。

在只有少数用户的办公室里，你可能可以使用个人邮箱来收发邮件。然而，在较大的办公室中，你应该创建一个专门留给技术支持问题的独立邮箱。与使用个人邮箱相比，这有以下几个优势：

- 支持消息不会与个人的、与支持无关的消息相混淆。
- 多个个人可以检查邮箱并共享管理责任，而无需阅读彼此的个人邮件。
- 当你休假时，支持邮件可以轻松重定向到另一个人的邮箱。你的个人邮件将继续发送到你的个人邮箱。

一个简单的解决方案是直接创建一个支持邮件别名，将消息重定向到实际的邮箱或邮箱列表。例如，假设你想创建一个支持别名，将电子邮件重新分发给员工 `Joe`、`Mary` 和 `Bob` 的用户账户。你将以 `root` 身份登录，编辑 `/etc/aliases` 文件，并添加类似下面的行：

```
# Technical support mailing list
support: joe, mary, bob
```

保存文件后，你需要运行 `newaliases` 命令将 `/etc/aliases` 文件重新编译为数据库格式。你的用户可以向支持邮箱地址发送邮件，消息将自动路由到列表中的每个人。当列表成员回复该消息时，他或她应该使用“回复所有人”`Reply To All` 选项，以便其他员工也能看到消息。否则，多人可能会尝试解决同一个问题，导致劳动的重复浪费。

你也可以选择创建一个支持用户账户。技术支持人员将登录此账户来检查消息并发送回复。通过这种方式，所有回复都将带有支持登录名称，而不是员工的个人电子邮件地址。

### 重置用户密码

用户会遇到的常见（如果不是最）问题是无法登录，因为：

- 他们的大写锁定 `Caps Lock` 开启了。
- 他们忘记了密码。
- 密码已过期。

如果大写锁定未开启，那么你可能需要重置用户的密码。你无法查找到密码，因为 Linux 以加密格式存储密码。相反，请使用 `passwd` 命令为用户账户分配新密码。给用户新密码（最好是明文的），然后将密码设置为过期，以便他或她必须自己选择一个（希望是容易记住的）。

如果你必须重置用户的密码，请使用 `passwd` 命令进行。在以 `root` 身份登录时，输入 `passwd` 后跟用户名。例如：

```
passwd mary
```

设置密码后，系统将提示你输入两次。如果你想强制用户在下次登录时更改密码，请使用选项：

```bash
passwd -e mary
```

### 修改账户

有时，用户需要的不仅仅是更改密码。`usermod` 命令与 `useradd` 命令类似，并共享一些选项。然而，它不是添加新账户，而是修改现有账户的各种细节。调用 `usermod` 命令时，你必须提供要修改的用户名。表 11-3 列出了 `usermod` 的可用选项。

#### 表 11-3：修改账户的 usermod 选项

| 选项 | 描述 |
|---|---|
| `-c "comment"` | 修改账户的描述字段。你也可以使用 `chfn` 命令执行此操作。将 `comment` 替换为名称或其他描述。由于 `comment` 可以包含多个单词，因此引号是必要的。 |
| `-d home_dir` | 将家目录更改为指定的位置。如果包含了 `-m` ，将复制家目录的内容。将 `home_dir` 替换为新目录的完整路径。 |
| `-e expire_date` | 为账户分配一个新的过期日期，用 `MM/DD/YYYY` 格式替换 `expire_date`。 |
| `-f inactivity` | 设置密码过期后账户永久禁的天数。将 `inactivity` 设置为 `0` 则过期后立即禁用。设置为 `-1` 则禁用该选项，这是默认行为。 |
| `-g group` | 修改用户所属的主组（如 `/group` 文件所示）。将 `group` 替换为新组名。 |
| `-G grouplist` | 设置用户所属的组列表。将 `grouplist` 替换为组列表。 |
| `-l login_name` | 将账户的登录名更改为 `-l` 选项后的名称。将 `login_name` 替换为新名称。这不会自动更改家目录名称；请使用 `-d` 和 `-m` 选项。 |
| `-m` | 此选项仅与 `-u` 选项配合使用。它导致用户家目录的内容复制到新目录。 |
