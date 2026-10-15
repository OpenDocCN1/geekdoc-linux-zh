

通过选择三个预定义的其中一个安全级别并选择 Next，所选的安全级别将被应用。通过选择 Details，您可以更改所选安全级别的设置。

如果您选择 Customs Settings 然后选择 Next，您可以直接更改安全配置的详细信息。

每个安全级别的详细设置对话框看起来都一样，但预选的选项不同。在以下对话框中，您可以看到 Level 3（Network Server）的设置。

在第一个对话框中，您可以更改系统接受的默认密码要求：

## Figure 6-4

![](img/8279afe915b153902294b0e58311b75a_109_0.png)

从此对话框中，您可以选择或输入以下密码设置（主要存储在 /etc/login.defs 中，部分值也存储在 /etc/default/passwd 和 /etc/security/pam_pwcheck.conf 中）：

- **Check New Passwords.** 选择密码时，重要的是选择一个不在字典中且不是姓名或其他简单常见词的密码。通过选择此选项，您强制按这些规则检查密码。
- **Test for Complicated Passwords.** 密码应由大小写字母混合以及数字构成。也可以使用特殊字符如 (: 等，但可能在不同的键盘布局上难以输入。这使得猜测密码变得非常困难。选择此选项以启用额外检查。
- **Password Encryption Method.** 从下拉列表中选择以下其中一种加密方法：
  - **DES.** 这是最低的共同标准。它在所有网络环境中都适用，但将密码限制为不超过八个字符。如果您需要与其他系统兼容，请选择此方法。
  - **MD5.** 此加密方法允许更长的密码，并得到所有当前 Linux 发行版的支持，但不被其他系统或旧软件支持。
  - **Blowfish.** 此加密方法使用 blowfish 算法对密码进行加密。尚未被许多系统支持。计算哈希需要大量 CPU 能力，这使得使用字典破解密码变得困难。它是 SLES 10 上的默认加密方法
- **Minimum Acceptable Password Length.** 输入可接受密码的最小字符数。如果用户输入的字符更少，密码将被拒绝。

输入 0 可禁用此检查。
- **Password Age.** Minimum 指的是在密码可以再次更改之前必须经过的天数。Maximum 是密码过期并必须更改的天数。

- **Days Before Password Expires Warning.** 在密码过期前此天数会向用户发出警告。

尽管 root 在设置密码时收到警告，但她仍可能在上述设置下输入一个不好的密码。

配置完密码设置后，选择 Next 继续。随后出现以下内容：

## Figure 6-5

![](img/8279afe915b153902294b0e58311b75a_111_0.png)

从此对话框中，您可以选择以下启动设置（将更新文件 /etc/inittab）：

- **Interpretation of Ctrl + Alt + Del.** 当有人在控制台按下 Ctrl+Alt+Del 键组合时，系统通常会重新启动。

- **Ignore.** 有时您希望系统忽略此键组合，尤其当系统既作为工作站又作为服务器使用时。按下 **Ctrl+Alt+Del** 键组合时什么也不会发生。
- **Reboot.** 按下 **Ctrl+Alt+Del** 键组合时系统会重新启动。
- **Halt.** 按下 **Ctrl+Alt+Del** 键组合时系统会关闭。

## Shutdown Behavior of KDM. 您使用此选项来设置谁有权从 KDM 关闭计算机。

- **Only Root.** 要停止系统，必须输入 root 密码。
- **All Users.** 每个人，甚至远程连接的用户，都可以使用 KDM 停止系统。
- **Nobody.** 没有人可以使用 KDM 停止系统。
- **Local Users.** 只有本地连接的用户可以使用 KDM 停止系统。
- **Automatic.** 注销后系统会自动关闭。

对于服务器系统，您应使用 **Only Root** 或 **Nobody** 以防止普通用户甚至远程用户停止系统

