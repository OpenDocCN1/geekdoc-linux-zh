
```bash
# rpm -q --provides emacs-common

config(emacs-common) = 1:24.3-fc21

emacs-common = 1:24.3-fc21

emacs-el (x86_64) = 1:24.3-fc21

emacs-el = 1:24.3-fc21

pkgconfig(emacs) = 1:24.4
```

```bash
# rpm -q --scripts httpd

 Add the "apache" -u 4 \
-s /sbin/useradd -s /sbin/nologin -r d /var/www/apache 2 >/dev/null ||

postinstall scriptlet (using /bin/sh):
```

```bash
# rpm -q --changelog httpd | less

Wed Sep 03 2014 Jan Kaluza<jkaluza@redhat.com> - 2.4.10-9

 fix hostname requirement and conflict with openssl-free
```

之前的示例中，你可以看到 `httpd` 软件包在安装时添加 `apache` 用户并通过 `chkconfig` 开启 `httpd` 服务。`--changelog` 选项让你看到对每个版本的软件包做了哪些更改。修复代表了可以在 `http://bugzilla.redhat.com` 查询的漏洞。

使用名为 `--queryformat` 的功能查询不同的标签并以你喜欢的格式输出。运行 `--querytags` 选项查看所有可用标签：

```bash
# rpm --querytags | less

ARCH

ARCHIVESIZE

BASENAMES

BUGURL
```

```bash
# rpm -q binutils --queryformat "The package is %{NAME} \nand the release is %{RELEASE}\n"

The package is and the release is 30.fc21
```

到目前为止的所有查询都是针对本地 RPM 数据库的。通过在这些查询中添加 `-p`，你可以查询本地目录中的 RPM 文件。`-p` 选项是在别人给你的软件包安装到系统之前对其进行调查的好方法。

如果你还没有，请获取 `zsh` 软件包并将其放入本地目录 (`yumdownloader zsh`)。然后对 RPM 文件运行 `rpm` 查询命令。

```bash
# rpm -q zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -qi zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -ql zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -qd zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -qc zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -q --requires zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -q --provides zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -q --scripts zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -q --changelog zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -qp zsh-5.0.7-4-fc21.x86_64.rpm
```

## 验证 RPM 软件包

使用 `-V` 选项，你可以检查系统中安装的软件包以查看它们是否发生了变化。虽然配置文件发生变化是正常的，但二进制文件（`/bin`、`/sbin` 等）变化是不正常的。每当你在 `-V` 输出中看到字母或数字而不是点时，表示发生了变化：

- S 大小不同
- M 模式不同（包括权限和文件类型）
- MD5 和不同
- D 设备/次设备号不匹配
- L readlink(2) 路径不匹配
- U 所有权不同
- G 组所有权不同
- T 时间不同
- P 能力不同

要将软件包恢复到原始状态，请使用带有 `--replace` 选项的 `rpm`，如下所示（`yum reinstall` 命令同样有效）。然后用 `-V` 进行检查。`-V` 无输出意味着所有文件都恢复到了原始状态。

```bash
# rpm --replace zsh-5.0.7-4-fc21.x86_64.rpm
# rpm -V zsh-5.0.7-4-fc21.x86_64.rpm
```
