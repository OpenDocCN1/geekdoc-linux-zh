

使用终端与系统交互乍看之下似乎是一项艰巨的任务。然而，随着时间的推移，打开终端进行快速系统更改会变得更加自然，而不是在菜单中来回移动鼠标，试图找到想要更改的选项。

## 运行命令

Bash 的核心能力是在你的系统上运行命令。让我们尝试一个快速的“Hello World”示例。在 bash shell 中，echo 命令会将文本显示到屏幕上，如下所示：

```
$ echo "Hello World"
```

在 bash 命令行中输入此内容，你会看到单词 Hello World 显示在屏幕上。这行代码运行存储在你的标准 bash 库中的 echo 命令。bash 将搜索这些标准命令的目录存储在一个名为 PATH 的环境变量中。你可以使用 echo 和 PATH 变量来查看其内容，如清单 0-1 所示。

```
$ echo $PATH
/Users/bperry/.rvm/gems/ruby-2.1.5/bin:/Users/bperry/.rvm/gems/ruby-2.1.5@global/bin:/Users/bperry/.rvm/rubies/ruby-2.1.5/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/X11/bin:/usr/local/MacGPG2/bin:/Users/bperry/.rvm/bin
```

清单 0-1：打印当前的 PATH 环境变量

> NOTE
> 在同时显示输入命令和输出的清单中，输入命令将以粗体显示，并以 $ 开头以区别于输出。

此输出中的目录由冒号分隔。这些都是 bash 在你要求它运行程序或命令时将检查的所有目录。如果你的命令未存储在这些目录中的任何一个中，bash 就无法运行它。另外，请注意 bash 会按 PATH 中出现的顺序检查这些目录。此顺序很重要，因为如果你的 PATH 中有两个目录中有两个同名命令，这可能会产生影响。如果你难以找到某个特定命令，你可以使用 which 命令并加上该命令的名称来查看 shell 中它的 PATH，如清单 0-2 所示。

```
$ which ruby
/Users/bperry/.rvm/rubies/ruby-2.1.5/bin/ruby
$ which echo
/bin/echo
```

清单 0-2：使用 which 在 PATH 中查找命令

现在有了这些信息，你可以将相关文件移动或复制到 echo $PATH 命令列出的目录之一，如清单 0-1 中所示，然后该命令就可以运行了。我们在全书中都使用 which 来确定命令的完整路径。这是在 PATH 损坏或异常时调试的有用工具。

## 配置你的登录脚本

在全书中，我们将编写脚本，然后在其他脚本中使用它们，因此能够轻松调用你的新脚本非常重要。你可以配置你的 PATH 变量，以便你的自定义脚本在启动新的命令 shell 时自动在 shell 中可用，就像任何其他命令一样。当你打开命令 shell 时，它会读取你主目录 (/Users/<username> 或 /home/<username>，分别在 OS X 或 Linux 中) 中的登录脚本并执行其中找到的任何自定义命令。登录脚本将是 .login、.profile、.bash_profile 或 .bashrc，具体取决于你的 shell。要测试使用的是哪个登录脚本，将如下行添加到每个文件中：

```
echo this is .profile
```

根据文件名调整最后一个词，然后登录。该行应打印在终端窗口顶部，报告登录时运行了哪个脚本。如果你打开终端并看到 this is .profile，你就知道 .profile 文件正在为你的 shell 环境加载；如果你看到 this is .bashrc，你就知道是 .bashrc 文件；依此类推。而现在你知道了！不过，这种行为可能会根据你的 shell 而变化。

你可以修改登录脚本，使其为 PATH 变量配置其他目录。你还可以设置各种 bash 设置，从更改 bash 提示符的外观到设置自定义 PATH 再到其他无数自定义。例如，让我们使用 cat 命令来看一下自定义的 .bashrc 登录脚本。cat 命令将文件名作为参数并将文件内容打印到控制台屏幕上，如清单 0-3 所示。

```
$ cat ~/.bashrc
export PATH="$PATH:$HOME/.rvm/bin" # Add RVM to PATH for scripting.
```

清单 0-3：此代码显示了 .bashrc 文件的内容，显示已为 PATH 分配了一个新值，从而允许本地 RVM（Ruby 版本管理器）安装管理任何已安装的 Ruby 版本。由于 .bashrc 文件在每次打开新的命令 shell 时都会设置自定义 PATH，因此 RVM 安装将默认在此系统上可用。

你可以实现类似的自定义，以便默认情况下你的 shell 脚本可用。首先，你将在主目录中创建一个开发文件夹来保存所有 shell 脚本。然后，你可以在登录文件中将此目录添加到 PATH 中，以便更轻松地引用你的新脚本。

