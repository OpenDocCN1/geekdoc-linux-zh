
# Wapiti

`ckpt@kali:~$ sudo wapiti -u http://192.168.1.4/`

WAPITI

`Wapiti-3.0.4 (wapiti.sourceforge.io)`

`[!] Connection error with URL http://192.168.1.4/`

`[+] Saving scan state, please wait...`

**Note**

此扫描已保存在文件 `/root/wapiti/scans/192.168.1.4_folder_7bd67c7d.db`

`[*] Wapiti found 0 URLs and forms during the scan`

`[*] Loading modules:`

`backup, blindsel, brute_logite_form, butter, cookieflags, crlf, csrf, csrf, exec, file, http_headers, htaccess, permissionss, redirect, shellshock, sql, ssrf, wapp, xss, xxe`

`Problem with local wapp database.`

`Downloading from the web...`

```bash
# WAPITI 的安装
ckpt@kali:~$ sudo apt install wapiti

Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
```

```bash
The following packages will be upgraded:
wapiti
1 upgraded, 0 newly installed, 0 to remove and 560 not upgraded.
Need to get 340 KB of archives.
After operation, 26 MB disk space will be freed.
get:1 http://ftp.harukasan.org/kali-rolling/amd64 wapiti 3.0.4+dfsg-1 [340 KB]
Fetched 340 KB in 5s (64.2 KB/s)
(Reading database ... 34282 files and directories installed.)
Preparing to unpack ...wapiti_3.0.4+dfsg-1_all.deb
Unpacking wapiti (3.0.4+dfsg-1) over (3.0.3+dfsg-2) ...
Setting up wapiti (3.0.4+dfsg-1) ...
Processing triggers for kali-menu (2021.1.4) ...
Processing triggers for main-db (2.9.4-1) ...
```

图 67 WAPITI 的安装

`WAPITI` 需要 `Python 2.1.x` 或更高版本。其他依赖包括 `Python-requests` 和 `Python-xml`。要开始安装，请先使用以下命令从 GitHub 克隆该工具。

`git clone https://github.com/wapiti-scanner/wapiti.org`

`Wapiti` 的扫描示例：

```bash
(wapiti kali)~
$ sudo wapiti -u scanner.nmap.org

[sudo] password for kali:

WAPITI
Wapiti-3.0.4 (wapiti.sourceforge.io)
[ERROR] No target URL specified, please give a URL with protocol scheme.

(wapiti kali)~
$ sudo wapiti -u http://scanner.nmap.org

WAPITI
Wapiti-3.0.4 (wapiti.sourceforge.io)
... (output continues)
```

```bash
[*] Wapiti found 0 URLs and forms during the scan
[*] Loading modules:
backup, blindsel, brute_logite_form, butter, cookieflags, crlf, csrf, csrf, exec, file, http_headers, htaccess, permissionss, redirect, shellshock, sql, ssrf, wapp, xss, xxe
Problem with local wapp database.
Downloading from the web...
```

# Secbay Press

帮助。
用法: `joomscan.pl [options]`

```
|--url | -u <url>
|--mass | -m <filename>
|--components | -ec
|--joomla-version | -jv
|--report | -nR
|--cookie <string>
|--user -U <User-Agent>
|--random | -r
|--timeout <Time-Out>
n代理示例: --proxy http://127.0.0.1:8080
|--proxy | -p <proxy>
|--update
|--help | -h
|--version
```

- 要扫描的 `Joomscan` URL/域名。
- 遍历 `txt` 文件中提供的 URL。
- 尝试枚举组件。
- 输出目标 `Joomla` 版本并退出不再进行进一步检查。
- 不生成报告。
- 设置 `cookie`，
- 使用指定的 `User-Agent`。
- 使用随机的 `User-Agent`。
- 设置超时。
- 使用代理连接到目标 URL
  - `http://127.0.0.1:8080`
  - `host://127.0.0.1:443`
  - `socks://127.0.0.1:10814`
- 关于作者
- 更新到最新版本。
- 此帮助屏幕。
- 输出当前的 `Joomscan` 版本并退出。

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_184_0.png)

# 8.4.3 `joomscan` 的用法

- 1. 默认扫描：
  `Perl joomscan.pl -u <url>`

![](img/8ce6ad080bbaee4f5508e48ea7a3d6ee_184_1.png)

- 2. 枚举已安装的组件
  `perl joomscan.pl --url www.example.com --enumerate-components`

- 3. 设置 `cookie`
  `perl joomscan.pl --url www.example.com --cookie "test=demo"`

- 4. 设置 `user-agent`
  `perl joomscan.pl --url www.example.com --user-agent "Googlebot/2.1 (+http://www.google.com/bot.html)"`

- 5. 设置随机 `user-agent`
  `perl jeomsplcan.pl -u www.example.com --random-agent`

- 6. 设置代理
  `perl jeomsplcan.pl --url www.example.com --proxy http://127.0.0.1:8080`

## 8.5 `Drupwn`

一个能够高效收集 `drupal` 信息的扫描器。

`Drupwn` 有两种独立的模式：

- `Enum`（枚举模式允许执行枚举）
- `Exploit`（允许检查和利用 `CVE`）

`Enum` 模式：

- 用户枚举
- 默认文件枚举
- 模块枚举
- 主题枚举
- 请求延迟
- 枚举范围
- 日志记录
- 支持 `Socks` 和 `HTTP` 代理
- 支持 `Cookies`
- 节点枚举
- `User-Agent` 支持
- 基础身份认证支持

`Exploit` 模式：

- `CVE` 漏洞利用工具
- 漏洞检查器

# 8.5.1 `Drupwn` 的安装

步骤 1：`Drupwn` 的 GitHub 仓库 `https://github.com/immunIT/drupwn.git`

步骤 2：`sudo git clone https://github.com/immunIT/drupwn.git`

```
$ kalikali:- sudo git clone https://github.com/immunIT/drupasswd.git

Cloning into 'drupwn'...
```
