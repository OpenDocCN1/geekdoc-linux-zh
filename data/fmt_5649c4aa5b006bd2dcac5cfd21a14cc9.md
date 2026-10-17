
```
抑制登录消息。
```

`$HOME/.login`

```
csh 的用户登录命令。
```

`$HOME/.profile`

```
sh 和 ksh 的用户登录命令。
```

# login

## 713

`$HOME/.hosts`
信任的主机名/用户名组合私有列表。

`/etc/.login`
全系统级 csh 登录命令。

`/etc/logindeperm`
基于登录的设备权限。

`/etc/motd`
每日消息。

`/etc/nologin`
在系统关机期间尝试登录的用户显示的消息。

`/etc/passwd`
密码文件。

`/etc/profile`
全系统级 sh 和 ksh 登录命令。

`/etc/shadow`
用户加密密码列表。

`/usr/bin/sh`
用户的默认命令解释器。

`/var/adm/lastlog`
最后登录时间。

`/var/adm/loginlog`
失败登录尝试记录。
`/var/adm/utmpx`
计费。

`/var/adm/utmpx`
计费。

`/var/mail/your-name`
用户的邮箱。

`/etc/default/login`
可以在 `/etc/default/login` 中设置的变量：

- `CONSOLE`: 如果设置，则拒绝 root 登录。
- `SHELL`: 设置初始 shell。
- `PATH`: 设置初始路径。
- `TZ`: 设置时区变量。
- `TIMEOUT`: 设置登录前等待的秒数（0 到 900 之间）。
- `ULIMIT`: 设置登录的文件大小限制。单位为磁盘块。
- `UMASK`: 设置初始文件创建掩码。

## 712

## 716

# logout

## 文件

- `/etc/profile`
用户登录时的环境设置。
- `/var/adm/utmpx`
用户和计费信息。

### 属性

关于以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNWcsu |

## 另请

`env(1)`, `login(1)`, `getlogin(3)`, `utmpx(4)`, `attributes(5)`, `environ(5)`

# logout — 退出登录会话的 Shell 内置函数

### 概要

```
csh

logout
```

# 说明

`logout` 命令终止一个登录 C shell。如果该 shell 不是登录 shell，则会显示消息 Not login shell。

### 属性

关于以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNWcsu |

## 另请

`csh(1)`, `login(1)`, `attributes(5)`

# look — 在系统字典中查找单词或在排序后的列表中查找行

### 概要

```
/usr/bin/look [-d] [-f] [-tc] string [filename]
```

# 说明

`look` 命令查询一个排序后的文件名，并打印所有以 `string` 开头的行。如果你未指定文件名，`look` 将使用 `/usr/share/lib/dict/words` 并使用排序序列 `-cd` 进行查找。`look` 将搜索长度限制在 256 个字符。

### 选项

- `-d` 字典顺序。比较时仅使用字母、数字、制表符和空格字符。
- `-f` 忽略大小写。比较时不区分大写字母和小写字母。
- `-tc` 设置终止字符。忽略字符串 `string` 右侧的所有字符。

### 示例

以下示例使用默认字典列出所有以字符串 `sun` 开头的行。

```
castle@ look sun

sun

sunbeam

sunbonnet

sunburn

sunburnt

Sunday

sunder

sundew

sundial

sundown

sundry

sfish

sunflower

sung

sunglasses

sunk

sunken

sunlight

sunlit

sunny

Sunnyvale

sunrise

screens
```

## 718

# lookbib

sunset
sunshade
sunshine
sunny
sunspot
suntan
suntanned
suntanning
SUNY
castle%

## 文件

- `/usr/share/lib/dict/words`
拼写列表。

### 属性

关于以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可用性 | SUNwesu |

## 另请

`grep(1)`, `sort(1)`, `attributes(5)`

# lookbib — 在参考文献数据库中查找

### 概要

```
/usr/bin/lookbib database
```

# 说明

参考文献是一组行，构成了参考文献信息字段。每个字段从以百分号（`%`）开头的行开始，后面跟着一个键字母、一个空格，最后是字段的内容，该内容可能持续到下一行以 `%` 开头的行。

`lookbib` 使用由 `indexbib` 创建的倒排索引来查找参考文献集。它读取你在终端提示符后输入的关键词，并检索包含这些关键词的记录。如果没有匹配项，除了返回另一个 `>` 提示符外不返回任何内容。

只要它们有由 `indexbib(1)` 创建的共同索引，就可以搜索多个数据库。在这种情况下，只有 `indexbib` 的第一个参数被传递给 `lookbib`。

`lookbib` 不查找索引文件（`.i[abc]`），它查找一个与参数同名但没有后缀的引用文件。它会创建一个带有 `.ig` 后缀的文件供 `grep` 使用，`lookbib` 然后使用该 `grep` 进行查找。

这种方法更易使用，但 `.ig` 文件的使用速度比 `i[abc]` 文件慢，且不允许使用多个引用文件。

# 缺陷

所有的日期可能都应该被索引，因为许多学科都引用了 1800 年或更早的文献。

### 示例

以下示例访问了名为 `bibliography` 的参考文献文件，显示指令，并搜索关键词 `dreams` 的参考文献。

```
castle lookbib bibliography

Instructions? y
```

在 `>` 提示符后输入关键词（如作者和日期）。
如果存在带有这些关键词的参考文献，将打印出来；
如果没有匹配项，你将收到另一个提示符。
要退出 `lookbib`，请在 `>` 提示符后按 CTRL-d。

- > dreams
&A Janice Winsor
@X Opening the Dream Door
@D 153
%I Merrill-West Publishing
%C Carmel, California
@D 1998

%K dreams, psychic development
%X 不仅仅另一本梦解析书！Opening the Dream Door是一本关于心理发展的实用指南。Opening the Dream Door 以友好、个人化的风格编写，并不尝试解释梦的符号。作者认为，每个人都有自己的个人神话和符号，无法以集体方式解读。通过用自己的梦境作为示例，Janice Winsor 为扩展潜意识生活和连接其他领域提供了实用的建议。记忆和访问梦境的过程是以易于理解的方式传授的。

```
~
"bibliography" 27 lines, 946 characters

> ^D

castle$
```
