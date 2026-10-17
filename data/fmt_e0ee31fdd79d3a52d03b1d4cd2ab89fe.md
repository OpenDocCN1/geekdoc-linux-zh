
## 第 8 章：密码破解

### 301

`/etc/shadow` 中的字段代表：

- 用户名
- 加密密码
- 自 1970 年 1 月 1 日以来上次更改密码的经过数
- 用户允许更改密码的剩余天数
- 用户必须更改密码的剩余天数
- 在用户必须更改密码前提前警告的天数
- 用户更改密码或账户被禁用的剩余天数
- 一个预留字段

要显示 `/etc/shadow` 文件仅对 `root` 用户可读：

```
$jdoe$ ls -l /etc/passwd /etc/shadow

-rw-r--r-- 1 root 842 Sep 12 16:24 /etc/passwd
r-------- 1 root 759 Sep 12 16:24 /etc/shadow
```

如你所见，`/etc/shadow` 不仅向未经授权的用户隐藏了加密密码，使得字典攻击变得非常困难，它还包含了用于密码维护的信息。

在当今敌对的网络环境中，密码影子是至关重要的，大多数 Linux 发行版都支持影子机制。如果你当前的 Linux 机器已经实现了影子机制，你应该现在就转换为影子密码。

#### 启用影子密码

启用密码影子仅仅是运行 Linux 机器已安装的几个系统程序。以下步骤描述了如何将未实现影子密码的机器转换为已实现的。

#### `pwck` 检查 `/etc/passwd` 的完整性

首先，运行 `pwck` 来验证 `/etc/passwd` 的完整性。`/etc/passwd` 中的每个条目都会被检查是否遵循正确的格式，以及每个字段是否有有效数据。`pwck` 程序验证：

- 正确的字段数量
- 唯一的用户名
- 有效的用户和组
- 有效的主组
- 有效的主目录
- 有效的登录 shell

```
~/root]# pwck

user adm: directory /var/adm does not exist
user gopher: directory /usr/lib/gopher-data does not exist
user gdm: directory /home/gdm does not exist
```

#### `pwconv` 转换为影子密码

接下来，运行 `pwconv` 将 `/etc/passwd` 转换为影子密码。它从现有的 `/etc/passwd` 创建了 `/etc/shadow` 文件。

```
~/root]# pwconv
```

恭喜，你现在已经通过 `/etc/shadow` 使用了影子密码。你可以通过检查 `/etc/shadow` 内容来验证转换是否成功。

```
~/root]# pwck
```

#### `pwunconv` 移除影子密码

如果需要，运行 `pwunconv` 将影子密码转换回并写入 `/etc/passwd`。

#### `chage` 命令

使用 `chage` 是为了管理密码过期信息。在影子系统中管理影子密码最重要的命令是 `chage`。它用于确保用户必须更改密码。

```
~/root]# chage
```

- `mindays`: 密码更改的最小天数
- `maxdays`: 密码有效的最大天数
- `lastday`: 自 1970 年 1 月 1 日以来上次更改密码的经过天数
- `inactive`: 密码过期后账户被禁用的天数
- `expiredate`: 密码必须更改的日期
- `warndays`: 在用户必须更改密码前警告的提前数

#### 其他实用的命令

影子工具中有很多命令。这里是常用命令总结：

- `passwd`: 将用户添加到组。
- `groupadd`: 创建组。
- `groupdel`: 删除组。
- `groupmod`: 修改组信息。
- `passwd`: 与 `/etc/passwd` 工作。
- `useradd`: 添加新用户。
- `userdel`: 删除用户。
- `usermod`: 修改用户信息。

#### APACHE 密码文件

使用 Apache 服务器，可以通过 `http` 保护部分内容（见第 12 章）。认证需要用户名和密码。这些用户名/密码值通常存储在名为 `passwd` 的文件中。

注意 Apache 也可以使用外部数据库，如 Oracle 或 LDAP。

文件的每一行都是由冒号分隔的用户名和加密密码。这些 Apache 密码文件可能使用 DES 或 MD5。

#### 304 Linux 破解：Linux 安全秘密与解决方案

这是一个使用 DES 的 Apache 认证文件示例：

```
al:/fOtYdf.SNqv6
george:280VwwBMRog
tcm:wNVFNEB2FXw
jerry:ultdpMRYky9
```

这是一个使用 MD5 的示例：

```
al:$apr1RawP..$GYwhLLC7Z09Na2u1Ypl
george:$apr1SNBJR..$CycN73KDFmYLOEc2c/
tcm:$apr1S451IT..$DwaASDc065Ne3Ilhb1
jerry:$apr1S82..$J9516u7
```
