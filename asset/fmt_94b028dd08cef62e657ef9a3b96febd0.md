
## 6.3 必要知识

```text
PASS_MAX_DAYS 99999 # 密码的最大天数
PASS_MIN_DAYS 0 # 密码的最少天数
PASS_MIN_LEN 5 # 密码最小长度
PASS_WARN_AGE 7 # 密码警告天数

UID_MIN 1000 # 普通用户最小UID
UID_MAX 60000 # 普通用户最大UID
SYS_UID_MIN 201 # 系统用户最小UID
SYS_UID_MAX 999 # 系统用户最大UID

GID_MIN 1000 # 自动创建普通用户主的最小GID
GID_MAX 60000 # 自动创建普通用户主的最大GID
SYS_GID_MIN 201 # 自动创建时自动的最小GID
SYS_GID_MAX 999 # 自动创建时自动的最大GID

CREATE_HOME yes # 是否创建用户目录
UMASK 077 # 创建用户的默认 umask 值(任务4的知识点6)

USERGROUPS_ENABLE yes # 允许 userdel 删除用户时删除其主组，如组中没有其他用户存在
ENCRYPT_METHOD SHA512 # 指定用户密码加密算法
```

`/etc/skel` 目录，该目录的文件合法框架，这个目录由 `root` 用户控制，使用 `useradd` 命令添加用户，默认情况下 `/etc/skel` 目录下的文件会自动复制新添加的用户目录下的文件。一个典型的 `/etc/skel` 目录下的文件会有若干隐藏文件，这些文件都是 shell 或者应用程序的配置文件。

6-26. 可以通过添加、删除 `/etc/skel` 目录下的文件，为用户提供统一的、标准的、默认用户环境。

```bash
$ ls -al /etc/skel
总容量 24
dwxr-xr-x. 3 root 78 4 11 2018 .
drwxr-xr-x. 14 root 8192 2 12 19:24 ..
-rw-r--r-- 1 root 18 4 11 2018 .bash_logout
-rw-r--r-- 1 root 193 4 11 2018 .bash_profile
-rw-r--r-- 1 root 231 4 11 2018 .bashrc
drwxr-xr-x. 4 root 39 11 21 23:14 .mozilla
```

## 6.3.2 知识点 2 操作用户组

### 1. groupadd 命令

下面介绍 `groupadd` 命令的用法，然后用范例来进行展示。

用法：`groupadd [选项][用户组]`
功能：新建用户组。`groupadd` 命令的常用选项如表 6-11 所示。

#### 表 6-11 groupadd 命令的通用选项

| 选项 | 说明 |
| --- | --- |
| `-g <gid>` | 后面接一个数字，用于给用户指定 GID，该值必须唯一，数值不可负 |
| `-r` | 创建一个系统用户组 |

范例：分别添加一个默认用户组 `group01`、默认的系统用户 `sys_group1` 和指定 GID 为 3000 的用户组 `group02`，如清单 6-27 所示。

```bash
# 添加一个默认用户组
groupadd group01

# 添加一个系统用户组
groupadd -r sys_group1 # 默认值为1000

# 添加一个 GID 为 3000 的用户组
groupadd -g 3000 group02
```

### 2. groupdel 命令

下面介绍 `groupdel` 命令的语法，然后用案例来演示。

用法：`groupdel [选项][用户组]`
功能：删除已有的用户组 (primary group)。范例：创建两个用户组 `group1` 和 `group2`，并创建一个新用户 `mpuser`，将 `group1` 作为主组，同时删除 `group1` 和 `group2`，如清单 6-28 所示。

```bash
groupadd group1
groupadd group2
useradd -g group1 -G group2 mpuser

# id mpuser
uid=1005(mpuser) gid=1009(group1) groups=1010(group2)

# 无法删除 group1 因为它是 mpuser 的主组
groupdel group1

# 可以删除 group2 它不是任何用户的主组
groupdel group2

# id mpuser
uid=1005(mpuser) gid=1009(group1) groups=1009(group1)

# 删除 mpuser 用户后
userdel mpuser
groupdel group1
```

在删除用户组的时候万分小心，因为可能涉及到其他关联的用户，影响用户的访问权限。

## 6.3.3 知识点 3 用户和组存储

在介绍 `user` 命令时已经提到，添加用户组时，命令将用户数据存储到特定的系统文件中，相关的文件有 4 个，包括：

- `/etc/passwd`：包含用户的基本信息。
- `/etc/shadow`：包含加密的密码的文件。
- `/etc/group`：包含组的基本信息。
- `/etc/gshadow`：包含加密的组密码的文件。

所有这些用户和组存储都是文本文件，因此理论上来说，可以通过直接编辑这 4 个文件添加或修改用户组。
一般不通过直接编辑存储文件来添加或修改用户组，因为修改后可能会造成用户管理的混乱。

### /etc/passwd 文件

`/etc/passwd` 系统记录用户的文本文件，内容包含一些用户信息，如用户名、用户 ID、用户组 ID、家目录、shell 环境等。清单 6-29 给出了一个样例 `passwd` 文件，其中每一行表示系统中的用户信息。每行都有 7 个字段，每个字段用冒号（`:`）分隔；在表 6-12 中对 7 个字段做了详细说明。

#### 清单 6-29:

```text
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
...此处省略
stu:x:1000:1000:stu:/home/stu:/bin/bash
```

#### 表 6-12 /etc/passwd 文件字段说明

| 字段 | 说明 |
| --- | --- |
| 1 | 用户名 |
| 2 | 密码占位符。该项由于太大，一般显示为“x”字符，用户的实际密码存储在 `/etc/shadow` 中。 |
| 3 | 用户 ID (UID)。它是用户的标识，每个用户的 UID 一般是唯一的。`root` 的 UID 是固定值 0，系统会将 1-200 留给系统用户，普通用户其 UID 从 1000 开始。 |
| 4 | 用户组 ID (GID)，用户组 ID 只有一个，这里的 GID 见表 6-13。CentOS 7 中 201-999 的 UID 保留给系统使用。 |
| 5 | 用户相关的信息，这是可选的，可以设置。 |
| 6 | 用户的家目录位置 |
| 7 | 用户登录使用的 shell |

### 2. /etc/group 文件

`/etc/group` 文件是用户组记录文件，内容包括用户组名、用户组 ID、密码、用户组和所属组。清单 6-30 给出了一个样例文件，其中每一行表示系统中的用户组信息。每行有 4 个字段，每个字段用冒号（`:`）分隔；在表 6-13 中对 4 个字段做了详细说明。

#### 清单 6-30:

```text
root:x:0:
bin:x:1:...此处省略
stu:x:1000:
```

#### 表 6-13 /etc/group 字段说明

| 字段 | 说明 |
| --- | --- |
| 1 | 用户组名 |
| 2 | 用户组密码。该项没有意义，一般显示为“x”字符，用户组的实际密码存储在 `/etc/gshadow` 中 |
| 3 | 用户组 ID (GID)，类似 UID，确认标识，每个用户组的 GID 是唯一的。`root` 组的 GID 固定值为 0。 |
| 4 | 属于该组的用户。每个用户之间用逗号（`,`）分隔，特别注意的是，这个字段为空表示该用户不会出现在列表中 |

### 3. /etc/shadow

`/etc/shadow` 文件是 `/etc/passwd` 的影子文件，这两个文件是互补的。`shadow` 包括加密的密码、账户有效期等敏感信息。这个文件访问权限非常严格，普通用户查看也会提示权限不足。如清单 6-31 所示。清单 6-32 给出了一个示例 `shadow`，其中一行代表系统中的用户，每行有 9 个字段，每个字段用冒号（`:`）分隔，在表 6-14 中对 9 个字段做了详细说明。

#### 清单 6-31:

```bash
$ ls -l /etc/shadow
---------- 1 root root 49 ...
$ cat /etc/shadow
cat: /etc/shadow: 权限不足
```

#### 清单 6-32:

```text
root:$6$...:18262:0:99999:7:::
bin:*:17632:0:99999:7:::...此处省略
stu:$6$...:18262:0:99999:7:::
```

#### 表 6-14 /etc/shadow 文件字段说明

| 字段 | 说明 |
| --- | --- |
| 1 | 用户名 |
| 2 | 加密后的密码 |
| 3 | 最后一次修改密码的日期（距离 1970-01-01 的天数） |
| 4 | 密码最短使用天数 (PASS_MIN_DAYS) |
| 5 | 密码最长使用天数 (PASS_MAX_DAYS) |
| 6 | 密码过期前警告天数 (PASS_WARN_AGE) |
| 7 | 密码过期后宽限天数 |
| 8 | 账户过期日期（距离 1970-01-01 的天数） |
| 9 | 保留字段 |
