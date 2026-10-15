
```
$ more /var/log/syslog
May 20 11:49:15 e6400 NetworkManager:  SCPlugin-Ifupdown: {19599648}
...	get_connections {Managed=false}: return empty list.
May 20 11:49:15 e6400 modem-manager: Loaded plugin Longcheer
May 20 11:49:15 e6400 modem-manager: Loaded plugin Option
May 20 11:49:15 e6400 modem-manager: Loaded plugin MotocG
May 20 11:49:15 e6400 modem-manager: Loaded plugin ZTE
May 20 11:49:15 e6400 modem-manager: Loaded plugin Gobi
May 20 11:49:15 e6400 modem-manager: Loaded plugin Novatel
May 20 11:49:15 e6400 modem-manager: Loaded plugin Nokia
May 20 11:49:15 e6400 modem-manager: Loaded plugin AnyData
May 20 11:49:15 e6400 modem-manager: Loaded plugin Huawei
May 20 11:49:15 e6400 modem-manager: Loaded plugin Sierra
May 20 11:49:15 e6400 modem-manager: Loaded plugin Ericsson NEM
--More-- (14%)
```

### 使用 `more` 命令查看文本文件

`more` 命令逐页显示命令或文本文件的输出。这对于大文件或产生大量输出行的命令非常有用。上述示例演示了如何使用 `more` 命令逐页读取大型文本文件。

> 空格键用于使用 `more` 滚动输出。Q 键可以在未滚动到末尾的情况下关闭文件。

常见用法示例：

- `more [FILE]` | 逐页显示指定文件
- `more +[NUM] [FILE]` | 从指定的行号开始读取文件
- `[COMMAND] | more` | 逐页显示命令的输出

#### less

**用途：** 一次显示一条命令或文本文件的输出的一页（或一行）。

**语法：** `less [OPTIONS] [FILE]`

```bash
$ less /var/log/syslog
May 20 11:49:15 e6400 NetworkManager: SCPlugin-Iifupdown: (19599648)
... get_connections (Managed=False): return empty list.
May 20 11:49:15 e6400 modem-manager: Loaded plugin Longcheer
May 20 11:49:15 e6400 modem-manager: Loaded plugin Option
May 20 11:49:15 e6400 modem-manager: Loaded plugin MotoC
May 20 11:49:15 e6400 modem-manager: Loaded plugin QcrtHigh-Speed
May 20 11:49:15 e6400 modem-manager: Loaded plugin Gobi
May 20 11:49:15 e6400 modem-manager: Loaded plugin Generic
May 20 11:49:15 e6400 modem-manager: Loaded plugin Novatel
May 20 11:49:15 e6400 modem-manager: Loaded plugin Nokia
May 20 11:49:15 e6400 modem-manager: Loaded plugin AnyData
May 20 11:49:15 e6400 modem-manager: Loaded plugin Huawei
May 20 11:49:15 e6400 modem-manager: Loaded plugin ZTE
May 20 11:49:15 e6400 modem-manager: Loaded plugin Sierra
May 20 11:49:15 e6400 modem-manager: Loaded plugin Ericsson MBM
:
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_71_0.png)

`less` 命令与前面讨论过的 `more` 命令类似，不同之处在于它支持双向滚动（向上和向下），而 `more` 只能向下滚动。

> 使用 `less` 时，可以使用方向键和 Page Up/Down 键来滚动输出。按 Q 键可关闭文件，无需滚动到末尾。

**常见用法示例：**

- `less [FILE]` 一次一页显示指定文件
- `less +[NUM] [FILE]` 从指定行号开始读取文件
- `[COMMAND] | less` 一次一页显示命令的输出

#### head

**用途：** 显示文件的开头部分。

**语法：** `head [OPTIONS] [FILE]`

```bash
$ head -n 2 ShoppingList.txt
Milk
Eggs
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_72_0.png)

`head` 命令显示指定文件的前几行（被称为 *head*）。在上面的示例中，`-n 2` 选项用于只显示指定文件的前两行。如果执行 `head` 命令时没有提供选项，它将默认显示文件中的前 10 行。

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `head [FILE]` | 显示指定文件的前 10 行 |
| `head -n [NUM] [FILE]` | 显示指定数量的行 |

#### tail

**用途：** 显示文件的末尾部分。

**语法：** `tail [OPTIONS] [FILE]`

```bash
$ tail -n 2 ShoppingList.txt
Cheese
Tacos
```

使用 `tail` 显示文件末尾的两行

`tail` 命令显示指定文件的最后几行（被称为 *tail*）。在上面的示例中，`-n 2` 选项用于只显示指定文件的最后两行。如果执行 `tail` 命令时没有提供选项，它将默认显示文件中的最后 10 行。

`tail` 命令的另一个实用功能是 `-f` 选项，它用于在文件增长时“跟踪”该文件。这指示 `tail` 命令打开指定文件，并在新行写入时显示它们。下一个示例演示了如何使用 `tail -f` 命令实时监控 `/var/log/syslog` 文件中的新日志条目。

```bash
$ tail -f /var/log/syslog
May 22 13:41:50 e6400 NetworkManager: <info>  (wlan0): supplicant
connection state:  completed -> group handshake
May 22 13:41:50 e6400 NetworkManager: <info>  (wlan0): supplicant
connection state:  group handshake -> completed
May 22 13:41:51 e6400 wpa_supplicant[848]: WPA: EAPOL-Key Replay
Counter did not increase - dropping packet
May 22 13:41:51 e6400 wpa_supplicant[848]: WPA: Invalid EAPOL-Key MIC -
dropping packet
May 22 13:42:15 e6400 wpa_supplicant[848]: last message repeated 6
times
May 22 13:45:13 e6400 anacron[1290]: Job 'cron.daily' started
May 22 13:45:13 e6400 anacron[2167]: Updated timestamp for job
'cron.daily' to 2010-05-22
...
```

使用 `tail` 命令实时监控不断增长的日志文件

**常见用法示例：**

| 命令 | 描述 |
| :--- | :--- |
| `tail [FILE]` | 显示指定文件的最后 10 行 |
| `tail -n [NUM] [FILE]` | 显示指定数量的行 |
