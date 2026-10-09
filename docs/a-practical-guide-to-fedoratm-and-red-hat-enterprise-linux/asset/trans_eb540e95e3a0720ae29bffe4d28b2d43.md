

## 启用 ACL

在使用访问控制列表（ACL）之前，必须安装 `acl` 包。Fedora/RHEL 官方仅支持在 `ext2`、`ext3` 和 `ext4` 文件系统上使用 ACL，尽管其他文件系统也提供非正式的 ACL 支持。要在 `ext2`/`ext3`/`ext4` 文件系统上使用 ACL，必须使用 `acl` 选项挂载该设备（`noacl` 是默认设置）。例如，如果你想挂载代表 /home 的设备以便在 /home 中的文件上使用 ACL，你可以将 `acl` 添加到 `/etc/fstab` 中该设备的选项列表中：

```bash
$ grep home /etc/fstab
LABEL=/home  /home  ext4  defaults,acl  1 2
```

更改 `fstab` 后，你需要重新挂载 /home 才能使用 ACL。如果没有其他人在使用系统，你可以卸载它并再次挂载它（在具有 `root` 权限的情况下），前提是当前工作目录不在 /home 层级结构中。或者，当设备正在被使用时，你可以使用 `remount` 选项重新挂载 /home：

```bash
# mount -v -o remount /home
/dev/sda3 on /home type ext4 (rw, acl)
```

有关 `fstab` 的信息请参见第 524 页，有关 `mount` 的信息请参见第 520 页。

### 处理访问规则

`setfacl` 实用程序用于修改文件的 ACL，`getfacl` 用于显示文件的 ACL。当你使用 `getfacl` 获取没有 ACL 的文件的信息时，它会显示与 `ls -l` 命令部分相同的信息，只是格式不同：

```bash
$ ls -l report
-rw-r----r--· 1 max pubs 9537 01-12 23:17 report

$ getfacl report
# file: report
# owner: max
# group: pubs
user::r-w
group::r-
other::r-
```

`getfacl` 输出的前三行组成标题部分；它们指定文件名、文件所有者以及文件所属的组。更多信息请参见第 191 页的“`ls -l`：显示权限”。`--omit-header`（或仅 `--omit`）选项使 `getfacl` 不显示标题部分：

```bash
$ getfacl --omit-header report
user::r-w
group::r-
other::r-
```

在以 `user` 开头的行中，中间没有名称的两个冒号（`::`）表示该行指定的是文件所有者的权限。类似地，`group` 行中的两个冒号表示该行指定的是文件所属组的权限。`other` 后面的两个冒号是为了保持一致性而存在的：`other` 不能关联任何名称。

**setfacl** 的 `--modify`（或 `-m`）选项使用以下格式在文件的 ACL 中添加或修改一条或多条规则：

```bash
`setfacl --modify ugo:name:permissions file-list`
```

其中 *ugo* 可以是 *u*、*g* 或 *o*，分别表示该命令为特定用户、特定组或所有其他用户设置文件权限；*name* 是要为其设置权限的用户或组的名称；*permissions* 是权限，可以采用符号格式或绝对格式；*file-list* 是要应用这些权限的文件列表。当为其他用户（o）指定权限时，必须省略 *name*。符号权限使用字母表示文件权限（如 *rwx*、*r-x* 等），而绝对权限使用八进制数。虽然 **chmod** 使用三组权限或三个八进制数（分别对应所有者、组和其他用户），但 **setfacl** 使用单组权限或单个八进制数来表示授予由 *ugo* 和 *name* 表示的用户或组的权限。有关文件权限的符号和绝对表示法的更多信息，请参见第 193 页关于 **chmod** 的讨论。

例如，以下两个命令都为 **report** 文件的 ACL 添加一条规则，该规则赋予 **Sam** 对该文件的读写权限：

```bash
$ setfacl --modify u:sam:rw-  report
```

*或*

```bash
$ setfacl --modify u:sam:6  report
$ getfacl  report
# file: report
# owner: max
# group: pubs
user::rw-
user:sam:rw-
group::r--
mask::rw-
other::r--
```

包含 **user:sam:rw-** 的行表明名为 **sam** 的用户对该文件具有读写访问权限（rw-）。有关如何读取访问权限的解释，请参见第 191 页。有关以 mask 开头的行的描述，请参见以下可选部分。

当文件具有 ACL 时，即使 ACL 为空，`ls -l` 也会在权限后显示加号（+）：

```bash
$ ls -l  report
-rw-rw-r--+  1 max pubs  9537 01-12 23:17  report
```

> **可选：有效权限掩码**
> **getfacl** 输出中以 *mask* 开头的行指定了*有效权限掩码*。此掩码限制了授予 ACL 组 и 用户的有效权限。它不影响文件的所有者或文件所属的组。换句话说，它不影响传统的 Linux 权限。然而，由于 **setfacl** 总是将有效权限掩码设置为文件最不严格的 ACL 权限，因此除非你在为文件设置 ACL 后显式设置该掩码，否则掩码不起作用。你可以通过在 **setfacl** 命令中用 **mask** 替代 *ugo* 且不指定 *name* 来设置掩码。

以下示例将 report 文件的有效权限掩码设置为*读取*权限：

```bash
$ setfacl -m mask::r-- report
```

以下 **getfacl** 输出中的 **mask** 行显示有效权限掩码已设置为读取权限（r--）。显示 Sam 的文件访问权限的行表明其权限仍设置为读写。然而，该行右端的注释显示其有效权限为读取权限。

```bash
$ getfacl report
# file: report
# owner: max
# group: pubs
user::rw-
user:sam:rw-                        #effective:r--
group::r--
mask::r--
other::r--
```

如下一个示例所示，**setfacl** 可以修改 ACL 规则，并且可以一次设置多条 ACL 规则：

```bash
$ setfacl -m u:sam:r--,u:zach:rw- report
```

```bash
$ getfacl --omit-header report
user::rw-
user:sam:r--
user:zach:rw-
group::r--
mask::rw-
other::r--
```

`-x` 选项用于删除某用户或某组的 ACL 规则。它不影响文件所有者或文件所属组的权限。下一个示例显示 **setfacl** 正在删除赋予 Sam 访问文件权限的规则：

```bash
$ setfacl -x u:sam report
```

```bash
$ getfacl --omit-header report
user::rw-
user:zach:rw-
group::r--
mask::rw-
other::r--
```

使用 `-x` 选项时，不能指定 *permissions*。相反，只需指定 *ugo* 和 *name*。`-b` 选项后仅跟文件名，将从你指定的文件或目录中删除所有 ACL 规则及 ACL 本身。

**setfacl** 和 **getfacl** 都有许多选项。使用 `--help` 选项可以显示简短的选项列表，或参阅 *man* 页面获取详细信息。

### 为目录设置默认规则

以下示例显示 **dir** 目录最初没有 ACL。`setfacl` 命令使用 `-d`（默认）选项为 **dir** 的 ACL 添加两条默认规则。这些规则适用于 **dir** 目录中没有显式 ACL 的所有文件。这些规则赋予 **pubs** 组成员读写和执行权限，并赋予 **adm** 组成员读、写和执行权限。

```bash
$ ls -ld dir
drwx------ 2 max pubs 4096 02-12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: pubs
user::rwx
group::---
other::---
$ setfacl -d -m g:pubs:rwX,g:adm:rwX dir
```

以下 `ls` 命令显示 **dir** 目录现在具有 ACL，如权限右侧的 `+` 所示。`getfacl` 显示的每条默认规则都以 `default` 开头。前两条默认规则和最后一条默认规则分别指定文件所有者、文件所属组以及所有其他用户的权限。这三条规则指定传统的 Linux 文件权限，并优先于其他 ACL 规则。第三条和第四条规则指定 **pubs** 和 **adm** 组的权限。接下来是默认的有效权限掩码。

```bash
$ ls -ld dir
drwx------+ 2 max pubs 4096 02-12 23:15 dir
$ getfacl dir
# file: dir
# owner: max
# group: pubs
user::rwx
group::---
other::---
default:user::rwx
default:group::---
default:group:pubs:rwX
default:group:adm:rwX
default:mask::rwX
default:other::---
```

请记住，默认规则适用于目录中未显式分配 ACL 的文件。你也可以为目录本身指定访问规则。当你在具有默认规则的 ACL 的目录中创建文件时，该文件的有效权限掩码将基于文件的权限创建。在某些情况下，掩码可能会覆盖默认 ACL 规则。

在下一个示例中，`touch` 在 **dir** 目录中创建一个名为 **new** 的文件。`ls` 命令显示该文件具有 ACL。基于 `umask` 的值（第 469 页），所有者和

