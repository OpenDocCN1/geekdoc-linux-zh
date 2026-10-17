
##### 描述

本手册页介绍了 GNU 版本的 `tar`，这是一个归档程序，用于将文件存储到称为 `tarfile` 的归档文件中，或从中提取文件。`tarfile` 可以制作在磁带驱动器上；然而，将 `tarfile` 写入普通文件也很常见。`tar` 的第一个参数必须是以下选项之一：`Acdrtux`，后跟任何可选功能。`tar` 的最后参数是要归档的文件或目录的名称。使用目录名总是意味着其下的子目录也应包含在归档中。

##### 功能字母

- `-A, --catenate, --concatenate` — 将 `tar` 文件附加到归档中
- `-c, --create` — 创建新的归档
- `-d, --diff, --compare` — 查找归档与文件系统之间的差异
- `--delete` — 从归档中删除（不适用于磁带！）
- `-r, --append` — 将文件追加到归档末尾
- `-t, --list` — 列出归档的内容
- `-u, --update` — 仅追加比归档中副本更新的文件
- `-x, --extract, --get` — 从归档中提取文件

##### 其他选项

- `--atime-preserve` — 不更改已转储文件的访问时间
- `-b, --block-size N` — 块大小为 `Nx512` 字节（默认 `N=20`）
- `-B, --read-full-blocks` — 读取时重新分块（用于读取 4.2BSD 管道）
- `-C, --directory DIR` — 切换到目录 `DIR`
- `--checkpoint` — 读取归档时打印目录名称
- `-f, --file [HOSTNAME:]FILE` — 使用归档文件或设备 `F`（默认为 `/dev/rmt0`）
- `--force-local` — 即使归档文件包含冒号，也将其视为本地文件
- `-F, --info-script F --new-volume-script F` — 每盘磁带结束时运行脚本（隐含 `-M`）
- `-G, --incremental` — 创建/列出/提取旧版 GNU 格式增量备份
- `-g, --listed-incremental F` — 创建/列出/提取新版 GNU 格式增量备份
- `-h, --dereference` — 不转储符号链接；转储它们指向的文件
- `-i, --ignore-zeros` — 忽略归档中的零块（通常表示 EOF）
- `--ignore-failed-read` — 遇到不可读文件时不要以非零状态退出
- `-k, --keep-old-files` — 保留现有文件；不要用归档中的文件覆盖它们
- `-K, --starting-file F` — 从归档中的文件 `F` 开始
- `-l, --one-file-system` — 创建归档时停留在本地文件系统中
- `-L, --tape-length N` — 写入 `N*1024` 字节后更换磁带
- `-m, --modification-time` — 不提取文件的修改时间
- `-M, --multi-volume` — 创建/列出/提取多卷归档
- `-N, --after-date DATE, --newer DATE` — 仅存储比 `DATE` 更新的文件
- `-o, --old-archive, --portability` — 写入 V7 格式归档，而非 ANSI 格式
- `-O, --to-stdout` — 将文件提取到标准输出
- `-p, --same-permissions, --preserve-permissions` — 提取所有保护信息
- `-P, --absolute-paths` — 不从文件名中去除开头的 `/`

- `--preserve` — 相当于 `-p -s`
- `-R, --record-number` — 在每条消息中显示归档中的记录编号
- `--remove-files` — 将文件添加到归档后删除它们
- `-s, --same-order, --preserve-order` — 要提取的名称列表经过排序以匹配归档
- `--same-owner` — 创建具有相同所有权的提取文件
- `-S, --sparse` — 高效处理稀疏文件
- `-T, --files-from F` — 从文件 `F` 中获取要提取或创建的名称
- `--null` — 处理以空字符结尾的名称，禁用 `-C`
- `--totals` — 使用 `--create` 时打印写入的总字节数
- `-v, --verbose` — 详细列出已处理的文件
- `-V, --label NAME` — 创建卷名为 `NAME` 的归档
- `--version` — 打印 `tar` 程序的版本号
- `-w, --interactive, --confirmation` — 对每个操作都请求确认
- `-W, --verify` — 写入后尝试验证归档
- `--exclude FILE` — 排除文件 `FILE`
- `-X, --exclude-from FILE` — 排除 `FILE` 中列出的文件
- `-Z, --compress, --uncompress` — 通过 `compress` 过滤归档
- `-z, --gzip, --ungzip` — 通过 `gzip` 过滤归档
- `--use-compress-program PROG` — 通过 `PROG` 过滤归档（`PROG` 必须接受 `-d`）
- `--block-compress` — 将压缩程序的输出分块以用于磁带
- `[0-7][lmh]` — 指定驱动器和密度

#### TOUCH

##### 名称

`touch` — 更改文件时间戳。

##### 摘要

```
touch [OPTION]... FILE...
```

##### 描述

或 `../src/touch [-acm] MMDDhhmm[YY] FILE...`（过时）— 将每个 `FILE` 的访问时间和修改时间更新为当前时间

- `-a` — 仅更改访问时间
- `-c` — 不创建任何文件
- `-d, --date=STRING` — 解析 `STRING` 并用它代替当前时间
- `-f` — （忽略）
- `-m` — 仅更改修改时间
- `-r, --reference=FILE` — 使用此文件的时间戳代替当前时间
- `-t STAMP` — 使用 `[[CC]YY]MMDDhhmm[.ss]` 代替当前时间
- `--time=WORD` — 访问 `-a`，atime `-a`，mtime `-m`，modify `-m`，使用 `-a`
- `--help` — 显示此帮助信息并退出
- `--version` — 输出版本信息并退出

如果未使用 `-drt` 中的任何一个选项，也未使用 `-`，则可以不使用 `-t` 而直接使用 `STAMP`。请注意，`-d` 和 `-t` 选项以及过时参数所识别的三种时间日期格式各不相同。

##### 报告错误

将错误报告发送至 `<bug-fileutils@gnu.org>`。

##### 另请参阅

`touch` 的完整文档以 Texinfo 手册的形式维护。如果 `info` 和 `touch` 程序已在你的系统中正确安装，那么命令

```
info touch
```

应该可以让你访问完整手册。

#### UMOUNT

##### 名称

`umount` — 卸载文件系统。

##### 摘要

```
umount [-hV]

umount -a [-nrv] [-t vfstype]

umount [-nrv] device | dir ...
```
