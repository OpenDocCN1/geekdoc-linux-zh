
# 附录 L. 历史命令

> 原文：[`tldp.org/LDP/abs/html/histcommands.html`](https://tldp.org/LDP/abs/html/histcommands.html)

Bash shell 提供了用于编辑和操作用户“命令历史”的命令行工具。这主要是为了方便，是一种节省按键的方法。

## Bash 历史命令

1. `history`
2. `fc`

```sh
bash$ history
 1  mount /mnt/cdrom
 2  cd /mnt/cdrom
 3  ls
     ...
```

## 与 Bash 历史命令关联的内部变量

1. `$HISTCMD`
2. `$HISTCONTROL`
3. `$HISTIGNORE`
4. `$HISTFILE`
5. `$HISTFILESIZE`
6. `$HISTSIZE`
7. `$HISTTIMEFORMAT`（Bash，版本 3.0 或更高）
8. `!!`
9. `!$`
10. `!#`
11. `!N`
12. `!-N`
13. `!STRING`
14. `!?STRING?`
15. `^STRING^string^`

不幸的是，Bash 历史工具在脚本编写中找不到用途。

```sh
#!/bin/bash
# history.sh
# A (vain) attempt to use the 'history' command in a script.

history                      # No output.

var=$(history); echo "$var"  # $var is empty.

#  History commands are, by default, disabled within a script.
#  However, as dhw points out,
#+ set -o history
#+ enables the history mechanism.

set -o history
var=$(history); echo "$var"   # 1  var=$(history)
```

```sh
bash$ ./history.sh
(no output)
```

[在 Bash Shell 中进步](http://samrowe.com/wordpress/advancing-in-the-bash-shell/)网站提供了关于在 Bash 中使用历史命令的良好介绍。
