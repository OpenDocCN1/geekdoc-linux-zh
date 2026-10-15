
```
（注：原文此处为 `pamd.d` 疑似笔误，应为 `pam.d`）

PAM 配置文件显示了 `login` 命令的认证规则，如图 30-1 所示。

以下是该文件中规则的逐行详细说明：

- 第 1 行：`/etc/pam.d/login` 的第一行是注释。你现在可以忽略该行，但注意你可以在注释中包含内容。

- 第 3 行：第三条规则要求当传递参数 `service=auth` 时，`pam_stack.so` 返回正向响应。`pam_stack.so` 本身实际上并不执行任何认证检查。它切换到存储在一个配置文件中的通用规则集。将用到的规则保留在单个文件中更容易管理 PAM 配置。如果另一个文件（在本例中为 `/etc/pam.d/system-auth`）被满足，`pam_stack.so` 就会返回正向响应。

#### 列表 30-1：PAM 登录配置文件

| | |
| :--- | :--- |
| 1 required | pam_security.so |
| 2 auth required | |
| 3 auth required | pam_stack.so service=system-auth |
| 4 auth required | pam_login.so |
| 5 account required | pam_stack.so service=system-auth |
| 6 session required | pam_stack.so |
| 7 session optional | pam_console.so |
| 8 password required | pam_stack.so |

![]![](img/be0c8e25e9bb10f39b0d8bbb67eb22db_224_0.png)

### 剖析配置文件 207

许多使用 `system-auth` 文件。`system-auth` 文件包含了通用信息。

当认证规则满足且 PAM 确认了用户身份后，将移动到账户规则。认证规则规定了证明身份必须遵循的程序。账户规则在身份验证完成后启动。

`pam_console` 模块在你登录时更改权限，并在注销时更改权限。`pam_console` 的理论是，如果你对机器有物理访问权限，你就应该对外设有物理访问权限。这是一个相当不稳定的模块，我们不建议使用。

- 第 4 行：第四条规则要求 `pam_login.so`。系统检查 `/etc/nologin` 是否存在。

- 第 6 行：首先应用 `required` 规则。`required` 规则引用 `system-auth`。在允许登录之前，必须满足 `pam_limits.so` 模块的要求。`pam_limits.so` 通过 `/etc/limits.conf` 文件对磁盘使用、CPU 使用、内存等进行限制。创建 `/etc/nologin` 文件可以在你维护期间阻止其他用户登录。完成后请务必删除该文件，因为其他用户（`root` 除外）被允许登录。

- 第 7 行：`optional` 规则不需要满足——它们是可选的。此规则指定在登录继续之前可以满足或不满足 `pam_console.so` 模块。

- 第 5 行：这是 `/etc/pam.d/system` 文件中唯一的账户规则。该规则简单引用 `system-auth`。你可以使用账户规则来实施与认证无关但仍然重要的策略——密码过期、禁用的账户等。

- 第 8 行：密码规则仅在登录程序请求更改密码时才被调用。`login` 文件中的 PAM 看到密码规则要求 `system-auth` 允许用户更改密码。我们的 `system-auth` 文件要求在接受新密码之前 `pam_cracklib` 必须满足。请注意，密码规则实际上并不是身份验证序列的一部分——它们只是为了更改密码（或视网膜扫描、指纹或你配置的任何内容）。

`system-auth` 文件包含了最常用的系统配置规则。你可以通过以下命令查看文件内容：

```
$ /etc/pam.d/system-auth
```

查看 `system-auth` 文件会告诉你调用了 `pam_unix.so` 模块。

## 208 技术 30：使用 PAM 自定义身份验证

`pam_cracklib` 模块仅对密码规则类型有效。它通过字典检查密码，以查看新密码是否容易被破解。如果你将 `pam_cracklib` 设置为 `required`（必须），则只接受复杂且难以破解的密码。

编辑窗口打开，显示 `/etc/group` 的内容。

1. 在文件中找到以 `wheel` 开头的行。
2. 在该行添加一个逗号，后跟你的用户名。

```
wheel:x:10:root,username
```

3. 保存文件并退出。
4. 输入以下命令：

```
edit /etc/pam.d/system-auth
```

## 使用 PAM 跳过密码

你可以通过 PAM 增强安全性，但在某些情况下也可以放宽安全标准以节省时间。在一个不存储生死攸关数据、且不是网络中不可或缺环节的系统上，当你在命令行需要超级用户权限时，可以让 PAM 跳过 `root` 密码。

> 如果你使用 Fedora，请找到类似下面的几行：
> # the following line to \
> implicitly trust users in the \
> "wheel" group.
> #auth sufficient \
> /lib/security/$ISA/pam_wheel.so \
> trust use_uid

当 `wheel` 组的成员尝试身份验证时，`pam_wheel.so` 会返回正结果。这意味着如果你是该组的成员，PAM 会假设你已经通过了验证，并允许你在无需密码的情况下继续。这个名字的意义是什么？我们可以查一下。

如果你使用的是 Mandatory（强制模式），你的 `system-auth` 中将不会包含该行。
你需要在 `system-auth` 的对应部分添加以下行：

```
auth sufficient \
/lib/security/$ISA/pam_wheel.so \
trust use_uid
```

> 在禁用 `root` 密码之前请三思。永远不需要输入密码是一种失败，但它是你所能使用的最不安全的方式。

以下示例适用于 Fedora 或 SUSE，因为 SUSE 不使用像 `system-auth` 这样的配置文件，你需要识别需要修改哪些文件。

5. 如果你使用 Fedora，删除 `auth` 开头的 `#` 注释行。
结果应该像下面所示：

```
# the following line to \
implicitly trust users in the \
"wheel" group.
auth sufficient \
/lib/security/$ISA/pam_wheel.so \
trust use_uid
```

允许超级用户无密码访问的 PAM 配置文件请遵循以下步骤：

1. 打开终端窗口并赋予自己超级用户权限。
2. 输入以下命令：

```
edit /etc/group
```

现在，当你使用 `su` 命令时，PAM 识别出你是 `wheel` 组的成员，不再询问 `root` 密码。

> 如果你决定允许 PAM 跳过密码提示并让桌面保持登录且无人看管，你可能会自找麻烦。

## 获取权限

### 技术

### 通过节省时间

每个 Linux 系统都有一个认为自己比所有人都要好的用户；一个想要比任何人都权限的用户；一个能做别人做不到的事的用户。我们称他为 `superuser`（超级），但他真正的名字是 `root`。

- 了解超级用户的力量
- 使用 `su` 命令获取额外权限
- 使用 `sudo` 限制权限

这项技术展示了如何从舒适的桌旁安全地获取和使用超级用户权限——不需要电话亭或任何花招。如果你想保持系统安全，限制超级用户的力量是非常重要的。如果你不需要从由于（无意中）过度展示超级肌肉而导致的灾难中恢复，你将节省大量时间。有时你 `需要` 超级用户权限来执行系统管理工作，如配置、用户管理。但我们展示了如何在需要时仅获取所需的权限来限制暴露。

## 感受力量

在系统中，一个名为 `root` 的用户拥有超级用户权限（你可以认为 `root` 等同于 `superuser`）。超级用户可以在你的系统上做任何事情，例如：

- 修改（或删除）任何文件。
- 修改任何密码。
- 使用任何设备。
- 创建新账户。
- 删除旧账户。
- 将你排除在系统之外。

听起来你想把自己排除在系统之外吗？

### 技术 31：获取权限

有时你需要做一些事情，因为用户会来往往去，密码会被遗忘，文件会变化。通过限制你所能造成的伤害来为你节省大量时间。当你真正需要时再保留力量。

5. 按如下方式覆盖 `/etc/motd` 文件：

```
[root@bastille /]# echo "Bastile will be down this evening" > /etc/motd

[root@bastille /]#
```
