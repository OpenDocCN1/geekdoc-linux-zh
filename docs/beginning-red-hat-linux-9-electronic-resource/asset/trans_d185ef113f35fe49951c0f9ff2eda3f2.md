
## 修改自己的用户账户

  创建用户账户后，其所有者可以对其进行一定程度的控制。不出所料，红帽 Linux 提供了图形界面和命令行工具，账户所有者可以更改密码、账户描述和 shell 等内容。

### 修改自己的密码

  如下面的两个示例所示，无论使用图形界面还是命令行流程，更改密码的基本步骤都是相同的。

  要通过图形界面更改密码，请选择 **主菜单 | 首选项 | 密码**，或在终端窗口中输入 `userpasswd`。将出现以下对话框。出于安全原因，您必须先输入旧密码：

![](img/b852150740856958b10aff9e8c9d2adc_315_0.png)

  然后系统会提示您两次输入新密码：

![](img/b852150740856958b10aff9e8c9d2adc_315_1.png)

  如果您两次输入相同的密码，且该密码不是太短或基于字典单词，则新密码将被接受。请记住，定期更改密码是个好主意，特别是当您的计算机与他人共享时，即使系统不强制执行密码过期也是如此。

  要通过命令行更改密码，您可以使用我们之前见过的 `passwd` 命令。首先，系统会要求您输入当前密码 – 再次强调，这是为了确保您有权更改它：

```
$ passwd
Changing password for user eziodm.
Changing password for eziodm
(current) UNIX password: (password not shown)
```

  然后系统会要求您输入新密码。我们可以借此机会了解哪些类型的密码是可以接受的。试着将 `ape5` 输入为您的新密码：

```
New password: (password not shown)
BAD PASSWORD: it is too short
```

  由于 `ape5` 太短，请尝试使用 `elephant6`：

```
New password: (password not shown)
BAD PASSWORD: it is based on a dictionary word
```

  `passwd` 命令也不接受基于字典的密码；它有一个内置机制，防止您选择容易猜到的密码。尝试使用更复杂的密码，例如 `e!eph4nt`：

```
New password: (password not shown)
Retype new password: (password not shown)
passwd: all authentication tokens updated successfully.
```

  如您所见，命令行流程中的步骤与基于 GUI 的流程中的步骤相同。

  最后，请记住，如果普通用户（如 eziodm）忘记了密码，root 可以运行以下命令将其重置为已知值：

```
# passwd eziodm
```

## 修改自己的账户描述和 Shell

  红帽 Linux 还提供了允许用户控制其账户其他方面的 GUI 和 CLI 实用程序。您可以通过选择 **主菜单 | 首选项 | 关于我** 或在命令行中输入 `userinfo` 来启动 GUI 实用程序。这将弹出用户信息对话框：

![](img/b852150740856958b10aff9e8c9d2adc_317_0.png)

  使用此对话框，您可以编辑系统的姓名记录，并按需添加联系信息。所有这些然后都以逗号分隔的格式存储在 `/etc/passwd` 记录的 *description* 字段中，如下所示：

```
eziodm:x:500:500:Pancrazio 'Ezio' de Mauro,,212 555-4343,,:/home/eziodm:/bin/bash
```

  您还可以使用此对话框来更改登录 shell。请注意，无法选择不在列表中的 shell。完成后，只需点击 **应用** 进行确认（如果您想放弃更改，请点击 **关闭**）。如果您修改并确认任何内容，工具会要求您输入密码以验证您的身份。

### 通过命令行修改账户描述

  从命令行，您可以使用 `chfn` 更改个人信息，使用 `chsh` 更改 shell。下面是一个示例，其中用户 *eziodm* 使用 `chfn` 更改个人信息：

```
$ chfn
Changing finger information for eziodm.
Password: (password not shown)
Name [Pancrazio 'Ezio' de Mauro]: Pancrazio de Mauro
Office []:
Office Phone [212 555-4343]: +44 20 1234 5678
Home Phone []: +39 02 1234 5678
Finger information changed.
```

  通过此操作获得的结果与使用我们刚才看到的 **用户信息** 对话框获得的结果非常相似。您会发现，该用户首先必须输入密码（以识别其身份），然后更改账户的 **姓名** 以及 **办公室** 和 **家庭电话** 号码。

  要更改登录 shell，您可以使用 `chsh` 命令 – 其工作方式非常相似：

```
$ chsh
Changing shell for eziodm.
Password: (password not shown)
New shell [/bin/bash]: /bin/tcsh
Shell changed.
```

  如果您想返回到之前的 shell，只需再次运行 `chsh` 并指定原来的那个：

```
$ chsh
Changing shell for eziodm.
Password: (password not shown)
New shell [/bin/tcsh]: /bin/bash
Shell changed.
```

  您可以通过在终端中使用 `man chfn` 和 `man chsh` 查阅它们的手册来了解有关 `chfn` 和 `chsh` 的更多信息。

## 使用 root 账户修改其他用户账户

  当我们需要采用 root 账户并对另一个账户应用更改时，最佳工具取决于我们需要进行的更改。某些较*常见*的操作（如账户或密码过期）很容易执行，使用 **红帽用户管理器**（我们选择账户然后按 **属性** 按钮）。

  然而，如果我们需要对账户进行更重大的更改（如更改 UID），**红帽用户管理器** 是不够的。实际上，我们甚至不能使用基于 CLI 的命令，如 `passwd`、`chfn` 和 `chsh` 实用程序来更改账户的 UID。

  如果您绝对*必须*更改账户的主目录、UID、GID 或甚至登录名，以下是如何在命令行上使用 `usermod` 来执行此操作。请记住，您必须以 root 身份登录才能执行此操作！假设我们在 `/etc/passwd` 中有以下用户：

```
eziodm:x:500:500:Pancrazio 'Ezio' de Mauro::/home/eziodm:/bin/bash
```

  如果我们要将账户从 `eziodm` 重命名为 `eziod`，我们可以这样运行 `usermod`：

```
# usermod -l eziod eziodm
```

  我们使用了 `-l` 选项来指示我们要更改登录名，并在现有登录名之前指定*新*登录名。结果，该用户在 `/etc/passwd` 中的记录更改为：

```
eziod:x:500:500:Pancrazio 'Ezio' de Mauro:/home/eziodm:/bin/bash
```

# 第 8 章

  如您所见，该账户保留了其 UID、描述、主目录等。如果您想更改用户主目录的位置，可以在之前的命令之后运行此命令：

```
# usermod -d /home/eziod -m eziod
```

  以下是如何解读此命令：

-   `-d /home/eziod` 选项指定新的主目录。
-   `-m` 选项指示 `usermod` 将旧目录的*内容*移动到新的目录。移动后，旧主目录将不再可见。
-   命令末尾指定的用户名（eziod）是 `usermod` 必须操作的账户。

  您可以通过 `usermod` 使用 `-u` 和 `-g` 选项分别更改账户的 UID 和 GID。但是，如果用户在主目录之外有文件，此操作可能会产生不良的副作用。特别是，该命令不会相应地更新这些文件的*所有权* – 它们必须手动更改（可能需要其他实用程序的帮助，如 `find`）。`usermod` 的手册页（在终端中运行 `man usermod`）对此以及其他关键点发出了警告。

  *要获取所有者或组在 /etc/passwd 或 /etc/group 中不存在的文件列表，您可以作为 root 使用以下命令：*

```
# find / -nouser -o -nogroup
```

  *`find` 命令是一个非常强大且有用的命令。您可以在终端中使用 `man find` 检查其他选项。第 2 章和第 7 章中对此有更多内容。*

## 删除用户账户

  删除用户账户非常容易。在 Red Hat 用户管理器的图形界面中，您可以通过在 Users 选项卡中选择用户，然后单击 Delete 按钮来删除用户。

  *在使用 Red Hat 用户管理器删除账户时要非常小心：将不会有确认！但是，用户的主目录不会被销毁。因此，在意外删除的情况下，可以恢复文件并创建具有与刚删除的账户相同属性的账户。*

  从 root 命令行，您可以运行 `userdel`。像这样使用命令将从 `/etc/passwd` 中擦除名为 *test* 的账户，但相关的主目录不会被删除：

```
# userdel markm
```

