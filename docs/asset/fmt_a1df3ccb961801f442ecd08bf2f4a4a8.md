
### 弹出 CD 并安装附加软件

- 3. 弹出 CD，并将标有 Solaris 8 Software 1 of 2 的 CD 插入 CD-ROM，允许 `vold` 自动挂载 CD。

按如下方式更改到已挂载 CD 上的 Tools 目录：

```
cd /cdrom/cdrom0/Solaris_8/Tools
```

- 4. 运行 `add_to_install_server` 脚本，将附加软件安装到安装服务器上的安装目录 `<install_dir_path>` 中，如下所示：

```
./add_to_install_server <install_dir_path>
```

例如，要将软件复制到 `/export/jumpstart` 目录，我发出以下命令：

```
./add_to_install_server /export/jumpstart
```

系统将响应以下消息：

```
The following Products will be copied to
/export/jumpstart/install/Solaris_8/Product:

Solaris_1_of_2

If only a subset of products is needed enter
Control-C and invoke ./add_to_install_server with
the -s option.

Checking required disk space...
Copying the Early Access products...
202847 blocks
Processing completed successfully.
```

在检查所需磁盘空间后，映像将从 CD 复制到磁盘。安装完成后，使用 Solaris 8 Software 2 of 2 CD 然后是 Solaris 8 Languages CD 重复此过程。

复制 Solaris CD 后，您可以使用 `patchadd -c` 命令修补安装服务器硬盘上的 Solaris CD 映像，以便每个客户端在安装后无需修补。

## 配置服务器

如果您为网络上的系统设置自定义 JumpStart 安装，您必须在服务器上创建一个名为配置目录的目录。此目录包含所有必要的自定义 JumpStart 配置文件，例如 `rules` 文件、`rules.ok` 文件、`class` 文件、`check` 脚本以及可选的 `begin` 和 `finish` 脚本。

包含 JumpStart 配置目录的服务器称为配置服务器。它通常与安装和引导服务器是同一系统，尽管它也可以是完全不同的服务器。配置服务器上的配置目录应由 `root` 所有，并且权限应设置为 `755`。

### 设置配置服务器

#### 21.3 设置配置服务器

要设置配置服务器，请按照以下步骤操作：

- 1. 选择充当服务器的系统，并以 `root` 身份登录。
- 2. 在服务器上的任何位置创建配置目录，例如 `/jumpstart`。
- 3. 为确保此目录在网络上共享，编辑 `/etc/dfs/dfstab` 文件，并添加以下条目：

  `share -F nfs -o ro,anon=0 /jumpstart`
- 4. 执行 `/etc/init.d/nfs.server start` 命令。如果系统已是 NFS 服务器，您只需输入 `shareall` 并按 Enter 键即可。
- 5. 将 JumpStart 文件即 `rules`、`rules.ok` 和 `class` 文件放在 `/jumpstart` 目录中。`rules`、`rules.ok` 和 `class` 文件将在本节后面介绍。

```
share -F nfs -o ro,anon=0 /jumpstart
```

你还可以使用 `add_install_client` 脚本来为你向 `/etc/dfs/dfstab` 文件中添加条目。`add_install_client` 脚本在标题为“设置客户端”的章节中进行了描述。

## 设置配置磁盘

设置配置服务器的一种替代方法是创建配置软盘，前提是要安装的系统具有软盘驱动器。如果您使用软盘进行自定义 JumpStart 安装，则必须将必要的自定义 JumpStart 文件规则文件、`rules.ok` 文件和类文件放在软盘的根目录上。包含 JumpStart 文件的软盘称为配置软盘。软盘上的自定义 JumpStart 文件应由 `root` 拥有，并且权限应等于 `755`。

#### 21.4 设置配置磁盘

以下是创建配置磁盘的步骤：

- 1. 通过键入来格式化磁盘

  `fdformat -U`
- 2. 在磁盘上创建 UFS 文件系统。如果您的系统使用卷管理器，请插入磁盘，它将自动挂载。
- 3. 通过发出 `newfs` 命令在磁盘上创建文件系统：

  `newfs /vol/dev/aliases/floppy0`

  `newfs` 命令在第 4 章“文件系统简介”中介绍。
- 4. 通过键入弹出磁盘

  `eject floppy`
- 5. 将格式化的磁盘插入磁盘驱动器。

您已完成可作为配置磁盘使用的磁盘的创建。现在，您可以在配置磁盘上创建规则文件并创建类文件以执行自定义 JumpStart 安装。

## 规则文件

规则文件是一个文本文件，应为要自动安装的每组系统包含一条规则。每条规则根据一个或多个系统属性区分一组系统，并将每组系统链接到一个类文件，该类文件是一个文本文件，定义了如何为该组中的每个系统安装 Solaris 软件。

在确定站点上每组系统如何安装后，您需要为要安装的每组特定系统创建一个规则文件。`rules.ok` 文件是 Solaris 安装程序用于执行自定义 JumpStart 安装的规则文件的已验证版本。

创建规则文件后，通过更改到 `/jumpstart` 目录并发出 `check` 命令，使用 `check` 脚本来验证它。如果 `check` 脚本成功运行，它将创建 `rules.ok` 文件。在自定义 JumpStart 安装期间，Solaris 安装程序读取 `rules.ok` 文件并尝试找到第一个具有与正在安装的系统匹配的系统属性的规则。如果发生匹配，安装程序将使用规则中指定的类文件来安装系统。

接下来显示 Sun Ultra 的示例规则文件。您可以在安装服务器上找到示例规则文件，位于 `<install_dir_path>/Solaris_8/Misc/jumpstart_sample` 目录中。其中 `<install_dir_path>` 是使用 `setup_install_server` 脚本设置安装服务器时指定的目录。

请注意，文件中的所有行都已注释掉。这些只是说明和示例条目，帮助系统管理员做出正确的条目。我为示例添加的最后一个未注释行是规则。我稍后会描述语法。代码表中的每一行都有一个规则关键字和该关键字的有效值。Solaris 安装程序从上到下扫描规则文件。如果程序将未注释的规则关键字和值与已知系统匹配；它将安装类文件字段中列出的类文件指定的 Solaris 软件。
