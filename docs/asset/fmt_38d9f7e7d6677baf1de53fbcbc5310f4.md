
这些软件包可以通过名称扩展名 `-devel` 来识别，例如 `alsa-devel`、`gimp-devel` 和 `kdelis-devel` 软件包。

# 验证软件包真实性

所有 SUSE RPM 软件包都使用以下 GnuPG 密钥签名：`1024D/9C80ACA2000-10-19` SUSE Package Signing Key `build@suse.de` 密钥指纹 = `1024D/9C80ACA2000-10-19`

> 对于许多软件包，软件开发所需的组件（库、头文件、包含文件等）被放在了独立的软件包中。只有在你想要编译软件时，才需要这些开发软件包（例如最新的 `GNOME` 软件包）。

这些软件包可以通过名称扩展名 `-devel` 来识别，例如 `alsa-devel`、`gimp-devel` 和 `kdelis-devel` 软件包。

# 管理 RPM 软件包

如果是这种情况，请将备份文件（`.rpmorig` 或 `.rpmsave`）与新安装的文件进行比较，并在新文件中进行更改。更新后：

- 如果配置文件已存在且 `.spec` 文件中指定了 `noreplace` 标签，则会创建一组 `.rpmnew` 文件。

如果文件未被 RPM 数据库识别，则分配 `.rpmnew` 扩展名；否则，使用 `.rpmsave`。

换句话说，`.rpmnew` 源于从外部格式更新到 RPM。`.rpmsave` 源于从旧版本 RPM 更新到新版本 RPM。

`.rpmnew` 不提供有关系统管理员是否对配置进行了任何更改的信息。
