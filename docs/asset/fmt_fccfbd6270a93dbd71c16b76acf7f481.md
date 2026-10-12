
第一个命令（`rpmbuild -ba`）创建二进制 RPM 和源码 RPM 软件包。第二个命令（`rpmbuild -bb`）仅创建二进制 RPM 软件包。

注意：从 Red Hat Enterprise Linux 3 开始，`rpm -ba` 和 `rpm -bb` 命令不再可用。它们的功能已从 `rpm-build-*` 移动到 `rpmbuild` 命令中。

## RPM 安全

一旦你学会了使用 RPM，就可以安装它们并忘记它们，而不必担心安全问题。黑客可能会在网上发布的 RPM 中发布病毒或木马。`rpm` 命令包含了检查 RPM 完整性的方法，即使用了“良好的隐私加密”（PGP）系统（见下一节）。你还可以验证软件包的内容，甚至是某个特定文件。

## RPM 与良好的隐私加密 (Pretty Good Privacy)

RPM 系统使用了与电子邮件安全相关的安全标准之一，即“良好的隐私加密”（PGP）。PGP 由 Phil Zimmermann 开发，提供了一套私钥和公钥系统。在 Red Hat Enterprise Linux 中，使用 PGP 的 GNU 版本被称为 GNU 隐私卫（GPG）。

这一切的关键是 Red Hat GPG 密钥。它应该默认安装在 `/usr/share/doc/rpm-version/RPM-GPG-KEY`。如果那里没有，你可以从以下至少一个来源获取：

- 从 Red Hat Enterprise 安装 CD 的主目录获取。如果你将 CD 安装在默认位置，密钥将在 `/mnt/cdrom/RPM-GPG-KEY`。
- 从 www.redhat.com 获取。截至本文写作之初，不同的密钥可以在 www.redhat.com/solutions/security/news/publish.html 获得。

接下来，导入 GPG 公钥。例如，如果你是从安装 CD 导入，你应该使用以下命令将其导入到 `/var/lib/rpm/keys` 文件中：

```
# rpm --import /mnt/cdrom/RPM-GPG-KEY
```

注意：`rpm --import` 命令相当新。如果你使用的是较旧版本的 Red Hat Linux（7.3 之前），你可能需要使用 `gpg --import publicKey` 命令。

## 验证软件包

现在，你可以验证任何 RPM 软件包是否具有正版的 Red Hat Enterprise Linux 签名。例如——在重新编译之前验证内核源码的完整性可能是一个好主意。

```
# rpm --import /mnt/cdrom/RPM-GPG-KEY
```

软件包，我意识到此命令会检查此包中所有文件的完整性。由于默认安装了 `initscripts` RPM，你可以使用以下命令列出与该 RPM 关联的文件列表：

```
# rpm --ql initscripts
```
