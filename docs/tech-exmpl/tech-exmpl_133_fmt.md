
# 在命令行或终端中运行 Ruby 语言代码：单行和多行

> 原文：[`techbyexample.com/ruby-command-line-terminal/`](https://techbyexample.com/ruby-command-line-terminal/)

## 概述

可以直接在命令行或终端中运行 Ruby 代码。我们需要传递`-e`标志。以下是相应的语法：

```bash
ruby -e "<ruby_code>"
```

## 单行程序

下面是一个简单的示例：

```bash
ruby -e "puts 'hello'"
```

在终端上运行上述命令，它将输出：

```text
hello
```

## 多行程序

如何运行多行 Ruby 代码？下面是相同的示例。你不需要使用`-e`标志。

```ruby
ruby <<END
 puts "Start"
 5.times do |i|
   puts i
 end
 puts "End"
END
```

上述程序将输出：

```text
Start
0
1
2
3
4
End
```

- [ruby](https://techbyexample.com/tag/ruby/)
