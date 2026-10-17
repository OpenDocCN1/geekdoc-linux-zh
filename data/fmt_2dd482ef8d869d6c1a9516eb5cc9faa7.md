
```
if [ echo $PATH | /bin/egrep -q "^(|:)\$1($|:)"; then

  if [ "$2" = "after" ]; then

    PATH=$1:$PATH

  else

    PATH=$PATH:$1

  fi

fi
```

### 路径操作
```
if [ 'id -u' = 0 ]; then
  pathmunge /sbin
  pathmunge /usr/sbin
  pathmunge /usr/local/sbin
```
```bash

pathmunge /usr/libR6/X11/bin after

unset pathmunge
```

### 默认不产生核心文件

```
ulimit -S -c 0 > /dev/null 2>&1
```

```bash

USER="id -u"

LOGNAME=$USER

MAIL="/var/spool/mail/$USER"

HOSTNAME=/bin/hostname

HISTSIZE=1000

NNTPSERVER=smtp.myservice.com
```

```bash

if [ -z "$INPUTHOME/.inutrc" ]; then

  INPUTRC=/etc/inutrc

fi
```

```bash

export PATH USER LOGNAME HOSTNAME HISTSIZE INPUTRC

export NNTPSERVER
```

```bash

for i in /etc/profile.*.sh; do

  if [ -x $i ]; then

    $i

  fi

done

unset i
```

### 配置 BASH Shell：.bashrc

`.bashrc` 是一个每次进入 BASH shell 或生成任何子 shell（`subshells`）时都会执行的配置文件。如果 BASH shell 是你的登录 shell，那么登录时 `.bashrc` 会同你的 `.bash_login` 文件一起执行。如果你从另一个 shell 进入 BASH shell，`.bashrc` 文件将自动执行，其定义的变量和别名也将被定义。如果你进入不同类型的 shell，则将执行该 shell 的配置文件。例如，如果你使用 `tcsh` 命令进入 TCSH shell，则将执行 `.tcshrc` 配置文件，而不是 `.bashrc`。

### Bash 脚本

`.bashrc` 配置文件实际上在每次生成 BASH shell 时都会执行，例如当你运行一个 shell 时。换句话说，每当创建一个子 shell 时，

`bashrc` 文件就会执行。这样做的效果是导出你在 `.bashrc` 初始化文件中定义的任何本地变量或别名。`.bashrc` 文件通常包含别名的定义以及任何用于开启 shell 特性的特性变量。别名和特性变量是在 shell 内部局部定义的。但 `.bashrc` 文件在每个 shell 中都定义了它们。由于这个原因，`bashrc` 文件通常持有别名，例如为 `rm`、`cp` 和 `mv` 命令定义的别名。下一个示例是一个许多标准定义的 `.bashrc` 文件：

```bash

.bashrc

# 加载全局定义

if [ -f /etc/bashrc ];

then
```

## 178 第二部分：环境

```bash

. /etc/bashrc

fi

set -o ignoreeof

set -o nococlobber

alias rm='rm -i'

alias mv='mv -i'

alias cp='cp -i'
```

你可以向你的 `.bashrc` 文件中添加任何你自己的命令或定义。如果你修改了 `.bashrc` 并且希望这些更改在当前登录会话中生效，你需要使用 `.` 或 `source` 命令重新执行该文件。

```bash

$ .bashrc
```
