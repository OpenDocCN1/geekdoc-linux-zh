
## 重要标志和选项
- `-c`/`-create`: 创建新归包。
- `-delete`: 从现有归包删除文件。
- `-f tarfile`/`-file tarfile`: 指定要创建或读取的归包名称。
- `-preserve`: 保留归包文件的权限和顺序。
- `-r`/`-append`: 将文件添加到现有归包。
- `-same-owner`: 表示提取的文件保留原始所有者。
- `-t`/`-list`: 显示归包内容的列表。
- `-u`/`-update`: 仅将比归包中副本更新的文件添加到现有归包。
- `-x`/`-extract`/`get`: 从现有归包中提取文件。
- `-z`/`gzip`/`-unzip`: 在打包和解包时通过 gzip 过滤归包。

## timeconfig
描述 配置时间参数。如果指定了时区，系统时区将更改为指定的时区。否则显示所有可用时区。

语法
```
timeconfig [-utc] [timezone]
```
- `-utc`: 假设系统时钟以格林威治时间运行。

## timed
描述 如果指定了时区，系统时区将更改为指定的时区。否则显示所有可用时区。

## sync
描述 将磁盘缓存保存到物理磁盘。这强制将任何更改的信息保存到磁盘。

语法
```
sync
```
重要标志和选项：无

## tail
描述 显示一个或多个文件的最后部分。默认情况下，除非另有指定，将显示每个文件的最后 10 行。如果没有提供文件名，则从标准输入读取数据，并按照文件规则显示数据的最后部分。

语法
```
tail [-c number[bkm]] [-n number] [-q] [-bytes number[bkm]] [-lines number] [-quiet] [-silent] [file ...]
```
重要标志和选项
- `-c`/`-lines number`: 显示每个文件末尾的指定行数。可选情况下，数字后可以 b 表示 512 字节块，k 表示兆字节。
- `-n`/`-lines number`: 显示每个文件末尾的指定行数。
- `-q`/`-quiet`/`-silent`: 在处理多个文件时防止打印文件名头。

## tar
描述 创建一个或多个文件或目录的归包。

语法
```
tar [-crtuxxz] [-f tarfile] [-file archive] [-create] [-delete] [-preserve] [-append] [-same-owner] [-list] [-update] [-extract] [-zip] [-gzip] [file ...]
```
重要标志和选项
- `-c`/`-create`: 创建新归包。
- `-delete`: 从现有归包删除文件。
- `-f tarfile`/`-file tarfile`: 指定要创建或读取的归包名称。
- `-preserve`: 保留归包文件的权限和顺序。
- `-r`/`-append`: 将文件添加到现有归包。
- `-same-owner`: 表示提取的文件保留原始所有者。
- `-t`/`-list`: 显示归包内容的列表。
- `-u`/`-update`: 仅将比归包中副本更新的文件添加到现有归包。
- `-x`/`-extract`/`get`: 从现有归包中提取文件。
- `-z`/`gzip`/`-unzip`: 在打包和解包时通过 gzip 过滤归包。

## unzip
描述：处理并提取 ZIP 压缩包。

语法
```
unzip [-cflptu] [-d xdir] file[.zip]
```
### 重要标志和选项
- `-c`: 将文件提取到标准输出，并在提取每个文件时打印文件名。
- `-d xdir`: 将压缩包解压到指定的目录，而不是当前目录。
- `-f`: 仅提取比现有文件版本较新的文件。
- `-l`: 显示压缩包的内容而不进行解压。
- `-p`: 将文件提取到标准输出，而不发送任何其他数据。
- `-t`: 测试压缩包内文件的完整性。
- `-u`: 提取比现有文件版本较新的文件，以及提取目录中已不存在的文件。
- `-z`: 显示压缩包注释。

说明：这是一个支持许多修饰符的程序。详情请参阅 `unzip` 手页。

## uptime
描述：显示系统运行的时间。

语法
```
uptime
```
重要标志和选项：无。

## useradd
描述：向系统添加用户。或者，可以更改新用户的默认值。如果不提供任何选项，程序将显示新用户的默认值。

语法
```
add [-d home_dir] [-e expire_date] [-f inactive_time] [-g initial_group] [-g group,[...]] [-s shell] [-u uid [-o]] username
useradd -D [-g default_group] [-b default_home] [-f default_inactive] [-default_expiration] [-s default_shell]
```
### 重要标志和选项
- `-default_home`: 将默认主目录前缀设置为该路径。仅在使用 `-d` 时使用。
- `-home_dir`: 为用户使用指定的主目录而不是默认主目录。
- `-D`: 表示更改新用户的默认值，而不是创建一个新用户。
- `-e expire_date`: 指定账户的过期日期。数据格式为 MM/DD/YY。当使用 `-D` 时，`-e` 将用于设置所有新密码的默认过期天数，而不是日期格式。
- `-f inactive_time`: 表示一旦密码过期后，应经过指定的时间后才禁用密码。当使用 `-D` 时，`-f` 将设置密码过期后禁用的默认时长。
- `-g initial_group`: 指定用户的登录组。当与 `-D` 使用时，`-g` 将指定所有新用户的默认组。
- `-G group[...]`: 指定用户应该所属的其他组。
- `-s shell`: 指定用户的默认 shell。如果不提供，则将使用新用户的默认 shell。当与 `-D` 使用时，`-s` 将指定所有新用户的默认 shell。
- `-u uid [-o]`: 为用户指定用户 ID `uid`，而不是自动分配。除非使用 `-o` 标志，否则该值必须是唯一的。

## userdel
描述：删除用户账户。

语法
```
userdel [-r] user
```
### 重要标志和选项
- `-r`: 在删除账户时删除用户的主目录。

说明：如果你选择删除用户的主目录，请记住，当删除账户时，该用户拥有的主目录之外的任何文件将不会被删除。这些文件必须手动删除。

## usermod
描述：修改现有用户账户的设置。

语法
```
usermod [-d home_dir [-m] [-e expire_date] [-f inactive_time] -g initial_group] [-G group[...]] [-l login_name] [-s shell] -u uid [-o]] login
```
### 重要标志和选项
- `-d home_dir [-m]`: 按指定更改用户的主目录，如果使用了 `-m` 选项，会将当前的主目录移动到新位置。
- `-e expire_date`: 为账户设置新的过期日期，日期后账户将被禁用。日期格式应为 MM/DD/YY。
- `-f inactive_days`: 为密码过期后永久禁用的天数提供新设置。
- `-g initial_group`: 为用户定义一个新的登录组。
- `-G group[...]`: 指定用户应该属于的其他组。如果用户目前属于不在列表中的组，他们将从该组中移除。
- `-l login_name`: 更改用户的登录名。
- `-s shell`: 按指定更改用户的默认 shell。
- `-u uid`: 按指定更改用户的 ID。

## users
描述：显示系统上当前用户的用户名。这通常通过查看 `/etc/utmp` 的内容找到。如果指定了文件，程序将在该文件中查找信息。

语法
```
users [file]
```
重要标志和选项：无。

## uudecode
描述：解码由 `uudecode` 创建的 ASCII 文件，以重建原始二进制文件。默认情况下，解码后的文件名将是编码文件的原始名称。

语法
```
uudecode [-o output] file
```
### 重要标志和选项
- `-o output`: 指定解码文件的替代名称。

## uuencode
描述：将二进制文件编码为 ASCII 格式。如果没有提供文件，程序将从标准输入。

语法
```
uuencode [-c output] file
```
### 重要标志和选项
- `-c output`: 指定编码文件的替代名称。

## vipw
描述 编辑系统的密码文件。

语法
```
vipw
```
重要标志和选项：无。

## vmstat
报告关于虚拟内存、进程和磁盘的统计。

语法
```
vmstat [delay] count
```
### 重要标志和选项
- `-count`: 指定报告次数。如果没有指定，默认为 1。
- `-delay`: 指定报告之间的间隔。

## wc
统计行数、单词数字节数。

语法
```
wc [-l] [-w] [-c]
```
### 重要标志和选项
- `-l`: 打印行数。
- `-w`: 打印单词数。
- `-c`: 打印字节数。

## whereis
尝试定位一个或多个命令的二进制文件、源代码和帮助页。

语法
```
whereis [-b] [-m] [-s] command
```
### 重要标志和选项
- `-b`: 仅查找二进制文件。
- `-m`: 仅查找帮助页。
- `-s`: 仅查找源代码。

`whereis` 命令至少会在以下目录查找它要定位的程序：
`/bin`
`/usr/bin`
`/etc`
`/usr/etc`
`/sbin`
`/usr/sbin`
`/usr/games`
`/usr/games/bin`
`/usr/emacs/etc`
`/usr/lib/emacs/19.22/etc`
`/usr/lib/emacs/19.23/etc`
`/usr/lib/emacs/19.24/etc`
`/usr/lib/emacs/19.25/etc`
`/usr/lib/emacs/19.26/etc`
`/usr/lib/emacs/19.27/etc`
`/usr/lib/emacs/19.28/etc`
`/usr/lib/emacs/19.29/etc`
`/usr/lib/emacs/19.30/etc`
`/usr/TeX/bin`
`/usr/tex/bin`
`/usr/interviews/bin/LINUX`
`/usr/bin/X11`
`/usr/X11/bin`
`/usr/X11R5/bin`
`/usr/X11R6/bin`
`/usr/X386/bin`
`/usr/local/bin`
`/usr/local/etc`
`/usr/local/sbin`
`/usr/local/games`
`/usr/local/games/bin`
`/usr/local/emacs/etc`
`/usr/local/TeX/bin`
`/usr/local/tex/bin`
`/usr/local/bin/X11`
`/usr/contrib`
`/usr/hosts`
`/usr/include`
`/usr/g++-include`

## which
描述：显示一个或多个程序的完整路径。只有在 `PATH` 环境变量指定的路径上的程序会被显示。

语法
```
which program ...
```
重要标志和选项：无

## whoami
描述：显示当前的有效用户 ID。

语法
```
whoami
```
重要标志和选项：无

## ypdomainname
描述：显示系统的 NIS 域。

语法
```
ypdomainname
```
重要标志和选项：无

## zcat
描述：解压一个或多个压缩文件并将结果输出到标准输出。如果未指定文件，则对标准输入进行解压并显示。

语法
```
zcat [-f] [file ...]
```
- `-f`/`-force` 强制解压，即使已存在相应的文件且该文件将被解压后的文件覆盖。

## zgrep
描述：在一个或多个压缩文件中搜索指定的模式。

语法
```
zgrep [options] pattern file ...
```
重要标志和选项：无

## zip
描述：从一个或多个文件和目录创建一个 ZIP 归档。

语法
```
zip [-EffGmSu@] [zipfile [file1 file2 ...]]
```
- `-@`：从标准输入接受要归档的文件列表。
- `-e`：在提示密码后对归档进行加密。从归档中提取文件时需要该密码。
- `-f`：仅当文件比归档中当前的文件新时，才替换归档中的条目。
- `-F`：尝试修复损坏的归档。
- `-g`：将文件添加到现有归档中。
- `-m`：将文件移动到归档中，一旦归档就会从原始位置删除。
- `-r`：递归处理目录，将子目录中的所有文件添加到归档。
- `-S`：在归档中包含系统和隐藏文件。
- `-u`：如果文件比归档中当前的文件新，或者文件在归档中不存在，则替换归档中的条目。

注意：`zip` 命令提供了许多其他选项，它们对程序的行为有细微但有时有用的影响。更多详情请参阅 `zip` 手页。

## zipgrep
描述：使用 `egrep` 在 ZIP 归档的一个或多个文件中搜索模式。如果未指定归档中的文件，则搜索归档中的所有文件。

语法
```
zipgrep [egrepoptions] pattern zipfile ...
```
注意：关于 `egrep` 和 `zipgrep` 模式语法的完整讨论，请参阅 `egrep` 命令。

## zipinfo
描述 显示 ZIP 归档的详细信息，包括加密状态、压缩类型、创建归档使用的操作系统等。默认情况下，归档中每个文件的信息也会分行列出。如果未指定 ZIP 文件，将处理标准输入。

语法
```
zipinfo [-12M] zipfile[.zip] [file ...]
```
重要标志和选项
- `-1`：仅列出文件名，每个行一个。
- `-2`：列出文件名，包括头文件、尾部和注释。
- `-l`：以长格式列出信息。
- `-M`：以类似于 `more` 的方式一次页显示一次信息。

## zmore
描述：逐屏显示压缩文本文件的内容，允许以与 `more` 命令非常相似的方式进行搜索。如果未指定文件，则使用标准输入。

语法
```
zmore [file ...]
```
