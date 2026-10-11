

## 表 10.1 NT4 域 V 的 Samba 策略控制项

| NT4 策略名称 | Samba 策略名称 | NT4 范围 | Samba 范围 | Samba 默认值 |
| :--- | :--- | :--- | :--- | :--- |
| 最大密码有效期 | maximum password age | 0 - 999 (天) | 0 - 4294967295 (秒) | 4294967295 |
| 最小密码有效期 | minimum password age | 0 - 999 (天) | 0 - 4294967295 (秒) | 0 |
| 最小密码长度 | min password length | 1 - 14 (字符) | 0 - 4294967295 (字符) | 5 |
| 密码唯一性 | password history | 0 - 23 (个) | 0 - 4294967295 (个) | 0 |
| 账户锁定 - 重置计数后 | reset count minutes | 1 - 99998 (分钟) | 0 - 4294967295 (分钟) | 30 |
| 登录失败次数达到锁定阈值 | bad lockout attempt | 0 - 998 (次) | 0 - 4294967295 (次) | 0 |
| *** 未知 *** | disconnect time | 待定 | 0 - 4294967295 | 0 |
| 锁定时长 | lockout duration | 1 - 99998 (分钟) | 0 - 4294967295 (分钟) | 30 |
| 用户必须登录以更改密码 | user must logon to change password | 0/1 | 0 - 4294967295 | 0 |
| *** 注册表设置 *** | refuse machine password change | 0/1 | 0 - 4294967295 | 0 |

由于创建用户账户被视为系统管理员的职责，因此 Samba 不会向操作系统请求创建用户账户。当使用 Windows NT4 域用户管理器添加账户时，Samba 将实现 **add user script**（以及其他接口脚本），以确保用户、组和机器账户被正确创建和更改。**pdbedit** 工具的使用不会调用这些接口脚本。

在尝试使用 **pdbedit** 工具管理用户和机器账户之前，请确保已经创建了系统（POSIX）账户。

### 列示用户和机器账户

以下示例展示了存储在 tdbssam 密码后端中的用户账户信息。此列表是通过运行以下命令生成的：

```
$ pdbedit -Lv
UNIX username:    met
NT username:        met
Account Flags:      [U               ]
User SID: S-1-5-21-1449123459-1407424037-3116680435-2004
Primary Group SID: S-1-5-21-1449123459-1407424037-3116680435-1201
Full Name:        Melissa E Terpstra
Home Directory: \\frod\met\Win95Profile
HomeDir Drive: H:
Login Script:  scripts\logon.bat
Profile Path: \\frod\Profiles\met
Domain:        MIDEARTH
Account desc:
Workstations:        melbelle
Munged dial:

Login time: 0
Logoff time: Mon, 18 Jan 2038 20:14:07 GMT
Kickoff time: Mon, 18 Jan 2038 20:14:07 GMT
Password last set: Sat, 14 Dec 2002 14:37:03 GMT
Password can change: Sat, 14 Dec 2002 14:37:03 GMT
Password must change: Mon, 18 Jan 2038 20:14:07 GMT
```

账户也可以以旧式的 smbpasswd 格式列示：

```
root# pdbedit -Lw
root:0:84B0DBE14D158FF8417EAF50FCAF29C3:
AF6D3DFDAE2EA8BDE1695A3F05E5FBF52:[U] ]:LCT-42681A88:
jht:1000:6B8C415902A052741486235A2333BA8D2:
CC099521AD564A3F255CF2556274DBCFBC:[U] ]:LCT-40D75B5B:
rcg:1002:E95D4331A6F33FAA8AD3B43B551404EE:
EB0FC2939B04C46100FE535DF933144CB:
CE92C2F9471594CCDC4E7860CA6BCB62D8:[T ]:LCT-40DA501F:
met:1004:A28485E3A76B43A5DA3B43355A144EE:
F25F5D34505085C55E236B80BTB22C0D2:[U ]:LCT-4244FA8B:
auroa$:1005:06DDE59EA3E3B88ACCAA419F14D2FF2B:
06DDE59AE3A3B88ACCAA419F14D2FF2B:[W ]:LCT-41735CEC:
temptation$::1006:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:
A96703C014E4040433D4049F706C45E9:[W ]:LCT-42BFC057:
valbos$::1001:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:
88A30A0595160072784C88FF811E899A94:[W ]:LCT-41C38780:
frod$:1008:15891DC6B843E3CA12A994C0834E316B:
B68EADCC18B1E75033D4D3E6B0B9A7A5:[W ]:LCT-42F7979F:
marvel$:1011:BF709959C3C94E0B395B87B843B8B6F3:
C610EFEA3365A3E8AA46A6DF576E6881:[W ]:LCT-40F07A4
```

### 添加用户账户

可以使用 pdbedit 将用户账户添加到独立服务器或域中。在本文所示的示例中，在尝试添加 SambaSAMAccount 之前，已先为用户 vlaan 创建了账户。

```
root#  pdbedit -a
new password: secretpw
retype new password: secretpw
Unix username:      vlaan
NT username:        vlaan
Account Flags:      [U          ]
User SID:           S-1-5-21-726309263-4128913605-1168186429-3014
Primary Group SID:  S-1-5-21-726309263-4128913605-1168186429-513
Full Name:
Home Directory:     \\frodo\vlaan
HomeDir Drive:      H:
Logon Script:       scripts\logon.bat
Profile Path:       \\frodo\profiles\vlaan
Domain:             MIDEARTH
Account desc:       Guest User
Workstations:
Munged dial:
Logon time:         0
Logoff time:        Mon, 18 Jan 2038 20:14:07 GMT
Kickoff time:       Mon, 18 Jan 2038 20:14:07 GMT
Password last set:  Wed, 29 Jun 2005 19:35:12 GMT
Password can change: Wed, 29 Jun 2005 19:35:12 GMT
Password must change: Mon, 18 Jan 2038 20:14:07 GMT
Last bad password  : 0
Bad password count : 0
Logon hours          FFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF
```

### 删除账户

可以从 SambaSAMAccount 数据库中删除账户。

```
root#  pdbedit -x vlaan
```

账户将被移除，且没有进一步的屏幕输出。该账户仅从 SambaSAMAccount (passdb) 后端数据库中移除，并不会从 UNIX 账户后端中移除。

使用 NT4 域用户管理器删除账户会触发 delete user 脚本，但使用 pdbedit 工具则不会。

### 修改用户账户

有关此工具支持的所有操作的完整说明，请参考 `pdbedit` 手册页。

修改用户账户信息的一个简单示例是更改此处显示的全名信息：

```
root# pdbedit -r --fullname="Victor Aluicious Laan" vlaan
 ...
Primary Group SID: S-1-5-21-726309263-4128913605-1168186429-513
Full Name: Victor Aluicious Laan
Home Directory: \\frodo\vlaan
...
```

让我们假设某用户的密码已过期，且该用户目前无法更改密码。可能必须给予用户额外的宽限期，以便可以使用该账户及原密码继续工作。此处展示了如何更新密码过期设置

```
root# pdbedit -L vlaan
 ...
Password last set: Sun, 09 Sep 2001 22:21:40 GMT
Password can change: Thu, 03 Jan 2002 15:08:35 GMT
Password must change: Thu, 03 Jan 2002 15:08:35 GMT
Last bad password : Thu, 03 Jan 2002 15:08:35 GMT
Bad password count : 2
...
```

该用户已记录 2 次失败的登录尝试，下一次将导致账户被锁定。但密码也已过期。以下是重置该账户的方法：

```
root# pdbedit -z vlaan
 ...
Password last set: Sun, 09 Sep 2001 22:21:40 GMT
Password can change: Thu, 03 Jan 2002 15:08:35 GMT
Password must change: Thu, 03 Jan 2002 15:08:35 GMT
Last bad password : 0
Bad password count : 0
...
```

“Password must change:” 参数可以像这样重置：

```
root# pdbedit --pwd-must-change-time=1200000000 vlaan
 ...
Password last set: Sun, 09 Sep 2001 22:21:40 GMT
Password can change: Thu, 03 Jan 2002 15:08:35 GMT
Password must change: Thu, 10 Jan 2008 14:20:00 GMT
...
```

使用此工具的另一种方法是像这样设置日期：

```
root# pdbedit -pwd-must-change-time="2010-01-01" \
-time-format="%Y-%m-%d" vlaan 
...
Password last set: Sun, 09 Sep 2001 22:21:40 GMT
Password can change: Thu, 03 Jan 2002 15:08:35 GMT
Password must change: Fri, 01 Jan 2010 00:00:00 GMT
...
```

有关具体时间格式的信息，请参考 strtptime 手册页。
有关 SambaSAMAccount 管理的更多信息，请参考 pdbedit 手册页。

### 域账户策略管理

要查看可配置的域账户访问策略，请执行以下命令：

```
root# pdbedit -P ? 
No account policy by that name 
Account policy names are : 
min password length 
password history 
user must logon to change password 
maximum password age 
minimum password age 
lockout duration 
reset count minutes 
bad lockout attemp 
disconnect time 
refuse machine password change 
```

将执行以下命令为我们的域建立控制：

1. 最小密码长度 = 8 个字符。
2. 密码历史 = 最近 4 个密码。
3. 最大密码有效期 = 90 天。
4. 最小密码有效期 = 7 天。
5. 登录失败锁定尝试次数 = 8 次失败登录。

