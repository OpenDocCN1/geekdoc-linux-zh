

## ACL 继承

与 POSIX ACL 类似，NFSv4 ACL 允许新创建的对象从其包含的目录继承访问控制条目。然而，NFSv4 系统功能更强大，也更令人困惑。以下是重要要点：

- 任何 ACE 都可以被标记为可继承。对新创建的子目录（`dir_inherit` 或 `d`）和新创建的文件（`file_inherit` 或 `f`）的继承是分别标记的。
- 你可以通过在父目录上创建单独的访问控制条目并适当地标记它们，来对新文件和新目录应用不同的访问控制条目。你也可以通过同时打开 `d` 和 `f` 标志，将单个 ACE 应用于所有新子实体（无论类型）。
- 从访问确定的角度来看，访问控制条目对父（源）目录的影响是否可继承是相同的。如果你希望条目应用于子项但不应用于父目录本身，请打开 ACE 的 `inherit_only`（`i`）标志。
- 新子目录通常会继承每个 ACE 的两份拷贝：一份关闭了继承标志，应用于子目录本身；另一份打开了 `inherit_only` 标志，用于设置新子目录传播其继承的 ACE。你可以通过在父目录的 ACE 拷贝上打开 `no_propagate`（`n`）标志来抑制第二个 ACE 的创建。最终结果是 ACE 仅传播到原始目录的直接子项。
- 不要将访问控制条目的传播与真正的继承混淆。你在 ACE 上设置继承相关标志，只是意味着该 ACE 会被复制到新实体。它并不会在父目录与其子目录之间创建持续的关系。如果你之后更改父目录上的 ACE 条目，子目录不会被更新。

表 6.10 总结了这些各种继承标志。

### 表 6.10 NFSv4 ACE 继承标志

| Code | Verbose name | Meaning |
|---|---|---|
| f | file_inherit | 将此 ACE 传播到新创建的文件 |
| d | dir_inherit | 将此 ACE 传播到新创建的子目录 |
| i | inherit_only | 传播，但不应用于当前目录 |
| n | no_propagate | 传播到新子目录，但不传播到其子目录 |

## Solaris 中的 NFSv4 ACL 查看

![](img/14d78e3cecac4581d37024baf1e94cca_217_0.png)

Solaris 已将其实 ACL 支持集成到 **ls** 和 **chmod** 中，这是一种不错的方法，也是对命令通常功能的直接扩展。POSIX 和 NFSv4 ACL 均以这种方式得到支持，尽管这里仅显示 NFSv4 示例。你看到或设置的 ACL 的具体类型取决于底层文件系统。

ls -v 显示文件系统对象的 ACL 信息。与 -l 一样，如果你想查看目录的 ACL，必须包含 -d 选项；否则 ls -v 会显示目录每个子项的 ACL。以下是一个简单的 (!) 示例：

```
solaris# mkdir /var/tmp/example
solaris# ls -dv /var/tmp/example
drwxr-xr-x 2 garth staff 2 jan 11 07:19 /var/tmp/example
0:owner@:deny
1:owner@:list_directory/read_data/add_file/write_data/add_subdirectory/append_data/write_xattr/execute/write_attributes/write_acl/write_owner:allow
2:group@:add_file/write_data/add_subdirectory/append_data:deny
3:group@:list_directory/read_data/execute:allow
4:everyone@:add_file/write_data/add_subdirectory/append_data/write_xattr/write_attributes/write_acl/write_owner:deny
5:everyone@:list_directory/read_data/read_xattr/execute/read_attributes/read_acl/synchronize:allow
```

这个新创建的目录似乎具有复杂的 ACL，但实际上它是假的——此 ACL 只是将第一行输出中显示的九位模式翻译成 ACLEse。它不需要文件系统存储实际的 ACL，因为 ACL 和模式是等效的。（此类 ACL 被称为“平凡的”。）如果目录具有实际的 ACL，ls 会在模式位末尾显示一个 +（即 drwxr-xr-x+）以指示 ACL 的存在。

每个编号的条款代表一个访问控制条目。格式为
index:entity:permissions:inheritance_flags:type

索引号由 ls 添加以提高清晰度，并不是实际 ACL 的一部分。它们可以在后面的 chmod 命令中用于标识要替换或删除的特定 ACE。

实体可以是关键字 owner@、group@ 或 everyone@，或 user:username 或 group:groupname 这样的形式。

ACE 的类型为 allow 或 deny。理论上，alarm 和 audit 也是允许的，但 ZFS 并未实现这些功能。

权限和 inheritance_flags 都是以斜杠分隔的选项列表。奇怪的是，如果标志全部关闭，ls 会省略 inheritance_flags 字段（以及其中一个冒号分隔符），但它不会对权限做同样的处理。

为增加混乱，ls 对 r（读取数据/列出目录）、w（写入数据/添加文件）和 p（追加数据/添加子目录）权限位显示多个名称，仿佛它们是单独的权限。事实上，它们是同一位的文件和目录特定解释，并且会始终一起存在或一起缺失。

