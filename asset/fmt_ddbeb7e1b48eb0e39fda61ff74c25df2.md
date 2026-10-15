
### Listing 413 - 使用 searchsploit 列出可用的 Windows SMB 远程漏洞利用

### 14.2.2.2 Nmap NSE 脚本

Nmap 是最流行的枚举工具之一。该工具的一个非常强大的功能是 Nmap 脚本引擎（Nmap Scripting Engine, NSE）<sup>374</sup>，如其名称所示，它引入了使用脚本自动化各种任务的能力。

Nmap 脚本引擎附带了各种脚本，用于枚举、暴力破解、模糊测试、检测以及利用服务。Nmap 脚本引擎提供的完整脚本列表可以在 `/usr/share/nmap/scripts` 下找到。使用 `grep` 快速搜索 NSE 脚本中的“Exploits”一词会返回大量结果：

```bash
kali@kali:~$ cd /usr/share/nmap/scripts

kali@kali:/usr/share/nmap/scripts$ grep Exploits *.nse

clamav-exec.nse:Exploits ClamAV servers vulnerable to unaauthenticated clamav command execution.

http-awststatstotals-exec.nse:Exploits a remote code execution vulnerability in Awststats Totals 1.0 up to 1.14

http-axis2-dir-traversal.nse:Exploits a directory traversal vulnerability in Apache Ax is2 version 1.4.1 by

http-fileupload-exploiter.nse:Exploits insecure file upload forms in web applications

...
```

Listing 414 - 列出包含“Exploits”一词的 NSE 脚本

我们可以通过运行带有 `--script-help` 选项后跟脚本文件名的 `nmap` 来列出特定 NSE 脚本的信息：

```bash
kali@kali:~$ nmap --script-help=clamav-exec.nse

Starting Nmap 7.70 ( https://nmap.org ) at 2019-05-17 13:41 MDT

clamav-exec

Categories: exploit vuln

https://nmap.org/nsedoc/scripts/clamav-exec.html

Exploits ClamAV servers vulnerable to unaauthenticated clamav command execution.

ClamAV server 0.99.2, and possibly other previous versions, allow the execution of dangerous service commands without authentication. Specifically, the command 'SCAN' may be used to list system files and the command 'SHUTDOWN' shut downs the service. This vulnerability was discovered by Alejandro Hernandez (nitr0us).
```

<sup>373</sup> (Ahrefs Pte. Ltd., 2018), https://ahrefs.com/blog/google-advanced-search-operators/

<sup>374</sup> (Nmap, 2019). https://nmap.org/book/nse.html

该脚本在未带参数时测试命令 'SCAN' 的可用性。

参考：
- [https://twitter.com/nitr0usmx/status/740673507684679680](https://twitter.com/nitr0usmx/status/740673507684679680)
- [https://bugzilla.clamav.net/show_bug.cgi?id=11585](https://bugzilla.clamav.net/show_bug.cgi?id=11585)

*列表 415 - 使用 Nmap NSE 获取脚本信息*

这提供了关于漏洞及外部信息资源的信息。

### 14.2.2.3 浏览器利用框架 (BeEF)

浏览器利用框架 (BeEF)³⁷⁵ 是一个专注于在 Web 浏览器中执行客户端攻击的渗透测试工具。不用说，它包含了大量利用工具。

要列出可用的利用工具，我们首先必须启动所需的服务。在 Kali Linux 中，可以使用 `beef-xss` 命令自动完成此操作：

```
kali@kali:-$ sudo beef-xss

[*] Please wait as BeEF services are started.

[*] You might need to refresh your browser once it opens.

[*] UI URL: http://127.0.0.1:3000/ui/panel

[*] Hook: <script src="http://<IP>:3000/hook.js"></script>

[*] Example: <script src="http://127.0.0.1:3000/hook.js"></script>
```
