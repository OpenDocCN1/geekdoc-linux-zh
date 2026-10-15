
## 更改你的 zsh 提示符

你的默认提示符（屏幕上你输入命令位置前方的文本）可能会因你的 Unix 系统而有所不同；你可能只看到一个美元符号（$），或美元符号加日期，或如“快速设置你的 zsh 提示符”侧边栏中所概述的其他信息。你可以将提示符设置为包含对你有用的信息。

实际上你拥有多个提示符：

- 主提示符，也就是你通常认为的 shell 提示符。这个提示符称为 PS1，或简称为 PROMPT。
- 辅助提示符，当系统需要额外信息来完成命令时你会看到它。在逻辑上，这个提示符被称为 PS2。

你可以按照以下步骤更改这两个提示符。首先找到你的提示符语句（代码清单 8.8），然后在编辑器中修改它（图 8.2）。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_175_0.png)

```
jdoe@sulley ~ $ grep -i PROMPT ~/.z* ; grep -i PS1 ~/.z*
/home/jdoe/.zshrc:# configuration for keys umask PROMPT and variable
/home/jdoe/.zshrc:# Set prompts
/home/jdoe/.zshrc:PROMPT="%n%m %3- %(!.#.$) "  # default prompt
/home/jdoe/.zshrc:# configuration for keys umask PROMPT and variable
/home/jdoe/.zshrc:# Set prompts
/home/jdoe/.zshrc:PROMPT="%n%m %3- %(!.#.$) "  # default prompt
jdoe@sulley ~ $
```

代码清单 8.8 使用 grep 在配置文件中搜索 zsh 提示符语句。

## 更改你的 zsh 提示符：

- 1. `grep -i PROMPT ~/.z*`; `grep -i PS1 ~/.z*`

首先，在你的主目录中的配置文件里搜索，如有必要，还可以在 /etc 目录中搜索，找到你的提示符语句。它看起来会像这样：PROMPT="%n@%m %~ %(!.#.$)"  # default prompt，如代码清单 8.8 所示。

侧边栏“快速设置你的 zsh 提示符”将帮助你理解这些符号。

- 2. `cp ~/.zshrc ~/.zshrc-backup; vi ~/.zshrc`

备份一份。~/.zshrc 文件很可能是设置提示符的地方，因为该文件只在你的 shell 交互式时才会被读取。

### 快速设置你的 zsh 提示符

你可以将提示符设置为包含各种信息。以下列表展示了使用哪些代码来向提示符添加特定类型的信息（同时帮助你理解现有提示符中的代码）：

- `%n` 显示当前用户的用户 ID——也就是你。
- `%~` 显示带路径的当前工作目录，在你的主目录内使用 ~ 记号。
- `%c` 显示不带路径的当前目录。
- `%t` 显示时间。
- `%D` 显示不带年份的日期。
- `%F` 显示带年份的日期。
- `\n` 强制换行，使提示符分成两行显示（你需要在提示符周围加上单引号）。
- `%m` 显示计算机的主机名（例如本书中的 frazz 和 hobbes 示例）。
- `%M` 显示计算机的完整域名。

```
jdoe@sulley ~ $ vi .zshrc
jdoe@sulley ~ $ su - jdoe
Password:
jdoe /home/jdoe $ PROMPT="$\n Top line \nNext
→ line $"
Top line
Next line $pwd
/home/jdoe
Top line
Next line $
```

代码清单 8.8 更新提示符后进行测试总是一个好主意。

### 3. PROMPT="%n %d $ "

例如，我们经常将提示符设置为包含两则小信息：用户 ID（因为我们有很多不同的账户，总能用它来提醒自己！）和日期（玩得开心时时间过得飞快，对吧？）。我们将这些信息添加到提示符中，而不是使用现有的默认提示符，但在开头用 # 号保留默认提示符，以防万一（图 8.2）。

### 4. 保存文件并退出编辑器。

### 5. su - ejr

使用更改后的提示符重新登录，试一下效果。

### 提示

- 请注意提示符代码末尾的空格：PROMPT="%n %d $ "。这个空格能让提示符更易于使用，因为它可以避免你的命令与提示符紧挨在一起。

- 你还可以将提示符设置为：你设置的信息显示在第一行，而实际的提示符出现在下一行（代码清单 8.9）。为此，请在环境变量设置中使用单引号（‘ ’）和 $，然后使用 \n 表示换行，例如 PROMPT-$’%n %m\n $’。这将强制 shell 将 \n 视为换行符，而不是提示符字符串中的普通字符。

