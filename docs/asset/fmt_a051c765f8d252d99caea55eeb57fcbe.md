
`SHELL=/bin/bash`

`PATH=/sbin:/bin:/usr/sbin:/usr/bin`

`MAILTO=root`

```
```

# run parts

`01 * * * * run parts /etc/cron.hourly`

`02 1 * * * run parts /etc/cron.daily`

`02 2 * * 0 run parts /etc/cron.weekly`

`02 3 1 * * run parts /etc/cron.monthly`

```
```

要创建、编辑、列出或删除用户 crontab，只需运行带有适当选项的 `crontab` 命令。登录的用户决定了访问哪个用户的 crontab。特权用户（通常是 root）可以使用 `-u` 选项编辑其他用户的 crontab。表 9-2 列出了用户 crontab 的编辑选项。

## 表 9-2 用户 crontab 编辑选项

| 选项 | 说明 |
|---|---|
| `crontab -e` | 编辑你的 crontab（使用你的默认编辑器） |
| `crontab -l` | 列出你的 crontab 条目 |
| `crontab -r` | （删除）你的 crontab |
| `crontab -u` | 编辑、列出或移除另一个用户的 crontab |
| `username` | |

## 第 9 章：系统管理简介 301

`crontab` 工具使用 `vi` 编辑器（你可以通过设置 `VISUAL` 或 `EDITOR` 环境变量来指定另一个编辑器）来编辑 crontab 文件（基本 vi 命令请参见第 1 章中的说明）。例如，要编辑你的 crontab——第一次执行时会创建它——请输入以下命令：

```
/usr/bin/crontab -e
```

> 执行此命令后你将立即进入命令模式，你必须输入 `i`、`a` 或 `o` 命令开始编辑。完成编辑后，你需要按 Escape 键并输入字符序列 `:wq` 来保存并退出编辑器。

若要给自己发送消息“Hello from Cron”，只需添加以下行：

```
* * * * echo "Hello from Cron"
```

该消息将每每分钟通过邮件发送一次。要检查 crontab 文件，输入命令 `crontab -l`，你将看到如列表 10-5 所示的 crontab 列表。

```
# 不要编辑此文件 - 请编辑主文件并重新安装。

# (/tmp/crontab.1018 安装于 1997年7月19日 周六 14:36:03)
```

```
# (Cron version) -Id: crontab.c.v 2.13 1994/01/17 03:20:37 vixie $)

* * * * echo "Hello from Cron"
```

我怀疑你并不想每分钟收到这样一条微不足道的消息。要删除该示例 cron 条目，输入以下命令：

```
crontab -r
```
