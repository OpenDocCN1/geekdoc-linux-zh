
### 版权

版权所有 © 1999 自由软件基金会（Free Software Foundation, Inc.）。这是自由软件；有关复制条件，请参阅源代码。不提供任何担保；甚至不保证适销性或针对特定用途的适用性。

#### SYNC

##### 名称

`sync`—刷新文件系统缓冲区

##### 摘要

```
sync [OPTION]
```

##### 描述

强制将更改的块写入磁盘，更新超级块。

- `--help` — 显示此帮助并退出
- `--version` — 输出版本信息并退出

##### 报告错误

将错误报告发送至 <bug-fileutils@gnu.org>。

##### 另见

`sync` 的完整文档以 Texinfo 手册的形式维护。如果 `info` 和 `sync` 程序已在您的站点上正确安装，则命令

```
info sync
```

应允许您访问完整手册。

#### TAR

##### 名称

`tar`—GNU 版本的 tar 归档实用程序。

##### 摘要

```
tar [ - ] A --catenate --concatenate [ -c --create ] [ -d --diff --compare ]
[ -r --append ] [ -t --list ] [ -u --update ] [ -x --extract --get ] [ --atime-preserve ]
[ -b, --block-size N ] [ -B, --read-full-blocks ] [ -C, --directory DIR ] [ --checkpoint ]
[ -f, --file [HOSTNAME:]F ] [ -F, --info-script F --new-volume-script F ]
[ -G, --incremental ]
[ -g, --listed-incremental F ] [ -h, --dereference ] [ -i, --ignore-zeros ]
[ --ignore-failed-read ] [ -k, --keep-old-files ] [ -K, --starting-file F ]
[ -l, --one-file-system ] [ -L, --tape-length N ] [ -m, --modification-time ]
[ -M, --multi-volume ] [ -N, --after-date DATE, --newer DATE ]
[ -O, --to-stdout ] [ -o, --old-archive, --portability ]
[ -p, --same-permissions, --preserve-permissions ] [ -P, --absolute-paths ] [ --preserve ]
[ -R, --record-number ] [ --remove-files ] [ -s, --same-order, --preserve-order ]
[ --same-owner ] [ -S, --sparse ] [ -T, --files-from F ] [ --null ]
[ --totals ] [ -v, --verbose ] [ -V, --label NAME ] [ --version ]
[ -w, --interactive, --confirmation ] [ -W, --verify ]
[ --exclude FILE ] [ -X, --exclude-from FILE ] [ -Z, --compress, --uncompress ]
[ -z, --gzip, --ungzip ] [ --use-compress-program PROG ] [ --block-compress ]
[ -[0-7][lmh] ] filename1 [ filename2, ... filenameN ] directory1
[ --directory, ...directory ]
```
