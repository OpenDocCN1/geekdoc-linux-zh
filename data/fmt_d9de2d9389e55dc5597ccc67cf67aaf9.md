
```
$ echo ${FRUITBASKET[1]}
orange
$ FRUITBASKET[1]=kiwi
```

The last command results in an error message similar to the following:

上条命令会导致类似以下的错误信息：

```
sh: FRUITBASKET[1]: is read only
```

This example used the bash style array assignment; if you are using ksh you will need to change the first command to the following:

本示例使用了 bash 风格的数组赋值；如果您使用的是 ksh，则需要将第一个命令更改为以下内容：

```
$ set -A FRUITBASKET apple orange pear
```

### Unsetting Variables
### 取消设置变量

`Unsetting` a variable tells the shell to remove the variable from the list of variables that it tracks. This is like asking the shell to forget a piece of information because it is no longer required.

*取消设置*变量会告诉 shell 从其跟踪的变量列表中移除该变量。这就像要求 shell 忘记某条信息，因为它不再需要。

Both scalar and array variables can be unset using the `unset` command:

标量变量和数组变量都可以使用 `unset` 命令取消设置：

```
unset name
```

Here `name` is the name of the variable to unset. For example, the following command unsets the variable `FRUIT`:

这里 `名称` 是要取消设置的变量的名称。例如，以下命令取消设置变量 `FRUIT`：

```
unset FRUIT
```

The `unset` command cannot be used to unset variables that have been marked read-only via `readonly`. There is no way to unset a read-only variable; it persists until the shell exits.

`取消设置` 命令无法用于取消设置通过 `readonly` 标记为只读的变量。无法取消设置只读变量；它会一直存在直到 shell 退出。

### Environment and Shell Variables
### 环境变量和 Shell 变量

When the shell starts a program, it passes that program a set of variables called the `environment`. The environment is usually a small subset of the variables defined in the shell. Each variable in the environment is called an `environment variable`.

当 shell 启动程序时，它会向该程序传递一组称为 `环境` 的变量。环境通常是 shell 中定义变量的一个小子集。环境中的每个变量称为 `环境变量`。

The variables we have examined thus far have been local variables. `Local variables` are variables whose value is restricted to a single shell. Local variables are not passed to programs started by the shell.

迄今为止我们检查过的变量都是局部变量。`局部变量` 是其值仅限于单个 shell 的变量。局部变量不会传递给由 shell 启动的程序。

In addition to local and environment variables, there is a third category of variables called `shell variables`. These are special variables set by the shell that are required for proper operation of the shell. Some shell variables are environment variables, whereas others are local variables.

除了局部变量和环境变量之外，还有第三类变量称为 `shell 变量`。这些是由 shell 设置的特殊变量，用于 shell 的正常运行。某些 shell 变量是环境变量，而其他则是局部变量。

Table 8.1 compares these three categories of variables.

表 8.1 比较了这三类变量。

TABLE 8.1 A Comparison of Local, Environment, and Shell Variables

表 8.1 局部变量、环境变量和 Shell 变量的比较

| Attribute | Local | Environment | Shell |
|---|---|---|---|
| Accessible by child processes | No | Yes | Yes |
| 可被子进程访问 | 否 | 是 | 是 |
| Set by users | Yes | Yes | No |
| 由用户设置 | 是 | 是 | 否 |
| Set by the shell | No | No | Yes |
| 由 shell 设置 | 否 | 否 | 是 |
| User modifiable | Yes | Yes | No |
| 用户可修改 | 是 | 是 | 否 |
| Required by the shell | No | No | Yes |
| 由 shell 要求 | 否 | 否 | 是 |

### Exporting Environment Variables
### 导出环境变量

Environment variables are just local variables that have been placed into the environment via the `export` command:

环境变量只是通过 `export` 命令放置到环境中的局部变量：

```
export name
```

The variable specified by `name` is placed in the environment. The process of placing variables into the environment is often referred to as exporting the variable. The standard shell idiom for exporting variables is

由 `name` 指定的变量被放置到环境中。将变量放置到环境中的过程通常称为导出变量。导出变量的标准 shell 惯用语是

```
name=value ; export name
```

An example of this is

例如

```
PATH=/sbin:/bin ; export PATH
```

Here a value is assigned to `PATH`, and then `PATH` is exported. Often, the assignment statement of an environment variable and the corresponding `export` statement are written on one line to clarify that the variable is an environment variable. This helps the next programmer, who has to maintain the script, quickly grasp the use of certain variables.

这里为 `PATH` 分配一个值，然后导出 `PATH`。通常，环境变量的赋值语句和相应的 `export` 语句写在一行上，以明确该变量是环境变量。这有助于维护脚本的下一个程序员快速掌握某些变量的使用。
