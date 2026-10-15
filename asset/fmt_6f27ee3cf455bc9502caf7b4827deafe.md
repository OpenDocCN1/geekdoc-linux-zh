
```
./configure --prefix=/usr
```

编译软件包：

```
make
```

为了准备测试，请确保用户 `tester` 可以写入源树：

```
chown -R tester
```

现在，以用户 `tester` 的身份运行测试：

```
su tester -c "TERM=xterm-256color LANG=en_US.UTF-8 make -j1 test"
&& vim.log
```

测试套件输出到二进制数据文件。这可能会导致当前终端设置出现问题（特别是当我们覆盖 `TERM` 变量以满足测试套件的某些假设时）。通过如所示将输出重定向到日志文件，测试成功后将在完成后在日志文件中显示 `DONE` 字样。

安装软件包：

```
make install
```

许多用户习惯性地使用 `vi` 而不是 `vim`。为了在用户习惯性输入 `vi` 时允许执行 `vim`，为二进制文件和提供语言的 `man` 页创建符号链接：

```
ln -sv /usr/bin/vim vi
for L in /usr/share/man/*/vim.1; do
  ln -sv vim.1 $(L) /vi.1
done
```

默认情况下，Vim 文档安装在 `/usr/share/doc/vim-9.1.0041`。以下符号链接允许通过 `/usr/share/doc/vim-9.1.0041` 访问文档，使其与其他软件包文档的位置一致：

如果在 LFS 系统上安装了 Windows 系统，则在安装 X 后可能需要重新编译 Vim。Vim 有 GUI 编辑器，需要安装 X 和一些额外的库。有关此过程的更多信息，请参考 Vim 文档以及 BLFS 书中的 Vim 安装页面：https://www.linuxfromscratch.org/blfs/vim/12.1/postfs/vim.html。

## 8.72. 配置 Vim

默认情况下，`vim` 以 `vi` 兼容模式运行。对于过去使用过其他编辑器的用户来说这可能是新的。下面包含了“`ncompatible`”设置，以强调正在使用新行为。它还提醒想要切换到“`compatible`”模式的用户，它应该是配置文件中的第一个设置。这是必要的，因为它更改了其他设置，覆盖项必须在此设置之后。通过运行以下命令创建一个默认 `vim` 配置文件：

```
cat > /etc/vimrc <<"EOF"
  Begin /etc/vimrc

  在自定义设置之前设置默认
  source VIMRUNTIME/defaults.vim
  let skip_defaults=1

  set notcompatible
  set backspace=2
  syntax on
  if ($term == "xterm") || ($term == "putty")
    set background=dark
endif
EOF
```

`notcompatible` 设置让 `vim` 的行为比 `vi` 兼容模式更有用。删除“`no`”保留旧行为。

> 注意

默认情况下，`vim` 只安装英语拼检查文件。要为你的语言安装拼检查文件，将 `runtime/spell` 中的 `.spl` 和可选的 `.s` 文件复制到 `/usr/share/vim/`。

要使用拼检查，需要在 `/etc/vimrc` 中配置，例如：

`set spelllang=en,ru`

更多信息请参见 `runtime/spell/README.txt`。

### 8.72.3. Vim 的内容

- 安装的程序：`ex`（链接到 `vim`），`rview`（链接到 `vim`），`rvim`（链接到 `vim`），`vi`（链接到 `vim`），`view`（链接到 `vim`），`vim`，`vimdiff`（链接到 `vim`），`vimutor` 和 `xxd`
- 安装的目录：`/usr/share/vim`

# Linux From Scratch - 版本 12.1

## 概要说明

- `ex`：以 `ex` 模式启动 `vim`
- `rview`：`view` 的限制版本；可以启动命令但无法退出
- `rvim`：`vim` 的限制版本；可以启动命令但无法退出
- `vi`：链接到 `vim`
- `view`：以只读模式启动 `vim`
- `vim`：编辑器
- `vimdiff`：用 `vim` 编辑两个版本的文件并显示差异
- `vimutor`：教授 `vim` 的基本键和命令
- `xxd`：创建文件的十六进制储；它也可以执行反操作，可以用于二进制补丁

## 8.72. Vim-9.1.0041

Vim 软件包包含一个强大的文本编辑器。

预计编译时间：2.5 SBU

所需的磁盘空间：236 MB

> Vim 的替代方案

如果你更偏于其他编辑器——例如 Emacs、Joe 或 Nano——请参考 https://www.linuxfromscratch.org/blfs/vim/12.1/postfs/editors.html 获取建议的安装说明。

### 8.72.1. 安装 Vim

首先，将 `vimrc` 配置文件的默认位置更改为 `/etc`：

```
echo #define SYS_VIMRC_FILE "/etc/vimrc" >> src/feature.h
```

为编译准备 Vim：

```
./configure --prefix=/usr
```

编译软件包：

```
make
```

为了准备测试，请确保用户 `tester` 可以写入源树：

```
chown -R tester
```

现在，以用户 `tester` 的身份运行测试：

```
su tester -c "TERM=xterm-256color LANG=en_US.UTF-8 make -j1 test"
&& vim.log
```

测试套件输出到二进制数据文件。这可能会当前终端设置出现问题（特别是当我们覆盖 `TERM` 变量以满足测试套件的某些假设时）。通过如所示将输出重定向到日志文件，测试成功后将在完成后在日志文件中显示 `DONE` 字样。

安装软件包：

```
make install
```

许多用户习惯性地使用 `vi` 而不是 `vim`。为了在用户习惯性输入 `vi` 时允许执行 `vim`，为二进制文件和提供语言的 `man` 页创建符号链接：

```
ln -sv /usr/bin/vim vi
for L in /usr/share/man/*/vim.1; do
  ln -sv vim.1 $(L) /vi.1
done
```

默认情况下，Vim 文档安装在 `/usr/share/doc/vim-9.1.0041`。以下符号链接允许通过 `/usr/share/doc/vim-9.1.0041` 访问文档，使其与其他软件包文档的位置一致：

如果在 LFS 系统上安装了 Windows 系统，则在安装 X 后可能需要重新编译 Vim。Vim 有 GUI 编辑器，需要安装 X 和一些额外的库。有关此过程的更多信息，请参考 Vim 文档以及 BLFS 书中的 Vim 安装页面：https://www.linuxfromscratch.org/blfs/vim/12.1/postfs/vim.html。

## 8.72. 配置 Vim

默认情况下，`vim` 以 `vi` 兼容模式运行。对于过去使用过其他编辑器的用户来说这可能是新的。下面包含了“`ncompatible`”设置，以强调正在使用新行为。它还提醒想要切换到“`compatible`”模式的用户，它应该是配置文件中的第一个设置。这是必要的，因为它更改了其他设置，覆盖项必须在此设置之后。通过运行以下命令创建一个默认 `vim` 配置文件：

```
cat > /etc/vimrc <<"EOF"
  Begin /etc/vimrc

  在自定义设置之前设置默认
  source VIMRUNTIME/defaults.vim
  let skip_defaults=1

  set notcompatible
  set backspace=2
  syntax on
  if ($term == "xterm") || ($term == "putty")
    set background=dark
endif
EOF
```

`notcompatible` 设置让 `vim` 的行为比 `vi` 兼容模式更有用（默认）。删除“`no`”保留旧行为。

> 注意

默认情况下，`vim` 只安装英语拼检查文件。要为你的语言安装拼检查文件，将 `runtime/spell` 中的 `.spl` 和可选的 `.sug` 文件复制到 `/usr/share/vim/vim9/`。

要使用拼检查，需要在 `/etc/vimrc` 中配置，例如：

`set spelllang=en,ru`

更多信息请参见 `runtime/spell/README.txt`。

### 8.72.3. Vim 的内容

- 安装的程序：`ex`（链接到 `vim`），`rview`（链接到 `vim`），`rvim`（链接到 `vim`），`vi`（链接到 `vim`），`view`（链接到 `vim`），`vim`，`vimdiff`（链接到 `vim`），`vimutor` 和 `xxd`
- 安装的目录：`/usr/share/vim`
