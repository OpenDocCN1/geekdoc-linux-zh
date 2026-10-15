
你可以对环境所做的最有更改之一就是向默认路径添加内容，该路径是由 path 语句定义的。path 语句告诉 shell 去哪里查找命令、脚本和程序。也就是说，如果你发布一个命令，path 语句会告诉系统按照特定顺序在每个命名目录中查找该命令。

除非你确定自己在做什么，否则请不要从你的 path 中删除任何内容，但你可以根据意愿添加任何额外的目录。

按照以下步骤，你通过识别 path 语句的位置，然后编辑包含它的文件来更改你的 bash path（**代码列表 8.11**）。

# 更改你的 Bash path

1. `more ~/.bash_profile ~/.bashrc`

   首先，按照执行的顺序修改你的配置文件（仅限你可以编辑的）。

   检查你的系统配置文件查找 path 语句。如代码列表 8.11 所示，它看起来像 `PATH=/bin:/usr/bin:/usr/local/bin`。如果你有多个 path 语句，找到最后一个执行的一个。

   记住，不同系统的配置会有不同，因此你可能需要稍微挖掘一下找到你个人的路径语句。

2. `cp .bash_profile .bash_profile_backup`

   为包含 path 语句的文件创建一个备份，以便在你出错时可以恢复。如果需要更多关于复制文件的信息，请参第 2 章。

**代码列表 8.11** 你的第一步是找到 path 语句的位置。

![](img/30f4227f5df2c6cea63896bef2fc574f_187_0.png)

3. `vi _bash_profile`

   使用你喜欢的编辑器打开 path 语句所在的文件。

4. `PATH=$PATH:/local/local`

   在紧下方添加一条新语句。

5. 保存文件并退出。

6. `su -`

   如你在第 3 章中所学的，此命令启动了一个新的 shell。

```bash
# jdoe@frazz.example.com:/home/j
# .bashrc

# 用户特有的别名和函数

# 加载全局定义
if [ -f /etc/bashrc ]; then
  /etc/bashrc
fi
PS1=\uu \d $ #
```

7. `echo $PATH`

## 提示

```bash
[ejr@hobbes ejr]$ echo $PATH
usr/bin:/usr/local/bin:/usr/local/games
```

- 如果你查看各种文件，可能会发现某个包含美元符号（$）的 path 语句。例如，你可能会发现类似 `PATH=/bin/` 的。

- 你可以使用 `grep` 更容易找到设置 path 的配置文件。`grep ~/.bash*` 是一个很好的开始。

- 如果你将所有更改保持在一起，以后你的系统配置文件将少很多混乱。因此，你应该将 path 语句放在一起，而不是随地在你的配置文件中插入随机语句。

# 设置你的 Bash 提示符

你可以设置提示符包含各种信息。以下列表显示了向提示符中添加特定类型信息时要使用的代码（并帮助你翻译现有提示符中的代码）：

- `\u` 显示当前用户的用户 ID。

- `\w` 显示带有路径当前工作目录，在主目录内使用 `~` 符号。

- `\W` 显示不带路径当前目录。

- `\t` 显示时间。

- `\d` 显示日期。

- `\n` 强制换行，使提示符分行显示。

- `\h` 显示计算机的主机。

2. `vi ~/.bashrc`

   由于设置提示符的文件位于系统级的 `/etc` 目录，我们无法直接修改它们，因此必须在我们主目录下的 `.bashrc` 或不同的配置文件中进行更改。

3. `PS1="u \d $ "`

   例如，我们经常设置提示符包含用户 ID（因为在不同系统上有许多个不同的账户，我们需要提醒）和日期（因为我们经常四处奔波）。我们将此内容添加到文件末尾，这样它的优先级将高于从 `~/.bashrc` 引用的 `/etc/bashrc` 文件中的 `PS1` 设置（图 8.4）。

4. 保存文件并退出编辑器。

5. `su - ejr`

   使用更改后的提示符登录以尝试效果。

### ✓ 提示

- 注意提示符代码末尾的空格：`PS1="u \d $ "`——这会让提示符更容易使用，因为可以避免命令与提示符重叠。

- 在修改配置文件之前，考虑像第 3 章讨论的那样，在 shell 提示符处更改你的 `PS` 环境变量。这样，你可以在更改配置文件之前尝试修改后的 shell 提示符。

# 查看你的 ksh 配置文件

如代码列表 8.14（在下一页）所示，你可以使用任选的编辑器查看 ksh 配置文件。请记住，配置文件按特定顺序运行：

- 系统级配置文件（如 `/etc/profile`）在登录时首先运行。

- 你的 Unix 账户特定的配置文件（如 `~/.profile`）如果存在，将随后运行。

查看你的 ksh 配置文件：

1. `more /etc/profile ~/.profile`

   输入 `more` 后跟传统 Korn shell 配置文件的名称。你将看到类似于代码列表 8.14 的内容。与之前一样，寻找列表中的任何其他文件名或 `ENV` 语句，这些语句会指示其他在配置 ksh 环境中起作用的文件。

2. 为了供个人参考，列出系统使用的系统配置文件及其调用顺序。对于我们的系统，我们有：

   - `/etc/profile`（系统自动调用）

   - `~/.profile`（系统自动调用）

> 提示

`.profile` 文件在你启动新的登录 shell（通过 `su - you` 登录）时执行。`.kshrc` 文件在每次启动任何 ksh 子 shell 时都会被读取。

填写你的 ksh 系统配置文件：

![](img/30f4227f5df2c6cea63896bef2fc574f_191_0.png)

```bash
$ more /etc/profile ~/.profile
::::::::::::::
/etc/profile
::::::::::::::
#ident "$(@)profile1.17 95/03/28 SMI" /* SVr4.0 1.3 */
# 所有登录用户都使用自己的 .profile 配置文件。
trap "" 2 3
export LOGNAME PATH
if [ "$TERM" = "" ]
then
    if /bin/i386
    then
        TERM=AT386
    else
        TERM=sun
    fi
    export TERM
# login and -su shells /etc/profile services.
# -rsh 在 .profile 中赋予了其环境.
case "$#" in
-sh -lksh -jsh)
    if [ ! -f .hushlogin ]
    then
        /usr/sbin/quota
        # 允许用户打破每日消息（Message-Of-The-Day）循环。
        trap "trap "" 2 2"
        /bin/cat -s /etc/motd
        trap "" -E"
        /bin/mail -E
case $? in
0)
    echo "You have new mail."
2)
    echo "You have mail."
esac
fi
umask 022
trap 2 3
```

**代码列表 8.14** 在配置文件列表中（你拥有的文件）寻找文件名或路径或 `ENV` 语句，以识别所有帮助设置环境的文件。

```bash
:::::::::::::::::
/home/users/e/ejray/.profile
:::::::::::::::::
#
PATH=$PATH:$HOME/bin:\  # 设置命令搜索路径
export PATH
if [ -z "$LOGNAME" ]; then
  LOGNAME='logname' # 登录用户的用户名
  export LOGNAME
fi
MAIL=/usr/spool/mail/$LOGNAME # 邮箱位置
export MAIL
if [ -z "$PWD" ]; then
  PWD=$HOME # 假设为 root
  export PWD
fi
if [ -z "$PWD" || -d "$PWD" ]; then
  PWD=$HOME # 假设为 root
  export PWD
if [ -z "$PWD" ]; then
  PWD=$HOME
  export PWD
if [ -z "$PWD" ]; then
  PWD=$HOME
  export PWD
if [ -z "$PWD" ]; then
  PWD=$HOME
  export PWD
if [ -z "$PWD" ]; then
  PWD=$HOME
  export PWD
```

（注：由于原文提供的 OCR 文本存在大量重复和错误，此处已根据上下文进行了清理和逻辑合并。）
