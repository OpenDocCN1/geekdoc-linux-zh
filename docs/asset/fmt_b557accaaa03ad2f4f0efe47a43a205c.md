
现在您应该能够进行认证，因为您已将 SSH Communications 的 SSH 客户端密钥转换为 OpenSSH 格式，并将密钥添加到了授权密钥列表文件：

```
/usr/bin/ssh SSH-Server -i id_dsa_2048_a_Open
```

## 如何在 VShell SSH 服务器上使用 SSH 客户端密钥

在 VShell SSH 服务器上使用 SSH Communications 的客户端密钥非常简单。由于 VShell SSH 服务器接受 SSH Communications 的 SSH2 密钥格式，因此无需将 SSH Communications 的密钥转换为其他格式，这节省了宝贵的时间和潜在的麻烦！VShell 接受 OpenSSH 密钥格式；因此，前一节中转换的 OpenSSH 密钥也可以用于 VShell SSH 服务器。现在我将演示如何在 VShell SSH 服务器上使用 SSH Communications 的 SSH 密钥和转换后的 OpenSSH 客户端密钥。

1. 将您的 SSH Communications 密钥和 OpenSSH 公钥文件复制到远程 VShell SSH 服务器，具体位于 `C:\Program Files\VShell\PublicKey\%USER%` 的公钥文件夹中。
2. 确保远程 VShell SSH 服务器上启用了公钥认证。
3. 从客户端机器使用以下语法连接到 VShell SSH 服务器。

```
ssh2 <VShell Server> -p 22 -i identification -l <username on VShell server>
ssh <VShell Server> -p 22 -i OpenSSHPrivateKey -l <username on VShell server>
```

使用前面的示例，以 `id_dsa_2048_a` 作为 SSH Communications 的密钥，`id_dsa_2048_a_Open` 作为转换后的 OpenSSH 客户端密钥，完成以下步骤以认证到 VShell SSH 服务器。

### SSH Communications 客户端密钥

```
ssh2 VshellServer -p 22 -i identification -l <username>
Enter passphrase for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

### OpenSSH 转换客户端密钥

```
ssh VshellServer -p 22 -i id_dsa_2048_a_Open -l <username>
Enter passphrase for key '<username>':
Authenticated with partial success
Shreya@VshellServer's password:
C:\
```

请注意，在密钥认证后，VShell 会在 VShell 服务器上要求输入密码。这只有在 VShell 服务器上同时要求勾选密码和公钥复选框时才会发生。如果公钥是唯一的必需认证方法，则不会出现密码提示；然而，这是一种强制实施双因素认证的绝佳方法，对于管理目的来说是必须的。

## 使用 SSH Communications 创建密钥（Windows GUI）

若要在 SSH Communications 的 SSH 客户端中创建密钥，应完成以下步骤。

1. 打开 SSH 客户端：开始 程序 SSH Secure Shell 安全 Shell 客户端。
2. 从菜单栏中，选择 编辑 设置。
3. 在设置显示中，应该有一个用户认证部分。在用户认证部分下，有一个名为密钥的子类别。选择密钥子类别。
4. 此时，您应该会看到类似于图 4.8 的屏幕。
5. 若要生成新的公钥和私钥对，选择写着“生成新...”的选项。
6. 应该显示向导，描述创建密钥对的过程。阅读完描述后，选择“下一步”。
7. 接下来应显示密钥属性屏幕。此屏幕为您提供选择 DSA 或 RSA 密钥类型以及您希望使用的密钥长度的选项。通常，密钥长度越好，安全性越强；但是，您将不得不接受更大的性能影响。选择密钥类型和密钥长度后，选择“下一步”。
8. 接下来应显示生成屏幕。此屏幕启动实际创建密钥的过程。密钥生成过程可能需要几分钟。过程完成后，选择“下一步”。
9. 接下来应显示输入密码短语屏幕。此屏幕允许您为公钥和私钥对输入名称，仅用于描述目的的注释，以及保护私钥的密码短语。输入您偏好的文件名，如您的用户名，一个注释，以及一个难以猜测但容易记住的密码短语。输入这些信息后，选择“下一步”。（注意，如果密码短语不匹配，“下一步”选项将不会启用。在尝试选择“下一步”之前，请确保您的密码短语匹配。）
10. 接下来应显示完成屏幕。在此阶段，公钥和私钥已生成并存储到您的本地机器。此时，如果当前存在有效连接，您有权将公钥上传到 SSH 服务器。如果存在有效连接（意味着您在开始密钥生成过程之前连接到 SSH 服务器），请选择“上传公钥”；然而，您稍后将在此部分中向多个 SSH 服务器上传密钥，因此如果您希望跳过此步骤，请选择“完成”并跳到步骤 13。

![](img/c99d6f526a5f9fa62f2c34daada85ad7_171_0.png)

**图 4.8** SSH Communications’ SSH 客户端的密钥子类别。

11. 选择上传公钥（Upload Public Key）后，应出现一个新的显示界面。该界面应包含公钥的名称、放置密钥的目标文件夹（即 SSH 服务器上放置密钥的文件夹，通常是 `/home/user/.ssh2`），以及要添加该密钥的授权文件（例如 `authorization`）。在核实所有项目均无误后，选择上传（Upload）。
12. 选择上传（Upload）后，您将看到上传成功完成的提示，此时可以选择完成（finish）；但是，如果您希望强制仅使用公钥，则必须返回并编辑 `sshd2_config` 文件，以强制仅允许使用公钥，并删除基于密码或主机的身份验证。此外，如果在上传过程中收到错误，可能是因为您尝试连接的 SSH 服务器不是 SSH Communications’ SSH 服务器，因此必须执行密钥转换过程，如下列清单所示。
13. 此时，您应被重定向到初始的密钥子类别屏幕。要确认密钥已正确生成，请浏览至 `Documents and Settings\username>\Application Data\SSH\UserKeys`。该文件夹中应同时存在公钥（`*.pub`）和私钥。此外，密钥子类别屏幕上的密钥（Keys）字段中应显示新生成的密钥，如图 4.9 所示。
14. SSH Communications’ SSH 密钥已生成！

![](img/c99d6f526a5f9fa62f2c34daada85ad7_172_0.png)

**图 4.9** SSH Communications' SSH 客户端中的私钥文件名。

创建过程完成后，接下来是上传公钥的过程。以下部分演示如何将 SSH Communications’ SSH 客户端的公钥和私钥对上传到 SSH Communications’ SSH 服务器、OpenSSH 服务器以及 VanDyke VShell SSH 服务器。

## 如何将 SSH 客户端密钥对上传到 SSH Communications’ SSH 服务器

如果两个系统相同（即来自同一应用程序，OpenSSH 与商业版），将 SSH 客户端密钥上传到 SSH 服务器的过程相对简单。要将 SSH Communications’ SSH 客户端公钥上传到 SSH Communications’ SSH 服务器（Windows 或 Unix），请完成以下步骤。

1. 打开 SSH 客户端：开始 程序 SSH Secure Shell Secure Shell Client。
2. 使用用户名和密码连接到 SSH Communications’ SSH 服务器。这可以通过“文件”->“快速连接”选项完成。
3. 身份验证并连接到 SSH 服务器后，从菜单栏中选择“编辑”->“设置”。
4. 在设置显示界面中，应有一个用户身份验证部分。在用户身份验证部分下，有一个名为密钥（Keys）的子类别。选择密钥子类别。
5. 在密钥子类别中，应有一个公钥管理部分，其中存在一个“上传...”按钮。只需选择“上传...”按钮即可将公钥上传到 SSH 服务器。
6. 选择“上传...”后，应出现一个新的显示界面。该界面应包含公钥的名称、放置密钥的目标文件夹（即 SSH 服务器上放置密钥的文件夹，通常是 `/home/user/.ssh2`），以及要添加该密钥的授权文件（例如 `authorization`）。SSH 服务器读取授权文件以识别哪些用户可以使用公钥进行身份验证。在核实所有项目均无误后，选择上传（Upload）。
