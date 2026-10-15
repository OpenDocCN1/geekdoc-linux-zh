
# 函数 (FUNCTIONS)

shell 函数与 shell 脚本类似，它们都存储了一系列命令以供以后执行。然而，由于 shell 将函数存储在计算机的主内存 (RAM) 中而不是磁盘上的文件中，shell 访问它的速度比访问脚本要快得多。shell 还会处理（解析）函数，使其启动得比脚本更快。最后，shell 在被调用的同一个 shell 中执行函数。如果你定义了许多函数，启动子进程（当你运行脚本时）的开销可能会变得无法接受。

你可以在 `~/.bash_profile` 启动文件、使用它的函数的脚本中或直接从命令行声明 shell 函数。你可以使用 `unset` 内置命令删除函数。在你注销后，shell 不会保留函数。

## 删除同名的变量和函数

- 如果你有一个与函数同名的 shell 变量，使用 `unset` 会移除该变量。如果之后再次对相同名称使用 `unset`，它将移除该函数。

声明 shell 函数的语法为：

```
[function] function-name () {

  commands

}
```

其中 `[function]` 是可选的，`function-name` 是你调用函数时名称，而 `commands` 包含了调用函数时执行的命令列表。这些命令可以是任何你会包含在 shell 脚本中的内容，包括对其他函数的调用。

左括号 `()` 可以出现在与函数名同一行。别名和变量在函数读取时展开，而不是在执行时展开。你可以在函数内部使用 `break` 语句（第 992 页）来终止其执行。

shell 函数既可以作为简写，也可以用于定义特殊命令。以下函数在后台启动一个进程，该进程的输出通常会被保存在 `.process.out` 中。

```
start_process() {

  process > .process.out 2>&1 & 

}
```

下一个示例创建了一个简单的函数，用于显示日期、标题以及系统上登录的用户列表。该函数运行与第 289 页描述的相同的命令。在这个示例中，函数是从键盘输入的。大于符号 (`>`) 是次级 shell 提示符 (PS2)；不要输入它们。

```
$ function name {

  date

  echo "Users Currently Logged On"

}
```

# SHELL Features

你可以通过开启和关闭功能来控制 Bourne Again Shell。不同的功能使用不同的方法来开启和关闭。内置命令控制一组功能，`shopt` 内置命令控制另一组。你也可以从你使用的命令行控制许多功能。

## Features, options, variables?

为了避免术语混淆，本书将你可以控制的各种 shell行为称为功能。bash 信息页将它们称为“选项”和“控制可选 shell 行为的值”。

### set ±0: TURNS SHELL FEATURES ON AND OFF

`set` 内置命令在带有 `-o` 或 `+o` 选项时，启用、禁用并列出某些 bash 功能。例如，以下命令开启了 `noclobber` 功能（第 237 页）：

```
$ set -o noclobber
```

你可以通过给出命令关闭此功能（默认值）：

```
$ set +o noclobber
```

不带选项的 `set -o` 命令会列出由 `set` 控制的每个功能以及其状态（开启或关闭）。不带选项的 `set +o` 命令会列出相同的功能，你可以作为 shell 输入的形式。下一页的表 9-13 列出了 bash 功能。

## 表 9-13 bash 特性

| 特性 | 说明 | 语法 | 备用语法 |
| --- | --- | --- | --- |
| allexport | 自动导出你在执行此命令后创建或修改的所有变量和函数（默认关闭）。 | `set–o allexport` | `set–a` |
| braceexpand | 导致 bash 执行大括号扩展（默认开启；见第 346 页）。 | `set–o braceexpand` | `set–B` |
| cdspell | 纠正作为 `cd` 参数参数的目录名称中的细微拼写错误（默认关闭）。 | `shopt–s cdspell` | |
| cmdhist | 将多行命令的所有行保存到同一个历史条目中，根据需要添加分号（默认开启）。 | `shopt–s cmdhist` | |
| dotglob | 导致 bash 在歧义的文件引用中的 shell 特殊字符（通配符；见第 244 页）匹配文件名开头的点。默认情况下，特殊字符不匹配文件名开头的点。你必须始终显式地指定文件名 `.` 和 `..`，因为没有模式可以匹配它们（默认关闭）。 | `shopt–s dotglob` | |
| emacs | 为命令行编辑指定 emacs 编辑模式（默认开启；见第 329 页）。 | `set–o emacs` | |
| erxit | 当较短的命令（非控制结构）失败时，导致 bash 退出（默认关闭）。 | `set–o erxit` | `set–e` |
| execfail | 当 `exec` 无法找到作为参数传递的文件时，调用脚本以继续运行。当 `exec` 无法找到作为参数的文件时，通过脚本终止执行（默认关闭）。 | `shopt–s execfail` | |
| expand_aliases | 导致别名（见第 334 页）被扩展（交互式 shell 默认开启，非交互式 shell 关闭）。 | `shopt–s expand_aliases` | |
| hashall | 导致 bash 记住使用 `PATH`（见第 308 页）找到的命令所在的位置（默认开启）。 | `set–o hashall` | `set–h` |
| histappend | 当 shell 退出时，导致 bash 将历史列表追加到 `HISTORYFILE`（见第 319 页）命名的文件中（默认关闭 [bash 会覆盖此文件]）。 | `shopt–s histappend` | |
| histexpand | 开启历史机制（默认使用感叹号；见第 323 页）。关闭此特性以关闭历史扩展（默认开启）。 | `set–o histexpand` | `set–H` |
| history | 启用命令历史记录（默认开启；见第 319 页）。 | `set --o history` | |
| huponexit | 指定当交互式登录 shell 退出时，bash 向所有作业发送 `SIGHUP` 信号（默认关闭）。 | `shopt -s huponexit` | |
| ignoreeof | 指定 bash 在进入拨号线路之前必须接收十个 EOF 字符（在嘈杂的拨号线上很有用（默认关闭））。 | `set --o ignoreeof` | |
| monitor | 启用作业控制（默认开启；见第 296 页）。 | `set --o monitor` | `set -m` |
| nocaseglob | 导致歧义的文件引用（见第 244 页）在不区分大小写的情况下匹配文件名（默认关闭）。 | `shopt -s nocaseglob` | |
| noclobber | 有助于防止覆盖文件（默认关闭；见第 237 页）。 | `set --o noclobber` | `set -C` |
| noglob | 禁止路径名扩展（默认关闭；见第 244 页）。 | `set --o noglob` | `set -f` |
| notify | 在启用作业控制（见第 296 页）时，立即报告后台作业的终止状态（默认关闭：bash 在下一个提示符出现前显示状态）。 | `set --o notify` | `set -b` |
| nounset | 在交互式 shell 中对未设置的变量显示错误并退出（默认关闭：bash 为未设置的变量显示空值）。 | `set --o nounset` | `set -u` |
| nullglob | 导致歧义的文件引用在没有匹配项时返回为空。 | `shopt -s nullglob` | |
| posix | 启用 POSIX 兼容模式命令历史。 | `set --o posix` | |
| verbose | 在 bash 执行命令前显示该命令。 | `set --o verbose` | |
| vi | 指定命令行编辑使用 vi 模式（默认开启）。 | `set --o vi` | |
| xpgecho | 当 无法找到作为参数传递的文件时，调用脚本来扩展。 | `shopt -s xpgecho` | |
| xtrace | 启用命令跟踪。 | `set --o xtrace` | |

## 使用 shopt 设置 shell 特性

你可以使用 `shopt` 来设置/取消由 `-o` 控制的特性。使用带 `-s` 或 `-u` 的 `shopt` 语法并包含 `-o` 参数。例如，以下命令开启 `noclobber` 特性：

```bash
shopt -o -s noclobber
```
