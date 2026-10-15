
通常，Linux 用户的家目录位于 `/home` 目录下。作为替代，你可以在系统名称之后创建一个新的家目录。使用该目录创建用户的家目录。因此，在名为 `dexter` 的 Linux 系统上，用户 `mary` 的家目录将是 `/home/dexter/mary` 而不是 `/home/mary`。这样做有非常充分的理由。

如果你登录在 Linux 系统 `ratbert` 上，并且可以像访问本地存储一样访问 `dexter` 上的家目录，那么最好的方法是使用网络文件系统 `NFS` 将 `dexter` 的家目录挂载到 `/home/ratbert`。这样，无论你登录到哪台机器，你的家目录内容都是可用的。

> 交叉引用：你可以在第 18 章阅读更多关于 NFS 的知识。

要按照描述的方法挂载 `dexter` 的 `/home` 目录，你需要在 `ratbert` 的 `/etc/fstab` 文件添加类似下面的一行：

```
dexter:/home nfs defaults 0 0
```

你还会在 `dexter` 的 `/etc/exports` 目录下添加类似如下的条目：

```
/home  ratbert
```

现在，当 `ratbert` 启动时，它会自动通过网络挂载 `dexter` 的家分区。这让你能够像读取本地存储在 `ratbert` 上的文件一样读取 `dexter` `/home` 上的远程文件和目录。遗憾的是，这有一个副作用，会“遮盖” `ratbert` 真实的 `/home` 目录。

这时，基于系统的额外目录层级就大显身场了。由于 `dexter` 的所有家目录都位于 `/home/dexter`，而 `ratbert` 的所有家目录都位于 `/home/ratbert`，你可以消除一个系统覆盖另一个系统家目录的危险。事实上，让我们来看这个示例：`dexter`、`ratbert` 和 `daffly` 系统拥有与其他系统共享的便携桌面。每个系统的 `/etc/fstab` 和 `/etc/exports` 文件都应该按照指示添加以下行内容。

`dexter` 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

```
/etc/exports file
/home/dexter ratbert, daffy
```

```
/etc/fstab file
ratbert:home/ratbert /home/ratbert nfs defaults 0 0
daffy:home/daffy /home/daffy nfs defaults 0 0
```

`ratbert` 的 `/etc/exports` 和 `/etc/fstab` 文件为：

```
/etc/exports
/home/ratbert dexter, daffy
```

```
/etc/fstab
dexter:home/dexter /home/dexter nfs defaults 0 0
daffy:home/daffy /home/daffy nfs defaults 0 0
```

`daffy` 的 `/etc/exports` 和 `/etc/fstab` 文件为：

```
/etc/exports
/home/daffy ratbert, dexter
```

```
/etc/fstab
ratbert:home/ratbert /home/ratbert nfs defaults 0 0
dexter:home/dexter /home/dexter nfs defaults 0 0
```

如所示，每个系统都使用 `NFS` 挂载来自另外两个系统的家目录。用户可以在不同的服务器之间移动，并在每个系统上看到完全相同的桌面。

## 为用户提供支持

创建新用户账户只是许多管理任务中的很小的一项。没有哪一个章节能够充分讨论持续支持用户所涉及的所有任务。但我会和你分享一些提示和步骤，以减轻这种负担。

### 创建技术支持邮箱

电子邮件是一个极佳的通信工具，特别是对于工作过度的系统管理员来说。人们通常在电子邮件上花费的思考和精力比他们留下的语音消息多。文本消息在发送之前可以进行编辑以确保清晰，并且重要的细节可以从其他源复制粘贴。这使得电子邮件成为 Linux 用户与系统管理员通信的绝佳方法。

在只有少数用户的办公室里，你可能可以使用个人邮箱发送和接收电子邮件。然而，在较大的办公室里，你应该创建一个专门留给技术支持问题的独立邮箱。与使用个人邮箱相比，这有几个优势：

- 支持消息不会与个人的、与支持无关的消息相混淆。
- 多人可以检查邮箱并分担管理责任，而无需联系彼此的个人电子邮件。
- 当你休假时，支持邮件可以轻松重定向到另一个人的邮箱。你的个人电子邮件将继续发送到你的个人邮箱。

一种解决方案是设置密码过期。例如，使用以下命令：

```
# change -d 0
```

保存文件后，将其设置为过期，以便用户在下次登录时必须更改。请记住使用 `change` 命令为密码设置有效期。

```
# change -M 30
```

`-M 30` 选项告诉系统每 30 天让 `Mary` 的密码过期。`-d 0` 欺骗系统认为她的密码自 1970 年 1 月 1 日以来未更改。（请记住，使用 `change` 命令会对使用的任何账户启用密码有效期。）

### 重置用户密码

有时，用户需要的不仅仅是重置密码。用户遇到的一个常见（如果不是最常见的话）问题是无法登录：

- 他们有密码。
- 他们忘记了密码。
- 密码已过期。

如果你重置用户密码，请使用 `passwd` 命令。在以 `root` 身份登录时，输入 `passwd` 以及你要重置的登录名。系统会提示输入两次密码。例如，要更改 `user` 的密码，输入：

```
# passwd
```

## 修改账户

偶尔，用户需要的不仅仅是更改用户所属的组、家目录所在的驱动器，或者由于婚姻状况导致的姓名变更。下文将介绍如何使用两种方法修改用户账户：`usermod` 或用户管理器窗口。

### 使用 usermod 修改用户账户

`usermod` 命令与 `useradd` 命令相似，并共享一些选项。然而，它不是添加新账户，而是允许你更改现有账户的各种细节。调用 `usermod` 命令时，你需要提供要更改的账户详情，以及账户的登录名。表 11-3 列出了 `usermod` 命令的可用选项。

| 选项 | 描述 |
| --- | --- |
| -c "comment" | 修改账户描述字段。非 root 用户可以使用 `chfn` 命令为自己修改此项。将 `comment` 替换为账户名称或描述。因为注释可能包含多个单词，所以引号是必要的。 |

# 第三部分：管理 Fedora 和 RHEL

| 选项 | 描述 |
|---|---|
| -d home_dir | 将账户的主目录更改为指定的位置。如果包含 `-m` 选项，则会将主目录的内容以及带有新目录完整路径的 `home_dir` 复制到那里。 |
| -e expire_date | 为账户分配新的过期日期，将 `expire_date` 替换为 `MM/DD/YYYY` 格式的日期。 |
| -f inactivity | 设置密码过期后到账户被永久禁用的天数。将 `inactivity` 设置为 0 会在密码过期后立即禁用账户。将其设置为 -1 则禁用此选项，这是默认行为。 |
| -g group | 更改用户所属的主组（如 `/etc/group` 文件中列出的组）。将 `group` 替换为组名。 |
| -G grouplist | 设置用户所属的组列表。将 `grouplist` 替换为组列表。 |
| -l login_name | 将账户的名称（登录名）更改为 `-l` 选项后提供的名称。将 `login_name` 替换为新名称。这不会自动更改主目录的名称；请结合使用 `-d` 和 `-m` 选项。 |
| -m | 此选项仅与 `-d` 选项配合使用。它会将用户主目录的内容复制到新目录。 |
| -o | 此选项仅与 `-u` 选项配合使用。它消除了用户 ID 必须唯一的限制。 |
| -s shell | 指定此账户使用的新命令 shell。将 `shell` 替换为新 shell 的完整路径。 |
| -u user_id | 更改账户的用户 ID 号。将 `user_id` 替换为新的用户 ID。如果使用了 `-o` 选项，则该 ID 号不能被其他账户占用。 |

假设有一名为 `Jenny Barnes` 的新员工将接替 `Mary` 的工作。我们要把 `mary` 账户更改为新名称 `-l jenny`、新注释 `-c "Jenny Barnes"` 和主目录 `-d /home/jenny`。你可以通过以下命令实现：

```
# usermod -l jenny -c "Jenny Barnes" -m -d /home/jenny mary
```

此外，如果转换账户后你发现 `Jenny` 更倾向于使用 `tcsh` shell，你可以通过 `-s` 选项进行更改 `-s /bin/tcsh`：

```
# usermod -s /bin/tcsh jenny
```

或者，你也可以使用 `chsh` 命令更改 shell。以下是一个示例：

```bash
$ chsh -s /bin/tcsh jenny
```
