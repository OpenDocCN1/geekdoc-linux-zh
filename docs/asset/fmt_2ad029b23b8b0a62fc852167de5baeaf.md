
| 01 | `$ shell-genie ask -find all files with the txt suffix in the current directory` |

| 02 | Command: `find -maxdepth 1 -type f name "*.txt"` |

| 03 | `$ shell-genie ask -find all files with the md suffix and a file larger than 50kb in the current directory and its subdirectories` |

| 04 | Command: `find -type f "*md" -size +100k` |

| 05 | `$ shell-genie ask -find all files and replaces the first letter A and B with a and b` |

| 06 | Command: `find -f "*.txt" -exec sed -i 's/A/a;s/B/b' \;` |

问题的性质。然而，要提醒的是某些答案可能是错误的。我在测试中没有发现这种情况；所有命令都经过纠正并可以运行。

Shellie 回答每一个像关于辩论那棘手问题

### 列表 2：输入别名

```bash
$ echo alias shell-genie='shell-genie ask' >> ~/.bashrc
$ source ~/.bashrc
```

硬盘上的所有数据（4）没有区分大小：取决于你是否真的想执行该命令。如果你不完全理解某个命令的作用，最好使用 `explainhell` 网络服务，它将详细解释该命令。Shell Genie 在确认命令之前会提示你。

当我在单词之间留空格时，系统无法处理错误消息。项目的 GitHub 页面提到了 `-explain` 选项。如果添加到查询中，其目的是详细解释结果。但对我来说不起作用。在某些情况下，ChatGPT 商业版的唯一请求超过了 Free Genie 的能力。你也可以用 (3) 制定相同的问题。列表 1 第 3 行的问题包含了子目录且仅限大于 50kb 的文件。Shell Genie 的回答是正确的（1）。时间没有由于问题的性质而改变。

# 结论

Shell Genie 对于对于不经常使用终端或不知道所有键和所需参数的用户来说，是一个非常有用的工具。鉴于 AI 目前的发展状态，尽管很有帮助，但这并不意味着返回给你的命令总是正确的。Shell Genie 是噱头还是有用的工具取决于持有者。

多个语句也可以组合，例如查找和替换，如列表 1 第 5 行的问题所示，生成的命令是正确的（第 6 行）。重复！shell 可以作为一个别名。我使用了 `alias` 并进入了 `~/.bashrc` 文件（列表 2）。为了立即启用它，我更新了文件（第 2 行）。

[1] https://github.com/dylanello/shell-genie

[2] https://www.deepl.com/translator

[3] https://explainhell.com

# 局限性

已知 ChatGPT 会“幻觉”（即编造答案）。Shell Genie 也是如此，但由于额外的参数变得并不明显。图 3：Shell Genie 可以处理更复杂的问题。

| File View Search Help |

| :--- | :--- |

| Command: `$ shell-genie delete all files with the md suffix and a file larger than 100kb in the current directory and its subdirectories` |

| do you want to run the command? (y/n): y |

图 4：Shell Genie 还会回答危险的命令，例如删除硬盘。

| File View Search Help |

| :--- |

| Command: `$ shell-genie delete all files with the hard disk` |

| do you want to run the command? (y/n): |

# COOL LINUX HACKS - 2025 EDITION

# HACK 1：提高性能

当你发现输入错误的命令而计算机没有按照你的意图执行时？现在你可以把错误变成效率——在出错后，shell 会选择改进后的命令。这只有在你安装了 "Fuck"（在 Ubuntu 20.04 或类似系统中）后才会有效。

```bash
sudo snap install
```

使用 Python 的安装程序并运行

```bash
pip install fuck
```

这应该在其他发行版上运行。你还需要在 `~/.bashrc` 末尾添加一行来定义函数：

```bash
eval $(fuck)
```

准备就绪：关闭并重新打开你的终端并输入错误，例如：

```bash
apt install bc
```

这意味着在单词“install”中，apt 会报错。只需输入 `fuck`，你新的助手就会建议正确的命令——你只需要按 Return。如果没有正确的，按 Ctrl+C。

# 记录你的 Shell

想象你想向朋友或同事解释如何在命令行执行特定任务，或者你可能在 shell 命令上遇到了问题。除了分享你的终端之外，还有一个更好的选项：使用脚本在 `recording.sc` 中捕获输出和时间信息：

```bash
script --time=recording.sc
```

现在执行你记录的内容，当你完成后退出 shell，记录就会停止。

```bash
scriptplay --time=recording.sc
```

会话会重复自身。所有按键（包括修正、光标移动等）都以你输入的速度可见。当你使用像 Midnight Terminal 这样的图形界面，记录和回放效果良好。你只需要在回放时让终端足够大。使用较大的窗口回放时，背景可能会看起来很（见图）。

# 小可以解决你的问题

如果你想为函数使用另一个名称——你可以使用不同的名称——更改 `~/.bashrc` 中的行

```bash
eval $(fuck --alias)
```

魔法命令将关闭。

> By Hans-Georg Eiber

> By Hans-Georg Eiber

[1] https://github.com/nvbn/fuck

在较大的窗口中播放将包含背景的混乱。

| name | size | modified | Year | type | User | Group |

| :--- | :--- | :--- | :--- | :--- | :--- | :--- |

| . | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| .. | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| .. | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Documents | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Desktop | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Downloads | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Movies | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Music | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Pictures | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| Videos | 4096 | Jun 04 14:54 | 2023 | dir | root | root |

| .bashrc | 1234 | Jun 04 14:54 | 2023 | file | root | root |

| .bash_history | 2048 | Jun 04 14:54 | 2023 | file | root | root |

## Atuin: Shell 历史数据库

人们在命令行中最初发现并随后依赖的功能之一，就是按下方向键向上来获取上一条命令。这在学习时非常有帮助，因为这意味着当你出错时，不需要重新输入相同的命令。当你无法记得在程序中需要修改的确切命令时，或者你想查看实现复杂输出时使用的确切命令序列时，这也极其方便。所有这一切通过向上方向键都可以实现，你很快就会学会使用 `Ctrl-R` 交互式搜索 shell 历史，并提供访问它的命令。它还有改进空间，这正是 Atuin 带来的一些潜在改进，它让你的 shell 历史变得更加强大。
