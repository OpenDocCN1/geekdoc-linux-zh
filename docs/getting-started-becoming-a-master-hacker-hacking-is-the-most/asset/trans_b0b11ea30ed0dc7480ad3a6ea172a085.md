
系统（参见 Wi-Fi 破解中的四次握手）并使它们离线，然后投入资源对它们进行破解。

在这里，我们将首先研究离线密码破解的工具和技术，然后研究在线密码破解的工具和技术。

### 关于词库（Wordlists）的说明

在线和离线密码破解都需要一个尝试的单词列表。

这些词库并不一定包含所有单词。其中一些可能是常被用作密码的字符组合，例如 qwerty、asdfghjk 或 123456。选择合适的词库可能是你在尝试破解密码时所做出的最重要的决定。

Kali 内置了大量词库。你可以通过输入 `locate wordlists` 来查找它们：

```
root@kali:~# locate wordlists
/usr/share/wordlists
/usr/share/applications/kali-wordlists.desktop
/usr/share/d/irb/wordlists
/usr/share/d/irb/wordlists/big.txt
/usr/share/d/irb/wordlists/catala.txt
/usr/share/d/irb/wordlists/common.txt
/usr/share/d/irb/wordlists/euskera.txt
/usr/share/d/irb/wordlists/extensions_common.txt
/usr/share/d/irb/wordlists/indexes.txt
/usr/share/d/irb/wordlists/mutations_common.txt
/usr/share/d/irb/wordlists/others
/usr/share/d/irb/wordlists/small.txt
/usr/share/d/irb/wordlists/spanish.txt
/usr/share/d/irb/wordlists/stress
/usr/share/d/irb/wordlists/vulns
/usr/share/d/irb/wordlists/others/best1050.txt
/usr/share/d/irb/wordlists/others/best110.txt
/usr/share/d/irb/wordlists/others/best15.txt
/usr/share/d/irb/wordlists/others/names.txt
/usr/share/d/irb/wordlists/stress/alpha_num_case.txt
/usr/share/d/irb/wordlists/stress/alpha_num_case_extra.txt
/usr/share/d/irb/wordlists/stress/char.txt
/usr/share/d/irb/wordlists/stress/double_uri_hex.txt
```

这些词库通常与某个应用程序关联，并包含该应用程序特有的单词。例如，Web 目录破解工具 **dirb** 的词库包含常用于网站目录的常用单词。通常，有效密码破解的关键在于选择合适的词库。

此外，网上还有大量词库可供查找，例如在 [www.skullsecurity.org](www.skullsecurity.org) 和 www.hackers-arise.com/password-lists 等网站。

最后，你可以考虑创建自己的词库，该词库应针对具体任务进行定制。

### 密码破解策略

在尝试破解密码时，除非你打算使用暴力破解（在这种情况下，你的策略就是耐心），否则在开始密码破解之前拥有一套策略会对你大有裨益。我总是从一个包含最常用密码的小列表开始。请记住，虽然这个星球上有 75 亿人，其中 15 亿人使用英语（尽管并非都是母语使用者），但人们的思维和行动方式往往相似。懒惰的人（或者那些不重视信息安全的人）会使用常见的单词或常见的键盘组合（即 qwerty、123456），而其他人则会再进一步，创建稍微复杂一些的密码，包括他们的名字、缩写、生日、纪念日、喜欢的电视节目、子女和配偶等。

根据暗网上的电子邮件泄露数据，我们可以构建出最常用密码的列表。2018 年，这些密码是：

1. 123456
2. password
3. 123456789
4. 12345678
5. 12345
6. 111111
7. 1234567
8. sunshine
9. qwerty
10. iloveyou
11. princess
12. admin
13. welcome
14. 666666
15. abc123
16. football
17. 123123
18. monkey
19. 654321
20. !@#$%^&*
21. charlie
22. aa123456
23. donald
24. password1
25. qwerty123

是的，信不信由你，最常用的密码是“123456”和“password”！

这些密码占所有用户账户的 10% 左右！而“123456”被近 3% 的账户使用！虽然我的分析不够科学，但我估计前 5,000 个密码被用于近三分之一的账户。拥有这些信息，如果尝试使用包含数百万密码的词库，从而花费数天、数周甚至数月的工作，那将是非常愚蠢的。相反，应有策略地首先尝试前 5,000 个左右最常用的密码，只有当它们失败时，才尝试使用更大、更复杂的词库。如果你拥有例如一个 1,000 个用户的域的所有密码哈希，仅通过尝试前 5,000 个密码，你很可能会找到其中 300 多个。记住，你只需要一个密码就可以攻陷整个网络。

### 使用 John the Ripper 破解密码

John the Ripper 是最古老的持续维护的密码破解工具之一。它最早出现在 1996 年的黑客界，由 Solar Designer 维护这款出色的 Unix/Linux 密码破解工具。在这里，我们将使用这个简单但优雅的工具来学习密码破解的原则和策略。

我们只需在终端中输入命令 **john** 即可查看 John 的帮助文件。

```
root@kali-2019:~# john
John the Ripper 1.8.0-1.j3-bluemoon-1-bleeding-973a245b96 2018-12-17 20:12:51 +0100 [linux-gnu 64-bit x86_64 AVX2 AC]
Copyright (c) 1996-2018 by Solar Designer and others
Homepage: http://www.openwall.com/john/

Usage: john [OPTIONS] [PASSWORD-FILES]
--single[-SECTION[,...]]	"single crack" mode, using default or named rules
--wordlist[=FILE]		wordlist mode, read words from FILE or stdin
--stdin			like --stdin, but bulk reads, and allows rules
--loopback[=FILE]		like --wordlist, but extract words from a .pot file
--duplicate-suppression		suppress all dupes in wordlist (and force preload)
--prince[=FILE]		PRINCE mode, read words from FILE
--encoding=NAME		input encoding (eg. UTF-8, ISO-8859-1). See also doc/ENCODINGS and --list-hidden-options
--rules[=SECTION[,...]]		enable word mangling rules (for wordlist or PRINCE modes), using default or named rule(s)
--rules=rule[,...]		same, using "immediate" rule(s)
--rules-stack=SECTION[,...]	stacked rules, applied after regular rules or to modes that otherwise don't support rules
--rules-stack=rule[,...]	same, using "immediate" rule(s)
--incremental[=MODE]	"incremental" mode (using section MODE)
--mask[=MASK]		mask mode using MASK (or default from john.conf)
--markov[=OPTIONS]	"Markov" mode (see doc/MARKOV)
--external=MODE		external mode or word filter
--subsets[=CHARSET]	"subsets" mode (see doc/SUBSETS)
--stdout[=LENGTH]		just output candidate passwords [cut at LENGTH]
--restore[=NAME]		restore an interrupted session [called NAME]
--session=NAME		give a new session the NAME
--status[=NAME]		print status of a session [called NAME]
--make-charset=FILE		make a charset file. It will be overwritten
--show[=left]		show cracked passwords [if --left, then uncracked]
--test[=TIME]		run tests and benchmarks for TIME seconds each
--users[~]LOGINS[UID[,...]	[do not] load this (these) user(s) only
--groups[~]GID[,...]		load users [not] of this (these) group(s) only
--shells[~]SHELL[,...]		load users with[out] this (these) shell(s) only
--salts[~]COUNT[~MAX]		load salts with[out] COUNT [to MAX] hashes
--costs[~]COST[,...]		load salts with[out] cost value [to MIN]. For tunable cost parameters, at LEVEL 1-3
--save-memory=LEVEL		enable memory saving, at LEVEL 1-3
--nodes=MIN[-MAX]/TOTAL	this node's number range out of TOTAL count
--fork=N		fork N processes
--pot=NAME		pot file to use
--list=WHAT		list capabilities, see --list-help or doc/OPTIONS
--format=NAME		force hash of type NAME. The supported formats can be seen with --list-formats and --list=subformats
```

```
root@kali-2019:~# useradd hacker
root@kali-2019:~# passwd hacker
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
root@kali-2019:~#
```

让我们通过破解我们自己 Kali Linux 系统上的密码来开始这段密码破解之旅。首先，让我们使用 Linux 命令 `useradd` 在系统上创建一些新账户。这个简单的命令需要一个用户名，然后输入命令 `passwd` 接着输入账户名称。

它会提示你两次输入密码。

创建五个新账户。在前两个账户中，使用短的词典单词。然后，在接下来的三个账户中，使用越来越长且更复杂的密码（添加数字、特殊字符等）。

现在我们已经在 Kali 上有六个用户账户（五个新账户和我们的 root 账户），让我们尝试用 John the Ripper 来破解它们。

破解这些密码的第一步是提取 /etc/shadow 文件（哈希值所在的地方），并去除除密码哈希之外的所有内容。我们可以使用 John 的 `unshadow` 命令来完成此操作。该命令要求 /etc/shadow 和 /etc/passwd 文件位于同一目录中。

```
root@kali-2019:~# cp /etc/passwd ./
root@kali-2019:~# cp /etc/shadow ./
root@kali-2019:~# unshadow passwd shadow > passwordhashes
```

```
root@kali-2019:~# john passwordhashes
Using default input encoding: UTF-8
Loaded 5 password hashes with 5 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Remaining 4 password hashes with 4 different salts
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Wordlist
Press 'q' or Ctrl-C to abort, almost any other key for status
```

