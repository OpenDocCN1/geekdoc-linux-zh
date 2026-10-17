
注意，我们在上面的脚本中使用了注释。`sed` 脚本中，任何以井号 `#` 开头的行都会被视为注释并被 `sed` 忽略。

## 选择性打印：案例研究

作者用于在计算机上安装软件的包管理器会打印如下格式的错误：

```
Installing...

package-name: /path/to/file already exists in filesystem

package-name: /path/to/file2 already exists in filesystem
```

这在你尝试安装一个已经存在的东西时发生。在这种情况下，包管理器不会覆盖文件，而是会将控制权交回用户，以便他们决定如何处理冲突文件。

很多情况下，安装后文件会遗留并且应该被删除。

> `Sed` 除了简单的文本替换外还提供了许多功能

## 使用 sed 编辑文件

使用普通的管道为文件运行 `sed` 命令是很容易的。例如：

```
$ sed s/dammarn/ > clean_email.txt
```

然而，这对于根据结果创建一个新文件是没用的。因此，使用 `sed -i` 直接修改文件：

```
$ sed -i orig.txt 's/dammarn/'
```

`-i` 后的 `.orig` 是可选的，但如果我们对 `sed` 命令犯了错，就会丢失原始文件。如果在 `-i` 之后添加扩展名，它将保存一份文件的副本。

```bash
#!/bin/sed -f
s3 's/abc//g'
s4 's/def//g'
s5 's/ghi//g'
s6 's/jkl//g'
s7 's/mno//g'
s8 's/pqr//g'
s9 's/stu//g'
s10 's/vwx//g'
s11 's/xyz//g'
```

## Essential admin commands

`Adam Oxford` runs South African tech news site
`WWW.techradar.co.za`
He learned many of these lessons the hard way.

Terminal commands that all Linux server administrators should know blindfolded.

You're an accidental admin! Someone resolved to late, that you were the responsibilities of Linux server - and because nothing has gone wrong lost in a world of terminals and commands.

Also can't remember that clever thing you did last week? The history is command you.

## Resources

All Linux distros are different and most have a number of terminal-based text editors you can access on the CLI

```
$ netstat -atnu
$ ifconfig -a
$ top
$ df -h
$ ls -ltr
$ uptime
$ pkill -f
$ grep
$ chroot
$ what it was doing
$ apt get update
```

## Tutorial sed

To write a script, we start off with the following shebang line:

```
#!//bin/sed -f
```

The commands we have learned are quite simple, but further commands that will help perform looping, saving of state and operations on multiple lines at a time. If you want to learn about these, a good place to start is by reading or better the script we wrote is an emulation of a filter that reverses its content. If you want to learn some of the advanced features of sed, a good place to start is by writing why this script works as it does.

...which tells that the script should be run by the `sed` command. If we want to extend the Regular Language, we should use `#!/bin/sed -ef` instead. We can then list the commands in one file. For example:

```
#!/bin/sed -f
# Replace spaces
s/ /g
# Replace 'gobi' with 'tuna'
s/gobi/tuna/g
```

Save this into a file named `loop-replace.sed` and then run with `sed -f loop-replace.sed`. You can then run it directly from the command line:

```
$ sed -f loop-replace.sed
forgo bite
fortunate
```

Note that we used comments in the script above. A `sed` script, any line with a hash `#` is treated as a comment and ignored by `sed`.

## Selective printing: a Case Study

The package manager that your author uses to install software on their computers prints out errors of the form:

```
Installing...

package-name: /path/to/file already exists in filesystem

package-name: /path/to/file2 already exists in filesystem
```

This happens when you try to install something that already exists. In this case, the package manager will not overwrite the files, but will pass control back to the user so they can decide what to do with the conflict files.

More than often, it turns out that the files are left over after a installation and should be deleted.

> `Sed` provides pieces of functionality besides simple replacement of text

## Editing files with sed

It is easy to use the normal pipeline to run a `sed` command for file. Example:

```
$ sed s/dammarn/ > clean_email.txt
```

However, this is useless to create a new file out of the result. So use `sed -i` in place to modify the file:

```
$ sed -i orig.txt 's/dammarn/'
```

The `.orig` after `-i` is optional, but if we make a mistake with our `sed` command, then we end up losing our original file. If we add the extension after `-i`, then it will save a copy of the

```bash
#!/bin/sed -f
s3 's/abc//g'
s4 's/def//g'
s5 's/ghi//g'
s6 's/jkl//g'
s7 's/mno//g'
s8 's/pqr//g'
s9 's/stu//g'
```

你不仅是一个可能试图恢复或修复某些不属于你的你的陌生人，而且这些东西只需花几英镑就很难处理，而你又不需要麻烦。
