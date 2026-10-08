

在该网站上，但我认为四个子目录的深度足以高效地捕获大多数关键词。现在我们就可以编写 `ceWL` 命令来实现这一目标，从 www.hackers-arise.com 抓取所有长度超过 8 个字符的单词。

```bash
kali > cewl -d 4 -m 8 https://www.hackers-arise.com -w cewlpasswords
```

```text
root@kali-2019:~# cat cewlpasswords
Metasploit
Forensics
Training
Subscribers
security
Automobile
Exploits
Facebook
computer
Raspberry
Security
Cracking
Bluetooth
information
Wireless
Password
directory
Engineering
Reconnaissance
Scripting
Forensic
Vulnerability
Investigator
Scanning
Information
Internet
Registration
Networks
Professional
Confessions
Fundamentals
Development
Schedule
Payments
Confidantes
DataBase
Honeypot
```

请注意，在目标网站 URL 前加上 http 或 https 非常重要。如果没有这个前缀，ceWL 将无法抓取目标 URL。根据网站的大小，这可能需要几个小时。

当 ceWL 完成潜在密码的抓取后，它会将所有潜在密码放入一个我命名为 cewlpasswords 的文件中（你可以随心所欲地命名）。我们可以使用 `cat` 命令查看该文件的内容：

```bash
kali > cat cewlpasswords
```

ceWL 在 www.hackers-arise.com 上发现了数百个潜在密码，其中一些非常具有行业针对性，例如 Metasploit、exploits、vulnerability、scripting 等。

要在 john 中使用该密码列表，我们可以输入：

```bash
kali > john -wordlist=/root/cewlpasswords -rules passwordhashes
```

john 将使用从目标网站抓取的单词列表（cewlpasswords），并应用规则通过字符替换来变形（-rules）这些单词，从而增加破解目标密码的机会。

## Crunch

有时，为了破解密码，我们可能需要创建一个满足特定已知参数的专用列表。例如，也许我们知道所有密码都以四个数字结尾（例如 password1234），或者我们知道目标的生日并怀疑他们将其用于密码中。如果目标的生日是 2 月 29 日，他们可能会创建诸如 “password0229” 这样的密码。Crunch 是我们创建此类列表的工具！

要开始使用 crunch，只需在 BASH shell 中输入 `crunch`。

```bash
kali > crunch
```

```text
root@kali-2019:~# crunch
crunch version 3.6
Crunch can create a wordlist based on criteria you specify. The output from crunch can be sent to the screen, file, or to another program.
Usage: crunch <min> <max> [options]
where min and max are numbers
Please refer to the man page for instructions and examples on how to use crunch.
root@kali-2019:~#
```

```text
CRUNCH(1)                General Commands Manual                CRUNCH(1)
NAME
crunch - generate wordlists from a character set
SYNOPSIS
crunch <min-len> <max-len> [<charset string>] [options]
DESCRIPTION
Crunch can create a wordlist based on criteria you specify. The output from crunch can be sent to the screen, file, or to another program. The required parameters are:
min-len
The minimum length string you want crunch to start at. This option is required even for parameters that won't use the value.
max-len
The maximum length string you want crunch to end at. This option is required even for parameters that won't use the value.
charset string
You may specify character sets for crunch to use on the command line or if you leave it blank crunch will use the default character sets. The order MUST BE lower case characters, upper case characters, numbers, and then symbols. If you don't follow this order you will not get the results you want. You MUST specify either values for the character type or a plus sign.
NOTE: If you want to include the space character in your character set you must escape it using the \ character or enclose your character set in quotes i.e. "abc ". See the examples 3, 11, 12, and 13 for examples.
OPTIONS
-b number[type]
Specifies the size of the output file, only works if -o START is used, i.e.: 60MB The output files will be in the format of starting letter-ending letter for example: ./crunch45-b 20mb -o START will generate 4 files: aaaa-gfved.txt, gfzee-omgbw.txt, omgbz-wcydu.txt, wcydu-zzzzz.txt valid values for type are kb, mb, gb, kib, mib, and gib. The first three types are based on 1000 while the last three types are based on 1024. NOTE There is no space between the number and type. For example 500mb is correct 500 mb is NOT correct.
```

```text
-t @%,$"
Specifies a pattern, eg: @@@@@@@%@@@ where the only the @'s, ,'s, $'s, and ^'s will change.
@ will insert lower case characters
, will insert upper case characters
% will insert numbers
" will insert symbols
```

尽管这里显示了一些关于 crunch 的基本信息，但我们确实需要查看 man 页面来理解如何使用 crunch。

```bash
kali > man crunch
```

在这里，我们可以看到为了高效使用 crunch 的所有关键选项。如果我们往下滚动一点，可以看到用于与 -t 选项配合使用的模式指定通配符。

```text
EXAMPLES
Example 1
crunch 1 8
crunch will display a wordlist that starts at a and ends at zzzzzzzz

Example 2
crunch 1 6 abcdefg
crunch will display a wordlist using the character set abcdefg that starts at a and ends at gggggg

Example 3
crunch 1 6 abcdeg\
crunch 1 6 abcdeg\
there is a space at the end of the character string. In order for crunch to use the space you will need to escape it using the \ character. In this example you could also put quotes around the letters and not need the \", i.e. "abcdefg". Crunch will display a wordlist using the character set abcdefg that starts at a and ends at (6 spaces)

Example 4
crunch 1 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt
crunch will use the mixalpha-numeric-all-space character set from charset.lst and will write the wordlist to a file named wordlist.txt. The file will start with a and end with "                "

Example 5
crunch 8 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt -t @dgg@@@ -s cbdogaaa
crunch should generate a 8 character wordlist using the mixalpha-number-all-space character set from charset.lst and will write the wordlist to a file named wordlist.txt. The file will start at cbdogaaa and end at " dog "

Example 6
crunch 2 3 -f charset.lst walpha -s BB
crunch with start generating a wordlist at BB and end with ZZZ. This is useful if you have to stop generating a wordlist in the middle. Just do a tail wordlist.txt and set the -s parameter to the next word in the sequence. Be sure to rename the original wordlist BEFORE you begin as crunch will overwrite the existing wordlist.
```

```text
root@kali-2019:~# crunch 9 9 -t dylan%%%% -o customwordlist.txt
Crunch will now generate the following amount of data: 100000 bytes
0 MB
0 GB
0 TB
0 PB
Crunch will now generate the following number of lines: 10000
crunch: 100% completed generating output
```

然后，当我们滚动到 man 页面底部时，可以看到一些简单的示例。

现在让我们尝试使用 crunch 创建单词列表。还记得我上面提到的那个目标吗？它的密码策略是至少八个字符且至少包含一个数字。让我们创建一个满足这些标准的自定义密码列表。

假设我们知道目标是一位 Bob Dylan 的粉丝。他们可能会使用那个名字，然后在后面加上四个数字（也许是他们的出生日期）。我们可以通过输入以下内容在 crunch 中创建这样一个列表：

```bash
kali > crunch 9 9 -t dylan%%%% -o customwordlist.txt
```

当我们按下回车键时，crunch 首先计算文件将变得多大，然后再创建它（那些《Mr. Robot》的粉丝（www.hackers-arise.com/mr-robot）可能会认出，Elliot 在第一季中使用了类似的技术破解了他治疗师的密码）。在这种情况下，crunch 估计将是 100,000 字节。这是至关重要的信息，因为使用 crunch 创建的文件可能极其庞大，会填满你的整个硬盘。例如，如果我想要创建一个在密码前有四个字母、后有四个数字且最多达十三个字符的单词列表，我会输入：

```bash
kali > crunch 13 13 -t @@@@dylan%%%% -o customwordlist.txt
```

```text
root@kali-2019:~# crunch 13 13 -t @@@@dylan%%%% -o customwordlist.txt 
Crunch will now generate the following amount of data: 63976640000 bytes 61012 MB 59 GB 0 TB 0 PB
Crunch will now generate the following number of lines: 4569760000
```

```text
root@kali-2019:~# git clone https://github.com/Mebus/cupp 
Cloning into 'cupp'... 
remote: Enumerating objects: 6, done. 
remote: Counting objects: 100% (6/6), done. 
remote: Compressing objects: 100% (6/6), done. 
remote: Total 194 (delta 1), reused 1 (delta 0), pack-reused 188 
Receiving objects: 100% (194/194), 109.18 KiB | 1.13 MiB/s, done. 
Resolving deltas: 100% (100/100), done.
```

如上所示，crunch 即将创建一个 59GB 的单词列表！这有点……

