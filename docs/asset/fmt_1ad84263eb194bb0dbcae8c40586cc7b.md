
# Metasploit Framework v6.3.0-rc4

## 这是一个开源漏洞利用框架

## 教程

## 计算机安全

### 尝试 Metasploable

我们更倾向于使用旧的 Distbuster（包含在 Parrot 系统中），但你可以使用 Metasploit 作为辅助工具/扫描器/`http_scanner`。设置 `RHOSTS`。现在，更改默认字典：`set DICTIONARY=/usr/share/wordlists/distbuster` 并更改线程数以加速破解：`set THREADS 10`。在开始攻击之前，你应该从字典文件中移除不需要的命令。

你的伪造 DNS 服务器，导航到任何网站，然后就会到达 `TARGETDOMAIN`。一旦完成后，只需杀掉伪造 DNS 服务器即可：`jobs -1`。你可以随时通过执行 `jobs` 来获取正在运行的任务列表。这里有一份你某些时候可能需要的模块列表：`modules/auxiliary/server/capture/*`。如你所见，它们都是直观的模块，旨在窃取 IMAP、HTTP Auth、FTP、POP3 和 SMTP 的凭据。

Metasploit 实现在一个非常惊人的虚拟机中。因此，你可以在不攻击自己电脑的情况下使用它。你可以在 `https://github.com/metasploit/metasploit-framework` 免费获取，其中包含所有可用模块，用于找到正确的 Metasploit 模块。

我们已经接触了 Metasploit 模块的边缘。以下内容对你有所帮助：

## Meterpreter 是 Metasploit 中最好的 Payload 之一

涵盖了方方面面，从破解攻击到文件上传，以及各种方法、技巧等等。

每个人都有适合的！访问 `https://www.offensive-security.com/metasploit-unashed/auxiliary-module-reference/` 查看官方的 Metasploit 辅助模块参考。

## 网络漏洞利用
