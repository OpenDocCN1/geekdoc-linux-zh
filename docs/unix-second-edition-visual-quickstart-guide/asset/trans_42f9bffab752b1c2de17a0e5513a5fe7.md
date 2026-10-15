

## Tips

- 如果你在协作进行一个项目，请让你的系统管理员为该项目创建一个专门的组。这样，你和你的团队成员就可以轻松共享文件。
- 你也可以使用 `groups` 或 `id` 命令，这提供了快速了解组成员身份的方法。它们提供了关于组成员身份（以及用户 ID）的基本细节，但不会用系统上其他最有趣且可能有用的细节淹没你。前往第 7 章了解更多信息。
- 查看第 1 章了解更多内容。
- 查看第 6 章了解关于 grep 的完整信息。

## Tips

- 如果你尝试更改组所有权并收到类似 "Not owner" 或类似晦涩的错误信息，你的用户 ID 没有必要的权限来做出更改。你将不得不请你的系统管理员提供帮助。

- 只有在有特定需要时才更改组关联；你不想不必要地让其他人访问你的文件。除非你是系统管理员，否则你将无法完全控制有权访问你文件的组的成员。

- 如果你更改了特定目录的组关联，你还需要检查包含它的目录的权限。用户将无法进入该特定目录（无论其组成员身份如何），除非他们对包含它的目录也具有读和执行权限。

- 就像第 2 章中介绍的 `cp` 和 `mv` 命令一样，你可以使用 `-R` 标志与 `chgrp` 一起使用，以递归地将更改应用于目录及其所有子目录和文件。例如，要将 LatestProject 目录及其所有内容与 project 组的关联更改，请从 LatestProject 上一级的目录中使用 `chgrp -R project LatestProject`。

## Changing Ownership of Files and Directories with chown

### Tips

- 在你更改文件的所有权后，你能对文件做什么取决于组和其他权限以及成员身份。然而，新所有者将能够对文件做任何事情。
- 当更改目录的所有权时，你可以添加 `-R` 标志到 `chown`，使其递归地应用于其下的所有文件和目录。
- 如果系统不允许你使用 `chown` 来赠送文件，请考虑使用 `cp` 来复制文件以达到同样的目的。如果你复制了别人拥有的文件（你有权限读取），复制的文件完全属于你了。（在这个赠送文件的例子中，接收者应使用 `cp`。）
- 即使你不能使用 `chown`，你仍可以请求系统管理员为你更改文件所有权："你能请用 `chown merrilee /home/shared/me/rowyourboat` 将我的 `rowyourboat` 文件的所有权更改为 Merrilee 吗？谢谢！"

假设你一直在处理一个名为 `rowyourboat` 的文件，而你的老板决定让同事 Merrilee 接手该项目。在这种情况下，为了完全把项目推给你的同事，你需要将文件的所有权从你更改为她。根据你的系统管理员如何设置系统，你通常可以使用 `chown` 来更改文件的所有权（代码清单 5.6）。

### To change ownership with chown

1. `ls -l`

   首先，在 shell 提示符下输入 `ls -l` 以验证文件的名称和所有权，如代码清单 5.6 所示。记住，所有权信息位于权限和链接信息之后。

2. `chown merrilee rowyourboat`

   输入 `chown`，后跟你想要转移所有权给的人的用户 ID 和文件名。在这种情况下，`chown` 命令将 `rowyourboat` 的所有权更改为 `merrilee`。`rowyourboat` 及其相关问题现在将属于她，生活将只是梦想。

```
[ejr@hobbes merrilee]$ ls -l
total 26
-rw-rw-r-- 1 ejr users 24850 Jul 24 15:17 rowyourboat
[ejr@hobbes merrilee]$ chown merrilee rowyourboat
[ejr@hobbes merrilee]$ ls -l
total 26
-rw-rw-r-- 1 merrilee users 24850 Jul 24 15:17 rowyourboat
[ejr@hobbes merrilee]$
```

Code Listing 5.6 Changing ownership of files transfers complete control.

