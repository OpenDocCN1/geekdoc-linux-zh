
```
$ cat /etc/security/limits.conf
# /etc/security/limits.conf
# 每行描述一个用户的限制，格式如下：
#<domain>          <type> <item> <value>
# 其中：
#*               soft    core               0
#*               hard    rss                10000
#@student         hard    nproc               20
#@faculty         soft    nproc               20
#@faculty         hard    nproc               50
#@ftp             hard    nproc               0
#@student              maxlogins  4
# 文件结束
```

## 第五部分：学习 Linux 安全技术

`domain`（域）和 `type`（类型）格式项比配置文件中的说明需要进一步解释：

- `domain`—限制适用于列出的用户或组。如果域为“*”，则适用于所有用户。
- `type`—硬限制（`hard limit`）不能被突破。软限制（`soft limit`）可以被突破，但仅是暂时的。

查看后续 `limits.conf` 文件设置示例。列出了 `faculty` 组，但注意 `nproc`。`nproc` 限制设置了用户可以启动的最大进程数。此设置可以防止炸弹。注意到类型选择的是 `hard`；因此，不能超过 50 个进程的限制。当然，由于该行被 `#` 注释，此限制并未生效。

```
@faculty hard nproc 50
```

限制设置是按登录设置的，且仅在登录会话期间有效。恶意用户可能会登录多次以创建炸弹。因此，限制这些用户账户的最大登录次数也是一个好主意。

限制最大登录次数可以按用户进行。例如，`johdoe` 只需要登录 Linux 系统。为了防止他人使用 `johdoe` 的账户，请设置他的 `maxlogins`：

```
johdoe hard maxlogins 1
```

限制此资源的最后一步是确保使用 `limits` 的 PAM 模块已包含在 PAM 系统配置文件中。使用 `limits.conf` 的 PAM 模块是 `pam_limits`。在接下来的部分列表中，使用 `grep` 来验证系统配置文件是否使用了该 PAM 模块。

```
# grep "pam_limits" /etc/pam.d/*
system-auth:session required pam_limits.so
system-auth:account required pam_limits.so
system-auth-local:session required pam_limits.so
```

服务和账户的时间限制不受 PAM `/etc/security/limits.conf` 配置文件的处理。相反，它们由 `time.conf` 文件处理。

## 使用 PAM 实现时间限制

PAM 可以让你的整个 Linux 系统按照“PAM 时间”运行。时间限制，例如在一天中的特定时间访问特定应用程序，或仅在指定的星期登录，都由 PAM 处理。

## 第 23 章：理解高级 Linux 安全

处理这些限制的 PAM 配置文件位于 `/etc/security` 目录。以下代码显示了良好的 `/etc/security/time.conf` PAM 配置文件。

```
$ cat /etc/security/time.conf
# 这是 pam_time 模块的示例配置文件

# 行的语法如下：
#
      services:ttys:users:times
```

我建议通读 `time.conf` 文件的内容。注意，每个有效条目的格式都遵循此语法：`services:ttys:users:times`。字段由分号分隔。有效字段在 `time.conf` 文件中已有记录。

虽然 `time.conf` 文档详尽，但示例总是有用的。例如，你决定允许普通用户在工作日（周一至周五）在终端上登录。在这些工作日，他们可以从早上 7 点到晚上 7 点登录。以下列表描述了需要设置的元素：

- `services`—`Login`（指定包含所有终端）
- `ttys`-`*`
- `users`—除 `root` 以外的所有员 (`!`)
- `times`—在工作日 (`Wd`) 从早上 7 点 (`0700`) 到晚上 7 点 (`1900`) 允许

`time.conf` 中的条目看起来如下：

```
login; * ; !root; Wd0700-1900
```

实现此时间限制的最后一步是确保使用 `limits` 的 PAM 模块已包含在 PAM 系统配置文件中。使用 `limits.conf` 的 PAM 模块是 `pam_limits`。在接下来的部分列表中，使用 `grep` 来验证系统配置文件是否使用了该 PAM 模块。

```
# grep "pam_limits" /etc/pam.d/*
system-auth:session required pam_limits.so
system-auth:account required pam_limits.so
system-auth-local:session required pam_limits.so
```

## 第 23 章：理解高级 Linux 安全性

你可以通过修改 `/etc/pam.d/system-auth` 文件来更改 `pam_cracklib` 用于检查新密码的规则。你可能认为这些更改应该在 PAM 感知的密码配置文件中进行。然而，`/etc/pam.d/password` 包含了 `system-auth` 文件。

```
# cat /etc/pam.d/password
##PAM-1.0
auth            include        system-auth
account         include        system-auth
password        subtrack       system-auth
-password      optional     pam_gnome_keyring.so use_authok
password        subtrack       postlogin
```

### 注意

在 Ubuntu 上，你需要修改 `/etc/pam.d/common-password` 文件，而不是 `system-auth` 配置文件。

这里显示了 `system-auth` 文件的当前设置。目前，其中一个条目调用了 `pam_cracklib` PAM 模块。

```
# cat /etc/pam.d/system-auth
##PAM-1.0
# User changes will be destroyed the next time authconfig is in run.
auth            required      pam_env.so
auth            sufficient   pam_fprintd.so
auth            sufficient   pam_unix.so nullock try_first_pass
auth            requisite      pam_succeeded_if.so uid >= 1000 quiet
auth            required      pam_deny.so

account         required      pam_unix.so
account         sufficient   pam_localuser.so
account         sufficient   pam_succeeded_if.so uid < 1000 quiet
account         required      pam_permit.so

password        requisite      pam_cracklib.so try_first_pass retry=3
..
```

上述列表中的 `pam_cracklib` 条目使用了 `retry` 关键字。`cracklib` 可用以下关键字：

- `retry=N`
  - 默认值 = 1
  - 在返回错误之前，最多向用户提示 N 次。
- `difok=N`
  - 默认值 = 5
  - 新密码中必须不存在于旧密码的字符数量。
  - 异常 1：如果新密码中有一半的字符是不同的，则接受新密码。
  - 异常 2：参见 `difignore`。
- `difignore=N`
  - 默认值 = 23
  - 在忽略 `difok` 设置之前，密码已拥有的字符数量。
- `minlen=N`
  - 默认值 = 9
  - 新密码的最小接受长度。
