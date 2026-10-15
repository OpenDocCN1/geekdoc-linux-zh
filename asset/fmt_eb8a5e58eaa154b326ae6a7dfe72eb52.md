
```bash
$ less /var/log/syslog
May 20 11:49:15 e6400 NetworkManager:     SCPlugin-ifupdown: (19599648)
...get_connections (Managed=False): return empty list.
May 20 11:49:15 e6400 modem-manager: Loaded plugin Longcheer
May 20 11:49:15 e6400 modem-manager: Loaded plugin Option
May 20 11:49:15 e6400 modem-manager: Loaded plugin MotoC
May 20 11:49:15 e6400 modem-manager: Loaded plugin High-Speed
May 20 11:49:15 e6400 modem-manager: Loaded plugin Generic
May 20 11:49:15 e6400 modem-manager: Loaded plugin Gobi
May 20 11:49:15 e6400 modem-manager: Loaded plugin Nokia
May 20 11:49:15 e6400 modem-manager: Loaded plugin AnyData
May 20 11:49:15 e6400 modem-manager: Loaded plugin Huawei
May 20 11:49:15 e6400 modem-manager: Loaded plugin ZTE
May 20 11:49:15 e6400 modem-manager: Loaded plugin Sierra
May 20 11:49:15 e6400 modem-manager: Loaded plugin Ericsson MBM
:
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_71_0.png)

`less` 命令与之前讨论的 `more` 命令类似，不同之处在于它支持双向滚动（向上和向下），而 `more` 只能向下滚动。

> **提示**：使用 `less` 时，使用方向键和 Page Up/Down 键进行滚动。按 Q 键即可关闭文件，无需滚动到末尾。

- `less [FILE]`：逐页显示指定文件
- `less +[NUM] [FILE]`：从指定行号开始读取文件
- `[COMMAND] | less`：逐页显示命令的输出

### head

**用途**：显示文件的前部分内容。

**用法语法**：`head [OPTIONS] [FILE]`

```bash
$ head -n 2 ShoppingList.txt
Milk
Eggs
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_72_0.png)

`head` 命令显示指定文件的前几行（即 *head*）。在上面的示例中，使用 `-n 2` 选项仅显示指定文件的前两行。如果执行 `head` 命令时不带任何选项，默认将显示文件的前 10 行。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `head [FILE]` | 显示指定文件的前 10 行 |
| `head -n [NUM] [FILE]` | 显示指定行数的内容 |

### tail

**用途**：显示文件的后部分内容。

**用法语法**：`tail [OPTIONS] [FILE]`

```bash
$ tail -n 2 ShoppingList.txt
Cheese
Tacos
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_73_0.png)

`tail` 命令显示指定文件的最后几行（即 *tail*）。在上面的示例中，使用 `-n 2` 选项仅显示指定文件的最后两行。如果执行 `tail` 命令时不带任何选项，默认将显示文件的最后 10 行。

`tail` 命令的另一个实用功能是 `-f` 选项，用于在文件增长时“跟踪”文件。这会指示 `tail` 命令打开指定文件，并在新行写入时显示它们。下一个示例展示了使用 `tail -f` 命令实时监控 `/var/log/syslog` 文件中新日志条目的方法。

```bash
$ tail -f /var/log/syslog
May 22 13:41:50 e6400 NetworkManager: <info>  (wlan0): supplicant connection state:  completed -> group handshake
May 22 13:41:50 e6400 NetworkManager: <info>  (wlan0): supplicant connection state:  group handshake -> completed
May 22 13:41:51 e6400 wpa_supplicant[848]: WPA: EAPOL-Key Replay Counter did not increase - dropping packet
May 22 13:41:51 e6400 wpa_supplicant[848]: WPA: Invalid EAPOL-Key MIC - dropping packet
May 22 13:42:15 e6400 wpa_supplicant[848]: last message repeated 6 times
May 22 13:45:13 e6400 anacron[1290]: Job 'cron.daily' started
May 22 13:45:13 e6400 anacron[1290]: Updated timestamp for job 'cron.daily' to 2010-05-22
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_73_1.png)

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `tail [FILE]` | 显示指定文件的最后 10 行 |
| `tail -n [NUM] [FILE]` | 显示指定行数的内容 |
| `tail -f [FILE]` | 跟踪文件增长过程 |

### tee

**用途**：显示命令的输出并将输出写入文件。

**用法语法**：`tee [OPTIONS] [FILE]`

```bash
$ ls -l /etc/ | tee etc.txt
-rw-r--r-- 1 root root 2975 2009-02-04 11:12 adduser.conf
-rw-r--r-- 1 root root 46 2010-06-27 16:53 adjtime
-rw-r--r-- 1 root root 532 2009-11-30 14:33 aliases
-rw-r--r-- 1 root root 12288 2010-07-01 12:23 aliases.db
drwxr-xr-x 2 root root 4096 2010-05-04 13:24 alternatives
drwxr-xr-x 4 root root 4096 2009-03-12 14:08 amavis
drwxr-xr-x 3 root root 4096 2009-02-08 12:49 apm
drwxr-xr-x 2 root root 4096 2009-08-28 14:45 apparmor
drwxr-xr-x 6 root root 4096 2010-06-27 16:53 apparmor.d
...
```

![](img/8f33496304c637dbf51ff6ddc3c7ff29_74_0.png)

`tee` 命令显示命令的输出，同时也将输出保存到文件中。在上面的示例中，`tee` 命令显示 `ls -l /etc` 命令的输出，同时将结果保存到一个名为 `etc.txt` 的文件中。查看 `etc.txt` 文件可以发现，其内容与在命令行上显示的输出相同，如下一个示例所示。
