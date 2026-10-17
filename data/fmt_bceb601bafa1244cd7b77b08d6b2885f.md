
```
~ z cli
cli-book git:(master) 
2. bash (bash)
MacBook-Pro-remy $ dull n (
MacBook-Pro-remy $PS1=\\[\e[1;30m\]\$PPID \\\e[1;30m\]\\[e[0;36m\]\\e[1;31m\]\[e[1;34m\]u@h\[e[1;30m\]\\e[0;37m\]\\[SSH_TTY\]\\e[0;32m\]\\[e[1;30m\]\\[e[1;37m\]w\\[e[0;37m\]\\[SHLVL\]!
[69342:69873:0584] 09:45:00 Jan 06 [@remy@MacBook-Pro.local +-2] ~
(2)$ # party time 
```

图 5.9: 提示符过度设计。

如果你已经切换到了 `zsh`，你更有可能拥有一个简洁的提示符（图 5.8）。
如果我们将其拆解开，我们在这个提示符中看到一个箭头 `➜`，后面跟着当前目录的名称（而不是完整路径）。当我们处于 Git 仓库时，它会显示 `git` 并注出哪个分支是激活状态。

提示符可以变得非常复杂。如果它们变得太复杂，看起来就像垃圾一样。如果我将 Bash 自定义 shell `PS1` 设置为一个新值，它会修改我的提示符——哇，那代码写得太糟糕了（图 5.9）。

幸运的是，在共享提示符和使其更具可读性方面取得了很大进展。共享提示符很重要，因为它能帮助人们进行实验、学习和改进。

我的通用建议是从 `zsh` 中选取一个你喜欢的主题，复制它并进行微调使其成为你自己的。假设你已经决定使用 `robbysruss` 主题并想对其进行一些自定义。首先，你需要创建一个它的副本，我们将其重命名为 `my.zsh-theme` 并将其放入 `themes` 目录：

```
$ cp ~/.oh-my-zsh/themes/robbyshell.zsh-theme ~/.oh-my-zsh/themes/my.zsh-theme
```

现在，用你喜欢的编辑器打开 `my.zshrc` 文件。尽量不要让它太把你搞晕了（就像我第一次遇到它时那样）。我们在这里感兴趣的是第一行，特别是文件中出现的箭头 `➜` 字符：

```
local ret_status="%(?:%{fg_bold[green]}%➜:%{fg_bold[red]}%➜) %s"

PROMPT='${ret_status}%{fg_bold[green]}%p

%%{cyan}%%c %%{fg_bold[blue]}%%$

$(git_prompt_info) %{fg_bold[blue]} %n%%{reset_color}'
```

变量 `ret_status` 根据上一个执行的命令是否执行成功来更改箭头：如果成功，则显示加粗箭头 `$fg_bold[green]`；如果发生错误，则显示加粗箭头 `$fg_bold[red]`。第二行设置了 `PROMPT` 的魔值，创建了你将看到的提示符。

现在，让我们把箭头改为雪人 `☃`。（这并不一定实用，但对于眼下的练习足够了。）我们还将显示完整路径，但让它单独占一行，放在提示符上方。

将箭头交换为雪人很简单，但由于如果我们使用外星人表示错误（并丢弃颜色信息），Emoji 将改变颜色。此外，在 `PROMPT` 值中获取完整路径将需要移动一些元素，完全合法地在 `PROMPT` 的值中放置一行，这就是我们获得多行提示符的方法：

```
local ret_status="%(?:☃:👾) %s"

PROMPT='%%{cyan}%%d

${ret_status}%{fg_bold[green]}%p

%%{fg_bold[blue]}%%$(git_prompt_info)

%%{fg_bold[blue]}%% %{reset_color}'
```

现在我们我们能够在出现随机错误时看到；我们的提示符将切换到外星人，直到命令执行成功（图 5.10）。

```
/Users/remy/Dropbox/Writing/cli-book

git:(master) # random error

zsh: command not found: random

/Users/remy/Dropbox/Writing/cli-book

git:(master) # █
```

图 5.10: 万岁。当一切正常时，我们的提示符现在显示雪人，当上一个命令失败时则显示外星人。

`zsh` 还有一个右侧提示符；这可以使用 `RPROMPT` 值设置。你可以对这个值做任何事情，添加当前时间（或者也许更有创意的东西）。

或者假设你想在方括号中添加蓝色的当前时间，纯粹为了好玩。只需向向你的 `my.zsh-theme` 文件中添加以下内容即可：

```
RPROMPT="%fg[blue]*"
```

24 小时制由 `*` 表示，因此最终的提示符看起来是一堆大括号和百分号的视觉混乱。对此我表示歉，但一旦你设置了提示符，你可能再也不会改变它了。

提示符变量的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名只是命令的替代品。为了创建一个别名，你需要知道如何

```
alias
```

因为 to create an alias, you need to know how to create an alias, you can read about the aliases to for all of.

对于 this I apologize, but once you get your prompt, you probably won't change it ever.

提示符变量的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名 `Aliases` 的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名只是命令的替代品。

For this I apologize, but once you get your prompt, you probably won't change it ever.

别名只是命令的替代品。

`zsh` 还有一个右侧提示符；这可以使用 `RPROMPT` 值设置。你可以对这个值做任何事情，添加当前时间（或者也许更有创意的东西）。

或者假设你想在方括号中添加蓝色的当前时间，纯粹为了好玩。只需向向你的 `my.zsh-theme` 文件中添加以下内容即可：

```
RPROMPT="%fg[blue]*"
```

24 小时制由 `*` 表示，因此最终的提示符看起来是一堆大括号和百分号的视觉混乱。对此我表示歉，但一旦你设置了提示符，你可能再也不会改变它了。

提示符变量的完整列表列在 `zsh` 中。一旦你设置了提示符，你可能再也不会改变它了。

别名只是命令的替代品。

为了创建一个别名，你需要知道如何

```
alias
```

因为 to create an alias, you need to know how to create an alias, you can read about the aliases to for all of.

对于 this I apologize, but once you get your prompt, you probably won't change it ever.

别名只是命令的替代品。
