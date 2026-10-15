
$ DIRECTORY [USER1]

      FILE                PROTECTION      SIZE      OWNER

LOGIN.COM          RW-W-R      10-JUL-96      512 USER1

MYFILE.TXT          RW-W-R      12-SEP-96      302 USER1

PROGRAM.FOR         RW-W-R      10-JAN-97      1024 USER1

TRAP                DIR-W-X      24-AUG-97      1340 USER1

```
$ DIRECTORY [USER1]

      FILE                PROTECTION      SIZE      OWNER

LOGIN.COM          RW-W-R      10-JUL-96      512 USER1

MYFILE.TXT          RW-W-R      12-SEP-96      302 USER1

PROGRAM.FOR         RW-W-R      10-JAN-97      1024 USER1

TRAP                DIR-W-X      24-AUG-97      1340 USER1
```

示例：

```
$ DIRECTORY [USER1]

      FILE                PROTECTION      SIZE      OWNER

LOGIN.COM          RW-W-R      10-JUL-96      512 USER1

MYFILE.TXT          RW-W-R      12-SEP-96      302 USER1

PROGRAM.FOR         RW-W-R      10-JAN-97      1024 USER1

TRAP                DIR-W-X      24-AUG-97      1340 USER1
```

示例：

```
$ DIRECTORY [USER1]

      FILE                PROTECTION      SIZE      OWNER

LOGIN.COM          RW-W-R      10-JUL-96      512 USER1

MYFILE.TXT          RW-W-R      12-SEP-96      302 USER1

PROGRAM.FOR         RW-W-R      10-JAN-97      1024 USER1

TRAP                DIR-W-X      24-AUG-97      1340 USER1
```

**UNIX**
示例：

```
% ls -s

total 1

drwxr--x  2 user staff 4096 Aug 24

-rw-r--r--  1 user staff 512 Jul 30 myfile

-rw-r--r--  1 user staff 302 Sep 12 program

-rw-r--r--  1 user staff 1024 Jan 10 test

drwxr-xr-x  2 user staff 1340 Aug 27 trap
```

示例：

```
% ls -i

total 1

drwxr-xr-x  2 user staff 4096 Aug 24

-rw-r--r--  1 user staff 512 Jul 30 myfile

-rw-r--r--  1 user staff 302 Sep 12 program

-rw-r--r--  1 user staff 1024 Jan 10 test

drwxr-xr-x  2 user staff 1340 Aug 27 trap
```

示例：

```
% ls -A

total 1

drwxr-xr-x  2 user staff 4096 Aug 24

-rw-r--r--  1 user staff 512 Jul 30 myfile

-rw-r--r--  1 user staff 302 Sep 12 program

-rw-r--r--  1 user staff 1024 Jan 10 test

drwxr-xr-x  2 user staff 1340 Aug 27 trap
```

示例：

```
% ls -R

total 1

drwxr-xr-x  2 user staff 4096 Aug 24

-rw-r--r--  1 user staff 512 Jul 30 myfile

-rw-r--r--  1 user staff 302 Sep 12 program

-rw-r--r--  1 user staff 1024 Jan 10 test

drwxr-xr-x  2 user staff 1340 Aug 27 trap

./trap:

total 0

-rw-r--r--  1 user staff 1024 Jan 10 test
```

![](img/e259ba2750941fa3d146eda78c65e89d_98_0.png)

### 4.2 文件特性

第三个示例 `ls -R` 不仅列出当前目录的内容，还列出目录树中所有子目录的内容（“递归”），在此示例包含了子目录 `trap`。此命令对应 OpenVMS 的 `DIRECTORY [...]`。`ls *` 命令（未显示）列出当前目录和目录下一级的文件。同样，`ls /*` 列出当前目录以及目录下一级和二级的文件。最后一个示例 `ls -l`（长列表）提供了有关文件特性的额外信息，包括文件类型、保护、所有者、组、大小和修改日期。参见第 4.2 节关于这些文件特性的讨论。这里所示选项可以组合：例如，`ls -Al` 显示包含隐藏文件的长列表。

除非通过选项修改，否则 `ls` 按字母顺序显示文件。以下条件定义了字母列表的排序：

1. 以点开头的文件
2. 数字
3. 大写字母
4. 小写字母

以下示例说明了 `ls` 显示文件的顺序：

```
% ls -A

.login

.test

123

123

Foo

foo

total 1
```

### 4.2 文件特性

让我们仔细观察 `ls -l` 和 `stat` 命令，它们产生文件特性的长列表。在这个示例中，`ls -i ../testfile` 使用相对路径显示位于当前目录上一级的 `testfile` 的特性。注意 UNIX 提供的完整列表比 OpenVMS 提供的列表更简洁。首先，我们看到 `ls` 不显示当前目录的名字。

![](img/e259ba2750941fa3d146eda78c65e89d_99_0.png) 第二，并不是所有的 UNIX 版本都支持访问控制列表 (ACL)。第三，UNIX 显示单个日期，在本例中，文件最后修改的日期。在某些 UNIX 实现中，可以通过额外的限定符获取最后备份和文件创建日期等日期。

示例：

```
% ls -i

total 1

drwxr-xr-x  2 user staff 4096 Aug 24

-rw-r--r--  1 user staff 512 Jul 30 myfile

-rw-r--r--  1 user staff 302 Sep 12 program

-rw-r--r--  1 user staff 1024 Jan 10 test

drwxr-xr-x  2 user staff 1340 Aug 27 trap
```

示例：

```
% stat mmb.txt

File: "mmb.txt"

Size: 63350

Device: 8,23

Access: Sat Sep

Modify: Tue Dec

Change: Tue Dec

user: staff

Filetype: Regular File

Inode: 77958

Links: 1

Created: 20 Feb 12:20 2002
```
