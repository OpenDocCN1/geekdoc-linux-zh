
```
martyp $ ls -al

total 22

drxr-xr-x 2 martyp staff 512 Mar 15 11:37 .

drwxr-xr-x 4 root sys 512 Mar 4 09:24 ..

-rw-r---- 1 martyp staff 124 Mar 15 11:36 .cshrc

-rw-r-- 1 martyp staff 562 Mar 4 09:24 .profile

-rw---- 1 martyp staff 7056 Apr 6 07:24 .sh_history

martyp $
```

这产生了一个短文件列表。这些文件（例如 `.profile` 和 `.cshrc`）分别是 `ksh` 和 `C shell` 的启动文件。登录系统时，你通常会执行 `shell` 的启动文件，并执行家目录中的任何本地启动文件。在这种情况下，我的家目录下有一个的 `ksh` 启动文件——只有一个内容很少的 `.profile`。该用户几乎所有的活动都来自系统使用的 `/etc/profile`。你可以轻松地读取 `/etc/profile`，从而看到你的系统管理员为你或其他用户设置了什么。你可以修改本地的 `.profile` 以包含各种功能。你的本地 `.profile` 通常在登录时运行，在所有与 `ksh` 相关的启动脚本执行后，你的环境就会为你设置好。

![](img/6969df54e516231f8e64fd1177ac1127_1426_1.png)

## 环境文件

你拥有的另一个文件是环境文件。该文件由 `ENV` 变量定义。使用环境文件，你可以定义哪些选项、别名和其他信息将传递给子进程。默认情况下，你的环境变量会被传递给子进程。你也可以使用环境文件传递其他信息。你应该查看 `ksh` 启动文件，包括 `/etc/profile.kshrc`。我们将在接下来的章节中讨论为你提供的许多特定 `ksh` 功能。

![](img/6969df54e516231f8e64fd1177ac1127_1427_0.png)

## 历史文件 `.sh_history`

`ksh` 记录了你执行过的命令列表。该列表保存在你家目录下的 `.sh_history` 文件中。如果你想查看之前执行过的命令，可以查看该文件。默认，`.sh_history` 存储了你执行过的所有命令。你可以通过设置 `HISTSIZE` 变量来限制历史命令的数量。

```bash
export HISTSIZE=500
```

当你退出 `shell` 时，当前的会话历史会被写入 `.sh_history` 文件中。当你下次登录时，这些命令会被重新加载。

## KornShell 简介

```bash
48  more .kshrc
49  cd ..
50  ls -al
51  ls -al | more
52  exit
53  ls -al
54  more .sh*
55  history
56  env | grep is
57  env | grep HIS
58  env | grep IS
59  env | more
60  env | grep FC
61  env | grep EDI
62  history
63  echo $HISTSIZE
64  echo $HISTSIZE
65  env | more
66  ls -al
67  history 128
68  history
69  history 1 104
70  exit
71  alias
72  more /etc/profile | grep alias
73  l1
74  la -al
75  ls -al
76  more .profile
77  ls -al
78  more .kshrc
79  alias l1="ls -al"
80  aliase
81  alias
82  l1
83  exit
84  alias
85  alias
86  history
87  fc -l
88  man fc
89  man fc
90  man fc
91  alias
92  ps
93  ps -ef
94  ps -efl
95  ps
96  ls -alF
97  ls -al
98  alias ls="ls -al"
99  alias
100 ls
101 alias
102 unalias ls
103 ls
104 ls -al
105 alias
106 history
107 alias
108 unalias history
109 history
110 fc -l
111 history
112 alias history="fc -1"
113 history
114 alias history="fc -1"
115 history
116 history 128
117 history 128 | more
118 history 200
119 alias
120 history 1
121 inv
122 env
123 env | more
124 history 1
125 more .profile
126 env | grep HIS
127 exit
128 env
129 env | grep HIS
130 more .profile
131 history
132 history 0
133 history
134 history -n
135 history 100
136 history -20
137 martyp $
```

`history 0` 会从第一条命令（0）一直打印到当前命令。因为默认只保存了 128 条命令，所以最早的几个旧命令（0 到 4）已经从历史列表中被移除了。这意味着当我们请求从第 0 号命令开始列表时，我们实际上是从第 5 号命令开始的。

要生成从第 *100* 命令到当前命令的列表，我们执行以下命令：

```bash
martyp $ history 100
100 ls
101 alias
```

要列出当前命令及其之前的 *20* 条命令，我们执行以下命令：

```bash
martyp $ history -20
116 history 128
117 history 128 | more
118 history 200
119 alias
120 history 1
121 inv
122 env
```

## 第 22 章 KornShell、C Shell 和 Bash 简介

`-20` 从当前命令向回追溯整 20 条命令。在这种情况下，`history` 使用当前命令作为默认起始位置。通过指定范围 `-l /20`，你可以列出当前命令之前的最后 20 条命令，如下：

```bash
martyp $ history -1 -20
136 history -20
135 history 100
134 history -n
133 history
132 history 0
131 history
130 more .profile
129 env | grep HIS
128 env
127 exit
126 env | grep HIS
125 more .profile
124 history 1
123 env | more
122 env
121 inv
120 history 1
119 alias
118 history 200
117 history 128 | more
martyp $
```

在此示例中，当前命令 `history -l -20` 没有显示在列表中，因为 `-l` 从之前的命令开始列出。这实际上是生成了一个命令范围。通过先指定 `-20` 再指定 `-l`，你可以反转最后 20 条命令的顺序，如下：

```bash
martyp $ history -20 -1
118 history 200
119 alias
120 history 1
121 inv
122 env
123 env | more
124 history 1
125 more .profile
126 env | grep HIS
127 exit
128 env
129 env | grep HIS
130 more .profile
131 history
132 history 0
133 history
134 history -n
135 history 100
136 history -20
137 history -1 -20
martyp $
```

你也可以生成从上一次执行命令到当前命令的列表。以下示例显示了从最后一个 `fc` 到当前命令的列表：

```bash
martyp $ history fc
110 fc -l
111 history
112 alias="fc -1"
113 history
114 alias="fc -1"
115 history
116 history 128
```
