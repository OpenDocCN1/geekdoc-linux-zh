
The `Enhaces` field also describes a suggestion, but in a different context. It is indeed located in the suggested package, and not in the package that benefits from the suggestion. Its interest lies in that it is possible to add a suggestion without having to modify the package that is concerned. Thus, all add-ons, plug-ins, and other extensions of a program can then appear in the list of suggestions related to the software. Although it has existed for several years, this last field is still largely ignored by programs such as `apt` or `synaptic`. The original goal was to let a package like `xul-ext-adblock-plus` (a Firefox extension) declare `Enhaces: firefox, firefox-esr` and thus appear in the list of suggested packages associated to `firefox` and `firefox-esr`.

### Conflicts: the Conflicts Field

The `Conflicts` field indicates when a package cannot be installed simultaneously with another. The most common reasons for this are that both packages include a file of the same name, provide the same service on the same transmission control protocol (TCP) port, or would hinder each other's operation.

If it triggers a conflict with an already installed package, `dpkg` will refuse to install a package, except if the new package specifies that it will replace the installed package, in which case `dpkg` will choose to replace the old package with the new one. `APT` always follows your instructions: if you choose to install a new package, it will automatically offer to uninstall the package that poses a problem.

### 不兼容性：Breaks 字段

`Breaks`字段具有与`Conflicts`字段类似的效果，但具有特殊含义。它表示安装某个软件包将破坏另一个软件包（或该软件的特定版本）。一般来说，这两个软件包之间的不兼容是暂时的，并且`Breaks`关系特指不兼容的版本。

当一个软件包破坏已安装的软件包时，`dpkg`将拒绝安装它，而`apt`会尝试通过将被破坏的软件包更新到更新的版本来解决这个问题（假设该版本已修复，因此再次兼容）。

这种情况可能出现在没有向后兼容性的更新中：如果新版本不再与旧版本兼容，并且在没有做特殊规定的情况下导致其他程序发生故障，就会出现这种情况。`Breaks`字段有助于防止此类问题。

### 提供项目：Provides 字段

此字段引入了虚拟软件包这一非常有趣的概念。它有许多角色，但有两个角色尤为重要。第一个角色是使用虚拟软件包来与其关联一个通用服务（该软件包提供该服务）。第二个表明一个软件包完全替代了另一个软件包，并且为了这个目的，它也可以满足另一个软件包本可满足的依赖关系。因此，可以在不使用相同软件包名称的情况下创建替代软件包。

![](img/46e3313ea1bb2892f314630a4f0677b8_235_0.png)

#### 提供服务

让我们通过一个例子更详细地讨论第一种情况：所有邮件服务器，如`postfix`或`sendmail`，都称为提供`mail-transport-agent`虚拟软件包。因此，任何需要此服务才能正常工作的软件包（例如邮件列表管理器，如`smartlist`或`sympa`）只需在其依赖关系中声明需要`mail-transport-agent`，而不是指定一长串但不完整的解决方案列表。此外，在同一台机器上安装两个邮件服务器是没有用的，这就是为什么这些软件包中的每一个都声明与`mail-transport-agent`虚拟软件包冲突。软件包与其自身的冲突被系统忽略，但这种技术将禁止同时安装两个邮件服务器。

#### 与另一个软件包的互换性

当一个软件包的内容包含在一个较大的软件包中时，`Provides`字段也很有趣。例如，`libdigest-md5-perl` Perl 模块在 Perl 5.6 中是一个可选模块，并在 Perl 5.8 中作为标准集成。因此，自 5.8 版本起，`perl`软件包声明了`Provides: libdigest-md5-perl`，以便在系统拥有 Perl 5.8（或更新版本）时满足对该软件包的依赖关系。`libdigest-md5-perl`软件包本身已被删除，因为在旧版 Perl 被移除后它不再有任何用途。

![](img/46e3313ea1bb2892f314630a4f0677b8_236_0.png)

此功能非常有用，因为永远无法预见发展的变化，有必要能够适应重命名以及过时软件的自动替换。

### 替换文件：Replaces 字段

`Replaces`字段表明该软件包包含的文件也存在于另一个软件包中，但该软件包有权合法地替换它们。如果没有此规范，`dpkg`会失败，声称它不能覆盖另一个软件包的文件（技术上，可以使用`--force-overwrite`选项强制这样做，但这不被视为标准操作）。这使得可以识别潜在问题，并要求维护人员在决定是否添加此字段之前研究此事。

在软件包名称更改或软件包包含在另一个软件包中时，使用此字段是合理的。这也发生在维护人员决定以不同方式在由同一源软件包生成的多个二进制软件包之间分发文件时：被替换的文件不再属于旧软件包，而仅属于新软件包。

如果已安装软件包中的所有文件都被替换，则该软件包被视为已移除。最后，如果有冲突，此字段还鼓励`dpkg`移除被替换的软件包。

## 8.4.2. 配置脚本

除了控制文件外，每个 Debian 软件包的`control.tar.gz`归档文件可能包含由`dpkg`在处理软件包的不同阶段调用的多个脚本（`postinst`, `postrm`, `preinst`, `prerm`）。我们可以使用`dpkg -I`来显示这些位于`.deb`软件包归档文件中的文件：

```
$ dpkg -I /var/cache/apt/archives/zsh_5.3-1_amd64.deb | head
new debian package, version 2.0.
size 814486 bytes: control archive=2557 bytes.
838 bytes, 20 lines control
3327 bytes, 43 lines md5sums
969 bytes, 41 lines * postinst #!/bin/sh
348 bytes, 20 lines * postrm #!/bin/sh
175 bytes, 5 lines * preinst #!/bin/sh
175 bytes, 5 lines * prerm #!/bin/sh
Package: zsh
Version: 5.3-1
```
```
$ dpkg -I zsh_5.3-1_amd64.deb preinst
#!/bin/sh
set -e
#### Automatically added by dh_installdeb
dpkg-maintscript-helper symlink_to_dir /usr/share/doc/zsh zsh-common 5.0.7-3 -- "$@"
#### End automatically added section
```
