
# DefaultUser

`DefaultUser` 是运行邮件发送器的用户 ID。如果 `Sendmail` 未以特定用户身份运行，它将以 `DefaultUser` 运行。启动时，`Sendmail` 将为名为 `mailnull` 的用户运行 `getpnam()` 命令。如果 `mailnull` 用户在 `/etc/passwd` 有条目，`Sendmail` 将使用 UID 和 GID 作为 `DefaultUser`。如果 `mailnull` 不存在，`Sendmail` 将采用 `User` 守护进程。如果 `/etc/passwd` 中没有定义 `mailnull` 或 `daemon`，`Sendmail` 将使用 UID 1 和 GID 1。如果你的 `/etc/passwd` 文件中不存在 `mailnull` 用户，则应将其创建一个没有密码且 shell 无效的空用户；`mailnull` 用户不应拥有任何文件。

当 `Sendmail` 检测到其意图以 `root` 身份运行时，也会使用 `DefaultUser`。

例如，如果 `root` 的主目录中有一个运行程序的 `.forward` 文件，`Sendmail` 将改为以 `DefaultUser` 身份运行该命令。

## TrustedUser

默认情况下，`root` 是 `Sendmail` 唯一信任的用户。在某些情况下，你可能希望 `Sendmail` 信任另一个用户拥有文件并运行自动化脚本，而不是 `root`。在这种情况下，可以使用 `TrustedUser`，它默认是 `root`。使用 `TrustedUser` 时要小心；由于 `Sendmail` 通常以 `root` 身份运行，对于获得 `TrustedUser` 访问的坚决入侵者来说，获取 `root` 权限并不困难。

## RunAsUser

虽然 `Sendmail` 通常以 `root` 身份运行，但它仅在启动时需要 `root` 权限来绑定 SMTP 套接字。可以强制 `Sendmail` `setuid` 到另一个用户 `RunAsUser`。遗憾的是，`Sendmail` 将强制以 `RunAsUser` 的权限 `own root` 运行。`RunAsUser` 的默认用户也是 `root`。

## 检查文件和目录权限

保护系统免受基于 `Sendmail` 的攻击从文件和目录权限开始。最易受到 `Sendmail` 攻击的关键文件和目录是 `/etc` 目录、邮件队列目录和 `Sendmail` 配置文件 `/etc` 目录应设置为 755 模式，且只有 `root` 有权限在 `/etc` 目录内写入文件。邮件队列目录 `/var/spool/queue` 应设置为 700 模式并由 `RunAsUser` 所有。邮件队列目录路径中的目录（`/var` 和 `/var/spool`）也应通过将其设置为 755 模式来保护，其所有者为 `root`。

由于 `Sendmail` 配置文件是受信任的，因此 `sendmail.cf` 应该受到严格保护。`sendmail.cf` 所在的目录 `/etc/mail` 也应该受到保护。该目录应设置为 755 模式并由 `TrustedUser` 所有，而 `sendmail.cf` 应设置为 644 模式并由 `TrustedUser` 所有。出于安全考虑，`Sendmail` 数据库文件和映射也应该放置在 `/etc/mail`。

## 清理 aliases 文件

`aliases` 文件位于 `/etc`，用于将邮件重定向到用户。邮件也可以被重定向到处理消息的程序；`aliases` 文件的特定功能可能被用来安全漏洞。移除 `aliases` 文件中任何未使用的重定向。到程序的重定向特别危险；请删除它们，或确保程序在执行传递给它的信息之前会验证信息的来源。

只有 `root` 或 `TrustedUser` 应该写入 `aliases` 文件。将文件设置为 755 模式并将所有者更改为 `TrustedUser` 将实现此目标。

## 使用 Sendmail 限制 shell

`Sendmail` 限制 shell（或 `smsh`）控制可以通过电子邮件运行哪些程序。程序被限制位于指定目录中的程序。该 shell 取替了 `sendmail.cf` 中的 `/bin/sh`，通过在 OS 的宏定义中指定 `FEATURE(smsh)` 来激活。`CONFBINDIR` 变量定义了放置信任程序和指向受信任程序链接的目录；可以在为 `Sendmail` 定义操作系统环境时设置此变量。

## 使用 SafeEnvironment 选项

在 `Sendmail` 的配置宏中可以设置 `SAFE_ENV` 的值。这将在写入文件之前将 `chroot` 到指定的目录。这仅适用于用户写入的文件，它们无法覆盖重要文件。例如，如果 `SafeEnvironment=/my` 且写入到 `/my`，它将被限制在在该处。

## 实验练习

这些练习将引导你使用前面的技术增强 `Sendmail` 的安全性。假设你已经知道如何正确配置和构建 `Sendmail`。

### 创建 mailnull 账户

为了充分利用 `DefaultUser`，请在 `/etc/passwd` 中创建 `mailnull` 账户。`mailnull` 应该具有唯一 UID 和 GID、无密码、无效 shell 无主目录的空账户。要创建账户，用编辑器打开 `/etc/passwd` 并添加以下行：

```
mailnull::200:200:DefaultUser::/bin/false
```

现在，保存文件，退出编辑器并重启 `Sendmail`。下次 `Sendmail` 启动时将检测到 `mailnull` 用户存在并在需要 `DefaultUser` 时使用 UID 和 GID。

### EnableTrustedUser

要使用 `TrustedUser`，必须创建一个受信任的用户。然后在 `Sendmail` 配置文件中定义变量 `CONTRUSTED_USER` 为该用户。要创建一个受信任的用户，用编辑器打开 `/etc/passwd`。添加一个具有唯一 UID、GID、主目录和有效 shell 的新复杂用户。新行应类似于：

```
trusteduser::201:201:TrustedUser:/home/trusteduser:/bin/bash
```

保存文件并关闭编辑器后，为新用户运行 `passwd` 命令并提供密码。

接下来，在 `Sendmail` 配置文件中定义变量。执行此操作，找到相应的配置文件并添加以下行：

```
define('CONTRUSTED_USER', 'trusteduser')
```

更改此配置文件将需要重新构建 `Sendmail` 以使更改生效。

### EnableRunAsUser

设置 `RunAsUser` 与设置 `TrustedUser` 。创建一个 `Sendmail` 在启动后 `setuid` 的新用户，并在 `Sendmail` 配置文件中定义变量 `confRUN_AS_USER`。

使用编辑器打开 `/etc/passwd` 并添加一个具有唯一 UID、GID、主目录和有效 shell 的新用户。新行应类似于此所示：

```
runasuser:202:202:RunAsUser:/home/runasuser:/bin/bash
```

保存文件并关闭编辑器。现在使用 `passwd` 命令为新用户设置密码。

最后，将以下行添加到 `Sendmail` 配置文件中：

```
define('CONFRUN_AS_USER', 'runasuser')
```

请记住，更改此配置文件将需要重新编译 `Sendmail`，更改才能生效。

### 确保你的目录结构安全

许多通过 `Sendmail` 的入侵都是由于文件和目录权限松散所致。为了提高 `Sendmail` 的安全性，你应该通过收紧对系统关键文件和目录的限制来提高整体安全性。对于 `Sendmail` 而言，最重要的文件和目录是 `/etc`、`/var/spool/mqueue` 以及 `/etc/mail` 中的 `Sendmail` 配置文件。

使用 `chmod` 命令将 `/etc` 目录设置为模式 755，并使用 `chown` 命令将所有者设置为 `root`。在这种情况下，这防止了目录的其他任何所有者在目录内写入文件。用户和组仍然对目录具有读取和执行权限。

邮件队列目录 `/var/spool/mqueue` 应该有更严格的限制。如果你决定使用该选项，请将目录模式更改为 700，并将所有者更改为为 `RunAsUser` 创建的用户。或者所有权应属于 `root`。对于此目录，只有 `RunAsUser` 将权访问内容。你邮件队列目录的整个路径（包括 `/`、`/var` 和 `/var/spool`）也应该受到保护。将所有这些目录设置为 755，并将它们的所有者设置为 `root`。

位于 `/etc` 的 `sendmail.cf` 应该受到保护，因为 `Sendmail` 会读取并信任它。此外，收紧对 `/etc/mail` 的权限。将 `sendmail.cf` 设置为模式 644，并将所有者设置为为 `TrustedUser` 创建的用户。这将防止所有对配置文件的写入操作。将 `/etc/mail` 设置为模式 755，所有者同样为 `TrustedUser`。

现在与 `Sendmail` 相关的最关键文件和目录都已拥有安全的权限。建议你还要改进入侵者可能用于破坏你系统的其他文件和目录的安全性。

## 清理别名文件
