
```
# usermod -G peons,users newguy
```

# 实验 2

- 1. 首先，创建新用户 `senioriadm` 并分配密码：

```bash
# useradd senioriadm
# echo changeme | passwd --stdin senioriadm
```

- 2. 关于 `sudo` 权限，你应该在 `/etc/sudoers` 文件中添加以下行：
`senioradm ALL=(ALL) ALL`
除了编辑 `sudoers` 文件（建议使用 `visudo`）外，你还可以在 `/etc/sudoers.d/` 目录下创建一个新文件并添加新配置。
另一个有效的解决方案是将用户成为 `wheel` 组的成员。事实上，如 `/etc/sudoers` 中此行的配置所示，`wheel` 组的成员可以使用 `sudo` 运行任何命令：
`%wheel ALL=(ALL) ALL`

- 3. 测试以 `senioriadm` 用户登录并运行带有 `sudo` 前缀的管理命令。例如，尝试以下命令：
`# sudo firewall-cmd --list-all-zones`
除非你在几分钟内运行过 `sudo` 命令，否则此操作将提示输入密码。输入用户 `senioriadm` 的密码。它将列出所有防火墙区域及其配置。

## 实验 3

- 1. 创建新用户 `junioriadm` 并分配密码：

```bash
# useradd junioriadm
# echo changeme | passwd --stdin junioriadm
```

- 2. 关于 `sudo` 权限，你应该在 `/etc/sudoers` 文件中添加以下行：
`junioradm ALL=(root) NOPASSWD: /sbin/fdisk`
除了编辑 `sudoers` 文件（建议使用 `visudo`）外，你可以在 `/etc/sudoers.d/` 目录下创建一个新文件并添加新配置。

- 3. 使用 `sudo` 运行 `fdisk` 命令：
`$ sudo fdisk -l`
如果成功，你将在输出中看到已连接驱动器的分区列表。

`https://t.me/CCNA_SECURITY`
`https://t.me/CCNPSECURITY`

## 实验答案 249

- 4. 尝试在不使用 `sudo` 的情况下运行相同命令，并观察区别：

```bash
$ fdisk -l
```

你应该收到一些权限错误。

## 实验 4

- 1. 此列表指定了“新用户”，这意味着你应该将目录添加到 `/etc/skel`，而不是拷贝到每个用户的家目录：

```bash
# cp -a /usr/share/doc/bash /etc/skel/
```

- 2. 通过 `useradd` 命令添加名为 `infouser` 的新用户来测试结果：

```bash
# useradd infouser
# echo changeme --passwd stdin infouser
```

- 3. 你发现了一个 `/home/infouser` 目录，其中包含 `/usr/share/bash` 的内容：

```bash
# ls -lR /home/infouser
```

## 实验 5

- 1. 创建用户账户：

```bash
# useradd mike
# echo changeme --passwd stdin mike
```

- 2. 运行以下命令检查该用户的密码过期时间：

```bash
# change -l mike
```

- 3. 将密码最后修改日期设置为自 1970 年 1 月 1 日以来 0。这将强制在下次登录时更改密码。

```bash
# change -d 0 mike
```

- 4. 设置密码更改之间的最小天数以及密码有效的最大天数：

```bash
# change -m 7 -M 30 mike
```

- 5. 再次确认用户 `mike` 的设置。

- 6. 对于最后一个实验，编辑 `/etc/login.defs` 文件并将 `PASS_MAX_DAYS` 设置为 30：

```bash
PASS_MAX_DAYS 30
```

## 250 第6章 用户管理

## 实验 6

- 1. 创建 `testlock` 账户并锁定密码：

```bash
# useradd testlock
# echo changeme | passwd -stdin testlock
# usermod -L testlock
```
在 `/etc/shadow` 中，你应该看到 `testlock` 的密码字段前面有一个感叹号 `!`。

- 2. 测试是否可以从终端以 `testlock` 用户身份登录。如果可以，以普通用户或 `root` 身份运行 `su`。首先检查是否能以 `testlock` 打开 `SSH` 会话。

- 3. 解锁密码并禁用账户，例如将账户过期日期设置为 2000 年 1 月 1 日：

```bash
# usermod -U testlock
# usermod -e 2000-01-01 testlock
```

- 4. 重复步骤 2。

- 5. 通过设置过期日期启用账户，并将登录 `shell` 设置为 `/bin/nologin`：

- 6. 重复步骤 2。你应该发现当用户密码被锁定且账户被禁用时，无法从终端或 `SSH` 登录。仅允许通过 `root` 运行 `su` 进行访问。然而，当用户密码被锁定时，你仍然可以通过无密码方法（例如使用 `SSH` 密钥认证，见第 8 章）登录用户账户。相反，将用户的 `shell` 设置为 `/bin/nologin` 会禁用 `SSH` 访问（带密码和密钥认证），以及从终端或通过 `su` 的访问。结论是，禁用用户账户并确保系统访问被禁的安全方法是什么？如果你不想删除账户，请使用所有方法：锁定用户密码、禁用账户并将登录 `shell` 设置为 `/bin/nologin`。

`https://t.me/CCNA_SECURITY`
`https://t.me/CCNPSECURITY`

## 实验 7

使用 `useradd` 命令为 `mike`、`rick`、`terri` 和 `maryam` 创建用户账户：

```bash
# useradd mike
# useradd rick
# useradd terri
# useradd maryam
# echo changeme | passwd --stdin mike
# echo changeme | passwd --stdin rick
# echo changeme | passwd --stdin terri
# echo changeme | passwd --stdin maryam
```

为这些用户设置组。通过以下命令赋予正确的所有权权限：

```bash
# mkdir /galley
# chown mike:rick:terri:maryam /galley
# chmod 770 /galley
```
