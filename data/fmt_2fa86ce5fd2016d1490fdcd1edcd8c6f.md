
# 示例扫描结果

Host is up (0.079s latency).

Other addresses for `scanme.nmap.org` (not scanned): `2600:3c61:0000:3e6::d4e:7061`

Not shown: 993 closed ports

```
PORT STATE SERVICE

22/tcp open     ssh             OpenSSH 6.6.1p1 (Ubuntu Linux; protocol 2.0)

80/tcp open     http            Apache 2.4.47 (Ubuntu)

143/tcp filtered  smtp

139/tcp filtered  netbios-ssn

445/tcp filtered  ldp

694/tcp open     ping-echo Kping echo

31337/tcp open tcpwrapped

Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/

Nmap done: 1 IP address (1 host up) scanned in 13.34 seconds
```

# 端口扫描

`-p` 有时你只想用 Nmap 扫描某些端口。`-p` 标志允许你为 Nmap 指定特定的端口。然后 Nmap 将扫描目标主机上的这些端口。

```bash
nmap -sS -T4 25,50,443 192.168.1.105
```

```bash
$ kati@kati[][~]$ sudo nmap -sS -T4 http,https,scanme.nmap.org

Starting Nmap 7.93 ( https://nmap.org ) at 2023-04-07 10:39 CDT

Nmap report for scanme.nmap.org (45.33.32.156)

Host is up (0.018s latency).

Other addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2f

PORT STATE SERVICE

80/tcp open http

143/tcp closed imaps

443/tcp closed https

8080/tcp closed https

map done: 1 IP address (1 host up) scanned in 0.54 seconds
```

## -A

到目前，你已经掌握了许多可以使用的参数。将所有参数放在一起使用会非常麻烦。Nmap 引入 `-A` 参数正是为了这个。它就像是一个“大杂烩”参数，告诉 Nmap 尽可能激地收集尽可能多的信息。

```bash
nmap -A 192.168.1.105
```

```bash
nmap -A scanme.nmap.org

start Nmap 7.92 (https://nmap.org) @ 2023-04-07 10:39 CDT

Nmap scan for scanme.nmap.org (45.33.32.156)

Host is up (0.00456s)

Addresses for scanme.nmap.org (not scanned): 2600:3c01::f03c:91ff:fe18:bb2

Not shown: 993 closed ports (conf-resolved)

PORT STATE VERSION

22/tcp open  OpenSSH 8.6p1-1ubuntu2.2.3 (Ubuntu Linux; protocol 2.0)

  ssh

80/tcp open  1024ac0a1b8e2ffcc5599d7c2b347b6075 (ECDSA)

443/tcp open  Apache 2.4.41 (Ubuntu)

256 960d2b5e57a1c442e5f4ca625f4cb257 (ECDSA)

256 33f9a5d8e9f1c783d5a2af1456 (ED25519)

80/tcp filtered

  _http-server-header: Apache/2.4.7 (Ubuntu)

  _http-favicon: Nmap Project

445/tcp filtered

139/tcp filtered netbios

843/tcp filtered

9929/tcp open  ping-echo Pinging echo

3137/tcp open  tcp-wrapped

service info: OS; CPE: /os:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/

Nmap done: 1 IP address (1 host up) in 17.07 seconds
```

## 日志输出

你可以存储 Nmap 的结果。是的，你可以这样做。Nmap 有另一个参数允许你以多种不同的格式存储输出。这对于像带有 `-p` 参数那样的扫描非常有用。要使用 Nmap 的日志功能，请配合文件名使用 `-oN` 或 `-oX`。`-oN` 记录普通输出。`-oX` 将输出记录为 XML 格式。Nmap 会用新日志覆盖旧日志，因此请务不要不要覆盖你想要保存的内容。

```bash
# nmap -sS -p -oN Documents/full-scan.txt 192.168.17.105
```

当 Nmap 完成后，你可以在文本文件中找到日志。如果你想要更特别的格式，可以尝试使用 `-oS` 参数。

# 7.5 Recon-recon

Recon-recon 是一个用 Python 编写的全功能 Web 侦察框架。通过自主模块、数据库通信、舒适的操作界面、智能帮助和目标实现，Recon-recon 为开源观察提供了一个突破性的环境，可以快速且完整地进行侦察。

Recon 看起来和感觉像 Metasploit 框架，减少了利用该系统吸收信息的预期。但就其本身而言，它是独特的。Recon-recon 并不打算与现有架构竞争，因为它专门为电子开源侦察设计。如果你需要使用利用，请使用 Metasploit 框架。如果你需要进行社会工程学，请使用 Social Engineering Toolkit。如果你需要进行监控，请使用 Recon-recon！更多信息请参阅使用指南。

Recon-recon 是一个完全标准的系统，使得即使是最顶的 Python 工程师也能轻松贡献。每个模块都是“module”类的子类。“module”类是一个经过修改的 "cmd" 翻译器，配备了内置功能，为基本任务提供基本接口，例如实例化输出、与数据库协作、发送 Web 请求以及管理 API 密钥。在这些方面，大量的性工作已经完成。

构建模块非常简单，只需花费几分钟。更多信息请参阅开发指南。

## 7.5.1 安装 recon-ng

```bash
apt-get install recon-ng

$ ulimit -s unlimited recon-ng

[*] Version check.
```

`img/8ce6ad080bbaee4f550e48ea7a3d6ee_161_0.png`

## 7.5.2 recon-ng 的使用

```bash
[recon-ng/default] > workspaces

管理工作

Usage: workspaces <create|list|remove>
```

### workspace create (创建工作)

```bash
[recon-ng/default] > workspaces create test

[recon-ng/test] >
```

### workspace list (列出所有工作)

```bash
[recon-ng/test] > workspaces list

+--------------------------------------+

| Workspaces           | Modified |

+--------------------------------------+

| default             | 2021-06-28 07:52:56 |

| test                 | 2021-06-28 08:02:15 |

+--------------------------------------+
```

### Workspace remove (移除工作)

```bash
[recon-ng/test] > workspaces remove test
```
