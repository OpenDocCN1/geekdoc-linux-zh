

## pvs

## 1143

对象，表示共享对象是一个依赖项。该依赖项在运行时必须满足。如果共享对象还包含版本定义，则这些满足动态对象全局符号要求的版本定义也将记录在正在创建的动态对象中。在进程初始化时，运行时链接器使用任何版本依赖作为验证构建进程所使用的动态对象接口要求的手段。

## Options

如果你既没有指定 -d 也没有指定 -r 选项，则两者都已启用。

- -C 反混淆 C++ 符号名。Solaris 8 版本中新增。
- -d 打印版本定义信息。
- -s 与 -s 选项配合使用时，输出任何从版本控制全局绑定中还原的符号。按照惯例，这些符号条目位于 .symtab 段，并位于表示输出文件的 FILE 符号和表示生成输出文件的第一个输入文件的 FILE 符号之间。

这些被还原的符号条目被分配了伪造的版本定义 *REDUCED*。如果文件已剥离（参见 strip(1)）或无法确定符号条目，则不打印任何符号。

- -n 规范化版本定义信息。默认情况下，显示对象内的所有版本定义。然而，版本定义可以继承其他版本定义，在规范化下，只显示每个继承列表的头部。
- -Name 仅打印指定的版本定义名称及其任何继承版本定义的信息（与 -d 选项配合使用），或指定的依赖名称（与 -r 选项配合使用）。
- -O 创建单行版本定义输出。默认情况下，文件、版本定义和任何符号输出都会缩进以便于人工检查。此选项在每个输出行开头加上文件名和版本名，可能对于自动化工具的分析更有用。
- -r 打印版本依赖（要求）信息。
- -s 打印与每个版本定义相关的符号。在每个数据符号旁边带有数据项的大小（字节）。
- -v 显示弱版本定义和任何版本定义继承。与 -N 和 -d 选项配合使用，还会显示基础版本定义的继承情况。与 -s 选项配合使用，显示版本符号定义。

## Operands

- file 显示关于内部版本信息的 ELF 文件。

## 1144

## Examples

以下示例显示了 libelf.so.1 的版本定义。

```
castelf pvs -d /usr/lib/libelf.so.1
libelf.so.1;
SUNW_1.2;
SUNW_1.1;
SUNW_0.7;
SUNW_private.1.1;
```

```
castelf
```

以下示例使用 -n 和 -o 选项产生一个规范化的单行显示，适用于创建 mapfile 版本控制指令。

```
castelf pvs -dn /usr/lib/libelf.so.1
/usr/lib/libelf.so.1 - SUNW_1.2; /usr/lib/libelf.so.1 -
SUNW_private_1.1;
```

```
castelf
```

以下示例显示了 ldd 和 pvs 的版本要求。

```
castelf pvs -r /usr/bin/ldd /usr/bin/pvs
/usr/bin/ldd:
libelf.so.1 (SUNW_1.2);
ibc.so.1 (SUNW_1.1);
```

```
libelf.so.1 (SUNW_1.2);
ibc.so.1 (SUNW_1.1);
```

```
castelf
```

## Exit Status

如果未找到请求的版本信息，则返回非零值，否则返回 0 值。

当满足任一条件时，未找到版本信息：

- 你选择了 -d 选项，但未找到版本定义。
- 你指定了 -r 选项，但未找到版本要求。
- 你既没有指定 -d 也没有指定 -r 选项，且未找到版本定义或要求。

## Attributes

参见 attributes(5) 获取以下属性的描述：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNW/tool |

## See Also

```
ldd(1), ldd(1), strip(1), elf(3), attributes(5)
Linker and Libraries Guide
```

## pwait 1145

## pwait — 进程工具

## Synopsis

```
/usr/proc/bin/pwait [-v] pid...
```

## Description

参见 proc(1).

## pwck, grpck — 密码/组文件检查器

## Synopsis

```
/usr/sbin/pwck [filename]
/usr/sbin/grpck [filename]
```

## Description

pwck 命令扫描密码文件并记录任何不一致之处。检查包括对字段数量、登录名、用户到使用的用户 ID、组 ID，以及登录目录和要用作 shell 的程序存在的验证。默认的密码 grpck 验证组文件中的所有条目。此验证包括对字段数量、组名、组 ID 的检查，检查是否有任何登录名超过了 NGROUPS_MAX 组，以及所有登录名是否都出现在密码文件中。默认的组文件为 /etc/group。

> Note — 如果未指定文件名参数，grpck 将检查本地组文件 /etc/group，并确保组文件中遇到的所有登录名都是系统已知的。登录名可能由 getpwn(3) 例程提供。

## Files

```
/etc/group
/etc/passwd
```

## Attributes

参见 attributes(5) 获取以下属性的描述：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNW/tool |

## See Also

```
getpwn(3), group(4), passwd(4), attributes(5)
```

## 1146

## pwd

## Diagnostics

/etc/group 中没有登录名的组条目被标记。
组文件 'filename' 为空
/etc/passwd 或 /etc/group 文件为空文件
cannot open file: No such file or directory
/etc/passwd 或 /etc/group 文件不存在

## pwd — 返回工作目录名

## Synopsis

```
/usr/bin/pwd
```

## Description

pwd（print working directory）命令将当前目录的绝对路径显示到标准输出。Bourne shell, sh(1) 和 Korn shell, sh(1) 也有内置 pwd 命令。

> Note — 如果你将当前目录移动到上方，pwd 可能不会给出正确的响应。使用带有完整路径名的 cd(1) 命令来修正此情况。

## Example

以下示例显示当前目录，切换到另一个目录并显示新的工作目录。

```
shell% pwd
/export/home
shell% cd /etc
shell% pwd
/etc
```

## Environment Variables

参见 environ(5) 获取影响 pwd 执行的变量描述：LC_MESSAGES 和 PATH。

## Exit Status

```
0 成功完成。
发生错误。
如果检测到错误，输出不会写入标准输出，诊断信息将写入标准错误，且退出状态不为 0。

## pwdx

## Attributes

参见 attributes(5) 获取以下内容的描述：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNW/tool |
| Status | Enabled |

## See Also

cd(1), ksh(1), sh(1), shell_builtins(1), attributes(5), environ(5)

## Diagnostics

Cannot open file...
Read error in... 表示可能存在文件系统问题。请咨询 UNIX 系统管理员。

## pwdx — 进程工具

## Synopsis

```
/usr/proc/bin/pwdx pid..
```

## Description

参见 proc(1).

## r

## ranlib — 将归档转换为库

## Synopsis

```
/usr/bin/ranlib archive
```

## Description

> Note — ranlib 命令在 SunOS 4.x 中用于为归档添加索引。由于 ar(1) 命令提供了所有功能，此命令不再需要。它是为需要维护跨操作系统的 Makefile 的开发者提供的便利。

## Exit Status

ranlib 退出状态为 0。

## Attributes

参见 attributes(5) 获取以下内容的描述：

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNW/tool |

## 1150

## See Also

ar(1), ar(4), attributes(5)

## rc — 远程文件复制

## Synopsis

```
/usr/bin/rcp [-p] filename filename
/usr/bin/rcp [-pr] filename... directory
```

## Description

使用 rcp 命令在系统间复制文件。每个文件名或目录可以是本地文件名（不包含冒号 : 或反斜杠 \ 字符），也可以远程名称。hostname:path

或者，从 Solaris 8 版本开始，你可以指定包含冒号 (:) 或反斜杠 (\) 的本地文件名。hostname 为 IPv4 或 IPv6 地址字符串。参见 inet(7) 和 inet(6)。由于 IPv6 地址已经包含冒号，请将 IPv6 地址包含在方括号中，如下例所示。

```
[1080::200:417]:/tmp/file
```

否则，第一个出现的冒号可以解释为 hostname 和 path 的分隔符。如果名称不是完整路径名，则相对于主目录进行解释。你可以通过 \ 或 " 对远程路径加引号，以便字符在远程被解释。rcp 不提示密码；你的当前用户名必须在 hostname 上存在并允许 rsh(1) 执行远程命令。rcp 处理源、目标文件都不在当前系统的第三方拷贝。主机名也可以采用以下形式，其中用户名是远程主机上的你的本地用户名。

```
username@hostname:filename
```

rcp 还支持主机的互联网域名地址，以下格式指定了用户名、主机及其所在的域。
username@host.domain:filename

不是完整路径名的文件名相对于远程用户的主目录进行解释。

## Notes

rcp 设计用于不同主机之间的复制；尝试在远程将文件复制到自身，如以下命令所示，会导致文件严重损坏。

```
rcp tmp/file myhost:/tmp/file
```

当复制目标是文件而不是目录时，rcp 可能无法正确失败。

