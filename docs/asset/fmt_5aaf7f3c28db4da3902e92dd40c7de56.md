
由于作为超级用户可能会犯灾难性错误，请始终作为普通用户使用系统，仅临时使用你的超级权限执行特定的管理任务。在 Ubuntu 中更容易这一点，因为默认使用 `sudo` 且 `root` 账户最初是禁用的。如果你在一个多用户系统上，请将此建议视为绝对法则；如果 `root` 删错了文件或杀掉了进程，结果对系统可能是灾难性的。

第三种类型的用户是系统用户。系统用户不是人，而是系统在日常运行各种服务时使用的管理账户。例如，系统用户 `www-data` 拥有 Apache Web 服务器以及所有的

## 第 11 章 管理用户

关联文件。只有该用户和 `root` 用户可以访问这些文件；其他人无法访问或更改这些文件。系统用户没有主目录或密码，也不允许通过登录提示访问系统。

你可以在 `/etc/passwd` 文件中找到系统上所有用户的列表。

### 用户 ID 和组 ID

计算机从本质上说是一台面向对象的机器。它通过被称为用户 ID (`UID`) 和组 ID (`GID`) 的数字来识别用户和组。为了方便使用，屏幕上显示的是字母名称。

如前所述，`root` 用户的 `UID` 为 `0`。数字从 `1` 到 `499` 的数字以及数字 `65,534` 是系统用户，有时也称为本地用户或伪用户。普通用户的 `UID` 从 `1,000` 开始；Ubuntu 从该数字开始顺序地分配它们。

除少数例外外，`GID` 与 `UID` 相同。

Ubuntu 会为每个大于或等于 `1,000` 的 `UID` 创建一个私有的 `GID`。系统管理员可以将其他用户添加到 `GID` 中，或者创建一个全新的组并将用户添加到组中。与 Windows NT 和某些 Unix 变体不同，在 Ubuntu（或任何 Linux 发行版）中，组不能成为另一个组的成员。

### 文件权限

正如第 3 章“在网上”中所学的，权限三种：读、写和执行 (`r`, `w`, `x`)。对于任何文件或目录，权限分配给三类对象：用户、组和其他。本节重点关注组权限。不过，我们想强调三个更改文件或目录的组、用户或访问权限的命令：

- `chgrp`—更改文件或目录的组所有
- `chown`—更改文件或目录的所有者
- `chmod`—更改文件或目录的访问权限

你可以使用这些命令在你的 Ubuntu 系统中重现现实世界的组织结构和权限（下一节，“管理组”）。例如，人力资源部门可以通过将可访问目录中的文件设为任何人都可读（但不可写）来向所有员工共享健康福利备忘录。公司研发部门的程序员虽然可以访问彼此的源代码文件，但对 HR 薪资或人事文件没有读取或写入权限（显然也不希望 HR 或市场部插手研发工作）。

这些命令用于从命令行易用地管理组和文件所有权及权限。了解这些命令至关重要，因为有时你可能只有命令行界面可以使用，例如当一个心意良好但手指手抖的系统管理员为 X11 设置了错误的权限，导致系统无法通过图形界面工作。（不，我们不会讲那个故事，但如果你按过那些键，大多数系统管理员都有类似的惨经历。）

### 用户刻板印象

正如许多职业一样，对于用户和系统管理员也出现了夸张的刻板印象。许多刻板印象包含真实的元素，并夹杂着大量的幽默，以帮助我们理解这些刻板印象对象的特征和差异。用户和 BOFH（分别是对用户和管理员的不友好的术语）的刻板印象作为警示案例，描述了计算环境中哪些行为是可以接受的，哪些是不可接受的。

理解这些刻板印象让你能够更好地定义系统管理员、用户和其他人的恰当角色。你可以在 Wikipedia 上找到每个人的描述，网址为 http://en.wikipedia.org/wiki/BOFH 和 http://en.wikipedia.org/wiki/Luser。

### 管理组

组可以让用户管理变得简单得多。不需要为每个用户分配单独权限，你可以使用组快速快捷地为大量用户授予或撤销权限。设置组权限允许你为协作工作设置工作空间，并控制可以使用哪些设备，如外部驱动器或 DVD 刻录机。这种方法也是将系统资源访问限制为仅需要的人的安全方法。例如，系统管理员可以将 Matthew、Ryan、Heather、Holly、Debra 等用户放在一个名为 `unleashed` 的新组中。这些用户可以各自为他们的组创建文件，并将这些文件 `chgrp` 到 `unleashed`。

现在，`unleashed` 组中的每个人（但除了 `root` 之外没有其他人）都可以处理这些文件。系统管理员可能会有一个易于访问的地方来存储这些文件。系统管理员可以将 Chris 和 Shannon 等其他用户添加到该组，并在他们完成部分工作后移除现有用户。系统管理员可以将该用户设为组管理员，这样 Matthew 就可以决定如何更改组成员身份了。你还可以对 DVD 刻录机设置限制，只有 Matthew 可以刻录 DVD，从而防止敏感材料落入坏人手中。

#### 组列表

不同的 UNIX 操作系统以各种方式实现组的概念。Ubuntu 使用一种名为 UPG（用户组）的方案，默认情况下，所有用户都被分配到一个与其名字同名的组（用户的用户名和组名相同）。系统上所有的组都列在 `/etc/group` 文件中。

这里是 `/etc/group` 文件部分的示例：

```
matthew@semour:-$ cat /etc/group
root:x:0
demon:x:1
bin:x:2
sys:x:3
adm:x:4:matthew
tty:x:5
disk:x:6
mail:x:8
news:x:9
fax:x:21:matthew
voice:x:22
cdrom:x:24:matthew
floppy:x:25:matthew
tape:x:26:matthew
www-data:x:33
system:x:42
backup:x:44:matthew
list:x:45:matthew
irc:x:46:matthew
plugdev:x:47:matthew
scanner:x:48:matthew
cdrom:x:24:matthew
audio:x:29:matthew
video:x:44:matthew
dialout:x:20:matthew
lp:x:21:matthew
samb:x:38:matthew
dev:x:54
games:x:56
users:x:57:matthew
scanner:x:58:matthew
slu:x:59:matthew
message:x:60:matthew
operator:x:81:matthew
nobody:x:65534
system:x:3
matthew
bdd:x:99:matthew
sudo:x:27:matthew
u:x:100:matthew
u:x:101:matthew
u:x:102:matthew
u:x:103:matthew
u:x:104:matthew
u:x:105:matthew
u:x:106:matthew
u:x:107:matthew
u:x:108:matthew
u:x:109:matthew
u:x:110:matthew
u:x:111:matthew
u:x:112:matthew
u:x:113:matthew
u:x:114:matthew
u:x:115:matthew
u:x:116:matthew
u:x:117:matthew
u:x:118:matthew
u:x:119:matthew
u:x:120:matthew
u:x:121:matthew
u:x:122:matthew
u:x:123:matthew
u:x:124:matthew
u:x:125:matthew
u:x:126:matthew
u:x:127:matthew
u:x:128:matthew
u:x:129:matthew
u:x:130:matthew
u:x:131:matthew
u:x:132:matthew
u:x:133:matthew
u:x:134:matthew
u:x:135:matthew
u:x:136:matthew
u:x:137:matthew
u:x:138:matthew
u:x:139:matthew
u:x:140:matthew
u:x:141:matthew
u:x:142:matthew
u:x:143:matthew
u:x:144:matthew
u:x:145:matthew
u:x:146:matthew
u:x:147:matthew
u:x:148:matthew
u:x:149:matthew
u:x:150:matthew
u:x:151:matthew
u:x:152:matthew
u:x:153:matthew
u:x:154:matthew
u:x:155:matthew
u:x:156:matthew
u:x:157:matthew
u:x:158:matthew
u:x:159:matthew
u:x:160:matthew
u:x:161:matthew
u:x:162:matthew
u:x:163:matthew
u:x:164:matthew
u:x:165:matthew
u:x:166:matthew
u:x:167:matthew
u:x:168:matthew
u:x:169:matthew
u:x:170:matthew
u:x:171:matthew
u:x:172:matthew
u:x:173:matthew
u:x:174:matthew
u:x:175:matthew
u:x:176:matthew
u:x:177:matthew
u:x:178:matthew
u:x:179:matthew
u:x:180:matthew
u:x:181:matthew
u:x:182:matthew
u:x:183:matthew
u:x:184:matthew
u:x:185:matthew
u:x:186:matthew
u:x:187:matthew
u:x:188:matthew
u:x:189:matthew
u:x:190:matthew
u:x:191:matthew
u:x:192:matthew
u:x:193:matthew
u:x:194:matthew
u:x:195:matthew
u:x:196:matthew
u:x:197:matthew
u:x:198:matthew
u:x:199:matthew
u:x:200:matthew
u:x:201:matthew
u:x:202:matthew
u:x:203:matthew
u:x:204:matthew
u:x:205:matthew
u:x:206:matthew
u:x:207:matthew
u:x:208:matthew
u:x:209:matthew
u:x:210:matthew
u:x:211:matthew
u:x:212:matthew
u:x:213:matthew
u:x:214:matthew
u:x:215:matthew
u:x:216:matthew
u:x:217:matthew
u:x:218:matthew
u:x:219:matthew
u:x:220:matthew
u:x:221:matthew
u:x:222:matthew
u:x:223:matthew
u:x:224:matthew
u:x:225:matthew
u:x:226:matthew
u:x:227:matthew
u:x:228:matthew
u:x:229:matthew
u:x:230:matthew
u:x:231:matthew
u:x:232:matthew
u:x:233:matthew
u:x:234:matthew
u:x:235:matthew
u:x:236:matthew
u:x:237:matthew
u:x:238:matthew
u:x:239:matthew
u:x:240:matthew
u:x:241:matthew
u:x:242:matthew
u:x:243:matthew
u:x:244:matthew
u:x:245:matthew
u:x:246:matthew
u:x:247:matthew
u:x:248:matthew
u:x:249:matthew
u:x:250:matthew
u:x:251:matthew
u:x:252:matthew
u:x:253:matthew
u:x:254:matthew
u:x:255:matthew
u:x:256:matthew
u:x:257:matthew
u:x:258:matthew
u:x:259:matthew
u:x:260:matthew
u:x:261:matthew
u:x:262:matthew
u:x:263:matthew
u:x:264:matthew
u:x:265:matthew
u:x:266:matthew
u:x:267:matthew
u:x:268:matthew
u:x:269:matthew
u:x:270:matthew
u:x:271:matthew
u:x:272:matthew
u:x:273:matthew
u:x:274:matthew
u:x:275:matthew
u:x:276:matthew
u:x:277:matthew
u:x:278:matthew
u:x:279:matthew
u:x:280:matthew
u:x:281:matthew
u:x:282:matthew
u:x:283:matthew
u:x:284:matthew
u:x:285:matthew
u:x:286:matthew
u:x:287:matthew
u:x:288:matthew
u:x:289:matthew
u:x:290:matthew
u:x:291:matthew
u:x:292:matthew
u:x:293:matthew
u:x:294:matthew
u:x:295:matthew
u:x:296:matthew
u:x:297:matthew
u:x:298:matthew
u:x:299:matthew
```

#### 组管理工具

Ubuntu 提供了几个管理组的命令行工具，但也提供了执行此操作的图形工具。大多数丰富的系统管理员倾向于使用命令行工具，因为它们快速易用，在没有图形界面时始终可用，并且可以包含在脚本中。

- `groupadd`—此命令创建一个新组。
- `groupdel`—此命令删除一个现有组。
- `groupmod`—此命令创建组名或 GIDs，但不添加或删除组中的成员。
- `gpasswd`—此命令创建组密码。每个组都可以有一个密码和一个管理员。`-A` 参数允许将用户指定为组管理员。
- `useradd`—`-G` 参数允许在创建用户时将用户分配到组（更多参数用于创建用户）。
- `usermod`—此命令允许你将用户添加到组，只要该用户此时未登录。
- `grck`—此命令检查 `/etc/group` 文件中的拼写错误。

假设我们的计算机上有一个 DVD 刻录设备（`/dev/scd0`），管理员要授予一个名为 Ryan 的普通用户访问权限。以下是授予 Ryan 该访问权限的过程：

1. 使用 `groupadd` 命令创建一个新组：

```
matthew@seymour:- sudo groupadd dvdwr
```

2. 使用 `chgrp` 命令将设备的组所有更改新组：

```
matthew@seymour:- sudo chgrp dvdwr /dev/scd0
```

3. 使用 `usermod` 命令将批准的用户添加到组：

```
matthew@seymour:- sudo usermod -G dvdwr ryan
```

4. 使用 `gpasswd` 命令将用户 Ryan 变为组管理员，这样他就可以向组添加用户了：

```
matthew@seymour:- sudo gpasswd -A ryan
```

现在 Ryan 有权使用 DVD 刻录驱动器，任何超级用户或 Ryan 添加到该组的其他人也可以使用，因为 Ryan 现在也是组管理员，并可以向组添加用户。

# 216 第11章 管理用户

![](img/71b571561538b2a14c3bd347f4fcb569_247_0.png)

图 11.1 使用“管理组”将用户分配到组。

注意，图形界面无法提供完整的组命令和选项。这限制了 GUI 的实用性，使其仅存在于最常用命令的子集。你将在本章的下一节中学习更多关于使用 Ubuntu 用户管理器 GUI 的知识。

### 管理用户

必须创建用户、分配 UID、提供 `/home` 目录、为其家目录提供一组初始文件，并将其分配到组，以便他们安全高效地使用系统资源。在某些情况下，系统管理员可能想要或需要限制用户对特定文件和文件夹的访问，还要限制账户可能使用的磁盘空间。

#### 用户管理工具

与组一样，Ubuntu 提供了几个命令行工具来管理用户，但也提供了图形化工具来进行此操作。大多数经验丰富的管理员倾向于使用命令行工具，因为它们快速易用，即使在没有 GUI 的情况下也可用，并且可以包含在系统管理员编写的用于执行重复任务的快速脚本中。以下是管理用户最常用的命令：

- `useradd`—此命令向系统添加新用户账户。其选项允许系统管理员指定用户的 `/home` 目录和初始组，或者使用默认的 `/home` 目录和组分配创建用户（基于新账户的用户名）。
- `useradd -D`—此命令设置创建用户的 `/home` 目录、账户过期日期、默认组和命令 shell 的系统默认值。请参 `useradd` 页面中的特定选项。在不带任何参数的情况下，它会显示系统默认值。用户的默认文件集位于 `/etc/skel`。

> 注意
> 最初用于填充新用户家目录的文件集保存在 `/etc/skel` 中。这对于系统管理员来说非常方便，因为任何需要通用放置在 `/etc/skel` 中的特殊文件或目录都会自动为每个新用户复制，并赋予适当的权限：

```
mathew@semour:-$ ls -la /etc/skel

total 32

drwr-xr-x 2 root 4096 2010-04-25 12:14

drwr-xr-x 154 2 root 12888 2010-07-01 16:30

-rw-r---- 1 root 220 2020-09-13 22:08 .bash_logout

-rw-r-- 1 root 3103 2010-04-18 19:15 .bashrc

-rw-r-- 1 root 179 2019-03-26 05:31 examples.desktop
```
