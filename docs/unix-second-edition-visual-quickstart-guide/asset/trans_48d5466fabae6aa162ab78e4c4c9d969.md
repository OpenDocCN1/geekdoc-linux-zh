

## 查看你的 zsh 配置文件

- 1. more ~/.z* /etc/zl* /etc/zprofile /etc/zsh*
在 shell 提示符下，输入 more 后跟每个可能的系统配置文件名来查看你的配置文件。如果你没有这里提到的所有文件（或任何文件），不用担心。只需记下你拥有的那些文件即可。代码清单 8.5 显示了你可能会看到的示例。

- 2. 为参考记录下系统配置文件及其运行顺序。（记住，最后一个文件中的设置会覆盖之前所有的设置。）我们的系统配置文件，全部由系统自动调用，包括
▲ /etc/zshenv 然后 ~/.zshenv
▲ /etc/zprofile 然后 ~/.zprofile
▲ /etc/zshrc 然后 ~/.zshrc
▲ /etc/zlogin 然后 ~/.zlogin
请记住，你拥有的文件可能与我们拥有的文件不同。

## 提示

- 特别注意任何文件中以路径和文件名结尾的行，或直接引用其他文件，例如一行单独的 /etc/profile。每条这样的行都引用了另一个在设置你环境中起作用的文件。请注意，其中一些行会引用并不直接配置你的环境的其他文件。

- 所有以 # 开头的行都是注释，其中包含帮助你更好地理解文件的说明。注释实际上什么都不做，但有助于你了解每个文件的作用。

某些文件包含像 export HISTFILE=${HOME}/.bash_history 这样的奇特内容，该文件引用了 .bash_history 文件，其中包含你已运行的命令列表。（看起来像是 Linux 发行商的失误。幸好你在检查他们，对吧？）

## 向你的 zsh PATH 添加内容

对环境最有用的更改之一是向默认路径添加内容，该路径由 path 语句决定。path 语句告诉 shell 在哪里查找命令、脚本和程序。也就是说，如果你发出一个命令，path 语句会告诉系统按特定顺序在每个命名目录中查找该命令：

请确保不要从路径中删除任何内容，除非你真的知道自己在做什么，但你可以随意向其中添加任意多个额外目录。例如，如果你开始编写脚本（见第 10 章所述），你可能会将它们放在 scripts 子目录中，并希望将该目录添加到你的路径中。

如下步骤所示，你通过首先确定 path 语句的位置，然后编辑包含它的文件来更改 zsh 路径（代码清单 8.6）。

## 要更改你的 zsh 路径：

- 1. more ~/.zshenv ~/.zprofile ~/.zshrc
首先以它们执行的顺序查看你的配置文件（仅限你可以编辑的那些）。
在你的系统配置文件中查找 path 语句。如代码清单 8.6 所示，它看起来会像 PATH=/bin:/usr/bin:/opt/bin。如果你有多个 path 语句，找到最后一个执行的那个。
记住不同系统会有不同的配置，因此你可能需要做一点挖掘才能找到你的个人 path 语句。

```
jdoe@sulley ~ $ more .zshrc

# See comment at top.

if [[ -r ${ZDOTDIR:-$HOME}/.zshrc ]] ;then
  if [[ -f /usr/share/zsh/$ZSH_VERSION/zshrc_default ]] ;then
    source /usr/share/zsh/$ZSH_VERSION/zshrc_default
  fi
fi

PATH=/bin:/usr/bin:/opt/bin

jdoe@sulley ~ $
```

代码清单 8.6 你将在配置文件中找到你的 path 语句。

continued on next page

## 第 8 章

- 2. cp .zshrc .zshrc_backup
备份包含 path 语句的文件，以便在出现问题或错误时可以恢复该文件。参见第 2 章，如果你需要有关复制文件的更多信息。

- 3. vi .zshrc
使用你喜欢的编辑器打开你想要更改其路径的文件。

- 4. PATH=$PATH:$HOME/scripts
在最后一个 path 语句正下方添加一个新的 path 语句。在此示例中，$PATH 将环境变量的当前值插入到环境变量定义中，并将其插入到你的主目录中的 scripts 目录中（图 8.1）。

- 5. 保存并退出编辑器。
如果需要帮助，请参阅第 4 章。

- 6. su - yourid
正如你在第 3 章中学到的，这个命令启动一个新的登录 shell，以便你可以在注销前测试你的更改。

- 7. echo $PATH
显示当前的 path 环境变量。这应该包括你刚刚添加的内容。它在那里，对吧？（参见代码清单 8.7。）

## 提示

- 如果你查看各种配置文件中的 path 语句，你可能会发现一个 path 语句只包含一个 .（点）。例如，你可能会看到类似 PATH=/usr/bin:/usr/local/bin:. 的内容。 . 会将你的当前目录，无论它是什么，添加到你的路径中。请记住，通常更安全的做法是不在路径中包含当前目录，以免无意中运行你正在处理的程序。

```
jdoe@sulley ~ $ su - jdoe
Password:
jdoe@sulley ~ $ echo $PATH
/usr/bin:/opt/bin:/home/jdoe/scripts/
jdoe@sulley ~ $
```

代码清单 8.7 测试你对配置文件的编辑。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_174_0.png)

图 8.1 你在编辑器中添加或修改 zsh 路径语句。

- 你可以使用 grep 使查找设置路径的配置文件变得更容易。grep -i path *.z* 是一个不错的开始方法。

- 如果你在配置文件中看到类似 path=($path $HOME/bin) 的内容，那也没关系。继续在下一行使用本节所示的语法即可。这是 zsh 的一个特性，它理解用无数种不同方式表达同一命令。

