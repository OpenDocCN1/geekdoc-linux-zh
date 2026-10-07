

## 实验 11.2

## exec 命令

## 实验目标

完成本实验后，你将能够：

- 使用 `exec` 执行另一个程序
- 使用 `exec` 打开和关闭文件
- 使用 `exec` 读写“有趣”的设备

`exec` 命令有两个不同的用途。一种是在执行 `exec` 时，让另一个程序替换当前正在运行的程序；另一种（可以与第一种用法结合使用）是打开和关闭文件描述符（fds）。在本实验中，我们将简要介绍第一种用法（这也是 `exec` 名称的由来），但我们将把大部分时间花在这一多功能命令更常用的用途上。

## 实验 11.2 练习

### 11.2.1 使用 exec 执行另一个程序

在名为 `tryexec` 的脚本中输入以下命令并运行它：

请确保你将其作为一个脚本而不是函数！如果你作为函数运行它，它会将你注销系统。

```bash
# tryexec -- 使用 exec 来执行另一个程序。
exec ls > ls.out
print "If you can read this . . . well, you can't.",
```

- a) 文件 `ls.out` 是否用 `ls` 命令的输出创建了？
- b) `print` 命令是否执行了？
- c) 如果用这些命令创建一个函数并运行它，或者从 shell 提示符运行这些命令，或者对脚本进行 source（dot），会发生什么？

### 11.2.2 使用 exec 打开并关闭文件

到为止，你已经学会了处理三个标准 I/O 文件描述符：`stdin`（fd 号 0）、`stdout`（fd 号 1）和 `stderr`（fd 号 2）。你在实验 2.3“重定向输入和输出”中看到了如何重定向和复制它们，并且已经看到 `print` 命令的 `-u` 参数是实现输出重定向的另一种方法。在本章的前面你还看到 `read` 命令也接受 `-u` 参数，但你还没有用过它。

现在是时候稍微扩展你对 I/O 处理的理解了。KornShell 允许通过在 `exec` 命令上编写 I/O 重定向操作符，一次处理多达 10 个编号为 0–9 的文件描述符。通常情况下，你在进行 I/O 重定向时不指定让 `exec` 运行的命令。

#### 示例

处理文件时的常规序列是：使用 `exec` 打开文件，然后使用该文件执行一系列 `read` 或 `print` 命令，最后使用另一个 `exec` 命令关闭文件。例如，以下两组命令将把 `file1` 复制到 `file2`。第二种方法显然不是完成此任务的高效方法，但它说明了 `exec` 的用法。

复制文件的正常方法：

```bash
cp file1 file2
```

使用 `exec` 相同的操作：

```bash
exec 3< file1
exec 4> file2
while read -ru3
do
  print -u4 "$REPLY"
done
exec 3<&-
exec 4<&-
```

- a) 前两个 `exec` 命令的作用是什么？
- b) 最后两个 `exec` 命令的作用是什么？
- c) `read` 命令上的 `-ru3` 起什么作用？
- d) `REPLY` 引用周围的引号有什么作用？
- e) 与第一个版本相比，第二个版本的低效之处在于哪里？

以下名为 `shuffle` 的脚本允许用户对文件对进行“完美洗牌”（完美洗牌是指洗牌一副扑牌，使得牌组的两部分中的牌逐一交替出现）。以下问题基于该脚本，“测试你的思考”问题将给你一个机会对其进行一些必要的改进。

你可以从此处下载该脚本的副本：

```
http://www.phpptr.com/phpptrinteractive/
```

```bash
# shuffle -- 对文件对进行完美洗牌。
while read -A inFiles
do
  print "输入要洗牌的两个： "
  [[ $(inFiles[0]) == "." || $(inFiles[0]) == "q" ]] && return
  [[ ${#inFiles[@]} != 2 ]] && (
    print -u2 \
    "请输入两个文件名。必要时使用引号。"
    continue
  )

  exec 3 < "${inFiles[0]}"
  exec 4 < "${inFiles[1]}"

  read outputFile?"你想把洗牌后的输出放在哪里？"
  exec 5 > "$outFile"

  IFS=
  while read -ru3
  do
    print -u5 "$REPLY"
    read -ru4
    print -u5 "$REPLY"
  done
  IFS=$' \t\n'
  exec 3<&-
  exec 4<&-
  exec 5<&-
done
print
```

- f) 用户输入哪四种内容会导致脚本停止执行？
- g) 脚本末尾 `print` 命令的作用是什么？
- h) 如果用户输入一个不存在的文件会发生什么？
- i) 如果用户输入一个已经存在的文件会发生什么？
- j) 如果用户输入一个不是文件的名称会发生什么？

