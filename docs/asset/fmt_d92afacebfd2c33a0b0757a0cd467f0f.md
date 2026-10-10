
www.redhat.com/docs/manuals/enterprise/RHEL-4-Manual/en-US/Security_Guide/

# 第 14 章：计算机安全问题 577

## 选择良好的密码

选择强密码的一种良好方法是取一个易记句句中每个单词的首字母。通过添加数字、标点符号和不同的大小写，可以使密码变得更好。你选择的句子应该只对你个人有意义，并且不应公开（在你的个人网页上选择句子是一个很坏的主意）。表 14-1 列出了强密码的示例以及用于记忆它们的技巧。

### 表 14-1：良好密码的构想

| 密码 | 如何记忆 |
|---|---|
| Mrci7yo! | My rusty car is 7 years old! |
| 2Embpl | 2 elphants make BAD PETs, 1 is better |
| ItMcGib | Is that MY coat? Give it back |

这些密码看起来像乱码，但实际上很容易记忆。如你所见，我可以对密码中代表大写字母的单词进行强调。你使用 `password` 命令来设置密码。在命令行终端中输入 `password` 命令，它将允许你更改密码。首先，它会提示你输入当前密码。为了防止“窥视攻击”（shoulder surfing）和他人获取你的密码，密码在你输入时不会显示出来。

只要你正确使用了旧密码，`password` 命令就会提示你输入新密码。当你输入密码时，`password` 命令会通过 `cracklib` 检查密码以判断这是一个好密码还是坏密码。如果非 root 用户选择的密码不是好密码，他们将被要求尝试不同的密码。root 用户是唯一被允许为其他用户分配密码的用户。一旦密码被 `cracklib` 接受，`password` 命令将要求你再次输入新密码以确保没有拼写错误（当你看不见自己输入的内容时，错误很难被检测）。当以 root 身份运行时，可以通过提供该用户的登录名作为 `password` 命令的参数来更改用户的密码。输入以下内容：

```
$ password joe
```

结果是 `password` 命令提示输入 joe 的新密码。在这种情况下，它不会提示输入他的旧密码。这允许 root 在用户忘记密码时重置其密码（这种事件发生得频繁）。

## 使用影子密码文件

在 UNIX 的早期版本中，所有用户账户和密码信息都存储在一个所有用户都可以读取的文件中（尽管 root 可以写入）。这通常不是问题，因为密码信息经过了加密。密码使用陷门算法（trapdoor algorithm）进行加密，使得未编码的密码可以编码成一段杂乱的字符字符串，但该字符串无法翻译回未编码的密码。

## 第三部分：管理 Fedora 和 RHEL

在这种情况下，系统是如何检查你的密码的？当你登录时，系统会对你输入的密码进行编码，将杂乱的字符串与密码文件中存储的杂乱字符串进行比较，并且只有当两者匹配时才允许你访问。你是否曾经问过系统管理员你账户的密码是什么，结果发现系统管理员并不知道？如果是这样，原因如下：管理员确实没有密码，只有加密后的版本。未编码的密码只在你输入的那瞬间存在。

## 破解加密的密码

然而，能够看到加密的密码存在一个问题。虽然反转陷门算法的加密可能困难（甚至是不可能的），但对大量的密码猜测进行编码并将其更改为文件中的加密密码是非常容易的。在数量级上，这比为每个用户名和密码尝试实际的登录尝试要高效得多。如果破解者可以获得你的密码文件的副本，破解者就有更大的机会破解你的系统。

幸运的是，Linux 和所有现代 UNIX 系统默认使用影子密码文件（shadow password file）。影子文件是 `passwd` 文件的特殊版本，只有 root 可以读取。它包含了加密的密码信息，因此可以从系统中任何用户都可以读取的 `passwd` 文件移除。Linux 也支持旧的单个密码文件方法以及较新的影子密码文件。你应该始终使用影子密码文件（它是默认使用的）。

## 检查影子密码文件

名为 `passwd` 的密码文件位于 `/etc` 目录。影子密码文件名为 `shadow`，也位于 `/etc`。如果你的 `/etc/shadow` 文件丢失，可能是 Linux 系统改为将密码信息存储在 `/etc/passwd` 文件中。通过使用 `less` 命令显示文件来验证这一点。

```
# less /etc/passwd

root:DkK66Uke799fq:0:0:root:/root:/bin

bin*:1:1:bin:/bin:

daemon:*:2:2:daemon:/sbin:

.

mary:KpRpUp2ozmyT5A:501:100:Mary Smith:/home/mary:/bin/sh

joe:osXrvnQnaksI:501:100:Joe Johnson:/home/joe:/bin/sh

jane:ptNoueYEJw:502:100:Jane Anderson:/home/jane:/bin/sh

bob:Ju2vY7A0X6Kz:503:100:Bob Reynolds:/home/bob:/bin/sh
```

此列表中的每一行都对应 Linux 系统上的单个用户账户。每行由七个用冒号（:）分隔的字段组成。从左到右，字段分别是登录名、加密的密码、用户 ID、组 ID、描述（通常是人的名字）、家目录和默认 shell。查看第一行，你可以看到它是 root 账户，并且有一个加密密码 `DkS6uke799FQ`。你还可以看到 root 的用户 ID 为零，组 ID 为零，家目录为 `/root`，且 root 的默认 shell 为 `/bin/sh`。

这些值对于 root 账户来说非常正常，但看到那个加密密码应该会在脑中敲响警报。它证实了你的系统没有使用影子密码文件。如果是这样，你应该立即转换密码，以便使用 `/etc/shadow` 来存储密码信息。你可以使用 `pwconv` 命令来实现。只需以 root 身份登录（或使用 `su` 命令变为 root），并在提示符处输入 `pwconv` 命令。它不会产生任何消息，但当你的 shell 返回时，你应该有一个 `/etc/shadow` 文件，并且你的 `/etc/passwd` 文件现在应该像这样：

```
root:x:0:root:/root:/bin/bash

bin:x:1:1:bin:/bin/sh

daemon:x:2:daemon:/sbin
```

```
mary:x:500:100:Mary Smith:/home/mary:/bin/sh

joe:x:501:100:Joe Johnson:/home/joe:/bin/sh

jane:x:502:100:Jane Anderson:/home/jane:/bin/sh

bob:x:503:100:Bob Renolds:/home/bob:/bin/sh
```
