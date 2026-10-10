
`antivir /var/log -s -allfiles -s -nolnk -r`

你可以通过执行 `antivirus -h` 命令来查看所有命令行选项，这在你忘记如何使用该程序时非常方便。表 3.1 显示了一些与 AntiVir 较相关的参数。

### 表 3.1 AntiVir 选项

| 参数 | 说明 |
| :--- | :--- |
| `-allfiles` | 扫描目录中的所有文件。 |
| `-z` | 扫描归档文件。 |
| `-fs` | 扫描 NFS 挂载的驱动器。 |

### 表 3.1 继续

| 参数 | 说明 |
| :--- | :--- |
| `-del` | 删除感染的文件。 |
| `-r` | 将 AntiVir 放入递归模式。 |
| `-ro` | 覆盖日志文件。 |
| `-ra` | 在日志文件中追加新信息。 |
| `-rf` | 强制删除现有文件（位于 `/usr/lib/AntiVir/` 下）。 |
| `-s` | 递归扫描所有目录。 |

### 图 3.1 命令行

![](img/a7a9caa80ec85507179284d91e216f9f_118.png)

## 密钥模式与非密钥模式

AntiVir 是通过某些公司出售的，具有密钥模式。非密钥模式允许你在无需输入完整路径（例如 `/usr/bin/antivir`）的情况下启动程序。在非密钥模式下，你无法使用所有选项。你可以通过执行以下命令来扫描本地目录：

```
antivir /var/log -s -allfiles -s -nolnk -r
```

## 授权 AntiVir

如果你计划使用密钥模式，请访问 `www.antivir.de/priv/order_e.htm`。最后，你将收到一个名为 `antivir` 的文件。一旦你获得了密钥，将其放入 `/usr/lib/AntiVir/` 目录。一旦你启动 AntiVir，你就可以使用它的选项。

## 练习：更新 AntiVir

假设你已经安装了 AntiVir。但你仍然无法使用 AntiVir 的所有选项。现在，打开浏览器并访问以下地址获取 AntiVir 的更新：

1. 创建名为 `lxrv` 的目录。
2. 从书中附带的 CD 中获取名为 `lxrv.tgz` 的文件，并将其解压到该目录。
3. 执行以下命令：`tar -xvzf lxrv.tgz`。

![](img/a7a9caa80ec85507179284d91e216f9f_119.png)

4. 将生成几个文件，包括 `install.sh` 脚本。按照所示执行命令：

```
./install.sh
```

5. 前述命令告诉系统运行 `install.sh` 脚本。执行后，你会看到程序创建了 `/usr/lib/AntiVir`。它询问你是否创建一个符号链接（程序使用 `symlink` 一词）。按 y 表示是。程序创建的符号链接是从 `/usr/lib/AntiVir/antivir` 指向 `/usr/bin` 目录。建立此符号链接允许你在无需输入完整路径的情况下启动 AntiVir。
6. 你现在已经安装了 AntiVir。但是，你仍然无法使用所有的更新。现在，访问以下地址获取更新：`www.antivir.com/download`。
7. 输入相关信息，然后订购你的密钥。密钥将在几分钟内发送给你。
8. 一旦你获得密钥，将其拷贝到 `/usr/lib/AntiVir/` 目录。现在，通过执行以下命令扫描本地目录中的病毒：

```
antivir
```

9. 系统将加载其文件（`/usr/lib/AntiVir/antivir.vdf`），然后扫描该目录。在所有情况下，它可能一无所获。现在，扫描你主目录下的所有文件和所有子目录：

```
antivir /root -allfiles -s
```

10. 到此为止，AntiVir 对其发现的内容一直并不直率。此外，注意所有输出都显示在屏幕上，而不是日志文件中。你可以通过执行以下命令更改这一点：

```
antivir -allfiles -s -r4 -rf/log.txt -ro
```

此命令让 AntiVir 进入详细模式，然后将其所有的标准输出存到你当前目录下的 `log.txt` 文件中。`-ro` 命令将删除任何名为 `log.txt` 的文件并用其发现的内容替换它。如果你想将信息追加到 `log.txt` 文件的末尾而不是覆盖它，请使用 `-ra` 选项。

11. 以下命令搜索 `var/spool/` 目录，该目录可能包含许多文件：

```
/var/spool/* -s -rf/log.txt -ro
```

12. 现在，切换到 `/etc/cron.daily` 目录。

13. 使用 `vi` 或 `pico` 等文本编辑器创建一个名为 `antivirus.cron` 的文件，并输入以下代码：

```
#!/bin/sh

antivirus / -allfiles -s -r4 -rf/root/log.txt -ro
```
