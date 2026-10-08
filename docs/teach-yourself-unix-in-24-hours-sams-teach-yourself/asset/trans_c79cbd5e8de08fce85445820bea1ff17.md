

# 通配符与正则表达式

5. 为了查看其他示例，我使用 `head` 命令来查看密码文件的前 10 行：

```
% head /etc/passwd
root:?:0:0:root:/bin/bash
news?:6:11:USENet News:/usr/spool/news:/bin/ksh
ingress?:7:59:INGRES Manager:/usr/ingles:/bin/bash
userlimit?:8:800:(1000 user system):mnt/bin/false
villa?:26:883:Vanilla Account:mnt:/bin/sh
charon?:21:807:The Ferryman:/users/tomb
actmain?:23:809:Maintenance:/usr/adm/actmain:/bin/ksh
pop?:26:819:/usr/spool/pop:/bin/bash
ip?:70:10:Adminuniverse(at):/usr/spool/ip
trouble?:97:501:Report Facility:/usr/trouble:/usr/local/lib/ms
```

现在我使用 `grep` 来搜索包含零次或多次字母 `z` 的行：

```
% grep "z*" /etc/passwd | head
root:?:0:root:/bin/bash
news?:6:11:USENet News:/usr/spool/news:/bin/ksh
ingress?:7:59:INGRES Manager:/usr/ingles:/bin/bash
userlimit?:8:800:(1000 user system):mnt/bin/false
villa?:26:883:Vanilla Account:mnt:/bin/sh
charon?:21:807:The Ferryman:/users/tomb
actmain?:23:809:Maintenance:/usr/adm/actmain:/bin/ksh
pop?:26:819:/usr/spool/pop:/bin/bash
ip?:70:10:Adminuniverse(at):/usr/spool/ip
trouble?:97:501:Report Facility:/usr/trouble:/usr/local/lib/ms
Broken
```

结果与之前的命令相同，但这并不令人意料。如果只指定匹配一次或多次的行，输出结果会更像这样：

```
% grep "z+" /etc/passwd | head
marg?:7:1234:Guize:/users/marg:/bin/ksh
axy?:12:1223:martinez:/users/axy:/bin/ksh
whiz?:26:1975:Co:/users/wizard:/bin/ksh
zhq?:27:2377:Zhong:/users/zhq:/bin/ksh
mm?:7:1522:Michael Kennedy:/users/mm:/bin/ksh
tanzm?:7:1680:Zhen:/users/tanzm:/bin/ksh
mendoz?:7:8176:Don Mendoza:/users/mendoz:/bin/ksh
pavlk?:5:1476:Mary Li:/users/pavlk:/bin/ksh
hurli?:9:1989:Liz Hurley:/users/hurli:/bin/ksh
tulip?:9:2222:Liz Richards:/users/tulip:/bin/ksh
Broken
```

6. 早些我使用 `head` 来统计 `/etc/passwd` 文件中未指定登录标志的账户行数。文件中的每一行都有特定数量的冒号；而这些账户的行最后一个字符是冒号，因此可以使用简单的 `grep` 模式：

```
% grep ":$" /etc/passwd
charon?:21:807:The Ferryman:/users/tomb
ip?:70:10:System Adminuniverse(at):/usr/spool/ip:
```

7. 考虑一下这种情况：我的会计给我打来电话，我需要找到一个包含关于花费 100 美元现金购买软件消息的文件。我可以使用 `grep` 搜索所有包含美元符号 `$` 且后跟一个或多个零的文件：

```
% grep "$100" -*
Mail/bob_gate: Unfortunately, our fees are currently $100 per test drive, budgets
Mail/dan_monster:We also pay $100 for Test Drives, our very short "First Looks" section. We often
Mail/james:has been dropped, so if I ask for $1000 is that out way out
Mail/john_sprangens:time testing things since it's a $100 test drive: I'm willing to $100 for
Mail/john_sprangens: Finally, I'd like to request $200 rather than
Mail/mac:again:expected pricing will be $10,000 - $16,000 and the Britolite LX with promoted $1000 / month for a first
Mail/news_postings:Win Lose or Die, John Gardner (hardback) $10
Mail/news_postings:id would be paying, I dunno, $100 / year for the space? I would
Mail to panic that they'd want their $10K advance back, but the good news is
Mail/sent:Would be fine. How about $100 USD for both, to include any.
Mail/sent: Amount: $100.00
```

匹配项有很多。注意在匹配项中包含了 $1000。

早些我使用 `head` 来统计 `/etc/passwd` 文件中未指定登录标志的账户行数。文件中的每一行都有特定数量的冒号；而这些账户的行最后一个字符是冒号，因此可以使用简单的 `grep` 模式：

7. 考虑一下这种情况：我的会计给我打来电话，我需要找到一个包含关于花费 100 美元现金购买软件消息的文件。我可以使用 `grep` 搜索所有包含美元符号 `$` 且后跟一个或多个零的文件：

