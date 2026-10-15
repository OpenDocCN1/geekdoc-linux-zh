
运行时错误发生在脚本开始运行并遇到使用错误的脚本名称、权限问题、路径问题或语法错误时，例如引号不匹配或拼写错误。

### 15.3.2 Naming Conventions

当你在 shell 提示符下输入命令时，shell 会在 UNIX/Linux 路径中搜索该命令。当你在提示符下输入脚本名称时，它被视为任何其他命令——shell 会在路径中搜索它。但假设你用与某个其他 UNIX 命令相同的名称命名脚本。假设例如你将程序命名为`ls`。哪个`ls`会被执行？这取决于路径中先找到哪个`ls`，而最可能的是 UNIX 命令会被执行而不是你的脚本。虽然避免将脚本命名为`ls`或`cat`似乎显而易见，但对于更晦涩的命令如`test`或`script`来说就不那么明显了。例如，由于 UNIX `test` 命令不产生输出，意识到存在命名问题可能很棘手。UNIX `script` 命令启动另一个交互式 shell，将你的终端会话复制到`typescript`文件中。另一个 shell 已开始运行并不明显，可能需要一些时间你才会意识到真的出了问题。因此，避免使用`test`和`script`作为文件名，就像你会避免使用`cat`或`ls`一样。

一种查看你是否已将脚本命名为 UNIX/Linux 命令的方法是使用 `which` 命令。它会显示找到命名程序的路径。参见 Example 15.1。你也可以在脚本前加上前导 `./`；然后脚本将在你的当前工作目录中运行。

#### EXAMPLE 15.1

```
1  $ cat test
#! /bin/sh
echo "She sells C shells on the C shore"
2  $ test
$ (no output)
3  $ echo $PATH
/usr/bin:/bin:/usr/local/bin:/usr/X11R6/bin:/home/ellie/bin:.
4  $ which test
/usr/bin/test
5  $ mv test nytest
6  $ nytest
She sells C shells on the C shore
```

#### EXPLANATION

- 1. 注意脚本名称是 `test`，它也是一个 UNIX/Linux 命令名称。
- 2. 当用户尝试运行名为 `test` 的脚本时，UNIX/Linux 命令反而运行了。UNIX `test` 命令不产生输出。

#### EXPLANATION (CONTINUED)

+ 3 用户的搜索路径被显示出来。第一个将被搜索的路径是`/usr/bin`。路径末尾的`.`代表用户当前的工作目录。
+ 4 `which` 命令定位了`test`命令并显示其完整路径名。UNIX/Linux 的`test`命令位于`/usr/bin/test`。
+ 5, 6 如果脚本名为`test`且使用的是唯一的名称，而非 UNIX/Linux 命令名，则应按预期运行。`test`脚本被重命名为`mytest`。

### 15.3.3 Insufficient Permissions

普通文件没有执行权限。如果脚本直接从命令行运行，它必须开启执行权限，否则 shell 会提示你权限不足。脚本通过 `chmod` 命令设置为可执行。

#### EXAMPLE 15.2

```
1 $ mytest
sh: ./mytest: Permission denied.
2 $ ls -l mytest
-rw-rw-r-- 1 ellie ellie 23 Jan 22 12:37 mytest
3 $ chmod +x mytest  # or chmod 755 mytest
4 $ ls -l mytest
-rwxrwxr-x 1 ellie ellie 23 Jan 22 12:37 mytest
5 $ mytest
She sells C shells on the C shore
```

#### EXPLANATION

+ 1 当脚本被执行时，会显示错误信息，表明脚本没有适当的权限运行。
+ 2 `ls -l` 命令显示脚本对任何人，包括脚本所有者，都没有执行权限。
+ 3 `chmod` 命令为所有人添加执行权限（`+x`）。现在脚本应该可以运行了。
+ 4 `ls -l` 命令显示新的权限。执行权限已打开。
+ 5 脚本按预期执行。

### 15.3.4 Path Problems

正如我们之前提到的，当你在命令行输入 shell 脚本的名称时，shell 会检查搜索 `PATH` 变量中列出的目录以定位你的脚本。如果 `.` 目录被列入路径，shell 会在当前工作目录中查找你的脚本。如果脚本在那里，它将被执行。然而，如果 `.` 不在你的路径中，你会收到错误信息：`Command not found`。要使 shell 能够定位你的脚本，你可以将点 (`.`) 目录添加到你的 `PATH` 中。然而，如果你拥有超级用户账户（`UID` 为 0 的账户），出于安全原因，建议你不要在搜索路径中包含 `.`。有两种替代方案，如果你选择不在 `PATH` 变量中放入 `.`：

- 1. 通过在脚本名前加上 `./` 来明确指出脚本的位置（例如，`./mytest`）。
- 2. 在脚本名前加上调用 shell 的名称（例如，`csh mytest` 或 `bash mytest`）。

当脚本名称作为参数传递给 shell 时，shell 会自动检查当前目录中是否存在该脚本名称。

#### EXAMPLE 15.3

```
1 $ cat mytest
#!/bin/sh
echo "Users may wish to include the . directory in their PATH"
2 $ echo $PATH
/usr/bin:/bin:/usr/local/bin:/usr/X11R6/bin:/home/ellie/bin:
3 $ mytest
not found
4 $ ./mytest  # this is one possible solution
Users may wish to include the . directory in their PATH
5 $ PATH=$PATH:.  # this solution should only be used by non-root
$ export PATH # bash, sh, ksh set PATH this way
% setenv PATH $PATH:.  # csh/tcsh set path this way
6 $ mytest
Users may wish to include the . directory in their PATH
```

#### EXPLANATION

+ 1. Bourne shell 脚本被显示出来。它位于用户当前的工作目录中。
+ 2. `PATH` 变量不包含 `.`；`.` 代表当前工作目录。
+ 3. shell 无法定位 `mytest` 脚本。
+ 4. shell 现在能够定位脚本，因为目录（即 `.`）已包含在脚本名称中。
+ 5. `PATH` 已更新以包含当前目录。第一种语法可用于 `sh`/`ksh`/`bash` shell，第二种用于 `csh`/`tcsh`。
+ 6. 脚本现在运行正确。

### 15.3.5 The Shbang Line

当你创建脚本时，脚本的第一行通常是 shbang (`#!`) 行。当脚本启动时，UNIX 内核会检查文件第一行以确定要执行什么类型的程序。shbang 标记 (`#!`) 之后跟随的路径是将被调用来解释此脚本的 shell 的位置。`#!` 字符必须是文件中的前两个字符，此功能才能正常工作。如果文件顶部有空行或空白，此功能将被忽略，该行将被解释为普通注释行。

#### EXAMPLE 15.4

```
(The Script)
1
2 #!/bin/csh
3 # Scriptname: shbang.test
setenv MYVAR 18
echo "The value of MYVAR is $MYVAR"
```

```
(The Output)
./shbang.test: line 3: setenv: command not found

The value of MYVAR is
```

```
(The Script)
4
#!/bin/csh
setenv MYVAR 18
echo "The value of MYVAR is $MYVAR"
```

```
(The Output)
The value of MYVAR is 18
```

#### EXPLANATION

+ 1 注意此脚本顶部有一个空行。另请注意，脚本是为 C shell 编写的。第 3 行的 `setenv` 命令在 Bourne、Korn 或 Bash shell 中无法工作。
+ 2, 3 因为 `#!` 行不是脚本的第一行，脚本将由用户的登录 shell 执行。如果登录 shell 是 `ksh`，则 Korn shell 将执行脚本；如果是 `bash`，则 Bash shell 将执行脚本。然而，如果用户的登录 shell 是 C shell，此脚本将由 Bourne shell 执行。错误信息显示是因为 Bourne shell 不理解 `setenv` 命令。
