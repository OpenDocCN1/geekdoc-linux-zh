
### 5. 与 `awk` 命令配合使用的 `-f` 选项指定______________________。

a. 字段分隔符的格式

b. 输入数据文件具有固定长度记录

c. 输入数据文件具有变长度记录

d. 命令来自磁盘文件而非键盘

### 6. 在指定 `join` 命令时，`-o` 参数用于______________________。

a. 指定输出到屏幕

b. 指定报告中标题行的数量

c. 运行额外的命令

d. 指定报告中输出的字段

### 7. ______________________ 是一个用于 `awk` 命令中打印格式化的 C 语言函数。

a. `-p`

b. `{ format }`

c. `printf`

d. `proccprint`

### 8. ______________________ 文件通常包含与串口设备或打印机通信所需的信息。

a. 供应商文件

b. 字符特殊文件

c. 块特殊文件

d. 主打印机文件

### 9. `Stdout`（标准输出）通常流向____________________。

a. 键盘

b. 调制器

c. 控制台

d. 网络连接

### 10. 正或错：在 `join` 命令中，`-j` 用于显示字段时反转字段。

### 11. 你可以使用 `touch` 命令来：

a. 创建新文件

b. 修改文件的日期和时间戳

c. 将排序后的数据合并到新文件

d. 以上所有

e. 仅 a 和 b

### 12. 命令 "`cat accounts persons > info`" 用于：

a. 排序 `accounts` 文件并将其与 `info` 文件合并，创建一个名为 `persons` 的新文件

b. 排序 `accounts` 和 `persons` 文件并打印到名为 `info` 的打印机

c. 用 `persons` 文件中的数值数据替换 `accounts` 文件中的数值数据，并将结果写入 `info` 文件

d. 将 `accounts` 和 `persons` 文件的内容合并到 `info` 文件

### 13. `2>` 运算符重定向：

a. 标准输出 (`stdout`)

b. 标准错误 (`stderr`)

c. 标准输入 (`stdin`)

d. 将一个文件的内容重定向到两个文件中

### 14. 命令 `cp source/accounts* newaccounts` 用于：

a. 将源目录下所有以 "`accounts`" 开头的文件复制到 `newaccounts` 目录

b. 将 `accounts` 程序的源代码移动到文件 `newaccounts`

c. 将所有以名称 "`accounts`" 开的文件合并为一个名为 `newaccounts` 的文件，并将该文件放在 `source` 目录

d. 将 `source` 目录的 `accounts` 文件合并到主目录的 `newaccounts` 文件

### 15. 正或错：`cut` 命令的 `-c` 选项用于引用字符位置。

### 16. 你想对一个变长度记录的文件进行排序，其中每个记录中字段之间的字符是分号 (`;`)。你使用 `sort` 命令时使用哪个参数来指定字段由分号分隔？

a. `-d;`

b. `+d;`

c. `-t;`

d. 以上所有

e. 仅 b 和 c

### 17. 命令 `paste vendors1 vendors2` 实现了什么功能？

a. 它将 `vendors1` 的内容覆盖到 `vendors2` 内容上，并将结果保存在 `vendors2` 文件。

b. 它将 `vendors2` 的内容覆盖到 `vendors1` 内容上，并将结果保存在 `vendors1` 文件。

c. 它将 `vendors1` 和 `vendor2` 合并后的内容显示在屏幕上。

d. 它将 `vendors1` 和 `vendor2` 文件的内容保存在缓冲区中，供 `vi` 编辑器以后访问。

### 18. 使用命令 `sort -o office -m industrial` 会发生什么？

a. `office` 和 `industrial` 文件的内容合并。

b. `industrial` 文件被删除，同时 `office` 文件的内容替换 `industrial` 文件。

c. `industrial` 文件按每个记录的最后一个字段排序，但仅当 `office` 文件包含与其中相同的字段时才进行。

d. 你看到错误信息，因为 `-o` 参数需要随带字段分隔符，例如 `":"`。

### 19. 使用 `join` 命令时，如果你想为未匹配记录显示文本 "`None`"，请使用 ________________ 选项。

a. `-u "None"`

b. `-e "None"`

c. `-N`

d. `nomatch`

### 20. 下列哪个命令允许你递归删除一个目录及其所有内容？

a. `rmdir -all`

b. `rm -r`

c. `cut -a`

d. `fail-on-empty`

# 第 4 章 UNIX 文件处理

### 21. 下列哪个命令允许你查看 `names` 文件，其中记录中字段之间的字符是分号 (`;`)？

a. `cat -d names`

b. `sort -t names`

c. `sort -t names`

d. `cut -t names`

### 22. 正或错：当字段显示时，`join` 命令中的 `-j` 用于反转字段。

### 23. 与 `join` 命令配合使用，以下哪个选项指定字段由冒号分隔？

a. `-o 4`

b. `-f 2`

c. `-t: 4`

d. `printf 2`

### 24. 与 `awk` 命令配合使用的 `-f` 选项指定______________________。

a. 字段分隔符的格式

b. 输入数据文件具有固定长度记录

c. 输入数据文件具有变长度记录

d. 命令来自磁盘文件而非键盘

### 25. ______________________ 是一个用于 `awk` 命令中打印格式化的 C 语言函数。

a. `-p`

b. `{ format }`

c. `printf`

### 26. 一个 ______________________ 文件通常包含与串口设备或打印机通信所需的信息。

a. 供应商文件

b. 字符特殊文件

c. 块特殊文件

d. 主打印机文件

### 27. `Stdout` 通常流向____________________。

a. 键盘

b. 调制器

c. 控制台

d. 网络连接

### 28. 你可以使用 `touch` 命令来：

a. 创建新文件

b. 修改文件的日期和时间戳

c. 将排序后的数据合并到新文件

d. 以上所有

e. 仅 a 和 b

### 29. 命令 "`cat accounts persons > info`" 用于：

a. 排序 `accounts` 文件并将其与 `info` 文件合并，创建一个名为 `persons` 的新文件

b. 排序 `accounts` 和 `persons` 文件并打印到名为 `info` 的打印机

c. 用 `persons` 文件中的数值数据替换 `accounts` 文件中的数值数据，并将结果写入 `info` 文件

d. 将 `accounts` 和 `persons` 文件的内容合并到 `info` 文件

### 30. `2>` 运算符重定向：

a. 标准输出

b. 标准错误

c. 标准输入

d. 将一个文件的内容重定向到两个文件中

### 31. 命令 `cp source/accounts* newaccounts` 用于：

a. 将源目录下所有以 "`accounts`" 开头的文件复制到 `newaccounts` 目录

b. 将 `accounts` 程序的源代码移动到文件 `newaccounts`

c. 将所有以名称 "`accounts`" 开头的的文件合并为一个名为 `newaccounts` 的文件，并将该文件放在 `source` 目录

d. 将 `source` 目录的 `accounts` 文件合并到主目录的 `newaccounts` 文件

### 32. 正或错：`cut` 命令的 `-c` 选项用于引用字符位置。

### 33. 你想对一个变长度记录的文件进行排序，其中每个记录中字段之间的字符是分号 (`;`)。你使用 `sort` 命令时使用哪个参数来指定字段由分号分隔？

a. `-d;`

b. `+d;`

c. `-t;`

d. 以上所有

e. 仅 b 和 c

### 34. 命令 `paste vendors1 vendors2` 实现了什么功能？

a. 它将 `vendors1` 的内容覆盖到 `vendors2` 内容上，并将结果保存在 `vendors2` 文件。

b. 它将 `vendors2` 的内容覆盖到 `vendors1` 内容上，并将结果保存在 `vendors1` 文件。
