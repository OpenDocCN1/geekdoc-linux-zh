

## 修改你的 csh 提示符

你的系统默认提示符可能只是一个美元符号 ($) 或者是一个美元符号和日期，或者如“快速设置你的 csh 提示符”侧边栏所述的其他信息。你可以使用以下步骤更改此提示符。你首先找到你的提示符语句（代码清单 8.21），然后在编辑器中修改它（图 8.7）。

## 如何更改你的 csh 提示符：

- 1. grep prompt ~/.cshrc ~/.login
开始时，列出位于你的主目录和 /etc 目录中的配置文件。在你的系统配置文件中查找你的提示符语句。它看起来像 set prompt=" $ " 或 set prompt="hostname> "。它很可能在你的 .cshrc 文件中，如代码清单 8.21 所示。
“快速设置你的 csh 提示符”侧边栏将帮助你翻译此代码。
- 2. vi .cshrc
使用你选择的编辑器编辑包含提示符设置的配置文件。
- 3. set prompt="$LOGNAME > "
将你的提示符设置为更合适的样式，如图 8.7 所示。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_196_0.png)

## 快速设置你的 csh 提示符

你可以将你的 csh 提示符设置为包含某些类型的信息，但没有 bash 或 zsh 提示符那么多。下面的列表显示了你可以使用什么代码向提示符添加某些类型的信息（以及帮助你翻译现有提示符中的代码）：

- $LOGNAME 显示当前用户的用户 ID——也就是你。
- ${cwd} 显示带路径的当前工作目录。
- `uname -n`% 显示计算机的主机名。

```
xmision> grep prompt ~/.cshrc ~/.login
/home/users/e/ejroy/.cshrc:if ($?USER == 0 || $?prompt == 0) exit
/home/users/e/ejroy/.cshrc:set prompt="hostname> "
/home/users/e/ejroy/.login: exit# leave user at regular C shell prompt
xmision>
```

代码清单 8.21 提示符语句很可能在你的 .cshrc 文件中。

- 4. 保存文件并退出编辑器。
- 5. su - yourid
再次登录以试用（代码清单 8.22）。

## 提示

- 注意提示符代码中的尾随空格：set prompt="$LOGNAME > "。这个额外的空格使提示符更容易使用。

```
xmision> su - ejray
Password:
Sun Microsystems Inc. SunOS 5.5.1 Generic May 1996
You have mail.
NOTE! As of 7/15/98, "tin" has been backed out its prior version. NNTP support was compiled in directly as well. We hope that this will stabilize its problems.

General questions email to "help" or "help@xmision.com".
Problems with the system mail to "support" or "support@xmision.com".

Type "acctstat" for a summary of your current account information.
Type "quota -v" to view your existing disk quota.
Type "help" for a list of online programs or "menu" for the assisted menu.
ejray>
```

代码清单 8.22 测试你的新提示符，看看你是否喜欢它。

## 设置别名
使用 alias

别名是一种昵称，你用它来更轻松地输入命令。例如，如果你经常使用命令 mail -s "Lunch today?" deb < .signature，你可以为此命令设置一个别名并将其命名为 lunch。然后，以后你只需输入 lunch，结果就与输入较长命令相同（图 8.8）。

## 如何使用 alias 设置别名：

- 1. 根据你使用的 shell 选择要编辑的适当文件。
  - zsh 用户应使用 ~/.zshrc
  - bash 用户应使用 ~/.bashrc
  - ksh 用户应使用 ~/.profile
  - csh 用户应使用 ~/.cshrc
如果没有适当的文件，你可以使用不同的配置文件。许多人将所有别名存储在单独的 .alias 文件中。

- 2. vi ~/.bashrc
编辑你选择的配置文件。

- 3. alias quit="logout"
输入 alias，后跟你想用作别名的词、= 和你要创建别名的命令（用引号括起来）。在这里，我们将单词 quit 设置为系统命令 logout 的别名，这样我们就可以输入 quit 而不是 logout（图 8.8）。

- 4. 添加任意多个其他别名。有关更多想法，请参阅名为“值得设置的良好别名”的侧边栏。

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_198_0.png)

图 8.8 设置别名可以让你免于输入长名称和代码。

## 值得设置的良好别名

以下是一些你可能认为值得在系统上设置的别名：

- alias rm="rm -i" 会导致系统在所有删除操作时提示你。
- alias quit="logout" 让你可以使用 quit 作为 logout 的同义词。
- alias homepage="lynx http://www.raycomm.com/" 让你可以使用 homepage 启动 lynx 浏览器并连接到 Raycomm 主页（根据需要替换为你的主页）。

或者，如果你来自 DOS 背景，你可能会发现以下别名很有用：

- alias dir="ls -l" 让你可以使用 dir 列出文件。
- alias copy="cp" 让你可以使用 copy 复制文件。
- alias rename="mv" 让你可以使用 rename 移动或重命名文件。
- alias md="mkdir" 让你可以使用 md 创建目录。
- alias rd="rmdir" 让你可以使用 rd 删除目录。

