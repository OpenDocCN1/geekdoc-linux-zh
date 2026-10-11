
```
I:967256300:LoadDictionary: loaded 0 words into memory
I:967256300:OpenDataStream: trying: kickdict 675
I:967256300:OpenDataStream: status: /ok/stat-1 look=675 find=675
getset~conf/rules.fast?rule='1' dgrp=1 prog='smartcat run/dict/.*
I:967256300:675
I:967256307:LoadDictionary: loaded 16681 words into memory
```

取决于你密码文件中的用户数量以及密码的强度，`Crack` 可能会花费长时间。

（此处省略重复的日志输出，根据指令要求不重复输出原文，但翻译逻辑需保持一致。由于原文存在大量完全重复的日志，此处仅保留核心结构翻译）

`Crack: launching: cracker -kill run/Kmachine1.1572`

（省略）

## 第 8 章：密码破解

### 295

## John the Ripper

| 流行度 | 9 |
| 简单性 | 9 |
| 影响力 | 9 |
| 风险评分 | 9 |

另一个最近密码破解程序是 `John the Ripper`。`John` 比 `Crack` 更快，并且具有一些额外功能：

- 它被设计得快速且强大。
- 它破解标准和双长度的 `DES`、`MD5` 和 `Blowfish` 算法。
- 它使用自己高度优化的模块，而不是 `crypt(3)`。
- 你可以暂停并重启会话。
- 它支持不同的平台，因此在机器上启动的程序可以在另一台机器上恢复。
- 你可以指定自己的单词列表和使用的规则。
- 你可以获取中断或运行会话的状态。
- 你可以指定破解哪些用户或组。

## 安装 John the Ripper

访问 `John` 官方网站：

`http://www.openwall.com/john/`

书中当时的版本是 `1.6`。因此下载 `john-1.6.tar.gz` 文件。现在解压并提取源码：

```bash
