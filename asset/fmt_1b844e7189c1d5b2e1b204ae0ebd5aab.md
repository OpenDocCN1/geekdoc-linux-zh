
| --- | --- | --- | --- |

| `ctrl+z` | 停止（挂起）一个前台作业。 | | 166 |

| `ctrl+c` | 终止（中止）一个前台作业。 | | 166 |

| `alias` | 语法：`alias [name=definition]` #Korn and Bash `alias [name definition]` #C shell 列出已存在的别名或为命令创建新别名。 | | 170 |

## 第 5 章 · shell 简介

| 命令 | 描述 | 选项 | 页 |
| --- | --- | --- | --- |
| `bash` | 语法：`bash` 创建一个新的 Bash shell。 | | 144 |
| `bg` | 语法：`bg [job_number]` 将挂起的作业移到后台。 | | 168 |
| `csh` | 语法：`csh` 创建一个新的 C shell。 | | 144 |
| `exit` | 语法：`exit` 将用户从子 shell 移动到父 shell。 | | 146 |
| `fg` | 语法：`fg [job_number]` 将挂起的作业移到前台。 | | 165 |
| `jobs` | 语法：`jobs` 显示活动作业列表。 | | 168 |
| `kill` | 语法：`kill [job_number]` 杀死一个作业。 | | 166 |
| `ksh` | 语法：`ksh` 创建一个新的 Korn shell。 | | 144 |
| `ps` | 语法：`ps` 显示活动进程的信息。 | | 170 |
| `set` | 语法：`set var=value` #C shell `set -o` #Korn and Bash `set +o` #Korn and Bash 为变量设置值或设置选项。当加号选项使用时，在 Korn shell 中还会取消选项。 | | 178 |
| `setenv` | 语法：`setenv var = value` 在 C shell 中，为环境变量设置值。 | | 182 |
| `stop` | 语法：`stop [job_number]` 停止（挂起）一个后台作业。 | | 167 |
| `tee` | 语法：`tee [-option] file-list` 将标准输入复制到标准输出，同时复制到一个或多个文件。 | a | 153 |
| `unalias` | 语法：`unalias alias-list` 某些或所有别名。 | a (Korn and Bash) | 173 |
| `unset` | 语法：`unset variable` `unset option` #C shell 取消变量的值或取消一个选项。 | | 182 |
| `unsetenv` | 语法：`unsetenv variable` 在 C shell 中，取消环境变量的值。 | | 182 |

### 5.19 总结

- UNIX 中有三种传统的 shell：Bourne、Korn 和 C。`Bash` shell 是 Bourne shell 的新版本。`tcsh` 是 C shell 的新版本。
- 当用户登录系统时，这三种 shell 中的一个处于激活状态。这个 shell 被称为登录 shell（`login shell`）。
- 系统管理员通过在 `/etc/passwd` 文件中插入它来确定登录 shell。
- 你可以随时切换到其他 shell，甚至是登录 shell 的另一个副本。
- 你可以随时确定你的登录 shell，但只有不在 Korn 或 Bash 中时，你才能确定当前的 shell。
- 如果你想退出系统，你应该处于登录 shell 中。如果你在其他 shell 中，你应该先回到登录 shell。
- 当你在后台运行命令时，通常你应该将输入、输出和错误重定向到文件。
- 作业号与进程 ID 是不同的。
- 管道是一个运算符，而不是一个命令。它只能用于两个命令之间。
- 管道只能从能够将输出数据发送到标准输出的命令中接收输入。
- 管道只能将其输出发送到能够从标准输入接收输入的命令中。
- 当你使用 `vi` 编辑器进行命令行编辑时，`vi` 总是以文本模式启动的。
- 在 Korn 和 Bash shell 中，可用于命令替换的标记是 `$(...)`。C shell 使用反引号。
- 作业无法从后台移动到前台，反之亦然，除非它已停止。
- 在不同的 shell 中，你需要不同的命令来设置和取消变量（用户定义或预定义）。
- 在不同的 shell 中，你需要不同的命令来设置和取消选项。
- 别名用于为命令赋予新名称；你不能使用别名来重命名文件。
- Korn 和 Bash shell 的 `alias` 和 `unalias` 命令格式与 C shell 不同。
- `Bash` shell 和 C shell 都有退出文件。

# 练习题复习题

- 1. 解释 shell 的两个不同职责。
- 2. 定义登录 shell。
- 3. 如何验证你的登录 shell？
- 4. 如何识别你当前的 shell？
- 5. 登录 shell 总是当前 shell 相同吗？
- 6. 如何创建一个子 shell？创建子 shell 后如何回到父 shell？
- 7. 如果你的登录 shell 是 Korn shell，你可以创建另一个 Korn shell 作为子 shell 吗？解释你的答案。
- 8. 什么是标准流？
