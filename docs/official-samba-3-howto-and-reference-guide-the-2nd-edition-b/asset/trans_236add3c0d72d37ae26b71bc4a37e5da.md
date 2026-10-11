
## 8. 以 maryl 身份连接到 OLORIN

```
root# smbclient //olorin/maryo -Umaryo%secret
OS=[UNIX] Server=[Samba-3.0.20]
smb: \> dir
.			D		0	Sat Jun 21 10:58:16 2003
..			D		0	Sat Jun 21 10:54:32 2003
Documents		D		0	Fri Apr 25 13:23:58 2003
DOCWORK		D		0	Sat Jun 14 15:40:34 2003
OpenOffice.org	D		0	Fri Apr 25 13:55:16 2003
.bashrc		H		1286	Fri Apr 25 13:23:58 2003
.ncbrowser6	DH		0	Fri Apr 25 13:55:13 2003
.mozilla		DH		0	Wed Mar 5 11:50:50 2003
.kde		H		164	Fri Apr 25 13:23:58 2003
.acrobat		DH		0	Fri Apr 25 15:41:02 2003

				55817 blocks of size 524288. 34725 blocks available
smb: \> q
```

到此时，你应该已经掌握了配置的基础。显然，是时候探索一些稍复杂的示例了。由于前文已有示例，本章剩余部分的指令将作简略处理。

### 2.3.2 域成员服务器

在本例中，我们考虑一种最简单的服务器配置，以便让会计部门满意。警告一下，这些用户是会计师，他们有一些苛刻的要求。该部门的预算只够购买一台服务器。

网络由内部信息服务组（ISG）管理，我们隶属于该组。内部政策通常是中等规模组织的典型情况：人力资源部门认为他们控制着 ISG，因为他们总是在添加和禁用用户。此外，各部门经理不得不费尽周折才能让员工获得基本的网络资源访问权限。不过会计部门不同，他们总能得到想要的东西。所以，这就是场景设置。

我们使用上一个示例中的用户。会计部门有一台通用打印机，所有部门用户均可使用。还有一台主管打印机，只有拥有支票打印权限的人才能使用。首席财务官（CFO）希望将该打印机完全限制访问，并将其放置在她办公室的私密存储区域。因此，它必须是一台网络打印机。

会计部门使用一个名为 SpydFull 的会计应用程序，该应用必须从中央应用服务器运行。该软件许可证仅允许在一台服务器上运行，没有工作站组件，并且通过映射共享运行。数据存储位于基于 UNIX 的 SQL 后端。UNIX 专家负责维护该部分，因此这不是我们的问题。

会计部门经理（maryo）希望建立一个通用文件共享系统，以及一个独立的文件存储区域用于信函（mustygrams）。信函存储区域对除经理外的所有会计员工应为只读。通用文件共享系统必须具备结构化布局，包括供所有员工存放通用文档的公共区域，以及供团队每位成员私人使用的独立文件区域，但她希望拥有所有区域的完全访问权限。用户必须有一个私人的主目录共享，用于存放与工作相关的个人文件以及非部门业务相关的材料。

#### 2.3.2.1 示例配置

服务器 valinor 将是公司域的成员服务器。会计部门将只有一台本地服务器。用户账户将位于域控制器上，桌面配置文件和所有网络策略文件也是如此。

```
Example 2.3.5 Member Server smb.conf (Globals)

# Global parameters
[global]
        workgroup = MIDEARTH
        netbios name = VALINOR
        security = DOMAIN
        printcap name = cups
        disable spoolss = Yes
        show add printer wizard = No
        idmap uid = 15000--20000
        idmap gid = 15000--20000
        winbind use default domain = Yes
        printing = cups
```

- 1. 不要将用户添加到 UNIX/Linux 服务器；所有这些都将在中央域上运行。
- 2. 根据示例 2.3.5 和示例 2.3.6 配置 **smb.conf**。

```
Example 2.3.6 Member Server smb.conf (Shares and Services)

[homes]
comment = Home Directories
valid users = %S
read only = No
browseable = No

[spyfull]
comment = Accounting Application Only
path = /export/spyfull
valid users = @Accounts
admin users = maryo
read only = Yes

[public]
comment = Data
path = /export/public
read only = No

[printers]
comment = All Printers
path = /var/spool/samba
printer admin = root, maryo
create mask = 0600
guest ok = Yes
printable = Yes
use client driver = Yes
browseable = No
```

- 3. 加入域。注意：在此步骤完成之前，不要启动 Samba！

```
root# net rpc join -Uroot%'bigsecret'
Joined domain MIDEARTH.
```

- 4. 务必确保在配置了 `winbind` 运行的任何系统上都禁用（关闭）`nscd` 守护进程。
- 5. 按照操作系统的正常方法启动 Samba。如果希望手动执行，请以 root 身份执行以下命令：

```
root# nmbd; smbd; winbind;
```

- 6. 配置系统的名称服务切换（NSS）控制文件，以通过 winbind 解析用户和组名。编辑 `/etc/nsswitch.conf` 中的以下行：

```
passwd: files winbind
group: files winbind
hosts: files dns winbind
```

- 7. 设置 **winbind** 使用的密码：

```
root# wbinfo --set-auth-user=root\'bigsecret'
```

- 8. 执行以下命令以验证域用户和组凭据能否正确解析：

```
root# wbinfo -u
MIDEARTH\\maryo
MIDEARTH\\jackb
MIDEARTH\\ameds
...
MIDEARTH\\root
```

```
root# wbinfo -g
MIDEARTH\\Domain Users
MIDEARTH\\Domain Admins
MIDEARTH\\Domain Guests
...
MIDEARTH\\Accounts
```

- 9. 检查 **winbind** 是否正常工作。以下示例展示了通过 **getent** 系统实用程序正确解析用户名的过程：

```
root# getent passwd mario
maro:x:15000:15003:Mary Urville:/home/MIDEARTH/mario:/bin/false
```

- 10. 最后，进行一项测试以确认我们已掌控局面可能会令人安心：

```
root# touch /export/a_file
root# chown mario /export/a_file
root# ls -al /export/a_file
...
-rw-r--r-- 1 mario users 11234 Jun 21 15:32 a_file
...
```

- 11. 配置现已基本完成，因此这是配置该站点目录结构的合适时机：

```
root# mkdir -p /export/{spyfull,public}
root# chmod ug=rwxS,o=rx /export/{spyfull,public}
root# chown maryo.Accounts /export/{spyfull,public}
```

### 2.3.3 域控制器

本章剩余部分的重点是域控制器的配置。接下来的示例针对两种实施策略。请记住，我们的目标是创建一个简单但可用的解决方案。本书剩余部分应有助于突出增强功能的机会及其随之而来的复杂性。

域控制器配置可以通过使用新的 tdbsam 密码后端进行简单配置来实现。这种类型的配置适合小型办公室，但可扩展性有限（无法复制），随着域规模和复杂性的增加，性能预计会下降。

tdbsam 的使用最好限于不需要多于一个主域控制器（PDC）的站点。随着域规模的扩大，对额外域控制器的需求变得明显。不要尝试在资源不足的 Microsoft Windows 网络环境中部署；域控制器提供必要的认证服务。以下是资源不足的域控制环境的症状：

- 域登录间歇性失败。
- 域成员服务器上的文件访问间歇性失败，给出权限被拒绝的错误消息。

更具可扩展性的域控制认证后端选项可能会使用 Microsoft Active Directory 或基于 LDAP 的后端。Samba-3 作为域成员服务器提供了这两种选项。作为 PDC，Samba-3 无法提供与 Active Directory 功能完全相同的替代方案。Samba-3 可以提供可扩展的基于 LDAP 的 PDC/BDC 解决方案。

tdbsam 认证后端不提供复制数据库内容的功能，除了通过外部手段（即，Samba-3 中没有用于安全管理器数据库 [SAM] 复制的自包含协议）。

> **注意**
> 如果需要多于一个域控制器，请勿使用 tdbsam 认证后端。

