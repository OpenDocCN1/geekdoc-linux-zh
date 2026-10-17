
# 9 创建 Debian 软件包

```bash
/apt# apt-ftarchive contents . > Contents
/apt# gzip -9 < Contents > Contents.gz
```

此外，提供一个经过签名的 `Release` 文件是一个好主意，特别是考虑到 APT 工具中即将集成的软件包签名（第 7.5 节）。为了这一点，我们需要创建一个与 `apt.conf` 风格相同的文件。

```bash
/apt# cat <<EOF > apt.conf

APT {

  Archive {

    Release {

      Origin "Wilhelm Tell";

      Label "Wilhelm Tell";

      System;

      Codename helvetia;

      Architectures i386;

      Description "Unofficial Debian packages by Wilhelm Tell";

    }

  }

}

EOF
```

`Release` 文件将包含 `Packages` 和 `Sources` 文件的 MD5 哈希值。因此，通过创建并提供（离线的）签名，我们允许访问仓库的人验证软件包的完整性和来源。未来版本的 APT 将自动完成这样做（第 7.5 节）。

```bash
/apt# apt-ftarchive --config-file=apt.conf \
release -> Release
/apt# gpg -b -o Release.gpg
```

APT 仓库现在准备好了。在 `/etc/apt/sources.list` 中添加必要的行后，就可以回到正题：

```bash
# cat <<EOF >> /etc/apt/sources.list
deb http://server/apt/
deb-src http://server/apt/
EOF
# apt-get update
Get: 1 http://server/apt/ Packages
Get: 2 http://server/apt/ Sources
```

```bash
# apt-cache show gruezi
Package: gruezi
Version: 1.2-2
Depends: gruezi-common (=1.2-2)
Filename: ./gruezi/gruezi_1.2-2_i386.deb
```

作为一个补充，`Release` 文件中一个有趣的选项是 `NotAutomatic`。将其设置为 `yes` 向 APT 表示此版本的软件包以最低优先级处理。

```bash
/apt echo NotAutomatic: yes >> /Release
/apt gpg -b Release.gpg
```

这会导致 APT 锁定该版本的所有软件包，除非用手动锁定覆盖。关于锁定的更多信息，请参见第 8.2.1 节。

作为最后一点说明，还可以嵌套架构。如果 `apt-ftarchive` 正确地在 `gruezi` 目录运行，`http://server/apt` 将变成它自己的 APT 架构。如果你的个人仓库包含较多软件包，并且你想让 APT 访问单个软件包，这可能有用。我的仓库使用这种技术，使其能够包含整个阶段区域或单个软件包。两者都是完整的 APT 存档，前者包含了后者。

## 9.3.2 上传工具

上传文件到个人仓库的步骤很少但很繁琐。惊讶的是，存在工具可以方便这一过程并提供有用的功能。`upload` 和 `dput` 是将软件包的所有文件拷贝到本地或远程仓库的常用程序。两者可以使用不同的上传方法，包括 FTP 和 SSH。与 `upload` 相比，`dput` 似乎维护得更活跃并且有一些有趣的功能。尽管如此，两者以相似的方式完成任务，对用户来说差不多。

在最简单的形式下，对 `changes` 文件调用 `dput`。`changes` 文件列出了软件包的所有组件（参见 9.2.12 节），`dput` 使用此列表来确定上传候选。因此，上传将涵盖源包（`dsc`、`diff.gz` 和 `orig.tar.gz` 文件）、从源包生成的所有二进制包以及 `changes` 文件本身。

`dput` 从配置文件读取管理到特定存档的参数。这些文件包含由规范上传名称标识的主机段（stanzas）。默认上传目标是主 Debian 上传队列，只有开发者可以使用（因为软件包必须由 Debian 开发者密钥签名）。此外，即使具有开发者身份，在使用默认值时也要小心，因为一旦上传队列中软件包的自动处理接管了软件包的文件，错误很难撤销。因此，将默认值重新定义为你自己的仓库并不是坏主意。如果软件包的最终目的地是官方 Debian 存档，通过额外参数指定要使用的上传队列是非常简单的。

在 `dput.cf` 中，我们可以为我们的本地上传队列创建一个规范命名为 "personal" 的段，并定义为上传到主 Debian 存档的默认值（文章的主要部分，但是主存档而不是美国分区）：

```bash
# cat <<EOF >> ~/.dput.cf

[DEFAULT]

default_host_main = personal

[personal]

method = local

incoming = /apt/incoming

EOF

# mkdir -p /apt/incoming
```

现在可以使用 `dput` 上传软件包。注意 `orig.tar.gz` 文件不是上传的一部分。这是因为我们上传了 Debian 版本 2，且 `orig.tar.gz` 文件与上传版本 1 时相同，假设它已存在于目标位置。`dpkg-genchanges` 的 `-sa` 参数覆盖了这一假设，如第 9.2.12 节所示。

```bash
# dput gruezi_1.2_2_i386.changes
Upload package to host apt .changes
Checking Signature on .changes
gpg: Signature made from Fri Jul 30 13:28:00 CEST DSA key ID B27C9467
gpg: Good signature from "Wilhelm Tell <hero@wilisse.ch>"
Good signature on /home/madduck/gruezi/1.2_2_i386.changes.
Checking Signature on .asc
```

> 对于官方 Debian，Debian 自动构建器似乎使得没有必要也上传二进制文件。然而，除了减轻负载之外，向存档上传二进制文件的要求迫使上传者至少在成功创建 DEB 文件的范围内验证软件的 Debian 化

```bash
gpg: Signature made Fri Jul 30 13:27:58 2004 CEST using DSA key ID B27C9
467
gpg: Good signature from "Wilhelm Tell <gruzi@suisse.ch>"
Good signature on /home/madduck/gruzi/gruzi_1.2-2.dsc
Successfully uploaded packages.
Not running default.
# 1. cp -F /apt/incoming
gruzi-common_1.2-2_all.deb gruzi_1.2-2.dsc
gruzi_1.2-2_i386.deb gruzi_1.2-2.diff.gz
gruzi_1.2-2_i386.changes
```

同样地，我们可以为可以通过 SSH 访问的远程主机仓库定义一个 `dput` 节（stanza），并使用 `scp` 进行传输。要 `dput` 到此主机而不是默认主机，我们必须将规范名称作为第一个参数：

```bash
# cat <<EOF >> ~/.dput.cf

[remote]

method = scp

qdn = the.remote.server

login = username

incoming = /apt/incoming

EOF

# dput remote gruzi_1.2-2_i386.changes

[...]
```
