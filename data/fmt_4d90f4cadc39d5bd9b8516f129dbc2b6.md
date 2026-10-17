
要从另一张 CD 安装，请更换驱动器中的 CD 并输入命令 > `from`。

```
Inst> quit
重启 ELF 文件（参见 rqalls(1)） .. 100% 完成。
```

再次，当你安装 IRIX 时，请按照手册中的说明操作。希望通过简短的 IRIX 产品安装过程能让你更好地理解手册说明的含义。手册并没有留出太多的解释空间。

如果你正在将机器从 IRIX 5.3 升级到 6.5，请访问在线查看 IRIX 管理书籍，地址为 http://techpubs.sgi.com/library/ 了解更多详情。那些说明非常详尽。

![](img/74418f52d5d454acca60721059dbdc99_670_0.png)

接下来，我们将看看一种独特的机器设置方法。鉴于我们只有纸质资料可以使用，我们将尽力感受这种体验。O2 带有极其令人兴奋的配置体验，称为“OutBox 体验”。它带有声音并让你在三维世界中导航！图 B 显示了之旅的开始。在此处还有背景音乐。

### 图 B8 开始 OutBox 体验。

![](img/74418f52d5d454acca60721059dbdc99_671_0.png)

### 图 B9 下楼。

在图 B9 中，你刚刚进入并下楼。地球正在旋转。在图 B10 中，你位于语言区。图 B11 显示了系统设置。在这里，女性提示你将配置机器并创建账户。你的终点是图 B12 所示的注册站。在这里你提供了机器信息。

![](img/74418f52d5d454acca60721059dbdc99_672_0.png)

### 图 B10 语言区。

![](d454acca60721059_672_1.png)

### 图 B11 系统设置。

![](d454acca60721059_673_0.png)

### 图 B12 注册站。

![](d454acca60721059_673_1.png)

这并不是全部。还有一个完整的现实建模语言（VRML）世界供你探索！图 B13 显示了虚拟 O2之旅，向你展示了关于新 O2 的信息。

### 图 B13 生活 VRML 世界。

![](d454acca60721059_674_0.png)

在图 B14 中，你在 VRML 世界之外，站在 O2 的底部。在图 B15 中，你已经调查并可以查看强大的 O2。图 B16 显示了更多的虚拟世界，带有步道和水。在远处，你可以看到丛林岛。SGI 的 O2 提供了一种独特的配置方式。即使你不使用 OutBox 体验来配置机器，也应该花些时间在特殊的 VRML 世界里玩玩。

### 图 B14 O2 的底部。

![](img/74418f52d5d454acca60721059dbdc99_675_0.png)

### 图 B15 中央广场区域。

![](d454acca60721059_675_1.png)

### 图 B16 世界概览。

![](d454acca60721059_676_0.png)

# APPENDIX C

## 有用文件

这里是一些示例配置文件，你可以作为配置机器或用户账户的起点。显然，这些文件的部分内容是特定于系统的，但你应该能够轻松地找到机器上对应的路径。

## 配置路径和别名

`csh` 和 `tsh` 的配置文件。配置我喜欢并经常使用的路径和别名。注意，它在添加自己的内容后会加载 `/usr/local/extras/csh_extensions`。存放在用户目录。

```
.cshrc
if($prompt) then
# 一个巧妙的小程序，将 X11 标题栏
# 设置为当前路径，并提示当前的
# 主机和目录
# set cdcmd=''
set cdcmd=echo n "_j;scwd_ "
```

# 附录 C

```
set norm_suff='\!'
set root_suff='\!#'
if ($SHELL = /bin/csh) || ($SHELL = *tcsh) then
    alias _normal   'set prompt=$HOST $scwd:t $norm_suff'
    alias _root     'set prompt=%HOST%scwd:t $root_suff'
    if ('*whoami' = *root*) then
        alias prmpt_s _root
    else
        alias prmpt_s _normal
    fi
endif
```

```
if ($term == xterm) then
    alias win_s 'eval "cd ~"'
    alias cd 'chdir *!;prmpt_s;win_s'
else
    alias win_s 'echo $PWD'
    alias cd 'chdir *!;prmpt_s'
fi
```

`prmpt_s;win_s`

`set history=200`

`savehist=200`

# 用于邮件/新闻的首选编辑器

`setenv VISUAL emacs`

# 设置我经常使用的变量

`setenv OPENWINHOME /usr/openwin`

`setenv TCL_LIBRARY /usr/local/lib/tcl`

`setenv TK_LIBRARY /usr/local/lib/tk`

`setenv ENVIRONMENT -./Xenv`

`setenv X11HOME /usr/local/X11R5`

`setenv X11PATH /usr/local/X11R5/bin`

`setenv LIBPATH /usr/local/X11R5/lib`

```

# 我不喜欢 /usr/bin/mail，但喜欢 /usr/ucb/Mail
alias mail mail Mail
alias lo exit
# 交互式 ftp 模式很麻烦
alias ftp ftp -l
alias h history
# 在交互式模式下始终使用 rm！
alias rm rm -i
# 一切，无无刻
alias ps "ps -auxww | more"
# 在文件中显示行号
alias grep grep -n
# 在通过 push 移动时保持窗口名称正确的的小技巧
alias push "find . -mtime '*';"
alias pop "popd; cd ."
# 快速查看系统上一次的操作
alias whodunit "/usr/lib/acct/wtmp /var/adm/wtmp | tail -30"
# Emacs 为自己开启新窗口很烦人。如果我想
# 在窗口中运行它，我会为它启动一个。
alias emacs 'emacs -nw'
# 查找大于...的文件
alias recent 'find . -mtime +*' -exec ls -ld {} \;'
alias xlock 'xscreensaver-command -activate'
# 用 Emacs 复制我的空白文本启动文档
alias startletter 'cp -ray/miscdatada/myltr.tex !*.tex'
# 使用修正后的伽马启动 xv，以及我旧的 8 位屏幕
alias xv 'xv -gamma 2 -8 -owncmap'

# 登录 Shell (Login Shells)

登录 shell 的配置文件。此文件的功能与 `.bashrc` 类似，
区别在于它仅用于登录 shell，而不用于其他派生的 shell。它存放在
用户的家目录下。

# .login

```

#

echo "一个可以接受的解决方案"

#

```

```

# 以防由于某种方式在没有设置这些的情况下来到这里，而我需要它们

# 用于我可能决定在这里做的任何操作。

`setenv X11HOME /usr/local/X11R`

`setenv X11PATH /usr/local/X11R/bin`

`setenv X11LIBPATH /usr/local/X11R/lib`

```

`set STDPATH=(/usr/bin $X11PATH /usr/ucb /usr/etc /usr/etc /usr/local/bin .)`
`set path=$path $STDPATH`

```

# 输出一个空行

echo

```

```bash

# 如果我们在控制台上，记录此登录 .loginfile - 用于

# 我自己的登录/注销跟踪

# 然后让我从 X11、标准控制台提示符或 Sun 的

# OpenWindows 环境之间进行选择。根据选择复制

# 适当的配置文件。Openwin 软件在 OPENWIN* 变量被设置时

有时会混淆事情，即使没有运行 OPENWIN，除非我必须，否则不要设置它们

if [ 'tty' == "console" ]; then

  echo login -> $(date) >> .loginfile

  echo "...控制台登录..."

  ask

  echo "a. Xwindows"

  echo "b. 无"
