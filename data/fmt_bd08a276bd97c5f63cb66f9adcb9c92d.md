
Now try them and see whether you’re correct.

- 2. Does the file size listed by `wc -c` always agree with the file size listed by the `ls` command? With the size indicated by `ls -s`? If there is any difference, why?

- 3. What do you think would happen if you tried to sort a list of words by pretending they’re all numbers? Try it with the command `ls -1 | sort -n` to see what happens. Experiment with the variations.

- 4. What wildcard expression would you use to find the following?
  
  - All files in the `/tmp` directory
  - All files that contain a `w` in that directory
  - All files that start with a `b`, contain an `e`, and end with `.c`

- All files that either start with `test` or contain the pattern `hi` (notice that it can be more than one pattern)

- 5. Create regular expressions to match the following:
  - Lines that contain the words `hot` and `cold` (tricky!)
  - Lines that contain the word `cat` but not `cats`
  - Lines that begin with a numeral

- 6. Use the `-v` flag with various `grep` commands and show the command and pattern needed to match lines that:
  - Don’t contain `cabana`
  - Don’t contain either `jazz` or `funk`
  - Don’t contain `jazz`, `funk`, `disco`, `blues`, or `ska`

## Preview of the Next Hour

The next hour introduces you to many more commands that are ideal for working with pipelines and filters—commands that will help you move from being a Unix amateur to being a true expert, a wizard at the command line!

## Hour 9. Slicing and Dicing Command-Pipe Data

## Goals for This Hour

In this hour, you will learn

- About the `awk` programming system
- How to use `cut` in pipes
- About using `sed` and `tr` for in-line transformations

By this point, you’ve learned enough about Unix to be able to build quite sophisticated command-line pipes, sequences of standard commands that offer flexibility and power. You need to add a couple of key tools to your toolkit to keep moving forward, however, and they’re the focus of this lesson.

The first and most powerful of the tools is `awk`, a programming system built specifically to work with data streams. You can build very complex processing systems in `awk`, but in fact the most common `awk` programs are typically just a line or two long.

Many modern Unix folk prefer Perl, but I find that Perl isn’t as pervasive across Unix, Linux, and other *nix platforms, so I’ll stick with `awk` for this lesson. I do cover Perl later in the book, though, in case you’re curious. If you’d prefer to just learn Perl, you can find a lot of really good tutorials on this sophisticated—and confusing—programming language.

In addition to explaining `awk`, this hour also talks about three additional pipeline commands that you will doubtless find essential for your toolbox: `sed`, a stream editor; `tr`, a character mapping facility; and `cut`, a utility that makes it remarkably easy to slice individual columns of data out of a pipeline of information.

There’s one interesting characteristic of `awk` that’s worth mentioning before we go further: It’s a powerful programming language, and you can use it to duplicate many of the actual utilities that are an essential part of the Unix operating system. In a moment, I’ll show you how to duplicate the `wc` command with a few lines of `awk`.

Later in the book, in Hour 23, “Perl Programming in Unix,” we’ll explore the Perl programming language and how it’s integrated into modern Unix systems. Like `awk`, Perl has the ability to duplicate many of the most common Unix commands. Perl is also considerably more powerful and sophisticated than `awk`.

Okay, true confession: I don’t recommend actually rewriting existing commands, but it is good to know which of the tools in the Unix toolbox are actually all-purpose utilities rather than just focused on a single, specific task.

# awk 编程系统

无论是 C、Pascal、BASIC、Java，甚至是 Swift，每种编程语言都有其擅长之处，也就是它真正闪光的领域。如果是 BASIC，那就是简单的入门编程。如果是 Java，那就是跨平台软件。Ruby、Python、C++、LISP 以及所有其他编程语言都有其专为之设计的特定类型编程。然而 `awk` 不同，它存在于简单的 shell 脚本和这些复杂语言之间。它不具备正式编程环境的大多数特性和功能，但以其自身的方式，`awk` 非常强大，并且对于轻量级、内联数据处理来说绝对是理想选择。

## 任务 9.1：学习使用 awk

每个 `awk` 脚本的基本结构都是一个模式后跟一条命令。如果你跳过模式，则该命令适用于数据流中的所有行。如果你跳过命令部分，则所有匹配的行都会被打印（发送到输出数据流）。

作为一个非常简单的例子，程序 `NF == 3`（没错，这就是这个程序所需的一切！）将打印输入中恰好有三个字段的所有行（`NF` 是指输入行中字段数量的简写）。程序 `$1 > 3 { print $1 }` 将打印所有该字段数值大于三的行中的第一个字段。

让我们更仔细地看看 `awk`。

- 1. 我想弄清楚我在构建的新系统上所有邮件文件的平均大小。为此，我将从 `ls` 开始获取文件大小：

Click here to view code image

```
