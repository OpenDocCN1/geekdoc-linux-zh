

# OffSec

```
kali@kali:# touch filename.txt
kali@kali:# ls -l newfilename.txt
-rw-r--r-- 1 kali kali 6 Jun 12:31 filename.txt
```

在某些情况下，你的 `touch` 命令可能会因为目录权限而失败¹。虽然这超出了本介绍的范围，但值得知道，目录权限适用于该目录下的所有文件和目录。如果目录权限不允许我们在该目录中创建文件，`touch` 命令显然会失败。

`touch` 命令没有产生任何输出。`ls` 命令的输出包含了有关权限的信息，如字母 `rwx` 所示，其中 `r` 代表读取，`w` 代表写入，`x` 代表执行。横杠 `-` 表示该用户类别不具备相应的权限。在这种情况下，我们有权限读取和写入我们的新文件，但输出中没有 `x` 字符，这意味着没有类别有权限执行该文件。

作为特定文件的所有者，我们在创建它时默认会被授予读取和写入权限，但不会被授予可执行权限。换句话说，如果 `filename.txt` 是一个程序，我们将无法执行它。这是一个微小的安全特性，防止我们意外运行某些可能不想运行的内容。

让我们继续。在这种场景中，假设我们有一个简单的程序可以给出员工姓名列表。这个程序是我们创建的 Python 脚本 `find_employee_names.py`。尝试运行它。

```
kali@kali:$ ./find_employee_names.py
zsh: permission denied: find_employee_names.py
kali@kali:$ ls -l find_employee_names.py
-rw-r--r-- 1 kali kali 286 Jun 7 12:31 find_employee_names.py
```

我们尝试通过直接在终端中输入文件名 `find_employee_names.py` 来运行脚本。`./` 命令指示系统寻找该文件。这本应该可以运行，但输出并不是我们预期的结果。（`Zsh: permission denied`）错误消息表示，由于某种原因，我们无法执行（或）我们的脚本。

我们之前也运行过 `ls` 命令。与我们新创建的文件一样，输出中没有 "x" 字符，意味着我们没有执行权限。这解释了 `permission denied` 的输出。

让我们更改文件的可执行权限，并赋予自己执行该文件的权限（换句话说，将其作为程序运行）。我们可以使用 `chmod +x` 为我们的脚本文件添加可执行权限。让我们这样做并尝试运行脚本。

> ¹ (Linux Foundation, 2022), https://www.linuxfoundation.org/blog/classic-sysadmin-understanding-linux-file-permissions

```
kali@kali:- chmod +x find_employee_names.py
kali@kali:- ls -l find_employee_names.py
-rwxr-xr-x 1 kali kali 206 Jun 7 12:31 find_employee_names.py
```

- kali@kali:- ./find_employee_names.py
R. Jones
D. Diggs
G. Grice
C. Smith
C. Woods
D. Coles
J. Hunter
L. Hawkins
E.Turner
D. Hill

> 列表 14 - chmod 后的第二次尝试。

在我们赋予自己权限后，我们使用 `ls` 进行了快速检查，以查看输出是否发生变化。确实变化了！输出包含 "x" 字符，表明所有三类用户都被允许具有执行权限。

接下来，我们运行了脚本，幸运的是，我们收到了预期的输出。脚本为我们提供了当前员工的列表。

现在让我们改回来，让我们不再拥有执行该文件的权限。为了添加权限，我们使用 `chmod +x`，而这次我们将使用 `chmod -x`。

```
kali@kali:- chmod -x find_employee_names.py
kali@kali:- ./find_employee_names.py
zsh: permission denied: ./find_employee_names.py
```

> 列表 15 - 恢复原状

我们回到了起点，收到了与之前完全相同的错误信息。通过这次实验，我们应该对可执行权限位、`chmod` 工具以及 `+x` 和 `-x` 选项有一个非常基本的理解。

## 4.4.2 深入探讨：遇到奇怪的问题

让我们花点时间提醒一下，如果我们没有遵循所涵盖的所有技术步骤也是没关系的。某些示例之所以专门包含，是为了增加对 Linux 有更好理解的学生的趣味性。

让我们继续探索并进一步推进学习。

我们将考虑这样一个事实：`chmod` 命令本身就是一个文件。它遵循系统上其他文件的相同规则，包括权限规则。它存在于一个略不同的位置（`/usr/bin/`），与我们的脚本不同，但我们之所以能够运行 `chmod +x find_employee_names.py` 命令，唯一原因是 `chmod` 文件的权限被设置为允许我们作为程序运行。

现在，让我们问自己一个有趣的问题。

## OffSec: 使用 Kali 进行渗透测试

幸运的是，我们运行了它。

```
kali@kali:- find_employee_names.py
zsh: permission denied: find_employee_names.py
```

```
kali@kali: ls -l find_employee_names.py
-rw-r--r-- 1 kali kali 286 Jun 7 12:31 find_employee_names.py
```

```
kali@kali: ./find_employee_names.py
zsh: permission denied: ./find_employee_names.py
```

> 列表 16 - 某些不对劲

