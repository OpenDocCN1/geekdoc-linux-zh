
## 转换和向量规则宏

类型转换规则设置用于创建对象的规则的转换类型。转换规则还需要相应的访问向量规则来启用对象或进程的权限。代替创建单独的规则，使用宏来生成所需的规则。以下示例使用 `file_type_auto_trans` 宏为主目录中的用户文件设置转换和访问规则：

```
file_type_auto_trans(privhome, user_home_dir_t, user_home_t)
```

下一个示例为创建进程设置 Amanda 进程转换和访问规则：

```
domain_auto_trans(inetd_t, amanda_inetd_exec_t, amanda_t)
```

## 约束规则

可以对进程（如转换）施加进一步的限制，以确保更高的安全性。这些通过在 constraints 文件中的约束定义来实现。约束规则通常应用于转换操作，例如要求在进程转换中，用户身份保持不变，或者进程 1 在具有 privuser 属性的域中，进程 2 在具有 userdomain 属性的域中。字符 `u`、`t` 和 `r` 分别指代用户（user）、类型（type）和角色（role）。

```
constrain process transition
   ( u1 == u2 or ( t1 == privuser and t2 == userdomain ) )
```

## SELinux 策略配置文件

配置文件通常使用 `.te` 和 `.fc` 文件进行更改。这些文件在 `/usr/share/selinux` 的模块头中缺失。如果您正在添加模块，需要为其创建 `.te` 和 `.fc` 文件。然后您可以按照下一节所述创建模块并将其添加。

如果您想创建或修改自己的策略，则需要按照下文所述章节下载并安装 SELinux 参考策略的源代码文件。参考策略代码包含完整的 `.te` 和 `.fc` 配置文件集。

## 编译 SELinux 模块

您无需每次进行更改时都编译整个源代码，只需编译您更改的区域的模块即可。模块目录包含不同的模块。每个模块都由相应的 `.te` 文件构建。`checkmodule` 命令用于从 `.te` 文件创建 `.mod` 模块文件，然后使用 `semanage_module` 命令创建可加载的 `.pp` 模块文件以及 `.fc` 文件上下文文件。如 SELinux 文档中所述，如果您只需要更改 syslogd 的配置，首先使用以下命令通过 `syslogd.te` 创建 `syslogd.mod` 文件。`-M` 选项指定对 MLS 安全级别的支持。

```
checkmodule -M -m syslogd.te -o syslogd.mod
```

然后使用 `semanage_module` 命令从 `syslogd.mod` 文件创建 `syslogd.pp` 文件。`-f` 选项指定文件上下文文件。

```
semanage_module -m syslogd.mod -o syslogd.pp -f syslogd.fc
```

要添加模块，请使用 `semodule` 和 `-i` 选项。您可以使用 `-l` 选项检查模块是否已加载。

```
semodule -l syslogd.pp
```

对基础策略的修改在 `policy.conf` 文件中进行，该文件被编译为 `base.pp` 模块。

## 使用 SELinux 源代码配置

要进行自己的配置，您需要从 SRPMS 目录（源代码）下载并安装 `selinux-policy` 源代码文件。用于配置 SELinux 的 `.te` 文件不再属于 SELinux 二进制软件包的一部分。

下载 SRPMS 文件后，您需要使用带有 `-i` 选项的 `rpm` 命令在终端窗口中安装源代码。

```
rpm -i selinux-policy-2.3.18-10.noarch.srpm
```

源代码的压缩存档（`tgz` 文件）以及各种策略配置文件将安装到 `/usr/src/redhat/SOURCES`。（请确保您已安装 `rpm-build`；它默认未安装。）有关使用源文件的文档出现在另一个源 SRPMS 文件中，称为 `selinux-doc`。

您使用 `rpmbuild` 操作将该文件提取到 `/usr/src/redhat/BUILD` 中的 `src` 目录。在此目录中，您会找到一个 `policy/modules` 子目录。在那里，组织在几个目录中，如 `admin`、`apps` 和其他，您会找到 `.tc`、`.fc` 和 `.if` 配置文件。

```
rpmbuild -bp security-policy.spec
```

然后切换到 `/usr/src/redhat/BUILD/selref-policy` 目录并运行以下命令，将 selinux 源安装到 `/etc/selinux/selrefpolicy/src`：

```
make install-src
```
