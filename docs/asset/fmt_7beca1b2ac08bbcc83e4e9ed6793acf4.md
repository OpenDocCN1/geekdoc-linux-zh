
## 步骤 1：查看 Hashcat 帮助

```bash
$ hashcat --help

[user] password for user:

hashcat (6.2.1) starting...

Usage: hashcat [options]... hash|hashfile [hccapsfile [dictionary|directory]]

[ Options ]

Options Short / Long | Type Description                               | Example
=====================|===============================================
-m, --hash-type   | 哈希类型，见下文引用               | -n 1000
-a, --attack-mode | 攻击模式，见下文引用             | -a 3
-v, --version     | 打印版本                                |
-h, --help        | 打印帮助                                |
-c, --charset     | 假设字符集以十六进制给出                 |
-s, --salt        | 假设盐值在字典列表或十六进制中给出 |
-w, --wordlist   | 假设字典列表以十六进制给出             |
--force           | 忽略警告                                |
--status          | 禁用状态屏幕更新                         |
--status-json     | 设置状态更新之间的间隔为 X 秒     | --status-timer:2
--timeout-abort   | 从 stdin 等待秒数                       | --timeout-abort:300
--machine-readable| 以机器可读格式显示值                   |
--keep-progress   | 当密码被破解时显示                     |
--self-test       | 启动时禁用自检                        |
--loopback        | 向诱导目录添加新的明文                |
--markov-hstat2    | 文件格式                                | --markov-hstat2.my.hstat2
--markov-disable  | 禁用马尔可夫链，模拟经典暴力破解 |
--markov-classic  | 启用经典马尔可夫链，不按位置划分
```

我为你创建了一个用于测试的典型哈希短列表，以便你使用。

## 步骤 2：获取你需要的所有哈希值。

| password123 | 482c1da5db4bcd7ffa98e38 |
| :--- | :--- |
| HELLO | bbfe0c18f9b661d0918ebdd |
| SECRETPASSWORD | b6d5758ba0fd61344587c |
| Test12345 | 66af2cd1976f098ce680a |
| P455word | 75b1aa6842e450f1aa00fd5 |
| GuessMe | 031bcccd3cb4155d |
| S3CuReP45Word | b5af0b0ff72b8c |

## 步骤 3：破解密码需要完美的字典列表。

Kali 位于 `/usr/share/wordlists`，你也可以在线获取。其中一些 [SecList](https://github.com/danielessler/SecLists/master/Passwords) 和 [rockyou](https://github.com/rarondsey/hashcat/releases/data/rockyou.txt)。

```bash
root@kali:~# cd /usr/share/wordlists/
root@kali:/usr/share/wordlists# ls
dirbuster fastrack.txt fern-wifi rockyou.txt wfuzz
```

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_259_0.png)

## 步骤 4：创建文件并将哈希加入文件中。

`sudo nano <filename>.txt`

```
GNU nano 5.4

482c81da5db4bcd7ffa98e38
b6e1ae903e0968c27a58160
6d5db7586af9f1d30450ac58c
62af123f19fbcc62
75b1aa6842e450f1aa00ffd5e4c3d
031bccfecd3cb4dad1556d99bb008
b5af0b0ff72b8c

root@kali:~# ls -la
total 180
drwxr-xr-x 24 clpkt clpkt 4096 Jun 30 02:02 .
drwxr-xr-x 5 root root 4096 Jun 22 06:23 .
-rw----r-- 1 clpkt root 127 Jun 22 03:23 .bash_history
drwxr-xr-x 1 clpkt 220 Jun 22 03:17 .bash_logout
drwxr-xr-x 1 clpkt 4653 Jun 25 23:11 .bashrc
drwxr-xr-x 1 clpkt root 3526 Jun 22 23:17 .bashrc.original
drwx------ 14 clpkt root 4096 Jun 28 11:17 .cache
drwxr-xr-x 3 clpkt root 4096 Jun 28 11:21 .cert
drwxr-xr-x 2 clpkt root 4096 Jun 22 04:43 crypt
-rw-r--r-- 1 root root 232 Jun 30 02:02 ckhash.txt
```

## 步骤 5：启动 hashcat 解密。

`sudo hashcat -m 0 hashes.txt -o passwords.txt /usr/share/wordlists/fasttrack.txt`

- `-m 0` 表示我们要破解的哈希类型。在这种情况下，我们正在破解 `MD5-raw`，因此指定 0，可以通过 `hashcat -h` 命令找到我们能够破解的哈希算法列表。
- `passwords.txt` 是破解密码的输出文件。
- `hashes.txt` 是我们的哈希输入文件。
- `/usr/share/wordlists/fasttrack.txt` 是此字典攻击字典文件的路径。

```
iptables -S; sudo hashcat -a hashcat.txt --pass /usr/share/wordlists/fasttrack

hashcat (v6.0.1) starting...

OpenCL API (OpenCL 1.2) pool 1, Non-Assert, LLV_NULL, RELOC, SLEEP, DISTRO, POOL_DEBUG) - Platform #1 [The cloj project]

****************************************************************
Device #1: Intel
Approaching final keyspace - workload adjusted.

Session: hashcat
Status: exhausted
Hash.name: MD5
Hash.file: hashcat.txt
Time.Started: Wed Oct 25 10:17:26 (1 sec)
Time.Estimated: Wed Oct 25 10:17:26 (0 secs)
Time.Elapsed: None (/usr/share/wordlists/fasttrack.txt)
Guess: 1/108 (0.0%)
Guess.Done: 1/108 (0.0%) Acc:1824 Loops:1 Thr:Ver:8
Recovered: 1/7 (14.29%)
Progress: 222/2222 (10.00%)
Rejected: 0/222 (0.00%)
Retries: 0/222 (0.00%)
Restore.Sub.#1: Salt:0 Amplifier:1-Iteration:0-1
Candidates.#1: Spring17 -> starstans
```
