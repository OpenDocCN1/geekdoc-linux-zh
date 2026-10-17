
你需要在 `/root/` 目录下创建一个 `.amandosts` 文件。该文件应包含任何连接到此客户端的备份服务器的全限定主机名和域名。例如，要在系统 `dexter.glaci.com` 上创建一个名为 `.amandosts` 文件以允许备份服务器 `rabtert.glaci.com` 连接：

```bash
# echo rabtert.glaci.com > /root/.amandosts
# chmod 600 /root/.amandosts
```

我使用 `chmod` 来更改该文件的访问权限。这确保了只有 root 可以读取或修改此账户。

# 执行 Amanda 备份

现在一切都配置好了，你准备好执行 Amanda 备份了。以 root 身份登录时，输入以下命令：

```bash
# /usr/sbin/amamdump normal
```

这将运行 `amdump` 命令并告诉它读取在 `/etc/amanda/normal` 目录下找到的配置文件。它会按照 `disklist` 文件中的系统和分区列表向下执行，按出现的顺序备份每个分区。`amdump` 的结果将写入 `/usr/adm/amanda/normal` 目录。

读取你在该处找到的文件以检查备份结果。（请参考上一节关于如何创建 `disklist` 文件的内容以了解 `amdump` 经历的过程。）

当然，你可以使用 `cron` 自动化此过程。要创建一个与之前节中讨论的常规备份计划类似的 amdump 计划，请执行以下操作：以 root 身份登录时，使用 `-e` 选项输入 `crontab` 命令：

```bash
# crontab -e
```

将在编辑器中打开 root 的 crontab。在文件末尾添加以下行：

| 02 * * 0 /usr/sbin/amdump normal |
| 02 * * 1 /usr/sbin/amdump incremental |
| 02 * * 2 /usr/sbin/amdump incremental |
| 02 * * 3 /usr/sbin/amdump incremental |
| 02 * * 4 /usr/sbin/amdump incremental |
| 02 * * 5 /usr/sbin/amdump incremental |

保存并退出文件。`cron` 守护进程现在会在每周的每天晚上 10:00（军用时间 22:00）运行 `amdump`。此示例显示已创建了第二个增量配置。你可以通过在 `/etc/amanda` 下创建一个名为 `incremental` 的子目录，并在其中填充经过适当修改的 `amanda.conf` 和 `disklist` 文件来实现。你还需要在 `/usr/adm/amanda` 下创建一个名为 `incremental` 的子目录，以便 Amanda 有地方写入此配置的日志文件。

准备好所有工作可能需要花费一些精力，但一旦完成，Amanda 就能让你的网络备份变得易于管理。这可能需要一些额外的工作。

# 使用 pax 进行归档

多年来，出现了许多归档文件的工具，但它们在不同系统之间是不兼容的。幸运的是：`pax`

`pax` 是一个 POSIX 标准程序，可以读取和写入各种格式。如果需要提取归档，使用 `-f` 选项指定名称。

```bash
# pax -f archive
```
