
`misamck`: error: Found wrong record at 0

MyISAM-table '`name.MYI`' is corrupted

Fix it using switch "`-r`" or "`-o`"

### 3. 要修复损坏的数据库，你可以运行以下命令：

```
# myisamck -r /var/lib/mysql/allusers/name.MYI
```
- recovering (with keycache) MyISAM-table '`name.MYI`'
Data records: 5
Found wrong stored record at 0
Data records: 4

### 4. 如果由于原因 `-r` 选项不起作用，你可以尝试使用 `-o` 运行 `myisamck` 命令。这是一种较慢的旧版修复方法，但它可以处理一些 `-r` 选项无法处理的问题。这是一个示例：

```
# myisamck -o /var/lib/mysql/allusers/name.MYI
```

如果你的电脑有大量内存，你可以在 `myisamck` 命令行提高键缓冲区大小值，这将减少检查数据库所需。例如，你可以使用以下命令行：

```bash
myisamck -r -O --key_buffer_size=64M *.MYI
```
