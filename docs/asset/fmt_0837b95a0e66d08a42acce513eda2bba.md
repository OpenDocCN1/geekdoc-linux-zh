
提供此功能的 Shell 允许你为较长的命令创建缩写快捷方式或*别名*。在某些情况下，这创建了更安全的环境，特别是如果你是 Linux 初学者。例如，许多发行版都没有提供 Linux *delete* 命令（已知为 `rm`）的别名。该命令会快速且静默地删除文件，没有提示或反馈，如果误用可能会毁灭你的整个主目录。然而，`rm` 命令的 `-i` 命令行选项会在删除文件前提示你按 `y` 或 `n`。因此，良好的系统管理员会将 `rm` 命令重新定义为 `‘rm -i’`，这样更安全！（如果你在 Mac 上运行 Linux，**你**就是系统管理员！）为此，请编辑系统的 `/etc/profile`（或 `/etc/profile.local` 或 `/etc/skel/.bashrc`）并添加：`alias rm='rm -i'`。

你会发现，大多数流行的 Linux Shell 都支持这些功能以及其他更多功能。大多数 Shell 都非常强大、极其稳定，并且经过长时间严格测试。毫无疑问，Shell 是 Linux 包含的最重要的程序类型之一，并为使用控制台完成工作提供了基本平台。以下章节包括适用于 Linux 的最常见的 Shell。

## bash

`bash` Shell 是几乎每个已安装 Linux 系统的默认 Linux Shell。虽然比其他后续提到的 Shell 稍大且内存占用更多，但 *bash* 拥有超越其他 Shell 的广泛功能列表。`bash` Shell 是最常用于 Linux Shell 脚本的 Shell，因为它能够完美模仿 Bourne 或 `sh` Shell，这是商业和免费 UNIX 操作系统的基本 Shell。`bash` Shell 还可以模仿其他 Shell，具体取决于其启动方式（例如通过符号链接）。

`bash` 拥有广泛的内置帮助，你可以通过其 `help` 关键字命令访问：

```
$ help
```

按 Enter 后，你将看到 `bash` 内置命令的长列表：

```
GNU bash, version 2.04.0(1)-release (powerpc-suse-linux)
These shell commands are defined internally.  Type 'help' to see this list.
Type 'help name' to find out more about the function 'name'.

Use 'info bash' to find out more about the shell in general.

A star (*) next to a name means that the command is disabled.

| Column 1 | Column 2 |
|---|---|
| $([DIGITS \| WORD] [a]) | . filename |
| : | [ arg... ] |
| alias [-p] [name=[value] ...] | bg [job_spec] |
| bind [-lvpvsVPS] [-m keymap] [-f f] break [n] |  |
| builtin [shell-builtin [arg ...]] | case WORD in PATTERN [ \| PATTERN]... |
| cd [-PL] [dir] | command [-pvV] _command [arg ...] |
| compgen [-abcdefkKuv] [-A action] | complete [-abcdefkKuv] [-pr] [-A a |
| continue [n] | declare [-afFrxI] [-p] name=[value |
| dirs [-clpv] [+N] [-N] | disown [-h] [-ar] [jobspec ...] |
| echo [-nEe] [arg ...] | enable [-pnds] [-a] [-f filename] |
| eval [arg ...] | exec [-cl] [-a name] file [redirec |
| exit [n] | export [-nf] [name ...] or export |
| false | fc [-e] [name] [-nlr] [first] [last |
| fg [job_spec] | for NAME in WORDS ... ; do COMMANDS ; } |
| function NAME { COMMANDS ; } or NA | gets optsring name [arg] |
| hash [-r] [-p pathname] [name ...] | help [-s] [pattern ...] |
| history [-c] [-d offset] [n] | or if COMMANDS; then COMMANDS; [ elif |
| jobs [-lnprs] [jobspec ...] or JOB | kill [-s] [sigspec] [-n signum] [-si |
| let arg [arg ...] | local name=[value] ... |
| logout | popd [+N] [-N] [-n] |
| printf format [arguments] | pushd [dir] [+N] [-N] [-n] |
| pwd [-LP] | read [-ers] [-t timeout] [-p prompt |
| readonly [-anf] [name ...] or read | return [n] |
| select NAME [in WORDS ... ;] do CO | set [--abefghkmnptuvxBCHP] [-o opti |
| shift [n] | shopt [-pqsu] [-o long-option] opt |
| source filename | suspend [-f] |
| test [expr] | time [-p] PIPELINE |
| times | trap [arg] [signal_spec ...] or tr |
| true | type [-atp] name [name ...] |
| typeset [-afFrxI] [-p] name=[value | ulimit [-HsaclmnpStuv] [limit] |
| umask [-p] [-S] [mode] | unalias [-a] name |
| unset [-f] [-v] [name ...] | until COMMANDS ; do COMMANDS ; done |
| variables – Some variable names an | wait [n] |
| while COMMANDS ; do COMMANDS ; done | { COMMANDS ; } |
```

然后，你可以通过再次使用 `help` 运算符和命令名称来获取特定内置命令的帮助：

```
$ help time
time: time [-p] PIPELINE

Execute PIPELINE and print a summary of the real time, user CPU time, and system CPU time spent executing PIPELINE when it terminates.

The return status is the return status of PIPELINE. The ‘-p’ option prints the timing summary in a slightly different format. This uses the value of the TIMEFORMAT variable as the output format.

times: times

Print the accumulated user and system times for processes run from the shell.
```

*bash* 的另一个*特性*是扩展，特别是命令补全。例如，如果你输入命令名称的前几个字母，然后按两次 Tab 键，*bash* 会提供一个匹配这些字母的命令列表，如下所示：

```
$ xp
xp-mapedit xpcd xpirot xplot xpot
xp-replay xpfx xpilots xpix xprompt
xpaint xpet xpinguin xpmtree xprop
xpanex xphoon xpipeman xpshow xpuzzle
xpat2 xpicted xplg xpmtoppm xpyraminx
```

几乎所有 `shell` 都使用重要的配置文件，也称为*资源*文件，`bash` 也不例外。在每个用户的主目录中，你至少会发现两个（也许还有第三个）文件：
