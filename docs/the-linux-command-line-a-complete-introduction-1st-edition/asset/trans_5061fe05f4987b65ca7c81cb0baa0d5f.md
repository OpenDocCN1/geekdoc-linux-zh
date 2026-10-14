

要添加第二个文件，请输入：

```
:e ls-output.txt
```

它应该会出现在屏幕上。第一个文件仍然存在，我们可以验证一下：

```
:buffers
1 # "foo.txt"               line 1
2 %a "ls-output.txt"        line 0
Press ENTER or type command to continue
```

> 注意：你不能使用 `:n` 或 `:N` 命令切换到通过 `:e` 命令加载的文件。要切换文件，请使用 `:buffer` 命令并跟上缓冲区编号。

## 将一个文件的内容复制到另一个文件中

在编辑多个文件时，我们经常希望将一个文件的部分内容复制到正在编辑的另一个文件中。使用我们之前用过的常规复制和粘贴命令，可以轻松实现这一点。我们可以如下演示。首先，使用我们的两个文件，通过输入

```
:buffer 1
```

切换到缓冲区 1（foo.txt）。这应该会显示以下内容：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
```

接下来，将光标移动到第一行，输入 `yy` 来复制（拷贝）这一行。

通过输入

```
:buffer 2
```

切换到第二个缓冲区。屏幕上现在会显示一些文件列表，如下所示（这里只显示了一部分）：

```
total 343700
-rw-r--r-- 1 root root     31316 2011-12-05 08:58 [
-rw-r--r-- 1 root root      8240 2011-12-09 13:39 411toppm
-rw-r--r-- 1 root root    111276 2012-01-31 13:36 a2p
-rw-r--r-- 1 root root     25368 2010-10-06 20:16 a52dec
-rw-r--r-- 1 root root     11532 2011-05-04 17:43 aafire
-rw-r--r-- 1 root root      7292 2011-05-04 17:43 aainfo
```

将光标移动到第一行，然后输入 `p` 命令，粘贴我们从前一个文件中复制的行：

```
total 343700
The quick brown fox jumped over the lazy dog. It was cool.
-rwx--xr-x 1 root root    31316 2011-12-05 08:58 [
-rwx--xr-x 1 root root    8240 2011-12-09 13:39 411toppm
-rwx--xr-x 1 root root   111276 2012-01-31 13:36 a2p
-rwx--xr-x 1 root root    25368 2010-10-06 20:16 a52dec
-rwx--xr-x 1 root root    11532 2011-05-04 17:43 aafire
-rwx--xr-x 1 root root     7292 2011-05-04 17:43 aainfo
```

## 将一个完整文件插入到另一个文件中

我们也可以将整个文件插入到正在编辑的文件中。为了看到实际效果，让我们结束当前的 vi 会话，并仅用单个文件开启一个新会话：

```
[me@linuxbox ~]$ vi ls-output.txt
```

我们将再次看到文件列表：

```
total 343700
-rwx--xr-x 1 root root    31316 2011-12-05 08:58 [
-rwx--xr-x 1 root root    8240 2011-12-09 13:39 411toppm
-rwx--xr-x 1 root root   111276 2012-01-31 13:36 a2p
-rwx--xr-x 1 root root    25368 2010-10-06 20:16 a52dec
-rwx--xr-x 1 root root    11532 2011-05-04 17:43 aafire
-rwx--xr-x 1 root root     7292 2011-05-04 17:43 aainfo
```

将光标移动到第三行，然后输入以下 ex 命令：

```
:r foo.txt
```

`:r` 命令（read 的缩写）会将指定文件插入到光标位置之前。现在我们的屏幕应该看起来像这样：

```
total 343700
-rwx--xr-x 1 root root    31316 2011-12-05 08:58 [
-rwx--xr-x 1 root root    8240 2011-12-09 13:39 411toppm
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
-rwx--xr-x 1 root root   111276 2012-01-31 13:36 a2p
-rwx--xr-x 1 root root    25368 2010-10-06 20:16 a52dec
-rwx--xr-x 1 root root    11532 2011-05-04 17:43 aafire
-rwx--xr-x 1 root root     7292 2011-05-04 17:43 aainfo
```

## 保存我们的工作

与 vi 中的其他所有操作一样，有几种方法可以保存我们编辑过的文件。我们已经介绍了 ex 命令 `:w`，但还有一些其他命令可能也很有用。

在命令模式下，输入 `ZZ` 将保存当前文件并退出 vi。同样，ex 命令 `:wq` 将 `:w` 和 `:q` 命令组合为一个命令，既可以保存文件，也可以退出。

`:w` 命令还可以指定一个可选的文件名。这相当于“另存为”命令。例如，如果我们正在编辑 foo.txt，并想保存一个名为 foo1.txt 的替代版本，我们可以输入以下命令：

```
:w foo1.txt
```

注意：虽然这会以新名称保存文件，但不会改变你正在编辑的文件名。当你继续编辑时，你仍然在编辑 foo.txt，而不是 foo1.txt。

