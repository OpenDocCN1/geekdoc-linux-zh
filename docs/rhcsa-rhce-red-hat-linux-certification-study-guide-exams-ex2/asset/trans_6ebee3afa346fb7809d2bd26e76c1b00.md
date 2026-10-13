

## 为 ACL 配置目录

设置支持 ACL 的目录有两种方法。首先，你可以为其他所有用户设置常规的执行位。在所述的目录上执行此操作的一种方法如下所示：

```
# chmod 701 /home/examprep
```

这是一种提供目录中文件访问权限的最小化方式。除 `examprep` 和 `root` 以外的用户无法列出该目录中的文件。他们必须知道 `TheAnswers` 文件确实存在才能访问该文件。

然而，当为其他用户设置了执行位后，任何用户都可以访问 `/home/examprep` 目录中他有权限访问的文件。这应该引起安全警报。任何用户？尽管文件是隐藏的，你是否真的想给所有用户真正的权限？当然，该 `/home/examprep` 目录中的 ACL 仅针对 `TheAnswers` 文件设置，但这是你自愿降低的一层安全防护。

正确的做法是对 `/home/examprep` 目录应用 `setfacl` 命令。与常规权限相关的控制权限有限；正确的 ACL 可以允许管理员向多种用户和组授予读、写和执行权限。因此，设置共享的最安全方法是仅为所述目录上的 `michael` 用户账户设置 ACL 执行权限，命令如下：

```
# setfacl -m u:michael:x /home/examprep
```

由于 `examprep` 用户是 `/home/examprep` 目录的所有者，该用户也可以运行上述 `setfacl` 命令。

有时，你可能希望将这些 ACL 应用于目录中的所有文件。在这种情况下，可以使用 `-R` 开关来递归地应用更改；例如，以下命令允许用户 `michael` 拥有 `/home/examprep` 目录中所有文件以及可能存在的任何子目录的读取和执行权限：

```
# setfacl -R -m u:michael:r-x /home/examprep
```

有两种方法可以取消这些选项。首先，你可以对前面的命令应用 `-x` 开关，省略权限设置：

```
# setfacl -R -x u:michael /home/examprep
```

或者，你可以使用 `-b` 开关；然而，这将擦除所述目录上为所有用户配置的 ACL（如果使用 `-R` 开关，则适用于适用的子目录）：

```
# setfacl -R -b /home/examprep
```

## ACL 的特殊限制

ACL 也可用于限制特定用户的权限。例如，某些 RHEL 6 安装包含 GUI 的标准访客用户 `xguest`。对于此类系统，你可能希望使用 ACL 来限制对特定文件或目录的访问。例如，以下 `setfacl` 命令可用于限制对 `/etc/passwd` 文件的访问：

```
# setfacl -m u:xguest:--- /etc/passwd
```

虽然 `/etc/passwd` 文件通常不包含任何密码，但它确实包含用户名。这通常是许多破解者的起点；拥有密码破解程序的恶意用户可以将其精力集中在已知存在弱点的标准用户上。如果没有 `xguest` 用户，此命令会导致一个略显令人困惑的错误消息。如果需要，你可以通过安装 `xguest` 包或替换其他用户名来测试此操作。

当然，这些操作可以递归应用；如果你不希望用户 `xguest` 访问 `/etc/` 目录树中的任何文件，以下命令将上述更改递归应用于：

```
# setfacl -R -m u:xguest:--- /etc
```

要测试结果，尝试在 `/etc` 目录树的某个位置的文件上使用 `getfacl` 命令。例如，`getfacl /etc/httpd/conf/httpd.conf` 命令检查与 Apache Web 服务器的主要配置文件相关的 ACL。请注意以下输出中常规用户和 `xguest` 用户之间的区别：

```
# file: etc/httpd/conf/httpd.conf
# owner: root
# group: root
user::rw-
user:xguest:---
group::r-
mask::r--
other::r--
```

用户所有者具有读和写权限。所有其他常规用户都具有读权限。但 `xguest` 用户没有任何权限对该文件执行任何操作。

与单个文件一样，可以使用 `-x` 开关取消对 `xguest` 用户的 ACL 更改。例如，以下命令递归取消该用户的 ACL 设置：

```
# setfacl -R -x u:xguest /etc
```

但是，在使用 ACL 时，你不能拒绝用户访问其主目录。

## ACL 与掩码

与 ACL 关联的掩码限制了文件上可用的权限。图 4-2 中显示的掩码是 `rwx`，这意味着没有限制。如果设置为 `r`，那么像 `setfacl` 这样的命令只能授予读权限。要将 `TheAnswers` 文件的掩码更改为只读，请运行以下命令：

```
# setfacl -m mask:r-- /home/examprep/TheAnswers
```

现在使用 `getfacl /home/examprep/TheAnswers` 命令检查结果。请注意特定用户的条目。根据之前授予用户 `michael` 的 ACL 权限，你将看到与图 4-2 的差异：

```
user:michael:rwx   #effective:r--
```

换句话说，使用 `r--` 掩码，你可以尝试为用户提供世界上的所有权限。但该掩码只能设置读权限。

## 练习 4-3

### 使用 ACL 拒绝用户

在本练习中，你将设置 ACL 以拒绝常规用户访问环回配置文件。这是位于 `/etc/sysconfig/network-scripts` 目录中的 `ifcfg-lo` 文件。本练习假设你已配置了一个常规用户。由于我在系统中配置了用户 `michael`，因此本练习中列出的常规用户是 `michael`。请相应地替换。要拒绝此类访问，请采取以下步骤：

- 1. 备份环回设备的当前配置文件副本。它是位于 `/etc/sysconfig/network-scripts` 目录中的 `ifcfg-lo` 文件。（提示：使用 `cp` 而不是 `mv` 命令。）
- 2. 执行 `setfacl -m u:michael:--- /etc/sysconfig/network-scripts/ifcfg-lo` 命令。
- 3. 检查结果。在 `/etc/sysconfig/network-scripts` 和备份目录中的该文件的两个副本上运行 `getfacl` 命令。它们之间有何不同？
- 4. 登录为目标用户。从 root 管理账户执行此操作的一种方法是使用 `su - michael` 命令。
- 5. 尝试在 vi 文本编辑器中甚至使用 `cat` 命令读取 `/etc/sysconfig/network-scripts/ifcfg-lo` 文件。会发生什么？
- 6. 使用备份目录中的文件重复上述步骤。会发生什么？
- 7. 现在从 `ifcfg-lo` 文件的备份运行 `cp` 命令，并覆盖 `/etc/sysconfig/network-scripts` 中的版本。（不要为此目的使用 `mv` 命令。）你可能需要作为 root 用户返回以执行此操作。
- 8. 再次尝试 `getfacl /etc/sysconfig/network-scripts/ifcfg-lo` 命令。你对结果感到惊讶吗？
- 9. 有两种方法可以恢复 `ifcfg-lo` 文件的原始 ACL 配置。首先对该文件应用 `setfacl -b` 命令。成功了吗？使用 `getfacl` 命令进行确认。如果已应用其他相关命令，可能成功也可能未成功。
- 10. 恢复文件原始 ACL 的唯一确定方法是恢复备份，即首先删除 `/etc/sysconfig/network-scripts` 目录中更改过的文件，然后从备份目录复制该文件。
- 11. 但是，如果你执行第 10 步，你可能还需要使用 `restorecon -F /etc/sysconfig/network-scripts/ifcfg-lo` 命令恢复文件的 SELinux 上下文。有关 `restorecon` 命令的更多信息将在本章稍后部分提供。

## NFS 共享与 ACL

虽然没有证据表明红帽考试会涵盖基于 NFS 的 ACL，但这是 Linux 管理员应该知道的功能。因此，本节中的描述仅提供示例，远非完整。IBM 在 www.ibm.com/developerworks/aix/library/au-filesys_NFSv4ACL/index.html 提供了更完整的描述。

通常，`/home` 目录取自共享的 NFS 目录。事实上，基于 NFS 的 ACL 比标准 ACL 更精细。此功能是在 RHEL 6 的标准 NFS 版本 4 中引入的。为此，`nfs4_getfacl` 命令可以显示共享目录中文件相关的 ACL。根据之前给出的 ACL，图 4-3 显示了 `nfs4_getfacl` 命令的输出。

输出采用以下格式：

```
type:flags:principal:permissions
```

其中各项设置由冒号分隔。简而言之，显示的两个类型要么允许 (A) 要么拒绝 (D) 所述主体（用户或组）获得指定权限。图 4-3 中没有显示标志，标志可以提供相对精细的控制。主体可以是小写的常规用户或组。它也可以是通用用户，如文件的 OWNER（所有者）、拥有该文件的 GROUP（组）或指定为 EVERYONE 的其他用户。如表 4-4 所示，权限更为精细。其效果取决于对象是文件还是目录。

NFS 作为客户端的配置在第 6 章中涵盖，与其他本地和网络文件系统一起。NFS 服务器的配置是 RHCE 目标，在第 16 章中涵盖。

### 图 4-3

NFS 版本 4 ACL

```
[michael@server1 ~]$ nfs4_getfacl /test/examprep/
A::OWNER@:rwatxTCy
A::michael@localdomain:xtcy
A::GROUP@:tcy
A::EVERYONE@:tcy
[michael@server1 ~]$ nfs4_getfacl /test/examprep/TheAnswers
D::OWNER@:x
A::OWNER@:rwatTCcy
A::michael@localdomain:rwaxtcy
A::GROUP@:rwatcy
A::EVERYONE@:tcy
[michael@server1 ~]$
```

