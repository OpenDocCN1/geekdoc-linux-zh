
输出显示，原始登录 -bash shell 的 PID 为 2393，而 script1 在执行时返回了日期和 PID 2413。记住这个概念非常重要。在这种情况下，PID 2413 是 PID 2393 的子进程。

图 13.1 表明，名为 -bash 的登录 shell 开启了另一个 bash 子 shell 来运行 script1，而 date 命令本身将在另一个子 shell 中运行。所有子 shell 仅在其相应命令执行期间存在。同样，当它们完成执行后，控制权将返回给登录 -bash shell，该 shell 在子 shell 执行其功能期间一直处于休眠状态。

## 选项 2：通过使脚本可执行来调用脚本

当 script1 被设置为独立可执行并被调用时，登录 -bash shell 会再次调用一个 bash 子 shell 来执行 shell 脚本文件（基本上与选项 1 中使用 bash 命令时的过程相同）。

唯一的区别在于——现在你可能已经意识到这一点——shell 脚本已被标记为可执行。这样，你可以直接执行该脚本，例如：

![](img/cae5c706c216875d12d4b7d28144cc71_425_0.png)

**图 13.1** 使用 bash 命令调用 shell 脚本。

```
$ script1<Enter>
Wed Jul 25 15:07:51 MDT 2001
```

如图 13.2 所示，在登录 shell 中单独调用 script1 会触发另一个 bash 子 shell，该子 shell 作为登录 shell 的子进程运行。当该子 shell 执行完 script1 文件中的命令后，它将终止，并将控制权交还给父进程，即登录 -bash shell。

### 示例 13.7 处理自行调用的 Shell 脚本

我们将以与选项 1（示例 13.6）相同的方式演示这种行为：

- 识别并回显当前 shell 的 PID。
- 在 script1 执行过程中，要求其回显实际执行它的 shell 的 PID。

使用 `$ chmod 775<Enter>`，Molinera 女士现在已使 script1 可执行。其长列表现在看起来如下：

```
$ ls -l script1<Enter>
-rwxrwxr-x 1 molinera knights3 13 Jul 14 15:10 script1
```

在运行脚本之前，她再次显示当前 shell 的 PID，以证明它与脚本最终将执行的子 shell 不同：

```
$ echo $$<Enter>
2393
$ bash script1<Enter>
Wed Jul 25 14:35:59 MDT 2001
2443
```

此输出显示原始登录 -bash shell 的 PID 为 2393，而 script1 在执行时返回了日期和 PID 2443。再次强调，记住这个概念很重要。这次 PID 2443 是 PID 2393 的子进程。

图 13.2 表明，名为 -bash 的登录 shell 开启另一个 bash 子 shell 来运行 script1，而 date 命令本身将在另一个子 shell 中运行。当它们完成后，控制权交还给登录 -bash shell，该 shell 在子 shell 执行功能期间一直处于休眠状态。

![](img/cae5c706c216875d12d4b7d28144cc71_427_0.png)

图 13.2 调用可执行的 shell 脚本。

## 选项 3：在同一 shell 中调用脚本

可以强制 shell 脚本在当前 shell 中执行，而不是打开所有其他子 shell。你可以通过将语法更改为以下内容来完成此任务：

```
$ . scriptfilename<Enter>
```

或者

```
$ source script1<Enter>
```

在第一个语法示例中，“.” 表示“在当前 shell 中”。该过程最终将类似于图 13.3 所示。

### 示例 13.8 在同一 shell 中调用脚本

Freston 告诉 Molinera 女士，如果她强制 script1 在她当前所在的 shell 中执行，可以节省一些 CPU 周期和纳秒时间。但为了证明这一点，他让她再次检查她的 shell 的 PID，就像她在选项 1 和 2 中所做的那样。

```
$ echo $$
2393
$ . script1
Wed Jul 25 15:55:28 MDT 2001
2393
```

她通过在脚本前加“.”来执行 script1。记住，“.” 意味着“在当前 shell 中执行此操作”。原始 shell 返回的 PID 为 2393，shell 脚本也返回了当前 PID 2393。“.” 的替代语法是 “source”。这两种方法是相同的，图 13.3 说明了这两种方法。

```
$ echo $$
2393
$ source script1
Wed Jul 25 16:05:53 MDT 2001
2393
```

### 示例 13.9 “即时”修改 .bash_profiles

你认为这种方法在其他什么场合有用？假设 Freston 刚刚修改了他的隐藏 .bash_profile 文件。使用 “.” 或 source，他可以让 shell 重新执行他的用户配置文件，而无需注销并重新登录。在对文件本身进行修改后，他只需输入以下任一命令：

```
$ . .bash_profile<Enter>
```

或者

```
$ source .bash_profile<Enter>
```

![](img/cae5c706c216875d12d4b7d28144cc71_428_0.png)

图 13.3. 在当前 shell 内部调用 shell 脚本。

## 创建脚本：一些实用示例

### 示例 13.10 导出变量和值以供脚本使用

以下脚本展示了经典 Hello World 脚本的一种变体：Sancho 正在向他的驴 Dapple 发送问候（好吧，也许其中一个训练员会念给他听，谁知道呢？）。我们将使用这个简单脚本来说明变量的导出以及如何在子 shell 中访问它们。

```
$ cat > hello<Enter>
1 #!/bin/bash
2 #This is a simple Hello World type of script
3 #
4 var1="Hi Dapple! Ready for our August journey?"
5 echo $var1
<Ctrl>-d
```

现在，要使脚本可执行，

```
$ chmod 755 hello<Enter>
```

当执行时，hello 脚本将返回以下内容：

```
$ hello<Enter>
Hi Dapple! Ready for our August journey?
```

hello 脚本列出了行号以供参考。在我们审查它时，不会提及所有行。实际上，如果你将这些脚本作为示例使用，请去掉行号。

第 1 行虽然包含一个井号（#），但实际上是一个 shell 声明（! 确保了这一点）。放入此类声明被认为是正确的做法，因为你永远不知道用户将在哪个 shell 中（并且此添加保证该脚本将在 bash shell 环境中执行）。

第 2 行是一个注释。描述脚本做什么以及有时提供联系支持的方式也被认为是一种最佳实践。在许多情况下，这些行包括大型环境中关于脚本版本控制的信息。

第 3 行是注释空行。此行使脚本编写“更易于阅读”（换句话说，更易于创建；更易于调试；更易于分析；甚至更易于复制）。

第 4 行将一个名为 var1 的用户定义变量设置为字符串 “Hi Dapple! Ready for our August journey?”。当在脚本内部设置变量时，永远不会质疑 var1 等于什么。

第 5 行将字符串回显到标准输出，即终端屏幕。

我们将使用此示例来演示如何访问脚本外的变量。在接下来出现的示例代码中，我们将设置另一个变量。但这一次，它将在当前 shell 环境中、脚本外部设置。这里需要注意的是，脚本将找不到该变量。这是有意为之，我们将在下一个示例代码中修复它：

```
$ cat >> hello<Enter>
<echo $var2<Enter>
<Ctrl>-d

$ var2="Yes I am. Let’s go!“<Enter>
$ echo $var2<Enter>
Yes I am. Let’s go!
$ cat hello<Enter>
#!/bin/bash
#
#This is a simple Hello World type of script
#
var1="Hi Dapple! Ready for our August journey?"
echo $var1
echo $var2
$ hello<Enter>
Hi Dapple! Ready for our August journey?
```

注意 var2 没有显示。原因是脚本在子 shell 中执行。在父登录 shell 中创建的 var2 变量未导出到子 shell。因此，子 shell 无法访问它。让我们现在使用 export 功能来修复这个问题。

```
$ export var2<Enter>
$ hello<Enter>
Hi Dapple! Ready for our August journey?
Yes I am. Let's go!
```

因此，许多系统管理员选择在需要变量的脚本内部设置所有变量。在依赖于 shell 外部变量的情况下，在继续执行任何希望进行的处理之前，你始终应该进行测试，以检查该变量是否为空。

### 示例 13.11 一个简单的备份脚本

一个更实用但仍然简单的脚本是一个备份脚本。但首先，让我们看看 Freston 的私有目录：

```
$ ls -l<Enter>
total 56
-rwxrwxr-x  1 freston knight84  110 Apr 14 12:47 monthly.rept
-rwxr-xr-x  2 freston knight84 4096 Jan  4 12:36 Desktop
-rwxrwxr-x  1 freston knight84  102 Mar 14 16:26 hello
-rwxrwxr-x  1 freston knight84   74 Jul 14 16:43 private_bu
-rwxrwxr-x  1 freston knight84   13 Jul 25 14:30 script1
-rwxr-xr-x  1 freston knight84   15 Jul 25 13:36 script2
-rw-rw-r--  1 freston knight84 2288 Jul 26 16:44 typescript
```

看看你能解释以下脚本的作用：

```
$ cat private_bu<Enter>
#!/bin/bash
BUF=$nightly/USER-backup-$(date +%Y%m%d).tgz
tar -cZf $BUF ~
```

脚本名为 private_bu，假设其权限为可执行。脚本指示在 bash shell 环境中运行。设置了一个名为 BUF 的变量，该变量被设置为一个字符串，该字符串将代表 tar 命令使用的备份文件名。BUF 的字符串将解析另一个名为 $USER 的变量，将其设置为 Freston，并将日期设置为指定的 年-月-日 格式，以保持文件名的唯一性。tar 命令将使用此 BUF 变量在名为 nightly 的目录内创建文件。基本上，Freston 正在一个特殊目录中创建一个单用户备份文件。

