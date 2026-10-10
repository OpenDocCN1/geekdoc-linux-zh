
```
if [ -f ~/.bash_aliases ]; then
  ~/.bash_aliases
fi
```

你也可以直接将别名放置在 `bashrc` 文件中。有些已经定义了，但被注释掉了。你可以编辑 `bashrc` 文件并删除这些行中的 `#` 注释符号来激活别名。

- 一些 `lr` 别名
`alias ll='ls -l'`
`alias la='ls -A'`
`alias li='ls -CF'`

## 命令与选项的别名

你可以使用 `alias` 来替换命令及其选项，但你需要将命令和选项都包含在单引号内。任何你设置了别名且包含空格的命令也必须包含在单引号中。在下一个示例中，别名 `ls` 引用带有 `-s` 选项的 `ls` 命令，别名 `isa` 引用带有 `-F` 选项的 `ls` 命令。带有 `-s` 选项的 `ls` 命令按块列出文件，而带有 `-F` 选项的 `ls` 在目录名后加上斜杠。注意单引号是如何封装命令及其选项的。

```bash
$ alias ls='ls -s'
$ ls
mydata 14 6 reports 1
$ alias isa='ls -F'
$ isa
mydata today reports/$
```

别名有助于简化复杂操作。在下一个示例中，`listlog` 成为根列表文件信息的另一个名称，以及用于使用人类可读格式文件大小的 `-h` 选项。务必将命令及其参数包含在单引号内，这样它们会被视为一个参数，而不是被 shell 解析。

```bash
$ alias listlog='ls -lh'
$ listlog
-rw-r--r-- 1 root 51K Sep 18 2008 mydata
-rw-r--r-- 1 root 16K Sep 27 2008 today
```

## 命令与参数的别名

你可以使用别名来包含一个命令名。你可能使用别名来包含根列表文件信息，以及用于使用人类可读格式文件大小的 `-h` 选项。请确保将命令及其参数包含在单引号内，这样它们会被视为一个参数，而不是被 shell 解析。

你可能使用别名来包含一个命令名。

```bash
$ alias ls='ls -s'
$ ls
mydata 14 6 reports 1
$ alias isa='ls -F'
$ isa
mydata today reports/$
```

```bash
$ alias listlog='ls -lh'
$ listlog
-rw-r--r-- 1 root 51K Sep 18 2008 mydata
-rw-r--r-- 1 root 16K Sep 27 2008 today
```

## 配置目录

你可能使用别名来包含一个命令名。

```bash
$ alias ls='ls -s'
$ ls
mydata 14 6 reports 1
$ alias isa='ls -F'
$ isa
mydata today reports/$
```

```bash
$ alias listlog='ls -lh'
$ listlog
-rw-r--r-- 1 root 51K Sep 18 2008 mydata
-rw-r--r-- 1 root 16K Sep 27 2008 today
```
