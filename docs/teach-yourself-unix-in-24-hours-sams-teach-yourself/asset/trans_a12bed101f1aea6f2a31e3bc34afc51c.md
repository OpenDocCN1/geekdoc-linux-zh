

# 第 7 小时

与之前运行到结束并返回命令行的示例不同，你所遇到的第一个交互式程序要复杂得多。当你看到 `--More-- (51%)` (51%)` 提示符时，光标会停在行尾，等待你告诉它该做什么。该程序还会让你知道你已经查看了文件的哪个部分；在示例中，你已经查看了文件的一半（51 百比）。

此时，有许多不同的命令可用。按下空格键可以查看屏幕上的信息，直到你看到整个文件为止。

- 2. 尝试从文件的第 12 行启动程序：

```bash
% +12 ~/.zshrc
alias mailq "/usr/lib/sendmail -bp"
alias aliases "echo you mean new aliases..."
alias rd "*readmsg $ | page"
alias rn "/usr/local/bin/rn -dHOME -L -M -m -e -S -"
```

```bash
# 如果我们在交互式 shell 中，则进行一些特殊处理

if ($prompt) then
alias cd "cd \|; ; setprompt"
alias env "printerenv"
alias setprompt "set prompt="$(cwd:t) \! : """
```

```bash
set noclobber=100 filec
umask 007

setprompt
endif
--More--(82)
```

- 3. 你可以在 `.bashrc` 文件大约中间位置看到有一行包含 `aliases` 单词。我可以启动更多内容，使得包含此模式的行显示在第一个屏幕的顶部。

```bash
% +/aliases/..bashrc
```

```bash
...skipping
alias mailq "/usr/lib/sendmail -bp"
alias aliases "echo you mean new aliases..."
```

```bash
# 如果我们在交互式 shell 中，则进行一些特殊处理
alias rd "*readmsg $ | page"
alias rn "/usr/local/bin/rn -dHOME -L -M -m -e -S -/"
```

```bash
if ($prompt) then
# shell 是交互式的。
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_150_0.png)

# 查看文件

```bash
alias cd             *chdir \!" ; setprompt*
alias env             *printerv*
alias setprompt      *setprompt="$system($cwd:t) \! : **

set noclobber history=100 filec
umask 007

setprompt
endif
```

## 特殊别名：

```bash
alias info          ssinfo
--More-- (86%)
```

实际上，请注意包含 `newaliases` 模式的行出现在第一个屏幕的第三行，而不是第一行。这样做是为了让你对匹配行有一点上下文，但这可能需要一些时间适应。还要注意 `more` 告诉我们——通过 `...skipping` 跳过第一行的消息——它正在跳过行来查找模式。

- 4. `--More--` 提示符下可用的命令非常广泛，如表 7.1 所示。表格后的侧边栏解释了所使用的惯例以及如何输入以下命令。

# 表 7.1. more 程序中可用的命令。

| 命令 | 功能 |
|---|---|
| [Space] | 按下空格键显示下一页文本。 |
| n[Return] | 显示后续 n 行（默认仅显示下一行）。 |
| h | 显示 `more` 程序中可用的命令列表。 |
| d |向下滚动半页。 |
| q | 退出 more 程序。 |
| ns | 向前跳过 n 行（默认为 1）。 |
| nf | 向前跳过 n 屏（默认为 1）。 |
| b 或 Control-b | 向后跳一页文本。 |
| = | 显示当前行号。 |
| /pattern | 搜索模式的出现处。 |
| n | 搜索当前模式的下一次出现。 |
| v | 在当前行启动 vi 编辑器。 |
| Control-l | (那是小写的 L.) 重绘屏幕。 |
| :f | 显示当前文件名和行号。 |

# 在 more 程序中输入

在标题和后续正文中，括号内的单词 `[Space]` 指的是作为命令的空格键。同样，`[Return]` 意味着你应该作为命令的一部分按下回车键。命令中的连字符——例如——意味着你应该按住第一个键。小写字母命令组合在一起，但没有连字符，意味着你应该按下相应的键。最后，在命令之前的条目意味着你可以在命令前加上一个数字，这将修改其操作。例如，`3[Return]` 显示文件的后续几行，`20` 跳过后续几行。通常，在按下回车键后显示文件的后续几行：

```bash
more /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/bin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:4:sync:/bin:/bin/sync
games:x:5:6:games:/usr/games:/usr/sbin/nologin
man:x:6:6:man:/var/man:/usr/sbin/nologin
sysx:x:7:7:sysx:/bin:/usr/sbin/nin
lp:x:8:8:lp:/var/lp:/usr/sbin/nologin
data:x:9:9:data:/root:/usr/sbin/nologin
backup:x:10:10:backup:/var/backups:/usr/sbin/nologin
list:x:11:11:list:/root:/usr/sbin/nologin
irc:x:12:12:irc:/var/spool/irc:/usr/sbin/nologin
mail:x:13:13:mail:/var/mail:/usr/sbin/nologin
uu:x:14:14:uu:/var/uu:/usr/sbin/nologin
proxy:x:31:31:proxy:/root:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backup:/usr/sbin/nologin
listd:x:38:38:listd:/var/listd:/usr/sbin/nologin
news:x:39:39:news:/var/spool/news:/usr/sbin/nologin
ircd:x:40:40:ircd:/var/spool/ircd:/usr/sbin/nologin
gnats:x:41:41:gnats:/var/lib/gnats:/usr/sbin/nologin
irc:x:42:42:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:43:43:irclist:/var/run/irclist:/usr/sbin/nologin
gnome:x:44:44:gnome:/var/lib/gnome:/usr/sbin/nologin
list:x:45:45:list:/nonexistent:/usr/sbin/nologin
irc:x:46:46:irc:/var/irc:/usr/sbin/nologin
gnatsapt:x:47:47:gnatsapt:/var/lib/gnatsapt:/usr/sbin/nologin
irc:x:48:48:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:49:49:irclist:/var/run/irclist:/usr/sbin/nologin
nobody:x:53:53:nobody:/nonexistent:/usr/sbin/nologin
system:x:999:999:system:/root:/usr/sbin/nologin
_apt:x:100:100:_apt:/var/lib/apt:/usr/sbin/nologin
nats:x:101:101:nats:/var/nonexistent:/usr/sbin/nologin
message:x:102:102:message:/var/message:/usr/sbin/nologin
irc:x:103:103:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:104:104:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:105:105:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:106:106:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:107:107:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:108:108:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:109:109:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:110:110:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:111:111:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:112:112:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:113:113:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:114:114:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:115:115:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:116:116:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:117:117:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:118:118:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:119:119:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:120:120:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:121:121:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:122:122:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:123:123:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:124:124:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:125:125:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:126:126:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:127:127:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:128:128:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:129:129:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:130:130:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:131:131:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:132:132:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:133:133:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:134:134:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:135:135:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:136:136:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:137:137:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:138:138:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:139:139:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:140:140:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:141:141:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:142:142:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:143:143:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:144:144:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:145:145:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:146:146:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:147:147:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:148:148:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:149:149:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:150:150:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:151:151:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:152:152:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:153:153:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:154:154:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:155:155:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:156:156:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:157:157:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:158:158:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:159:159:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:160:160:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:161:161:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:162:162:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:163:163:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:164:164:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:165:165:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:166:166:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:167:167:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:168:168:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:169:169:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:170:170:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:171:171:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:172:172:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:173:173:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:174:174:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:175:175:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:176:176:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:177:177:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:178:178:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:179:179:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:180:180:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:181:181:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:182:182:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:183:183:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:184:184:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:185:185:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:186:186:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:187:187:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:188:188:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:189:189:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:190:190:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:191:191:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:192:192:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:193:193:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:194:194:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:195:195:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:196:196:irc:/var/run/irc:/usr/sbin/nologin
irclist:x:197:197:irclist:/var/run/irclist:/usr/sbin/nologin
nats:x:198:198:nats:/var/cache/nats:/usr/sbin/nologin
irc:x:199:199:irc:/var/run/irc:/usr/sbin/nologin
```
