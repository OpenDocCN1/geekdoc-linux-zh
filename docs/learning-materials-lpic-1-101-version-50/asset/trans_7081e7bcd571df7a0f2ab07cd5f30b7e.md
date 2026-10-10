

在这里，我们使用 `-n` 参数调用 `sed`，这样 `sed` 根据 `p` 命令的指示，除了匹配表达式 `processor` 的内容外，不会打印任何内容。正如我们在 `grep` 解决方案中所做的那样，`wc -l` 将计算行数，从而得出处理器数量。

研究下一个示例：

```
$ sed -n /processor/p /proc/cpuinfo | sed -n '$='
```

该命令序列提供了与上一个示例相同的结果，在上一个示例中，`sed` 的输出被管道传输到 `wc` 命令。这里的区别在于，我们不是使用 `wc -l` 来计算行数，而是再次调用 `sed` 以提供等效功能。再次使用 `-n` 选项抑制 `sed` 的输出，除了我们显式调用的表达式 '$='。该表达式告诉 `sed` 匹配最后一行 ($)，然后打印该行号 (=)。

### 2. 按照以下任务，使用 `grep`、`sed`、`head` 和 `tail` 命令探索你本地的 `/etc/passwd` 文件：

- 哪些用户拥有 Bash 外壳的访问权限？

```
$ grep ":/bin/bash$" /etc/passwd
```

我们将通过仅显示使用 Bash 外壳的用户名来改进这个答案。

```
$ grep ":/bin/bash$" /etc/passwd | cut -d: -f1
```

用户名是第一个字段（`cut` 命令的 -f1 参数），并且 `/etc/passwd` 文件使用 `:` 作为分隔符（`cut` 命令的 -d: 参数），所以我们只需将 `grep` 命令的输出管道传输到合适的 `cut` 命令即可。

- 你的系统中有各种用户，它们的存在是为了处理特定程序或用于管理目的。它们没有外壳的访问权限。你的系统中有多少这样的用户？

找到这些用户的最简单方法是打印出不使用 Bash 外壳的账户的行：

```
$ grep -v ":/bin/bash$" /etc/passwd | wc -l
```

- 你的系统中有多少用户和组（记住：仅使用 `/etc/passwd` 文件）

`/etc/passwd` 文件中任何一行的第一个字段是用户名，第二个通常是 x，表示用户密码不存储在这里（它在 `/etc/shadow` 文件中加密）。第三个是用户 ID (UID)，第四个是组 ID (GID)。因此，这应该能给出用户数量：

```
$ cut -d: -f3 /etc/passwd | wc -l
```

嗯，大多数时候它是这样。然而，存在你设置不同的超级用户或其他特殊类型用户共享相同 UID（用户 ID）的情况。因此，为了保险起见，我们将 `cut` 命令的结果管道传输到 `sort` 命令，然后计算行数。

```
$ cut -d: -f3 /etc/passwd | sort -u | wc -l
```

现在，关于组的数量：

```
$ cut -d: -f4 /etc/passwd | sort -u | wc -l
```

- 仅列出 `/etc/passwd` 文件的第一行、最后一行和第十行

这样做即可：

```
$ sed -n -e '1'p -e '10'p -e '$'p /etc/passwd
```

请记住，参数 -n 告诉 sed 除了 p 命令指定的内容外不打印任何东西。这里使用的美元符号 ($) 是一个正则表达式，意味着文件的最后一行。

- 考虑这个 `/etc/passwd` 文件示例。将下面的行复制到一个名为 mypasswd 的本地文件中，用于本练习。

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
nvidia-persistenced:x:121:128:NVIDIA Persistence Daemon,,,:/nonexistent:/sbin/nologin
libvirt-qemu:x:64055:130:Libvirt Qemu,,,:/var/lib/libvirt:/usr/sbin/nologin
libvirt-dnsmasq:x:122:133:Libvirt Dnsmasq,,,:/var/lib/libvirt/dnsmasq:/usr/sbin/nologin
carol:x:1000:2000:Carol Smith,Finance,,Main Office:/home/carol:/bin/bash
dave:x:1001:1000:Dave Edwards,Finance,,Main Office:/home/dave:/bin/ksh
emma:x:1002:1000:Emma Jones,Finance,,Main Office:/home/emma:/bin/bash
frank:x:1003:1000:Frank Cassidy,Finance,,Main Office:/home/frank:/bin/bash
grace:x:1004:1000:Grace Kearn,Engineering,,Main Office:/home/grace:/bin/ksh
henry:x:1005:1000:Henry Adams,Sales,,Main Office:/home/henry:/bin/bash
john:x:1006:1000:John Chapel,Sales,,Main Office:/home/john:/bin/bash
```

从你的 mypasswd 文件中列出组 1000 中的所有用户（使用 sed 仅选择适当字段）：

GID 是 `/etc/passwd` 文件中的第四个字段。你可能会想试试这个：

```
$ sed -n /1000/p mypasswd
```

在这种情况下，你还会得到这一行：

```
carol:x:1000:2000:Carol Smith,Finance,,Main Office:/home/carol:/bin/bash
```

你知道这是不正确的，因为 Carol Smith 是 GID 2000 的成员，匹配是因为 UID 发生的。但是，你可能已经注意到，在 GID 之后，下一个字段以一个大写字母开头。我们可以使用正则表达式来解决这个问题。

```
$ sed -n /1000:[A-Z]/p mypasswd
```

表达式 [A-Z] 将匹配任何单个大写字母。你将在相应课程中对此了解更多。

仅列出该组所有用户的完整姓名（使用 sed 和 cut）：

使用你解决此练习第一部分时使用的相同技术，并将其管道传输到 `cut` 命令。

```
$ sed -n /1000:[A-Z]/p mypasswd | cut -d: -f5
Dave Edwards,Finance,,Main Office
Emma Jones,Finance,,Main Office
Frank Cassidy,Finance,,Main Office
Grace Kearns,Engineering,,Main Office
Henry Adams,Sales,,Main Office
John Chapel,Sales,,Main Office
```

还不完全正确！请注意结果中的字段可以由 `,` 分隔。因此，我们将输出管道传输到另一个 `cut` 命令，使用 `,` 作为分隔符。

```
$ sed -n /:1000:[A-Z]/p mypasswd | cut -d: -f5 | cut -d, -f1
Dave Edwards
Emma Jones
Frank Cassidy
Grace Kearns
Henry Adams
John Chapel
```

## 探索性练习答案

1. 再次使用之前练习中的 mypasswd 文件，设计一个 Bash 命令，从 Main Office 中随机选择一个人赢得抽奖比赛。使用 `sed` 命令仅打印 Main Office 的行，然后使用 `cut` 命令序列从这些行中获取每个用户的第一部分姓名。接下来，你想随机对这些姓名进行排序，并仅打印列表中的顶部姓名。

首先探索参数 -R 如何操作 `sort` 命令的输出。在你的机器上重复此命令几次（注意你需要用单引号括住 'Main Office'，以便 `sed` 将其作为单个字符串处理）：

```
$ sed -n /'Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f1 | sort -R
```

这是该问题的解决方案：

```
$ sed -n /'Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f1 | sort -R | head -1
```

2. Finance、Engineering 和 Sales 中有多少人工作？（考虑探索 `uniq` 命令。）

在之前练习所学的基础上继续构建。尝试以下操作：

```
$ sed -n /'Main Office'/p mypasswd
$ sed -n /'Main Office'/p mypasswd | cut -d, -f2
```

注意，现在我们不再关心 `:` 作为分隔符。当我们按 `,` 字符拆分行时，我们只想要第二个字段。

```
$ sed -n /'Main Office'/p mypasswd | cut -d, -f2 | uniq -c
      4 Finance
      1 Engineering
      2 Sales
```

`uniq` 命令仅输出唯一行（非重复行），参数 -c 告诉 `uniq` 计算相等行出现的次数。这里有一个注意事项：`uniq` 仅考虑相邻行。当这种情况不适用时，你必须使用 `sort` 命令。

3. 现在你想准备一个 CSV（逗号分隔值）文件，以便你可以轻松地从上一个示例中的 mypasswd 文件导入文件 names.csv 到 LibreOffice。文件内容将具有以下格式：

```
First Name,Last Name,Position
Carol,Smith,Finance
...
John,Chapel,Sales
```

提示：使用 `sed`、`cut` 和 `paste` 命令来实现所需结果。注意，逗号 (,) 将是此文件的分隔符。

从 `sed` 和 `cut` 命令开始，在之前练习所学的基础上构建：

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d" " -f1 > firstname
```

现在我们有文件 firstname，其中包含员工的名。

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d" " -f2 | cut -d, -f1 > lastname
```

现在我们有文件 lastname，其中包含每个员工的姓。

接下来我们确定每个员工在哪个部门工作：

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f2 > department
```

在我们开始处理最终解决方案之前，尝试以下命令，看看它们产生什么类型的输出：

```bash
$ cat firstname lastname department
$ paste firstname lastname department
```

现在是最终解决方案：

```bash
$ paste firstname lastname department | tr '\t' ','
$ paste firstname lastname department | tr '\t' ',' > names.csv
```

