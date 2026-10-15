
## Legacy字符集（LegacyCharset）

对于许多键盘布局，`Kbd` 软件包中没有内置的 `Unicode` 键位。如果此变量设置为可用的非 `UTF-8` 键位的编码，控制台显示器（console deict）将即时将可用的键位转换为 `UTF-8`。

一些示例：

- 对于非 `Unicode` 的设置，通常只需要 `KEYMAP` 和 `FONT` 变量。例如，对于波兰语设置，可以使用：

```
cat /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="pl12"
FONT="lat2a-16 -m 8859-2"

# End /etc/sysconfig/console
EOF
```

- 如上所述，有时需要对内置的键位进行微调。以下示例为德语键位添加了欧元符号：

```
cat > /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
FONT="lat0-16 -m 8859-15"

# End /etc/sysconfig/console
EOF
```

- 以下是一个针对保加利亚语的 `Unicode` 示例，该语言存在内置的 `UTF-8` 键位：

```
cat > /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

UNICODE="1"
KEYMAP="bg_bds-utf8"
FONT="LatArCyrHeb-16"

# End /etc/sysconfig/console
EOF
```

由于上一个示例使用了 512 个字形的 `LatArCyrHeb-16` 字体，除非使用缓冲区（framebuffer），否则 `Linux` 控制台将无法使用亮色。如果希望在不使用缓冲区的情况下使用亮色，且不属于该语言的字符，仍然可以使用特定语言的 256 字字体，如下所示：

```
cat > /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

UNICODE="1"
KEYMAP="bg_bds-utf8"
FONT="cyr-sun16"

# End /etc/sysconfig/console
EOF
```

以下示例说明了键位从 `ISO-8859-15` 到 `UTF-8` 的自动转换以及启用 `Unicode` 模式下的死键（dead keys）：

```
cat > /etc/sysconfig/console << "EOF"
# Begin /etc/sysconfig/console

UNICODE="1"
KEYMAP="de-latin1"
KEYMAP_CORRECTIONS="euro2"
LEGACY_CHARSET="iso-8859-15"
FONT="LatArCyrHeb-16 -m 8859-15"

# End /etc/sysconfig/console
EOF
```

某些键位具有死键（即本身不产生字符，但会在下一个按键产生的字符上添加重音）或定义了组合规则（例如：默认键位中的“按下 `Ctrl` 以获得 `Æ`”）。`Linux-4.15.3` 仅在源字符组合在一起时时才会解释键位中的死键和组合规则，而不是多字节字符。这种多样性不会影响欧洲语言的键位，因为在这些语言中，重音是添加到未分配的 `ASCII` 字符或两个 `ASCII` 字符组合之上的。例如，对于希腊语，有时需要在字母“alpha”上添加重音。解决方案是避免使用 `UTF-8`，或者安装在输入处理方面具有此类局限性的 `Windows` 系统。

对于中文、日语、韩语及某些其他语言，`Linux` 控制台无法配置为显示所需的字符。需要这些语言的用户应该包含涵盖必要字符范围的 `X` 系统字体，以及正确的输入法（例如 `SCIM`），它支持多种语言。

> 注意

`/etc/sysconfig/console` 文件仅控制 `Linux` 文本控制台本地化。它与 `Windows` 系统、`SSH` 会话或串行控制台的键盘布局和字体无关。在这些情况下，上述两项限制不适用。

## 7.6.6 启动时创建文件

有时需要在启动时创建文件。例如，可能需要 `/tmp/.ICE-unix` 目录。这可以通过在 `/etc/sysconfig/createfiles` 中创建一个条目来实现。该文件的格式嵌入默认配置文件。

## 7.6.7 配置 syslog 脚本

`syslog` 脚本作为 `System V` 初始化的一部分调用 `syslog` 程序。`-m` 选项禁用了 `syslog` 每 20 分钟写入日志文件的定期时间戳。如果你想开启定期时间戳，请编辑 `/etc/sysconfig/rc.site` 并定义 `SYSLOG_PARMS` 为所需的值。例如，要删除所有参数，将变量设为空：

```
SYSLOG_PARMS=
```

更多选项请参阅 `syslog`。

### 7.6.8 rc.site 文件

可选的 `/etc/sysconfig/rc.site` 包含为每个 `SystemV` 启动脚本自动设置的内容。它也可以设置 `/etc/config/` 中的主机、控制台和时钟文件。如果变量在独立文件和 `rc.site` 中同时存在，则脚本特定的值具有优先级。

`rc.site` 还包含可以自定义启动过程其他方面的参数。设置 `PROMPT` 变量将启用选择性运行启动脚本。其他选项见文件内容。文件的默认版本如下：

```
# rc.site
# 启动脚本的可选参数。

# 发行版信息
# 如果在此指定，将覆盖默认值
#DISTRO="Linux From Scratch" # 发行版名称
#DISTRO_CONTACT="lfs-dev@linuxfromscratch.org" # 错误报告地址
#DISTRO_MINI="LFS" # 用于发行版配置文件名的短名称

# 定义打印到控制台的消息中使用的自定义颜色

# 请咨询 `console_codes` 以了解更多信息
# 在“ECMA-48 Set Graphics Rendering”章节下
#n# 警告：从 8 位字体切换到 9 位字体时，
# 控制台将重新解释加粗 (l)；直到
# 顶部
```

`Linux From Scratch` - 版本 `8.2`

- 正常情况下，`/tmp` 目录下的所有文件会在启动时被删除。根据存在的文件或目录数量，这可能会导致启动过程明显延迟。要跳过这些文件，请设置变量 `SKIPMTCLEANUP`。
- 在关机期间，`init` 进程会向其启动的每个程序（例如 `getty`）发送 `TERM` 信号，等待设定的时间（3 秒），然后向所有进程分别发送一个 `KILL` 信号。此过程在 `signalsend` 脚本中重复，适用于任何未被所有者关闭的进程。可以通过传递参数来设置 `init` 的延迟。例如，要移除 `init` 的延迟，请在关机或重启时设置 `-t0`（例如 `/bin/shutdown -t0 -r now`）。通过设置参数 `KILLDELAY=0` 可以跳过 `signalsend` 脚本的延迟。

## 7.7. Bash 启动文件

Shell 程序 `/bin/bash`（称为“the shell”）使用一组设置文件来创建一个运行环境。每个文件都有自己的用途，并可能影响登录和交互式环境。与之不同，`/etc` 目录下的文件提供全局设置。如果家目录中存在相应的文件，它可能会覆盖全局设置。

交互式登录 shell 在成功登录后通过 `/bin/login` 启动，并会读取 `/etc/passwd` 文件。交互式非登录 shell 在命令行启动（例如 `[prompt]#/bin/bash`）。当脚本正在运行时，通常会存在一个非交互式 shell。它是非交互的，因为它正在处理脚本，而不是在命令下等待用户输入。

更多信息，请参阅 `Bash` 启动文件（Bash Startup Files）和交互部分（Interactive Sections）下的 `info bash`。

当 shell 作为交互式登录 shell 被调用时，会读取 `/etc/profile` 和 `~/.bash_profile`。下方的基础 `/etc/profile` 设置了一些原生语言支持所需的的环境变量。设置这些变量会导致：

- 程序的输出被翻译为本地语言
- 字符被正确归类为字母、数字和其他类别。这对于 `bash` 在非英语语言区域中接受命令行中的非 `ASCII` 字符是必要的
- 国家的正确字母顺序
- 适当的纸张大小
- 货币、时间和日期的正确格式化

将 `<LL>` 替换为所需语言的两个字母代码（例如 "en"）以及相应国家的两个字母代码（例如 "GB"）。`<charm>` 应被替换为所选语言区域的标准字符集。可能还存在可选的修饰，如 `@euro`。

通过运行以下命令可以获取 `Glibc` 支持的所有语言区域（locales）列表：

```
locale -a
```
