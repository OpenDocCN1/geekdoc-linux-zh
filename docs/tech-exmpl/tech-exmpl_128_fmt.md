

# 在 Ruby 语言中执行系统命令

> 原文：[`techbyexample.com/execute-system-commands-ruby/`](https://techbyexample.com/execute-system-commands-ruby/)

## 概述

Ruby 的`system`方法可以用来在 Ruby 中运行系统命令。以下是相应的语法：

```ruby
system(some_command)
```

关于系统命令的一些重要事项：

- 它将等待直到命令执行完毕。
- 如果命令成功，它将返回`true`。
- 如果命令执行失败并返回错误代码，它将返回`false`。
- 如果命令未找到，它将返回`nil`。

让我们来看一个相应的程序：

## 程序

```ruby
output = system("pwd")
puts "For pwd command: " + output.to_s

output = system("exit 1")
puts "For exit 1 command: " + output.to_s

output = system("pwd1")
puts "For pwd1 command: " + output.to_s
```

### 输出

```text
<current_directory>
For pwd command: true
For exit 1 command: false
For pwd1 command:
```

在上面的程序中，有三种情况。

### 当命令成功时

```ruby
output = system("pwd")
puts "For pwd command: " + output.to_s
```

在这种情况下，输出是`true`：

```text
<current_directory>
For pwd command: true
```

### 当命令失败时

```ruby
output = system("exit 1")
puts "For exit 1 command: " + output.to_s
```

在这种情况下，输出是`false`：

```text
For exit 1 command: false
```

### 当命令不存在时

例如，`pwd1`是一个无效命令：

```ruby
output = system("pwd1")
puts "For pwd1 command: " + output.to_s
```

在这种情况下，输出是`nil`：

```text
For pwd1 command:
```

