
以下与 Erlang shell 的交互将帮助你澄清许多与列表相关的事项：

```erlang
-module(cmdArgs).
-export([main/1]).

main(Args) ->
  io:format("Printing arguments:~n",[]),
  lists:foreach(fun(Arg) -> io:format("Arg: ~p~n", [Arg]) end, Args).
```

从命令行执行`cmdArgs.erl`中的`main/0`函数会产生以下类型的输出：

```bash
$ erlc cmdArgs.erl
$ erl -noshell -s cmdArgs main 1 2 3 4 five -s init stop

Printing arguments:
Arg: 1
Arg: 2
Arg: 3
Arg: 4
Arg: five
```

## 以读模式打开文本文件

以下 Erlang 代码打开由`File`标识的文件以供读取：

```erlang
{ok, FD} = file:open(File, [read])
```

`workText.erl`中说明了`file:open()`的用法。从`workText.erl`中执行`lineByLine/1`会产生以下类型的输出：

```erlang
1> c(workText).
{ok, workText}
2> workText:lineByLine("cmdArgs.erl").
-module(cmdargs).
ok.
```

`lineByLine/1`函数逐行读取文件，并在`read_line_by_line(FD)`函数的帮助下打印其内容。

你可以看到，以读模式打开文件可能会因各种原因失败，包括文件未找到以及没有正确的文件权限来打开文件。因此，如果存在此类错误，你将得到以下类型的错误消息：

```erlang
4> workText:lineByLine("cmdargs").
** exception error: no match of right hand side
   value {error,enotfound}
5> in function workText:lineByLine/1 (workText.erl, line 5)
```

学习如何解释和处理错误消息至关重要且实用，因为它允许你根据获得的错误类型决定采取何种措施。请注意，当你处理二进制文件时，也会收到相同的错误消息。

图 1 展示了在`workText.erl`中发现的`lineByLine/1`和`read_line_by_line/1`两个函数的实现。`file:read_line()`函数从文件中读取单行。

![](img/6866071e033820549b214c239744aaa0_47_0.png)

右侧：使用`file:open/2`函数打开文件以供读取，并使用`file:read_line/1`从打开的文件中读取单行

## 以写模式打开文本文件

为了以写模式打开文件，你需要更改`file:open()`函数第二个参数的值，即 Mode。如果你要写入的文件已经存在，它将被截断，因此请格外小心。如果你不希望出现这种行为，请使用追加模式。

图 2 展示了`writeToFile/1`的实现，该实现说明了`file:write()`函数的用法。执行`writeToFile/1`会产生以下结果：

```erlang
1> c(workText).
{ok, workText}
2> workText:writeToFile("./testing").
ok
3> q().
ok
$ cat testing
A Message.
```

![](img/6866071e033820549b214c239744aaa0_47_1.png)

右侧：使用`file:write/1` Erlang 函数向文件写入数据

## 错误处理

当你需要处理文件读写操作时，错误处理是一项关键任务，因为在文件 I/O 过程中很多事物都可能出错。再次强调，Erlang 中的错误处理是通过模式匹配实现的。以下 Erlang 函数介绍了一种处理与`file:open/1`相关错误的简单方法：

```erlang
open_file_with_error_handling(File) ->
   case file:open(File, [read]) of
       {ok, Fd} ->
           io:format("File ~p opened successfully.~n", []),
           [File],
           file:close(Fd);
       {error, Reason} ->
           io:format("Error opening ~p.~n", [File]),
           io:format("Reason:~p.~n", [Reason])
   end.
```

你可以通过访问`bit.ly/2XMOHCm`来了解各种与文件相关的错误代码及其描述。

## 创建临时文件

本节将解释如何在 Erlang 中使用随机文件名创建临时文件，当你要保存数据而不必担心意外选择现有文件名时，这非常实用。开发的函数利用了`erlang:timestamp/0`函数，该函数返回当前系统时间作为包含三个元素的元组，这对于每个给定的系统都是唯一的。该元组被转换为单个变量，可用于生成新的文件或目录。图 3 展示了`workBin.erl`文件中找到的`create_temporary/0`函数的 Erlang 代码。执行该函数会产生以下结果：

![](img/6866071e033820549b214c239744aaa0_47_2.png)

右侧：本图中展示的 Erlang 代码说明了如何创建唯一的名称

```erlang
10> c(workBin).
   {ok, workBin}
11> workBin:create_temporary().
   Unique filename: "1485-326598-527282"
   ok
12> workBin:create_temporary().
   ok
   Unique filename: "1485-326600-978734"
```

## 使用 Erlang 开发 wc

本节将展示`wc(1)`在 Erlang 中的一个基础实现。`wc.erl`的代码将不支持命令行开关，也不会打印读取的字符、单词和行的总数，因为这需要太多的代码。

你也允许专门处理某些错误消息。你可以在`workBin.erl`中找到代码。执行它会产生以下类型的输出：

图 4 展示了`wc.erl`的 Erlang 代码的一部分。从`wc.erl`的实现中你可以理解，Erlang 可能不是此类命令行工具的最佳选择！

```erlang
2> workBin:open_file_with_error_handling("wc.erl").
File "wc.erl" opened successfully.
ok
["wc.erl"]
3> workBin:open_file_with_error_handling("wc").
Error opening "wc".
Reason:enoent.
ok
```

输入文件作为列表传递给`wc:start/1`函数进行处理。但是，如果你想要处理单个文件，可以使用`wc:one_file/1`函数代替。`wc.erl`中最重要的是两个函数：`process_file/0`和`count_bin/0`。第一个函数确保所有文件都被处理，而第二个函数在`which_char/1`的少量帮助下执行实际的处理。每个文件的内容使用列表操作逐字符处理，这在函数式编程语言中相当常见。此外，`which_char/1`的定义允许你轻松更改处理特殊字符的方式。

## Erlang 适合文本处理吗？

以多个文件名作为参数执行`wc:start/1`会产生以下类型的输出：

| 文件 | 单词数 | 字符数 | 行数 |
| :--- | :--- | :--- | :--- |
| wc.erl | 217 | 1828 | 84 |
| mvc.erl | 1899 | 222 | 88 |
| ok | | | |
