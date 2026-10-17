
在发布新的 DEB 文件之前，你应该在本地进行测试，以确保它们完整且运行正常。`dpkg -c` 允许你验证每个 DEB 文件包含的文件列表，而 `dpkg --install` 安装软件，允许你维护程序的脚本和操作。这种验证对于高质量的 Debian 包来说是关重要的。

上述 `dpkg` 命令都需要 DEB 文件的精确名称。除非你知道名称并愿意在命令行中输入（可以使用 Tab 键补全），否则你需要查看包含该文件的目录，获取其名称并传递给 `dpkg`。

`devscripts` 包包含两个尝试简化包验证过程的辅助工具：`debc` 显示二进制包的控制信息和内容，`debi` 安装它们。这两个工具都接受更改文件的路径作为参数。在没有此类参数的情况下，工具将使用 `debian/changelog` 来确定要使用的更改文件。

```
# fakeroot debian/rules binary
...
dpkg-deb: building package 'gruezi'
in './gruezi_1.2-2_i386.deb'.
...
dpkg-deb: building package 'gruezi-common'
in './gruezi-common_1.2-2_all.deb'.
# debc
gruezi_1.2-2_i386.deb
-----------------
new debian package, version 2.0.
size 1576 bytes: control archive= 562 bytes.
17 bytes, 1 lines confiles
367 bytes, 13 lines control
164 bytes, 3 lines md5sums
Package: gruezi
Version: 1.2-2
....
drwxr-xr-x root root 0 2004-12-30 09:02:14 ./

drxr-xr-x root root 0 2004-12-30 09:02:14 ./

-rw-r--r-- root 104 2004-12-30 09:01:56 /etc/

.conf

gruezi-common_1.2-2_all.deb
```

你会注意到 `debi` 是通过 `sudo` 调用的；因为在本地系统上安装包，所以需要 root 权限。在内部，`debi` 使用 `debpkg` 包装器，在安装请求的包之前获取权限。作为使用 `sudo` 的替代方案，你也可以将包设置为 `setuid root`。你应该意识到，通过 `sudo` 访问 `debpkg` 可能会被用户用来获取整个系统的完全 root 权限。因此，请确保只有信任的用户可以使用该包装器。setuid 位应通过 `dpkg-statoverride` 配置（见第 6.1.2 章）：

```
# dpkg-statoverride --update --add root root 4754 /usr/bin/debpkg

$ debi

[...]
```

## 9.2 使用软件包维护工具进行 Debian 化

必须匹配。默认值为 `PACKAGE-*`，其中 `PACKAGE` 会自动替换为源包名称。

这两个选项都可以在 `devscripts` 文件中设置，该文件在 `devscripts(5)` 中有详细解释。

### 9.2.14 软件包文件签名

如果你打算将软件包提交到 Debian 归档，你必须对某些组件文件进行密码加密签名，以便 Debian 归档工具在上传后验证软件包的完整性。此外，由于只有 Debian 开发者才能向官方归档上传软件包，Debian 工具可以验证软件包的来源。尽管如此，即使你打算从自己的服务器提供软件包，对源包签名也能为用户提供一种手段，确保他们安装的包确实是生成的包。你显然需要一个 GnuPG 密钥⁶。

需要签名的两个文件是 `dsc` 文件和 `changes` 文件。前者标识构成源包的文件，后者则包含了二进制包的 MD5 和（并借此识别它们）。

#### 手动签名软件包

标准的签名方法是使用 GnuPG，签名应该是明文 ASCII 格式并嵌入文件中。以下命令生成一个嵌入签名的 `dsc` 文件。

```
# gpg --armor --clearsign --textmode gruezi_1.2-2.dsc

你需要一个密码来解锁用户:"Wilhelm Tell<herr@suisse.ch>" 的私钥

1024位 DSA 密钥，ID B27C9467，创建于 1307-11-18

Enter passphrase:

# mv gruezi_1.2-2.dsc.asc gruezi_1.2-2.dsc
```

`changes` 文件包含了 `dsc` 文件的 MD5 和，该和会因为签名而改变。这使得在签名 `dsc` 文件后必须重新运行 `dpkg-genchanges`（或者在运行 `dpkg-genchanges` 之前先对 `dsc` 文件签名）。

> ⁶ <advocacy>无论如何人都应该拥有这些</advocacy>

#### 使用 debign

`descripts` 软件包带有一个实方便的 `debign` 工具，它可以自动化软件包的签名过程。同时，它解决了上述手动（以及传统）方法的一个缺点：软件包必须在构建软件包的机器上签名，因为 `changes` 包含了 `dsc` 文件的 MD5。如果用于构建软件包的机器没有持有用于签名的 GnuPG 密钥，则必须将 `dsc` 传输到本地机器（密钥所在处），签名，后再传回构建机器，然后在本地创建并签名 `changes` 文件。

由于这个过程可能变得繁琐，`debign` 提供了一种改进的签名机制。它会在签名后替换 `changes` 文件中的 `dsc` MD5，并可以自动调用远程机器（通过 SSH）进行签名。或者，可以在本地机器调用签名，从构建机器获取这两个文件。显然，也支持在构建机器上签名：

```
# debign gruezi_1.2-2_i386.changes

[...]

Successfully signed dsc and changes files
```

假设文件位于远程构建机器的 `/deb/gruezi/` 目录下，可以在本地使用 `debign` 获取、签名并远程存储它们。

```
local:"# debign -r user@remote deb/gruezi/gruezi_1.2-2_i386.changes

[...]
```

若要将文件推送到另一台机器（本地）进行签名，可以使用 `debign`：

```
# debsign user@local gruezi_1.2-2_i386.changes

[...]
```

### 9.2.15 检查软件包

尽管创建 Deb 文件并没有魔法（正如我希望展示的那样），但有很多规则需要遵守以及潜在的陷阱。如第5.7节所示，Debian 的核心优势之一是遵循一套严格的规则。因此，按照其标准检查软件包至关重要。`lintian` 和 `linda` 两个工具用于此目的。虽然 `lintian` 可能更受欢迎（且由于历史较久，测试更多），但 `linda` 运行更快且更容易扩展。

> 2 GnuPG 密钥不应存储在其他人可以访问的地方。这包括他人管理的机器，因为他们可以获得 root 权限并窃取密钥

两者都可以通过对 DEB 文件、`dsc` 文件或 `changes` 文件调用工具来检查二进制包、源包，或源包及其所有相关的二进制包。`--info` 允许你显示失败测试的详细信息。`lintian` 会输出警告和错误。

例如，我忘记了在 `debhelper 4` 上添加版本化的构建依赖，`lintian` 报告了此错误：

```
$ lintian --info gruezi_1_2_2_1386.changes

E: gruezi source: package-lacks-versioned-build-depends-on-debhelper 4

N: 如果软件包将 debhelper 的兼容版本设置为 >= 1（无论是通过 DH_COMPAT，还是通过 debian/compat，亦或通过 dh_testversion（已弃用）），它必须对所需的 debhelper 版本声明版本化的 Build-Depends。
```
