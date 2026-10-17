
### 命令与标志

| `-c, --line-bytes=n` | 指定在每个输出文件中放入不超过 `n` 字节的行。 |
| `-l, --lines=n` | 指定在每个输出文件中放入 `n` 行。 |
| `--verbose` | 指定提供详细输出。 |
| `--help` | 指定显示帮助信息。 |
| `--version` | 指定显示版本信息。 |
| `sort` | 用于按行对文本文件进行排序。 |
| `-c` | 检查文件是否已排序。 |
| `-m` | 将已排序的文件合并在一起。 |
| `-b` | 忽略每行开头的额外空格。 |

## 表 C.1

### 命令与标志（续）

| 命令/标志 | 说明 |
|---|---|
| `-v, --verbose` | 指定始终显示文件名。 |
| `--help` | 显示帮助信息。 |
| `--version` | 显示版本信息。 |
| `talk` | 用于与其他用户交谈。 |
| `tar` | 用于创建 tar 归档文件。 |
| `-A, --concatenate, --concatenate` | 指定将 tar 文件追加到归档中。 |
| `-c, --create` | 创建新归档。 |
| `-d, --diff, --compare` | 识别归档与文件系统之间的差异。 |
| `--delete` | 从归档中删除文件。 |
| `-r, --append` | 将文件追加到归档中。 |
| `-t, --list` | 列出归档的内容。 |
| `-u, --update` | 用较新的文件更新归档。 |
| `-x, --extract, --get` | 从归档中提取文件。 |
| `--atime-preserve` | 指定不更改访问时间。 |
| `-b, --block-size n` | 指定块大小为 `n`*512 字节。 |
| `-C, --directory DIR` | 切换到指定目录。 |
| `--checkpoint` | 处理时显示目录名称。 |
| `-f, --file` | 使用指定的文件或设备。 |
| `--force-local` | 无论文件名如何，强制使用本地归档文件。 |
| `-h, --dereference` | 处理链接文件，而非符号链接。 |
| `-i, --ignore-zeros` | 指定忽略归档中的零（不将其解释为文件结束符）。 |
| `-k, --keep-old-files` | 指定保留旧文件，不进行覆盖。 |
| `-K, --starting-file file` | 从归档中的文件 `file` 开始处理。 |
| `-l, --one-file-system` | 指定保持位于当前文件系统中。 |
| `-m, --modification-time` | 指定不提取文件修改时间。 |
| `-M, --multi-volume` | 指定按多卷归档处理。 |
| `-N, --after-date date, --newer date` | 存储晚于 `date` 的文件。 |
| `-o, --old-archive, --portability` | 指定旧归档格式。 |
| `-O, --to-stdout` | 指定将文件提取到标准输出。 |
| `-p, --same-permissions, --preserve-permissions` | 指定提取所有权限数据。 |
| `-P, --absolute-paths` | 指定保持绝对路径。 |
| `--remove-files` | 指定移除已添加到归档中的文件。 |
| `-s, --same-order, --preserve-order` | 指定与归档匹配的文件名列表。 |
| `--same-owner` | 指定以相同的所有者提取文件。 |
| `-T, --files-from file` | 从文件 `file` 中获取要提取或创建的文件名称。 |
| `--totals` | 显示所创建文件的总字节数。 |
| `-v, --verbose` | 显示已处理文件的详细信息。 |
| `-V, --label name` | 创建卷名为 `name` 的归档。 |

## 表 C.1

### 命令与标志（续）

| 命令/标志 | 说明 |
|---|---|
| `--version` | 显示版本信息。 |
| `-w, --interactive, --confirmation` | 执行操作前需要确认。 |
| `-W, --verify` | 创建归档后验证归档中的信息。 |
| `--exclude file` | 指定从归档中排除文件 `file`。 |
| `-X, --exclude-from file` | 指定从归档中排除文件 `file` 中列出的文件。 |
| `-Z, --compress, --uncompress` | 指定压缩或解压缩归档。 |
| `-z, --gzip, --ungzip` | 指定使用 gzip 处理归档。 |
| `--use-compress-program program` | 指定压缩程序的名称为 `program`。 |
| `tee` | 用于从标准输入读取，并写入标准输出和文件。 |
| `-o, --append` | 追加到指定文件而非覆盖。 |
| `--help` | 打印帮助信息。 |
| `-i, --ignore-interrupts` | 指定忽略中断信号。 |
| `--version` | 打印版本信息。 |
| `telnet` | 用于连接和使用远程计算机。 |
| `-8` | 指定 8 位操作，这不是 telnet 的默认设置。 |
| `-E` | 禁用转义字符。 |
| `-L` | 指定输出时采用 8 位操作。 |
| `-a` | 尝试使用当前用户名自动登录。 |
| `-d` | 启用调试输出。 |
| `-r` | 指定登录仿真。 |
| `-e character` | 指定用于控制命令模式访问的转义字符。 |
| `-l user` | 指定用于远程登录的用户。 |
| `-n tracefile` | 开始将连接跟踪记录到 `tracefile`。 |
| `tidy` | 用于验证、更正和清理 HTML 文件。 |
| `--config file` | 指定从文件 `file` 中设置选项。 |
| `-indent, -i` | 指定对元素内容进行缩进。 |
| `-omit, -o` | 指定省略可选的结束标签。 |
| `-wrap n` | 指定在第 `n` 列换行输出。 |
| `-upper, -u` | 指定以大写形式输出标签。 |
| `-clean, -c` | 指定用 CSS 样式属性替换格式标签。 |
| `-raw` | 指定输出大于 127 的字符值时保持不变。 |
| `-ascii` | 指定输入使用 Latin-1（ISO 8859-1）字符集，输出使用 US ASCII 字符集。 |
| `-latin1` | 指定输入和输出均使用 Latin-1（ISO 8859-1）字符集。 |
| `-iso2022` | 指定输入和输出均使用 ISO 2022 字符集。 |
| `-utf8` | 指定输入和输出均使用 UTF-8 字符集。 |
| `-mac` | 指定输入使用 MacRoman 字符集。 |
| `-numeric, -n` | 指定输出数字实体而非命名实体。 |
| `-modify, -m` | 指定直接修改原始文件。 |
| `-errors, -e` | 指定仅显示错误而不修改原始文件。 |

下页继续

## 表 C.3

### 命令和标志（续）

| 命令/标志 | 描述 |
|---|---|
| `-quiet, -q` | 指定抑制额外输出。 |
| `-f file` | 指定将错误写入文件。 |
| `-xml` | 指定输入为格式良好的 XML。 |
| `-asxml` | 指定将 HTML 转换为格式良好的 XML。 |
| `-slides` | 指定根据 `<H2>` 元素将文件拆分为幻灯片。 |
| `-help, -h` | 指定显示帮助信息。 |
| `-configuration-option value` | 指定将任何可配置选项设置为 `value`。 |
| `time` | 用于对作业进行计时。 |
| `tin` | 用于阅读 Usenet 新闻。 |
| `-c` | 创建或更新所列组的索引，并将所有文章标记为已读。 |
| `-f file` | 指定用于 newsrc 数据的文件。 |
| `-h` | 显示帮助信息。 |
| `-H` | 显示 tin 的介绍。 |
| `-I dir` | 指定保存新闻组索引文件的目录。 |
| `-m dir` | 指定要使用的邮箱目录。 |
| `-M user` | 将未读文章邮寄给 `user`。 |
| `-n` | 指定仅加载活动的、已订阅的组。 |
| `-q` | 指定启动时不检查新的新闻组。 |
| `-P` | 清除所有不存在的文章。耗时，尤其是在慢速连接上。 |
| `-r` | 指定从 nntpserver 远程读取新闻。 |
| `-s dir` | 将文章保存到指定目录。 |
| `-S` | 保存未读文章，以便以后使用 `-R` 选项阅读。 |
| `-u` | 为所有组创建和更新索引文件。 |
| `-U` | 在后台启动 tin 以更新索引文件，同时阅读新闻。 |
