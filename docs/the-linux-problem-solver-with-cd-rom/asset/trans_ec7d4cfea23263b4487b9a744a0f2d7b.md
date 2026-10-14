

```
# for file in *; do
> ln -s /opt/fdutils/default/bin/$file /usr/local/bin/$file
> done
```

同样，在 /opt/fdutils/default/man/man1 中：

```
# for file in *; do
> ln -s /opt/fdutils/default/man/man1/$file /usr/local/man/man1/$file
> done
```

现在该软件包可以直接从 /usr/local/bin 运行。其他软件包可能还有一些其他文件，例如手册页，为此你需要创建额外的链接。

## PROBLEM 71

症状：升级库后，使用该库的程序出现段错误、找不到库或给出错误结果。

问题：共享库在升级过程中不一致。

我们对共享库有一个警告。它们的名字会随着版本的变化而改变，这可能会造成严重的混乱。例如，不要让 /usr/local/lib/libfoo.so.1 链接到 /opt/foo/default/lib/libfoo.so.1。如果以后要链接该库，请选择以下方法之一。

修复（情况 1）：如果它是一个相对较小的库，如 libpm，只需将其制作成静态库（即库的安装名为 libpm.a）。如果你想让库对用户进行通用开发可用，将（以 pm 为例）/usr/local/lib/libpm.a 链接到 /opt/netpm/default/lib/libpm.a，以及 /opt/netpm/default/include 中的头文件对应的适当链接。使用 GNU autoconf 系统制作静态库的标准 configure 选项是 --disable-shared。

修复（情况 2）：如果它是一个较大的库，例如 libgtk，你可以制作一个共享库。但是，如上所述，不要在 /usr/local 中创建任何链接，因为这会导致升级问题。编译时 [例如 libgtk] 使用 -I/opt/gtk/gtk-version/include 进行包含，链接时使用 -L/opt/gtk/gtk-version/lib 和 -Wl,-rpath=/opt/gtk/gtk-version/lib 选项。你必须使用版本号而不是默认链接，因为库的大版本升级往往会对链接到它的任何东西造成破坏。

特别注意删除包含共享库的任何软件包的旧版本。系统可能包含链接到旧库的程序，而且你的用户也可能这样做。

请注意，当例如 fdutils-5.4 发布时，你所需要做的就是 configure --prefix=/opt/fdutils/fdutils-5.4，然后在运行 make 和 make install 之后更改 /opt/fdutils/default 链接。因为我们将之前版本的所有内容都放在一个地方（/opt/fdutils/fdutils-5.3），并且不再有指向该目录的特定链接（我们使用的是 /opt/fdutils/default），所以你不必担心安装新版本时出现问题。有时新版本的程序确实会更改文件名——对此要保持警惕。

因此，如果你需要知道 /usr/local 中的任何项目是什么，只需使用 ls -l，链接就会告诉你它属于哪个软件包——例如：

```
$ ls -l /usr/local/bin/superformat
lrwxrwxrwx 1 root root 36 /usr/local/bin/superformat -> /opt/fdutils/default/bin/superformat
```

## 6.7 Troubleshooting Failed Compiles

你运行了 make，但事情并没有按计划进行。也许它没有通过编译阶段，或者已安装的软件包不能正常工作。原因可能从微不足道——例如，库路径不正确——到非常严重——例如，程序包编程不良甚至硬件问题。不幸的是，除非你查看源代码，否则你无法确切知道问题是什么。这对非程序员帮助不大。然而，通过一些指导，你可以猜测一些常见错误并制定适当的修复方法。

### Reading Error Output

首先，你必须知道如何阅读错误输出。假设编译失败，make 立即终止，并且在提示符之前最后一条消息看起来像这样：

```
make: *** [target] Error 1
```

满足 target 要求的某个步骤失败了。通常是一个文件名（可能是目标文件），编译器未能创建它。（我们将在“编译器错误”部分讨论如何修复该问题的策略。）

如果你收到这样的错误消息：

make: *** [target] Error 1 (ignored)

你通常可以忽略它（被忽略的错误不会导致 make 终止）。此错误可能意味着 make 尝试创建已存在的目录或其他项目，命令失败，但没人关心。

