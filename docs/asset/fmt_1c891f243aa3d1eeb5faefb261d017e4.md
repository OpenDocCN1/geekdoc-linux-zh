
## Secbay Press

解密后的密码存储在主目录下的`pass.txt`文件中。

```bash
clkptkali:-$ ls -l
total 76
drwxr-xr-x 2 clkpt 4096 Jun 22 02:43 clkpt
-rw-xr-r-- 1 root 232 Jun 30 00:02 clkthash.txt
-rw-rw-wwx 1 root 4096 Jun 22 04:51 clkpt.txt
drwxr-xr-x 8 root 4096 Jun 29 02:43 Cmsmap
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Desktop
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Documents
drwxr-xr-x 3 clkpt 4096 Jun 22 07:58 Downloads
drwxr-xr-x 9 root 4096 Jun 29 01:38 drupwn
-rw-r--r-- 1 root 0 Jun 22 04:54 example.txt
drwxr-xr-x 7 root 4096 Jun 28 11:22 joomscap
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Music
drwxr-xr-x 5 root 4096 Jun 28 07:06 framework
-rw----r-- 1 root 45 Jun 30 02:10 pass.txt
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 passwordlist
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Public
drwxr-xr-x 16 root 4096 Jun 28 09:08 engine
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Templates
drwxr-xr-x 10 root 4096 Jun 28 08:29 theHarvester
drwxr-xr-x 5 root 4096 Jun 28 07:14 Uhiscan
drwxr-xr-x 2 clkpt 4096 Jun 22 03:18 Videos
```

在结果中，由于我们使用的字典列表，只有一个哈希值被破解了；如果我们选择完美的字典列表，就可以获得所有哈希的明文。

```bash
ckptkali:-$ cat pass.txt
482c811da5d5babbc6d7ffa9841e38:password123
```

## 11.3 John the Ripper

- `John the Ripper` 是一款开源密码破解软件。
- `John Ripper` 使用字典攻击。它对一组示例字典密码进行加密，并将其与加密后的密码进行比较。
- `John the Ripper` 的设计目标是功能丰富且运行快速。它将多种破解模式整合在一个程序中，并可以根据你的需求进行完全配置。
- 开箱即用，`John` 支持（并自动检测）以下 `Unix crypt(3)` 哈希类型：传统的基于 `DES` 的 `"bigcrypt"` 基于 `BSDI` 扩展 `DES` 的、基于 `FreeBSD MD5` 的（也用于 `Linux` 和 `Cisco IOS`）以及基于 `OpenBSD Blowfish` 的（现在也已用在某些 `Linux` 发行版中，并受新版本 `Solaris` 的支持）。
- 开箱即用还支持 `Kerberos/AFS` 和 `Windows LM`（基于 `DES`）的哈希，以及基于 `DES` 的 `tripcodes`。
- `John the Ripper` 增加了对 `Windows NTLM`（基于 `MD4`）和 `Mac OS X 10.4+` 加盐的 `SHA-1` 哈希的支持。

### 11.3.1 运行 John the Ripper 解密加密 ZIP 的步骤

步骤 1：首先，我们需要使用此命令将哈希导出到`.txt`文件。

```bash
# sudo zip2john zipfile.zip > zipfile.txt
```

```bash
kali~$ sudo zip2john temp.zip temp.hash
Created directory: /root/john
ver 2.0 eh 9981 temp.zip/PKZIP Encr: cmplen=878, decplen=1715, crc=E6CF5B22
```

这里`temp.zip`是一个密码加密的 zip 文件，`hash.txt`是存储导出 zip 密钥的文件。

步骤 2：现在使用此命令在 `john` 中破解这些密钥。

```bash
# sudo john --format=zip zipfile.txt
```

我们将之前保存 zip 密钥的`hash.txt`文件附加到此文件（此处示例如此）。

```bash
kali~$ sudo john --format=zip hash.txt
Using default input hash: UTF-8
Loaded 1 hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2])
Will run 0 OpenMP
Proceeding with single mode, rules:single
Press Ctrl+C to abort, Almost any other key for status
Warning: 9 candidates buffered for the current salt, minimum 16 needed for performance.
Warning: 8 candidates buffered for the current salt, minimum 16 needed for performance.
Almost done: the remaining passwords, if any.
Warning: 10 candidates buffered for the current salt, minimum 16 needed for performance.
Processing with wordlist /usr/john/password.txt, rules:wordlist
12:00:01 DONE 1/1 (2021-06-30 02:42)
Session completed.
```

## 11.4 Hydra

通过简单方法演示 `Hydra` 获取未经授权。

**注意：** 你需要知道要攻击机器的 `IP` 地址。这可以通过 `Linux` 中的`ifconfig`命令查看。

### 运行 Hydra 的步骤

步骤 1：安装 `hydra`

```bash
sudo apt install hydra
```

```bash
apt-get install hydra
Reading package lists...
Building dependency tree...
Reading state... Done
The following packages will be removed and no longer required
The following packages will be installed:
libcurl4-openssl-dev libgnutls-bin libncurses5 libncurses-dev libpcre-dev libreadline-dev libssl-dev libsqlite3-0-dev libncurses-dev libssl.1 libxml2-dev libtiff-dev
100 upgraded, 1 newly installed, 0 to remove and 0 configured
hydra
```

步骤 2：`hydra -help`

```bash
sudo hydra -help
```

```bash
hydra
Version 9.2 by Maurer & Davidleish - 不要用于 military or organizations, or illegal purposes (this is for educational and research only)

Usage: hydra [options] [protocol] [host]

Options:
  -l <user>               单个用户名或从文件读取
  -U <file>               从文件读取用户名
  -p <pass>               单个密码或从文件读取
  -P <file>               从文件读取密码
  -s <port>               指定端口
  -S <range>              端口范围
  -T <threads>            并行连接数（默认: 16）
```
