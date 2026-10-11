
在 `$` 命令提示符后，输入 `vi awrp` 并按 **Enter** 键以启动 vi 编辑器并创建文件 `awrp`。

输入代码：

```
BEGIN {  
    { FS = ":"}  
    { print "\t\tVendors and Products\n" }  
    { "date" | getline d }  
    { printf "\t %s\n",d }  
    { print "Vendor Name\t\t Product Names\n" }  
    {print"====================================\n" }  
}  

{ printf "%-28s\t%s\n",$1, $2 }
```

按 `Esc`。

输入 `:wq` 以退出 vi 编辑器。

在 `$` 命令提示符后，输入 `awk -f awrp report > v_report`，并按 **Enter** 键。

这意味着“使用 Awk 程序，将 awrp 文件中的字段与 report 文件中的字段结合，并将它们发送到名为 `v_report` 的新文件。”

输入 `cat v_report` 并按 **Enter** 键。

你看到以下报告：

```
Vendors and Products
Sun Dec 20 21:03:41 EST 1998
Vendor Name    Product Names
==============================

Cromwell Interiors          Lobby Furniture
Design Extras Inc.          Ballroom Specialties
Piedmont Plastics Inc.      Poolside Carts
Morgan Catering Service Ltd.  Formal Dining Specials
Pullman Elevators           No Products
Johnson Office Products     No Products
```

要在默认打印机上打印报告，输入 `lpr v_report` 并按 **Enter** 键。

你制作了一份供应商和产品名称报告，并对报告进行了格式化和打印。

### 摘要

- 要自动化命令处理，请将命令包含在脚本文件中，以后可以作为程序执行。使用 `vi` 编辑器创建脚本文件，并使用 `chmod` 命令使其可执行。
- 使用 `join` 命令从两个共享通用字段的文件中提取信息。你可以使用此通用字段连接两个文件。你必须按连接字段对两个文件进行排序——即你想用来连接文件的那个字段。连接字段也称为“键”。在执行连接之前必须对文件进行排序。
- `Awk` 是一种模式扫描和处理语言，对于创建格式化和外观专业的报告非常有用。你可以使用 `vi` 编辑器将 `Awk` 语言指令输入程序文件，并使用 `awk` 命令调用它。

### 命令摘要

#### 第 4 章命令

| 命令 | 用途 | 本章涵盖的选项 |
| :--- | :--- | :--- |
| `awk` | 启动 Awk 程序以格式化输出 | `-F` 标识字段分隔符<br> `-f` 表示代码来自磁盘文件，而非键盘 |
| `cp` | 复制一个或多个文件 |  |
| `cut` | 从文件中提取指定的列或字段 | `-c` 指代字符位置<br> `-d` 指示指定字符分隔字段<br> `-f` 指代字段 |
| `find` | 查找文件 | `-name` 指定要定位的文件名称 |
| `join` | 结合具有通用字段的文件 | `-a n` 为文件 n 中每个无法配对的行产生一行<br> `-e str` 用指定字符串替换无法配对文件中的空字段<br> `-j` 在连接时使用指定的通用字段<br> `-o` 输出指定的字段列表<br> `-t` 指示指定字符分隔字段 |

#### 第 4 章 命令（续）

- `less`: 显示文件内容，在每屏结束时暂停
- `lpr`: 在默认打印机上打印命令输出
- `more`: 显示文件内容，在每屏结束时暂停
- `mv`: 移动一个或多个文件
- `paste`: 合并两个或多个文件的字段
- `rm`: 删除一个或多个文件
  - `-i`: 指定 UNIX 在删除文件前应请求确认
  - `-r`: 指定递归删除目录
- `rmdir`: 删除目录
- `sort`: 对文件内容进行排序
  - `+n`: 按 n 指定的字段进行排序
  - `+.`: 指定加号（+）后的偏移量位置为字符位置，而非字段位置
  - `-t`: 表示使用指定字符分隔字段
  - `-m`: 表示在排序前合并文件
  - `-o`: 将输出重定向到指定文件
- `touch`: 更新现有文件的日期和时间戳命令，或创建新的空文件
  - `-a`: 指定仅更新访问日期和时间
  - `-m`: 指定仅修改日期和时间
  - `-c`: 指定不创建文件

### 复习题

1. 以下哪个陈述是错误的？
   - a. `join` 程序要求你按连接字段对文件进行排序。
   - b. 脚本文件类似于 MS-DOS 批处理文件。
   - c. `Awk` 程序有时可以替代其他高级语言。
   - d. 你可以使脚本文件具有可执行权限。

2. `join` 命令_______。
   - a. 合并具有共同字段的文件
   - b. 只能用于已合并的文件
   - c. 是 `paste` 命令的反操作
   - d. 格式化输出

3. 与 `awk` 命令一起使用时，`-F` 选项指定_______。
   - a. 包含指令的外部文件
   - b. 输入文件具有固定长度记录
   - c. 输出的格式
   - d. 以上都不是

4. `Awk` 程序中的 `BEGIN` 块_______。
   - a. 在程序周期中仅执行一次
   - b. 如果你发出多个命令，通常需要用花括号括起来
   - c. 在程序加载时执行
   - d. 以上都是

5. `join` 命令使用哪个选项来指定输出字段列表？
   - a. `-o`
   - b. `-f`
   - c. `-x`
   - d. `-e`

6. `join` 命令使用哪个选项来指定在行不匹配时打印的字符串？
   - a. `-c`
   - b. `-o`
   - c. `-f`
   - d. `-x`

7. 与 `join` 程序一起使用时，以下哪个显示第一个文件的第二个字段？
   - a. `-o 2.1`
   - b. `-o 1.1`
   - c. `-o 1.2`
   - d. 以上都不是

8. `join` 命令类似于数据库程序，因为两者都_______。
   - a. 必须处理关系数据库文件
   - b. 访问表而不是文件
   - c. 使用关系连接操作连接文件
   - d. 必须仅由数据库程序读取

### 练习

1. 使用脚本文件有什么优势？
2. `join` 和 `paste` 有什么区别？
3. 为什么 `join` 命令执行的操作被称为“关系连接”？
4. 使用 `awk` 命令指定模式和动作的两种方法是什么？
5. 为一个 `vendors` 和 `products` 文件创建一个 `join` 脚本，显示哪些产品没有匹配的供应商记录。
6. 编写一个简单的 `Awk` 程序，打印图 4-3 中的 `phones1` 文件。
7. 编写一个脚本文件来显示 `vendor` 文件，然后运行该脚本。

### 探索练习

1. 使用 `vi`、`Emacs` 或你选择的方法创建 `cust_names`、`cust_ids` 和 `cust_status` 文件。这些文件应具有以下内容。
   - `cust_names` 的内容：
     - Smith Furniture Co.
     - Wells Manufacturing
     - Rose Department Store
     - Haywood Resort
   - `cust_ids` 的内容：
     - 101
     - 102
     - 114
     - 197
   - `cust_status` 的内容：
     - ACTIVE
     - ACTIVE
     - INACTIVE
     - ACTIVE

2. 使用 `paste` 命令创建一个名为 `cust1` 的文件。合并 `cust_ids` 和 `cust_names` 文件以创建 `cust1`。使用冒号字符作为字段分隔符。

3. 使用 `paste` 命令创建一个名为 `cust2` 的文件。合并 `cust_ids` 和 `cust_status` 文件以创建 `cust2`。使用冒号字符作为字段分隔符。
