

要识别你的主目录，请使用命令 echo $HOME 在终端中打印目录路径。导航到该目录并创建你的开发文件夹（我们建议将其命名为 scripts）。然后，要将你的开发目录添加到登录脚本中，在文本编辑器中打开登录脚本文件，并在文件顶部添加以下行，将 /path/to/scripts/ 替换为你的开发文件夹的目录。

```
export PATH="/path/to/scripts:$PATH"
```

完成此操作后，你保存在开发文件夹中的任何脚本都可以在 shell 中作为命令调用。

## 运行 Shell 脚本

我们现在已经使用了几个命令，例如 echo、which 和 cat。但我们只单独使用它们，还没有全部一起写在 shell 脚本中。让我们编写一个 shell 脚本，按顺序依次运行它们，如清单 0-4 所示。此脚本将打印 Hello World，然后打印 neqn shell 脚本的文件路径，neqn 是一个 shell 脚本，默认情况下应存在于你的 bash 文件中。然后它将使用此路径将 neqn 的内容打印到屏幕上。（neqn 的内容目前并不重要；这只是用作示例脚本。）这是一个很好的例子，说明如何使用 shell 脚本来按顺序执行一系列命令，在本例中是为了查看文件的完整系统路径并快速检查其内容。

```
echo "Hello World"
echo $(which neqn)
cat $(which neqn)
```

清单 0-4：我们第一个 shell 脚本的内容

打开你喜欢的文本编辑器（Linux 上流行的编辑器有 Vim 或 gedit，OS X 上有 TextEdit）并输入清单 0-4。然后将 shell 脚本保存到你的开发目录中，并将其命名为 intro。Shell 脚本不需要特殊的扩展名，因此保持扩展名为空（或者如果你愿意，也可以添加 .sh 扩展名，但这不是必需的）。Shell 脚本的第一行使用 echo 命令简单地打印文本 Hello World。第二行稍微复杂一些；它使用 which 找到 bash 文件 neqn 的位置，然后使用 echo 命令将位置打印到屏幕上。要像这样运行两个命令，其中一个命令作为另一个命令的参数，bash 会使用子 shell 运行第二个命令并存储输出以供第一个命令使用。在我们的示例中，子 shell 运行 which 命令，它将返回 neqn 脚本的完整路径。然后此路径用作 echo 的参数，这意味着 echo 将 neqn 的路径打印到屏幕上。最后，相同的子 shell 技巧将 neqn 的文件路径传递给 cat 命令，cat 命令将 neqn shell 脚本的内容打印到屏幕上。

文件保存后，我们可以从终端运行 shell 脚本。清单 0-5 显示了结果。

```
$ sh intro
Hello World
/usr/bin/neqn
#!/bin/sh
# Provision of this shell script should not be taken to imply that use of
# GNU eqn with groff -Tascii|-Tlatin1|-Tutf8|-Tcp1047 is supported.

GROFF_RUNTIME="${GROFF_BIN_PATH}/usr/bin":
PATH="$GROFF_RUNTIME$PATH"
export PATH
exec eqn -Tascii $1("${*}")

# eof
$
```

清单 0-5：运行我们的第一个 shell 脚本

使用 sh 命令并将 intro 脚本作为参数传递来运行 shell 脚本。sh 命令将逐行处理文件中的内容并像在终端中输入的 bash 命令一样执行它。你可以看到这里 Hello World ① 被打印到屏幕上，然后打印出 neqn 的路径 ②。最后，neqn 文件的内容被打印出来 ③；这是你硬盘上简短的 neqn shell 脚本的源代码（至少在 OS X 上如此——Linux 版本可能略有不同）。

## 使 Shell 脚本更直观

你不需要使用 sh 命令来运行脚本。如果你再向 intro shell 脚本添加一行并修改脚本的文件系统权限，你将能够直接调用 shell 脚本，而无需 sh，就像调用其他 bash 命令一样。在文本编辑器中，将你的 intro 脚本更新为以下内容：

```
#!/bin/bash
echo "Hello World"
echo $(which neqn)
cat $(which neqn)
```

我们在文件最顶部添加了一行，引用文件系统路径 /bin/bash ①。此行称为 shebang。shebang 允许你定义将运行哪个程序来解释脚本。在这里我们将文件设为 bash 文件。你可能见过其他 shebang，例如 Perl 语言的（#!/usr/bin/perl）或 Ruby 的（#!/usr/bin/env ruby）。

添加了这一行后，你仍需要设置文件权限，以便能够像程序一样执行 shell 脚本。在 bash 终端中按清单 0-6 所示执行此操作。

```
$ chmod +x intro
$ ./intro
Hello World
```

