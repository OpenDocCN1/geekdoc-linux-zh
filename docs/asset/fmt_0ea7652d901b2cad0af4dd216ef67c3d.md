
- `dcredit`, `ucredit`, `lcredit` 和 `ocredit` 的设置如何影响 `minlen`。

- `dcredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含数字的最大额度。如果你的数字少于 N 个，每个数字计数 +1 以满足当前信用值。
  - `(N < 0)`：新密码必须满足的最小数字数量。

- `ucredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含大写字母的最大额度。如果你拥有的大写字母少于 N 个，每个字母计数 +1 以满足当前信用值。
  - `(N < 0)`：新密码必须满足的最大写字母数量。

- `lcredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含小写字母的最大额度。如果你拥有的小写字母少于 N 个，每个字母计数 +1 以满足当前 `minlen` 值。
  - `(N < 0)`：新密码必须满足的最小小写字母数量。

- `ocredit=N`
  - 默认值 = 1
  - 如果 `(N >= 0)`：新密码中包含其他字符的最大额度。如果你拥有的其他字符少于 N 个，每个字符计数 +1 以达到当前信用 `minlen` 值。
  - 如果 `(N < 0)`：新密码必须满足的最小其他字符数量。

- `minclass=N`
  - 默认值 = 0
  - 新密码需要四种字符类中的某类。这四类是数字、大写字母、小写字母和其他其它字符。

- `maxrepeat=N`
  - 默认值 = 0
  - 拒绝包含多于 N 个相同连续字符的密码。

- `reject_username`
  检查新密码中是否包含正向或反向形式的用户名。如果找到，则拒绝新密码。

- `try_first_pass`
  尝试从之前的 PAM 模块获取密码。如果无效，则提示用户输入密码。

- `use_authtok`
  此参数用于强制模块不向用户提示新密码。相反地，新密码将由之前堆叠的密码模块提供。

- `dictpath=/path`
  `cracklib` 字典的路径。

例如，如果你的组织要求密码长度为十个字符，且必须包含两个数字，你可以在 `/etc/pam.d/system-auth` 文件中添加类似下行的内容：

`password required pam_cracklib.so minlen=10 dcredit=-2`

在此示例中与 `pam_cracklib` 使用的关键字是：

- `minlen=10`—新密码至少必须是十个字符。
- `dcredit=-2`—新密码必须包含两个数字。

### 第五部分：学习安全性

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
  - `dcredit`, `ucredit`, `lcredit` 和 `ocredit` 的设置如何影响 `minlen`。

- `dcredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含数字的最大额度。如果你的数字少于 N 个，每个数字计数 +1 以满足当前信用值。
  - `(N < 0)`：新密码必须满足的最小数字数量。

- `ucredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含大写字母的最大额度。如果你拥有的大写字母少于 N 个，每个字母计数 +1 以满足当前信用值。
  - `(N < 0)`：新密码必须满足的最大写字母数量。

- `lcredit=N`
  - 默认值 = 1
  - `(N >= 0)`：新密码中包含小写字母的最大额度。如果你拥有的小写字母少于 N 个，每个字母计数 +1 以满足当前 `minlen` 值。
  - `(N < 0)`：新密码必须满足的最小小写字母数量。

- `ocredit=N`
  - 默认值 = 1
  - 如果 `(N >= 0)`：新密码中包含其他字符的最大额度。如果你拥有的其他字符少于 N 个，每个字符计数 +1 以达到当前信用 `minlen` 值。
  - 如果 `(N < 0)`：新密码必须满足的最小其他字符数量。

- `minclass=N`
  - 默认值 = 0
  - 新密码需要四种字符类中的某类。这四类是数字、大写字母、小写字母和其他其它字符。

- `maxrepeat=N`
  - 默认值 = 0
  - 拒绝包含多于 N 个相同连续字符的密码。

- `reject_username`
  检查新密码中是否包含正向或反向形式的用户名。如果找到，则拒绝新密码。

- `try_first_pass`
  尝试从之前的 PAM 模块获取密码。如果无效，则提示用户输入密码。

- `use_authtok`
  此参数用于强制模块不向用户提示新密码。相反地，新密码将由之前堆叠的密码模块提供。

- `dictpath=/path`
  `cracklib` 字典的路径。

例如，如果你的组织要求密码长度为十个字符，且必须包含两个数字，你可以在 `/etc/pam.d/system-auth` 文件中添加类似下行的内容：

`password required pam_cracklib.so minlen=10 dcredit=-2`

在此示例中与 `pam_cracklib` 使用的关键字是：

- `minlen=10`—新密码至少必须是十个字符。
- `dcredit=-2`—新密码必须包含两个数字。

### 第五部分：学习安全性

### 注意

在 Ubuntu 上，你需要修改 `/etc/pam.d/common-password` 文件，而不是 `system-auth` 配置文件。

这里显示了 `system-auth` 文件的当前设置。目前，其中一个条目调用了 `pam_cracklib` PAM 模块。
