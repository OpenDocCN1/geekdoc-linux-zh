
warnings from the rest of the Postfix logs, respectively, so look here if you want a quick view of errors or warnings.

- **/etc/init.d/postfix**  
  这是 Postfix 的初始化脚本，并且应该自动设置在系统启动时启动。

## Administering Postfix

你用来管理 Postfix 的主要工具恰好命名为 postfix。它与 apache2ctl 的工作方式非常相似，因为它接受几个不同的命令作为参数，并且也可以用作 init 脚本的替代品来启动和停止服务。例如，要停止 Postfix 然后重新启动它，你需要输入

```
$ sudo postfix stop
$ sudo postfix start
```

其他命令通常以相同的方式工作。以下是你可以传递给 Postfix 的主要命令及其功能：

- **reload**  
  每当你对 Postfix 配置进行更改并希望加载它时，使用此命令。此操作与 apache2ctl graceful 函数非常相似，因为它允许每个进程在可以时终止并重新加载，因此它比停止然后启动 Postfix 更安全，并且提供更平滑的过程。

- **flush**  
  此命令告诉 Postfix 刷新其邮件队列。通常 Postfix 会分散其邮件投递以免占用网络，当消息因某种原因被延迟时，它会在队列中延迟一段时间，然后 Postfix 才会尝试重新投递。有时你会遇到一些问题，例如网络中断，导致大量电子邮件在服务器上积压，一旦问题得到解决，你希望将其投递。当你使用 flush 命令时，Postfix 会立即强制投递所有延迟的消息。一般来说，你应该让 Postfix 按照自己的计划积压和投递消息，因此只有在你确实需要时才使用此命令。

- **status**  
  返回当前的 Postfix 状态。如果 Postfix 正在运行，此命令还会返回 master 进程的 PID。

- **abort**  
  这是 stop 命令的更强制版本，并且会立即杀死所有正在运行的 Postfix 进程，无论它们是否已完成。

- **check**  
  此命令与 apache2ctl check 非常相似。它扫描 Postfix 目录结构以查找不好的文件或目录权限，并警告你它发现的任何问题并纠正它们。

除了 Postfix 命令行工具之外，Postfix 还提供一些其他工具来帮助管理服务。postfix 命令可以被普通用户使用来获取有关当前邮件队列的信息。这很有用，这样你就可以跟踪延迟的消息并回答“我在两小时前发送了这封电子邮件，收件人说他们没有收到。发生了什么？”之类的问题。例如，要获取当前队列中所有消息的完整列表，输入

```
$ postqueue -p
```

有时你希望对队列中的消息采取除简单刷新之外的操作。有时你可能想要删除队列中的某条消息（甚至可能是所有消息）。postsuper 命令允许超级用户对队列执行特权操作。例如，要删除队列 ID 为 522 的消息，你需要输入

```
$ sudo postsuper -d 522
```

如果你确实想要删除队列中的所有消息，可以使用大写的单词 ALL 代替特定的队列 ID。你可能还想将一条消息挂起，以便 Postfix 将其保留在队列中但不尝试投递它。使用 -h 选项后跟队列 ID 将消息挂起，然后使用 -H 选项和相同的队列 ID 将消息放回队列。

之前我讨论了 /etc/alias 文件以及它如何用于将一个用户名映射到另一个用户名以进行邮件投递。/etc/alias 文件实际上只是供人类编辑的。Postfix 并不会直接读取它。相反，它会从该文件创建一个数据库，以便可以更快地引用它。每当你编辑该文件时，输入 sudo newaliases 以更新 /etc/alias.db 文件。此外，对于一些更高级的 Postfix 配置，例如规范映射、虚拟账户或其他功能，你将在 /etc/postfix 中有一个单独的文件也需要数据库。你可以在 main.cf 文件中通过其路径前面带有 hash: 来识别这些文件。如果你确实创建或编辑了其中一个查找表，运行 sudo postmap /path/to/file。如果我在 /etc/postfix/virtual 中设置虚拟用户，我会使用以下命令更新数据库

```
$ sudo postmap /etc/postfix/virtual
```

最后，有时当你调整 main.cf 文件时，你想查看 Postfix 运行实例上的当前活动设置。postconf 命令会将每个（我的意思是每个）Postfix 设置及其值输出到屏幕上。因此，如果我想查看运行配置中 myhostname 的当前值，我可以输入

```
$ sudo postconf | grep ^myhostname
myhostname = mail1.example.net
```

## Default Postfix Example

Postfix 安装脚本的优点之一是，一旦你完成它，你应该拥有一个功能性的邮件服务器。当然，这取决于你计划如何使用服务器，可能仍需要进行更多配置。虽然你可以用 Postfix 进行几乎无限的调整和微调，但有许多常见的配置选项你会想要查看。我介绍了一些主要选项，然后提供几种不同的邮件服务器配置示例。

对于所有这些示例，我从 Postfix 安装脚本设置的 Internet 站点的基本 main.cf 文件开始。此配置接受来自

