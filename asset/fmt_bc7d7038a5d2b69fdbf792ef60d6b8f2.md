
## crontab 条目

一个 crontab 条目有六个字段：前五个字段用于指定操作的时间，最后一个字段是操作本身。第一个字段指定分钟（0–59），第二个字段指定小时（0–23），第三个字段指定每月的几（1–31），第四个字段指定年的月份（1–12，或像 `Jan` 和 `Sep` 这样的前缀），第五个字段指定星期几（0–6，或像 `Wed` 和 `Fri` 这样的前缀），其中 0 代表星期日。在每个字段中，你可以指定一个范围、一组值，或使用星号 `*` 表示所有值。例如，星期字段中的 `1–5` 表示周一到周五。在小时字段中，`8`、`12` 和 `17` 分别指定上午 8 点、正午和下午 5 点。月份字段中的 `*` 表示每个月。crontab 字段的格式如下：

```
minute day-month month day(s)-week task
```

以下示例在每个工作日的凌晨 2:00 备份 `projects` 目录：

```
0 2 * * 1-5 tar cf /home/backup /home/projects
```

此处再次使用月份和星期几的前缀列出了相同的条条目：

```
0 2 * * Mon-Fri tar cf /home/backup /home/projects
```

要指定特定的月份、日期、星期或小时，你可以单独列出它们，并用逗号隔开。例如，要在周日、周三和周五执行之前的任务，你可以在星期字段中使用 `0,3,5`，或者它们的等效前缀 `Sun, Wed, Fri`。

```
0 2 * * 0,3,5 tar cf /home/backup /home/projects
```

Cron 还支持注释。注释是以 `#` 符号开头的任何行。

```
# Weekly backup for Chris's projects
0 2 * * Mon-Fri tar cf /home/backup /home/projects
```

## cron 环境变量

cron 服务还允许你为执行的任务定义环境变量。Red Hat 定义了 `SHELL`、`PATH`、`HOME` 和 `MAILTO` 变量。`SHELL` 指定执行任务时使用的 shell，在本例中为 bash shell。`PATH` 列出了可以找到程序和脚本的目录。此示例列出了用于该月的标准目录 `/usr/bin` 和 `/bin`，作为为系统应用程序保留的系统目录 `/usr/bin` 和 `/bin`。`MAILTO` 指定接收任务结果邮件的用户。默认情况下，这些结果会发送给调度任务的用户，但你可以将结果发送给特定用户，例如管理员的电子邮件地址，或网络上另一个系统的帐户。`HOME` 是任务的家目录，在本例中是根目录。

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=
```

## cron.d 目录

在频繁使用的系统中，`/etc/crontab` 文件很容易变得拥挤。可能还有某些条目需要不同的变量。例如，你可能需要在不同的 shell 下运行某些任务。为了帮助组织 crontab 任务，你可以将相同的 crontab 条目放在 `cron.d` 目录。`cron.d` 目录中的文件均包含与 `/etc/crontab` 格式相同的 crontab 条目。

## crontab 命令

你使用 `crontab` 命令来安装你的条目。要这样做，创建一个任意名称的文件，例如 `mycron`。然后，输入 `crontab mycron` 安装这些内容。在下面的示例中，root 用户安装文本文件的内容。普通用户可以通过 `/etc/allow` 文件控制 crontab。如果这两个文件都不存在，则拒绝所有用户访问。如果 `/etc/allow` 文件不存在，而 `/etc/deny` 文件存在，则未列在 `/etc/deny` 中的用户被允许访问。

## 编辑 cron

永远不要直接编辑你的 crontab 文件。相反，使用带有 `-e` 选项的 `crontab` 命令。这会在标准编辑器中打开你的 crontab 文件，Vi 使用 `EDITOR` 环境变量指定的默认编辑器。要为 crontab 使用不同的编辑器，通过将编辑器名称赋值给 `EDITOR` 变量并导出。通常，该变量在 `/etc/profile` 脚本中设置。运行带有 `-r` 选项的 `crontab` 会删除整个文件。调用另一个包含 crontab 条目的文本文件会覆盖你当前的 crontab 文件，用文本文件的内容替换它。

## 组织调度任务

你可以将管理任务组织为两大类：可以定期运行的常见管理任务，以及需要在特定时间运行的特殊任务。特殊任务可以作为 `/etc/cron.daily` 文件的条目，如下一节所示。从 `/etc/cron.daily` 文件运行的常见管理任务最好组织到专门的 cron 目录中。在这些目录中，每个任务都放在自己的 shell 脚本中，该脚本将调用 cron 任务。例如，可能有多个管理任务都需要每周在同一天执行，如果系统维护安排在周日的晨。对于这类任务，cron 提供了几个用于自动每日、每月和每年任务的专门目录。每个目录都包含时间间隔的前缀和后缀。`/etc/cron.daily` 目录用于每天执行的任务，而每周任务可以放在 `/etc/cron.weekly` 目录。cron 目录如表 27-2 所示。

### 第六部分：系统管理

| cron 文件和目录 | 说明 |
| :--- | :--- |
| `/etc/crontab` | 系统 *crontab* 文件，仅限 root 用户访问 |
| `/etc/cron.d` | 包含多个 *crontab* 文件的目录，仅限 root 用户访问 |
| `/etc/cron.hourly` | 每小时执行一次任务的目录 |
| `/etc/cron.daily` | 每天执行一次任务的目录 |
| `/etc/cron.weekly` | 每周执行一次任务的目录 |
| `/etc/cron.monthly` | 每月执行一次任务的目录 |
| `/etc/cron.yearly` | 每年执行一次任务的目录 |
| `/etc/cron.hourly` | 每小时执行一次任务的目录 |
| `/etc/cron.allow` | 允许提交 *cron* 任务的用户 |
| `/etc/cron.deny` | 禁止访问 *cron*的用户 |

表 27-2 cron 文件和目录

## 运行 cron 目录脚本

每个目录包含同时运行的脚本。每个组的调度由 `/etc/crontab` 文件中的条目决定。脚本的实际执行由 `/usr/bin/run-parts` 脚本执行，它会运行给定目录中的所有脚本和程序。给定目录下所有任务的调度由 `/etc/crontab` 文件中的条目处理。Red Hat 提供了指定时间的条目，你可以根据需要进行修改。这里显示了默认的 Red Hat *cron* 文件，其中包含了在不同 *cron* 目录中运行脚本的时间。在这里你可以看到，大多数脚本在凌晨 4 点运行，可能是每天（4:02）、周日（4:22）或每月的第一天（4:42）。每小时运行的任务在每整点后一分钟运行。

```
SHELL=/bin/bash
PATH=/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME/
# run-parts
01 * * * root run-parts /etc/cron.hourly
02 4 * * root run-parts /etc/cron.daily
22 4 * * root run-parts /etc/cron.weekly
42 1 * * root run-parts /etc/cron.monthly
```

> 提示 *cron* 目录内的脚本按字母顺序运行。如果你需要某个脚本在其他任何脚本之前运行，你可能需要修改它的名称。一种方法是在名称前加上数字。例如，在 *cron.weekly* 目录中，*anacron* 脚本被命名为 *0anacron*，这样它就会在其他脚本之前运行。

## 第 27 章：基础系统管理 499

请记住，这些是包含可执行文件的目录。实际调度是由 `/etc/crontab` 文件中的条目执行的。例如，如果 `cron.weekly` crontab 条目中的每周字段改为 `*` 而不是 `0`，并将每月字段改为 `1`（使用 `22 4 * * *` 代替 `22 4 * * 0`），那么 `cron.weekly` 文件中的任务最终将每天（每天）运行，而不是每周运行。

## cron 目录名称

这些目录使用的名称仅仅是约定。它们对于 cron 守护进程没有特殊意义。事实上，你可以创建自己的目录，将脚本放入其中，并调度 `run-parts` 在任何时间运行这些脚本。在示例中，存放在 `/etc/cron.mydocs` 目录中的脚本将在每个周三的中午 12 点运行。

```
* * 3 root run-parts /etc/cron.mydocs
```

## Anacron
