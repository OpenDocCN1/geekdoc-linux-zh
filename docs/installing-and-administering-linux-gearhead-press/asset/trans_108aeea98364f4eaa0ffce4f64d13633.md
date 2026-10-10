

为了确保该后续版本的 Linux 无论您是普通用户还是 root 用户都保持一致性，Freston 向 Lady D 展示了他默认的（root 用户）umask：

```
# umask<Enter>
022
$ ls -id /home/ducinea<Enter>
```

### 更改权限模式

您还可以使用 umask 命令来指定在同一会话中创建的任何新文件或新目录上要设置的权限位。参数为数值：

```
$ umask numeric<Enter>
```

从默认值 666 和 777 中减去新的 umask 参数，您可以分别确定您想要用于文件和目录的新权限位。

在更改权限模式时，请记住以下事项：

- umask 值，因此权限位，仅适用于当前正在进行的会话，在所有者/用户注销并重新登录后不生效。新登录时应用默认值。
- 新的 umask 值仅影响在指定新 umask 值之后创建的文件和目录。因此，该命令对现有文件和目录没有影响。要更改现有文件和目录的权限，必须使用 chmod 命令。

请记住，一般来说，chmod 命令应用权限，而 umask 减去权限。通过操作这些命令，用户和系统管理员可以在适当的安全性和可访问性之间取得平衡。

### 创建个人目录

话虽如此，我们将演示如何创建一个具有适当权限的目录（准确地说是子目录），用于存储个人文档和数据。这样的目录将仅允许所有者访问它并在其中存储信息。之后，只有所有者会访问它，并查看和更改个人目录内的子目录结构和/或文件。此类目录的 ls -l 列表将类似于以下内容：

```
drwx----   5   me mygroup   4096 date time mydirectoryname
```

此类目录的数值模式为 700。

> 注意：这里建议的权限模式现在是使用最新版本的 Linux（内核版本约为 2.4.5 及更高版本）创建的主目录的默认模式。因此，如果您拥有最新版本的 Linux，这些信息可能有点多余。但如果您正在使用旧版本，那么这些资料可能仍然对您有益。

不过，要注意个人目录——您的主目录或您可能创建的任何目录。它们仍然可以被 root 用户（换句话说，系统管理员）访问和读取。

正如我们之前所学，创建目录的命令是 `mkdir`：

```
$ mkdir directoryname<Enter>
```

但是，有两种不同的方式来创建这样的目录：

- 临时更改您的 umask，创建目录，然后将您的 umask 改回另一个值（很可能是原始值）。这是较慢的方法。
- 创建目录，然后使用 `chmod` 更改其权限位。这种方法分一两步进行，是更简单、更快的方法。

在创建个人目录时，请考虑以下几点：

- 用户应在其个人目录上维护自己的执行 (x) 值，以确保自己的访问权限。
- 用户应意识到，虽然个人目录对所有其他用户不可见，但 root 用户仍然可以访问个人目录并读取其中包含的文件。

我们现在来看看这两种方法的示例。

#### 示例 6.5 使用 umask 和 mkdir 创建个人目录

唐·吉诃德想要在他的主目录中创建一个名为 *personal* 的私有目录。他记得可以用 `umask` 来实现。以下是他的操作方式：

```
$ cd<Enter>
$ pwd<Enter>
/home/quixoted
$ umask 077<Enter>
$ mkdir personal<Enter>
$ ls -l<Enter>
total 8
drwxrwx---5 quixoted knights 4096 May 26 10:18 admin
drwxr-x---5 quixoted knights 4096 Mar 07 08:11 Desktop
-rw-rw-r---1 quixoted knights 144 Jul 11 11:42 manuals
-rw-------1 quixoted knights 1116 May 26 10:18 mbox
drwxr-x---5 quixoted knights 4096 Apr 05 14:30 misc
drwxr-x---5 quixoted knights 4096 Jul 11 15:21 noble
drw----5 quixoted knights 4096 Jul 24 10:05 personal
$ umask 022<Enter>
$ umask<Enter>
022
```

#### 示例 6.6 使用 mkdir 和 chmod 创建个人目录

您使用 `chmod` 更改目录权限：

```
$ chmod numeric dirname<Enter>
```

这样，所有者/用户可以移动到其主目录，在其中创建子目录，更改新子目录的模式，然后检查新子目录上的权限。使用此策略，用户无需更改 umask 然后将 umask 恢复到之前的值。

让我们看看唐·吉诃德如何使用 chmod 策略在其主目录内创建同名 *personal* 的私有目录：

```
$ cd /home/quixoted<Enter>
$ mkdir personal<Enter>
$ chmod 700 personal<Enter>
$ ls -ld personal<Enter>
drw----5 quixoted knights 4096 Jul 23 13:45 personal
```

### 命令及其所需权限的示例

我们提供表 6.6 作为参考，帮助您确保在文件和目录上设置正确的权限以实现您想要的结果。请记住，要删除文件，您需要对包含该文件的目录拥有写权限。您不需要对该文件本身拥有写权限。

| 命令 | 源目录 | 源文件 | 目标目录 |
| :--- | :--- | :--- | :--- |
| cd | x | N/A | N/A |
| ls | r | N/A | N/A |
| ls -l | r, x | N/A | N/A |
| mkdir | x, w (parent) | N/A | N/A |
| rmdir | x, w (parent) | N/A | N/A |
| cat, more | x | r | N/A |
| mv | x, w | None | x, w |
| cp | x | r | x, w |
| touch | x, w* | N/A | None |
| rm | x, w | None | N/A |

* 当使用 `touch` 命令创建零长度文件时，需要源目录中的写权限，但在对现有文件使用 `touch` 以更新修改日期时则不需要。

### 练习

1. 切换到您的 *myscripts* 目录。显示该目录中文件的详细列表。记录您在第 5 章练习中复制的文件的拥有者和权限。记录 *mycal* 和 *mycat* 的权限：

```
$ cd myscripts<Enter>
$ ls -l<Enter>
```

2. 对 `/usr/bin` 目录中原始的 `cal` 和 `cat` 文件执行详细列表，并将权限与 `myscripts` 目录中的权限进行比较：

```
$ ls -l /usr/bin/cat /usr/bin/cal<Enter>
```

3. 更改 `myscripts` 目录中 `mycal` 和 `mycat` 的修改时间。检查时间是否已更改：

```
$ touch mycal mycat<Enter>
$ ls -l<Enter>
```

描述 `touch` 命令的另一种用法。

4. 执行必要的命令，以便您可以在主目录中通过名称 `home_mycal` 来引用 `myscripts` 目录中的 `mycal` 文件。

```
$ ln mycal ../home_mycal<Enter>
$ ls -l mycal<Enter>
$ ls -l /home/tsamx/home_mycal<Enter>
```

或者

```
$ ls -l ../home_mycal<Enter>
```

比较两个文件的详细信息。有区别吗？链接计数是多少？

5. 将目录更改为您的主目录。执行 `home_mycal`：

```
$ cd<Enter>
$ ./home_mycal<Enter>
```

> 注意：由于 Linux 中默认路径的限制，仅输入 `home_mycal` 将无法工作。

输出看起来像什么？现在，更改 `home_mycal` 文件的权限，使得您（该文件的所有者）只有只读权限。尝试运行 `mycal` 命令：

```
$ chmod 455 home_mycal<Enter>
$ ls -l home_mycal<Enter>
$ myscripts/mycal<Enter>
```

你能做到吗？为什么或为什么不？

删除 `home_mycal`：

```
$ rm home_mycal<Enter>
```

这会删除 `myscripts/mycal` 吗？为什么或为什么不？

```
$ ls -l myscripts/mycal<Enter>
```

将目录更改为 `myscripts` 目录。使用符号表示法配合 `chmod` 命令，从 `mycat` 文件中移除其他权限位上的读权限。检查新权限：

```
$ cd myscripts<Enter>
$ chmod o-r mycat<Enter>
$ ls -l mycat<Enter>
```

使用八进制表示法，更改 `mycat` 的权限，使得所有者权限位设置为只读，其他任何人没有权限。检查新权限：

