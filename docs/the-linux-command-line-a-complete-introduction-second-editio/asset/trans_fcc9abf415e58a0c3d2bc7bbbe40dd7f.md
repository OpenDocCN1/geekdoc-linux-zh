

测试完成后。

## 测试用例

要进行有用的测试，重要的是开发并应用良好的 *测试用例*。这是通过仔细选择反映 *边界* 和 *角落* 情况的输入数据或操作条件来完成的。在我们的代码片段中（它很简单），我们想知道代码在三种特定条件下的表现如何。

- `dir_name` 包含现有目录的名称。
- `dir_name` 包含不存在的目录的名称。
- `dir_name` 为空。

通过在每种条件下执行测试，可以实现良好的 *测试覆盖率*。

与设计一样，测试也是时间的函数。并非每个脚本功能都需要进行广泛测试。这实际上是确定什么最重要的问题。由于如果出现故障可能会造成极大的破坏，我们的代码片段在设计和测试期间都值得仔细考虑。

## 调试

如果测试揭示了脚本的问题，下一步就是调试。“问题”通常意味着脚本在某种程度上没有达到程序员的预期。如果是这种情况，我们需要仔细确定脚本实际在做什么以及为什么。查找错误有时需要大量的侦探工作。

设计良好的脚本会尝试提供帮助。它应该以防御性方式编程，以检测异常条件并向用户提供有用的反馈。然而，有时问题却很奇怪且出乎意料，需要更复杂的技术。

## 查找问题区域

在某些脚本中，特别是较长的脚本，有时将脚本与问题相关的区域隔离是有用的。这不一定总是实际错误，但隔离通常会提供对实际原因的见解。用于隔离代码的一种技术是“注释掉”脚本的某些部分。例如，我们的文件删除片段可以被修改以确定被删除的部分是否与错误相关。

```
if [[ -d $dir_name ]]; then
    if cd $dir_name; then
        rm *
    else
        echo "cannot cd to '$dir_name'" >&2
        exit 1
    fi
# else
#     echo "no such directory: '$dir_name'" >&2
#     exit 1
fi
```

通过在脚本逻辑部分的每一行开头放置注释符号，我们可以防止该部分被执行。然后可以再次进行测试，以查看删除代码是否对错误的行为有任何影响。

## 跟踪

错误通常是脚本中意外逻辑流的情况。也就是说，脚本的某些部分要么从未被执行，要么以错误的顺序或错误的时间被执行。为了查看程序的实际流程，我们使用一种称为跟踪的技术。

一种跟踪方法是在脚本中放置信息性消息以显示执行位置。我们可以向我们的代码片段添加消息。

```
echo "preparing to delete files" >&2
if [[ -d $dir_name ]]; then
    if cd $dir_name; then
    echo "deleting files" >&2
        rm *
    else
```

```
echo "cannot cd to '$dir_name'" >&2
exit 1
fi
else
    echo "no such directory: '$dir_name'" >&2
    exit 1
fi
echo "file deletion complete" >&2
```

我们将消息发送到标准错误以将其与正常输出分开。我们还不对包含消息的行进行缩进，这样在需要删除它们时更容易找到。

现在执行脚本时，可以看到文件删除已执行。

```
[me@linuxbox ~]$ deletion-script
preparing to delete files
deleting files
file deletion complete
[me@linuxbox ~]$
```

bash 还提供了一种跟踪方法，通过 -x 选项和带有 -x 选项的 set 命令实现。使用我们之前的故障脚本，我们可以通过在第一行添加 -x 选项来为整个脚本激活跟踪。

```
#!/bin/bash -x

# trouble: script to demonstrate common errors

number=1

if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi
```

执行时，结果如下所示：

```
[me@linuxbox ~]$ trouble
+ number=1
+ '[' 1 = 1 ']'
```
