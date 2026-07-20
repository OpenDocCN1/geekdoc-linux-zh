# Unix 使用指南



![cover.jpg](img/b2edff5ed726e650c0ffff756d0d73ab.jpg)



![aa.gif](img/514cd173582c87de9750ed5601a9a28f.gif)



第第 ii 页

使用 UNIX，第二版
© 1998 Que® 保留所有权利。未经出版者书面许可，本书的任何部分均不得以电子、机械、复印或其他方式进行复制、存储在检索系统中或传输。对于书中书中信息的 l 使用，本版不承担任何责任。尽管在编写本书时已采取一切预防措施，出版者和作者对错误或遗漏不负责。对于因使用书中信息而造成的损害，也不承担任何责任。

国际标准号：0-7897-1632-1
美国国会图书馆目录号：98-84201
美国打印
首次印制：1998 年 7 月
00 99 98 4 3 2 1

商标：本书中提到的所有已知的商标或服务标记均已进行适当的大写处理。QUE 无法证明这些信息的准确性。在书中使用某术语不应被视为对任何商标或服务标记有效性的影响。

编辑：
- Stan Spink, Billy Barron
- Laura A. Knox, Pamela Woolf
- 执行：Koch
- 采购：Williams
- 开发：Hatton
- 管理：Sarah Kearns
- 项目：Dinse
- 拷贝：Cline
- 索引：Ginny Bess





## 第一部分 什么是 UNIX？
### 1 UNIX 与 Shell 简介 (11)
### UNIX 是一个操作系统 (12)
### 通用硬件 (12)
### 通用软件 (13)
### UNIX 的历史 (15)
### UNIX 如何构建了互联网 (18)
### UNIX 的多样性 (19)
### 世界上有多少种类型的系统？ (19)
### 非 AT&T 版本 (20)
### 与 MS-DOS 有何不同 (22)
### UNIX 标准与修订 (24)
### AT&T 之后的 UNIX (26)
### 你必须先了解的重要 UNIX 概念





## UNIX 内核
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## UNIX Shell
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## Shell 提示符
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## Shell 变量
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 标准输出、标准错误、标准输入
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 管道与过滤器
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 用户与组
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 获取 UNIX 访问
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

#以 UNIX 的方式做事
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 没有消息就是好消息
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 命令是构建块
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 最少按键次数
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## UNIX 目录与路径名
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 介绍 UNIX 树形结构
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 根目录包含所有其他目录
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 查找名称的路径（完整路径名）
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### UNIX 中的目录
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 标准 UNIX 名称
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### SVR4 (Solaris) 中的新目录
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换到目录
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换目录并查看其内容 (cd, ls)
![content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 basename 和 dirname





### 显示您当前的目录名称
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换到主目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换到绝对目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换到当前目录的子目录（相对路径）
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 逐步切换目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 访问当前目录 (.)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 回到父级目录 (..)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 切换到父目录的子目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 返回到上一个目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 如何构建文件的相对路径
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 创建目录 (`mkdir`)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 删除现有目录 (`rmdir`)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 删除整个目录树 (`rm`)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 提高访问目录的效率
### 为经常访问的目录设置 `PATH`
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 保存经常使用的目录名称
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示系统信息
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示关于你和你的系统信息
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示其他用户的信息
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示关于 UNIX 密码文件的信息
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





### 获取日期 (date)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 获取系统名称信息 (uname)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 理解 UNIX 文件系统

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### UNIX 进程

### 输入 UNIX 命令的 4 条规则

### Shell 提示符复习

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### UNIX 选项、参数和注释

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在命令行中添加注释

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

##为命令输入选项

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

##为选项输入参数

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在哪里可以获取帮助 (man)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 从帮助页 (Man Pages) 获取帮助

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 识别子程序的帮助页

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在帮助页中查找信息

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 如果知道命令，如何查找所需的帮助页

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用置换索引 (Permuted Index)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### "command not found" 错误

### 设置命令的路径

### 将当前目录添加到 PATH

### PATH 的安全影响

### PATH 与附加软件包





### 命令在何？(type, which, whence)

## 100

### 用户在输入 UNIX 命令时常见的错误
### 101
### 大小写错误
### 101
### 间距错误
### 102
### 误用方向键、Insert、Page Up 等键
### 102
### 使用 Backspace（退格键）对比 Delete（删除键）纠错误
### 103
### 误用三种不同的类型
### 104
### UNIX 在告诉我什么？
### 105
### 用法
### 105
### `>` 符号 (PS2 提示符)
### 106
### 在没有提示符的情况下跳到下一行
### 107
### 无法获取文件名 (Cant Stat Filename)
### 108
### 当会话挂起时该怎么办
### 108
### 检查 Intr 和 Erase 键 (`stty`)
### 111
### 将输出或错误保存到文件中
### 112
### 将命令或管道输出保存到文件中 (`>`)
### 112
### Korn Shell 中的 noclobber 选项
### 114
### 输入文件不能同时作为输出文件
### 114
### 将错误保存到文件中 (`2>`)
### 115
### 将输出或错误追加到文件中 (`>>`)
### 116
### 将输出和错误同时保存到同一个文件中 (`2>&1`)





### 将输出复制到文件和屏幕 (tee)

## 5 UNIX 图形用户界面 (GUI)

### 介绍 GUI 和 X Windows
### X Windows
### X 终端
### 窗口管理器
### 控制台 GUI
### Solaris 桌面
### 旧版版 GUI：Windows
### 常见桌面环境 (CDE)
### 使用 Windows
### 在窗口之间传输文本
### CDE 支持哪些应用程序？
### CDE 中的详尽帮助
### 在 CDE 中运行 Shell 命令
### 在 CDE 中编辑文件

### CDE 文本编辑器
### 打开文件
### 基础编辑
### 检查拼写
### 格式化段落
### 复制

### CDE 文件管理器
#### 通过 CDE 文件管理器复制和移动文件/目录

### CDE 邮件客户端
#### 使用 CDE 邮件客户端收发/发送电子邮件





# 第二部分：操作 UNIX 文件

### 6 列出、查找、显示或打印文件

### 简介 UNIX 文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 如何确定文件类型 (ls)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 确定文件内容的类型 (file)

### 列出文件 (ls)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 查找 (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 根据文件名或名称部分查找 (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### find 选项对比 find 动作 (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 如何查找包含特定单词的文件 (find, grep)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在 find 选项中使用 AND、OR 和 NOT (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示小文件 (cat)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 分页显示文件/管道内容 (pg/more/less)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在文件显示添加行号 (nl, cat)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示包含字符的文件 (cat, od, strings)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 以大字母显示文本 (banner)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示 DOS 文件 (col)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 清理 man pages (col)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 打印文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 简介 UNIX 打印打印系统





# 如何确定系统打印机名称 (lpstat)

## 如何打印文件或管道内容 (lp, lpr)

## 如何检查打印队列 (lpstat)

## 如何取消打印作业 (cancel, lprm, qcan)

## 如何从离线打印机移动打印请求 (lpmove)

## 如何格式化输出 (pr)

## 复制、移动、重命名或删除文件

### 选择目标位置

### 处理权限拒绝（Permission-Denied）错误

### 复制、移动或重命名文件 (cp, mv)

### 在当前目录下复制、移动或重命名文件 (cp, mv)

### 向不同目录复制、移动或重命名文件 (cp, mv)

### 确定你的文件去向 (cp, mv)

### 将文件列表复制/移动到目录 (cp, mv)

### 处理确认请求

### 移动/重命名目录 (mv)

### 复制整个子树结构 (cpio)

### 删除文件 (rm)

### 在当前目录下删除文件 (rm)

### 在不同目录下删除文件 (rm)

### 删除文件列表 (rm)




## 删除整个目录子树 (rm)

- 192
- ![192content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 为同一文件创建多个名称 (ln)

- 193
- ![193content/fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用硬链接创建多个名称 (ln)

- 194
- ![194](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查找文件的所有硬链接 (ls, find)

- 195
- ![195](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 删除硬链接 (rm)

- 197
- ![197](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用软链接/符号链接创建指针 (ln)

- 197
- ![197](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 确定命令是否遵循软链接

- 199
- ![199](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 修改、合并和分割文件

- 201
- ![201](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 对文件或管道进行排序 (sort)

- 202
- ![202](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 确定行的排序方式 (ASCII)

- 202
- ![202](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 排序时忽略空白 (sort -b)

- 204
- ![204](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按大小排序 (sort -n)

- 204
- ![204](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 将结果保存回原始文件

- 206
- ![206](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 忽略大小写合并排序 (sort -f)

- 207
- ![207](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 逆序排序 (sort -r)

- 207
- ![207](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 排序时忽略标点符号 (sort -d)

- 208
- ![208](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 根据行内字段排序 (sort +n)

- 209
- ![209](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按主键和次键排序 (sort +m -n)

- 210
- ![210](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 显示文件或管道的开头行 (head, sed)

- 215
- ![215](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 显示文件或管道的结尾行 (tail)

- 216
- ![216](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 加密文件或管道 (crypt)

- 217





## 压缩文件 (`compress`, `gzip`)
第 219 页

## 将文件编码为可传输的简单文本 (`uuencode`)
第 221 页

## 合并文件
第 223 页

## 共同排序多个文件 (`sort`)
第 223 页

## 顺序连接文件 (`cat`)
第 223 页

## 将文件并排粘贴 (`paste`)
第 223 页

## 根据字段合并排序后的文件 (`join`)
第 224 页

## 将文件拆分为更小的文件
第 226 页

## 将文件拆分为等长度文件 (`split`)
第 226 页

## 按章节分割文件 (`csplit`)
第 227 页

## 生成并使用文件列表
第 231 页

## 使用文件名生成通配符
第 231 页

## 生成开头、结尾或包含模式 (*) 的名称
第 232 页

查看 Man Pages 以确定是否允许文件列表和通配符
第 232 页

## 减少长文件名的输入量
第 234 页

## 忽略文件列表中的目录
第 236 页

## 从多个模式生成一个文件列表
第 237 页

## 包含文件
第 237 页

## 生成其他目录的文件列表
第 238 页

## 在特定模式位置允许任意字符 (?)
第 239 页

## 指定固定长度的文件名
第 239 页





## 在模式位置上指定允许的字符 ([...])
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在模式位置上指定不允许的字符 ([!...])
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 处理参数列表过长的错误
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用反引号 (`) 生成文件列表
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 处理反引号无空格的情况
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用 xargs 处理文件列表 (xargs)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按日期、大小或内容比较文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按日期比较文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按最后修改日期比较文件 (ls)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按最后访问日期比较文件 (ls)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查找比给定文件更新的文件 (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按最后访问或修改查找文件，即使跨目录 (find)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按大小比较文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查看文件大小 (ls)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按大小列出文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按大小查找文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 比较文本文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 显示两个文件之间的差异 (diff)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 并排显示差异 (sdiff)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 显示三个文件之间的差异 (diff3)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查找排序文本文件中的共同行和唯一行 (comm)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





## 通过内容比较任意类型的文件 (cmp)

## 比较不同系统文件 (sum)

## 查找不同名称下的相同文件 (sum)

## 第三部分 用户与系统管理

### 11 文件权限与系统安全

### 安全性

### 登录后的延迟

### 二级密码

### 密码老化

### 修改你的密码

### 能看到你的密码吗？

### 允许用户变为另一个用户或 root (su)

### 系统规划

### 理解文件和目录权限

### SUID/SGID 程序

### 目录位保护你的文件

### SGID 在新文件上设置组

### 目录的读取和执行权限

### 修改权限/所有者/组

### 使用数字模式设置权限 (chmod)

### 使用符号模式设置权限 (chmod)

第 vii 页




# 修改文件的所属组 (chgrp)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 修改文件的所有者 (chown)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 设置新文件的默认权限 (umask)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 监控危险的 SUID、SGID 权限
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 挂载文件系统时的 SUID/SGID 文件

# 12 启动、关机和任务管理
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 启动系统
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 移除任何可启动介
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在主计算机之前开启辅助子系统
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 开机诊断
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 将内核加载到内存
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 挂载根磁盘并检查 (fsck)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 单用户模式
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 多用户模式
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# System V 运行级别 (Run Levels)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 关机系统 (shutdown)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 启动或关机时的任务自动化
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### System V UNIX 启动时的任务自动化 (rc2.d)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### System V UNIX 关机时的任务自动化 (rc0.d)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### BSD UNIX 系统启动时的任务自动化 (rc 脚本)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 任何用户的任务自动化 (profile, cron, at, batch)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 用户登录时的任务自动化





# 定期重新运行任务 (cron)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在 Crontabs 中使用星号 (*) 通配符

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在工作日清晨运行任务

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在特定日期/时间调度一次性任务 (at)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在系统负载低时调度运行一次性任务 (batch)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按用户启用或禁用 `crontab/at`

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 优先级

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查看任务和优先级 (`ps`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 以低优先级启动任务 (`nice`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 修改现有任务的优先级 (`renice`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 后台任务

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 启动后台任务 (`&`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 防止注销杀死后台任务 (`nohup`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 杀死后台任务 (`kill`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## Korn Shell 下的额外任务控制

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 列出后台任务 (`jobs`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 暂停和恢复任务 (`Ctrl+Z`, `bg`, `fg`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## Korn Shell 下的杀死后台任务 (`kill`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 暂停有输出的后台任务 (`stty`)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 13 使用 `tar` 和 `cpio` 保存和恢复文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 备份文件





# UNIX 设备文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 软磁盘驱动器
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# UNIX 软磁盘设备名称
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 选择 tar 或 cppio 或其他备份程序
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 使用 tar 备份和恢复文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 列出 tar 归档的目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 使用 cpio 备份和恢复文件
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 管理资源
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 管理磁盘
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 挂载文件系统
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 卸载文件系统
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 空间信息
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 为用户限制磁盘空间
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# lost 目录
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 磁盘管理命令
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# UNIX 处理

# 在文件或管道中搜索行
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 仅显示包含模式的行 (grep)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 选择行时忽略大小写 (grep -i)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 将选定的行保存到文件 (grep)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 将选定的行传递给其他命令 (grep)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 选择你的模式 (grep)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





## 显示不包含模式的行 (grep-v)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 为匹配到的行添加行号 (grep-n)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 只显示包含模式的文件名 (grep-l -c)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查找包含两个模式的行 (grep | grep)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 行中的通配符模式匹配（正则表达式）

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 选择包含模式的行 (grep)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 选择以模式开头的行 (^)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 选择以模式结尾的行 ($)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 指定整行的内容 (^$)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在正则表达式中包含变量

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在正则表达式中包含替换

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 引用正则表达式以防止问题

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 支持正则表达式的 UNIX 命令

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 比较文件名通配符与正则表达式通配符

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在特定位置允许任意字符 (.)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在模式中指定允许的字符 ([...])

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在模式中指定不允许的字符 ([^...])

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 指定正则表达式元素的出现次数 ({})

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 指定正则表达式元素零次或多次的出现 (*)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 丢弃无界或多个正则表达式通配符





# egrep 中提供的额外正则表达式通配符

## 402

## 使用 egrep 指定元素出现一次或多次 (+)

## 403

## 使用 egrep 使正则表达式元素出现零次或多次 (?)

## 403

## 搜索多个模式中的某一个 (|)

## 403

## 仅在 perl 中提供的额外正则表达式通配符

## 404

## 查找不是较大单词部分的单词 (\b)

## 405

## 关闭正则表达式通配符 (\fgrep)

## 406

## 通过检查特定字段来选择行 (awk)

## 407

## 当某个字段完全匹配时显示行 (awk)

## 407

## 根据某个字段的数值值显示行 (awk)

## 407

## 当某个字段符合正则表达式匹配时显示行 (awk)

## 408

## 根据多条件显示行 (&&)

## 409

## 在文件或管道中替换或删除文本

## 411

## 替换或删除字符串（使用正则表达式）

## 412

## 用另一个字符串替换一个字符串 (sed, 正则表达式)

## 在 sed 字符串中使用正则表达式通配符

## 412

 将替换后的输出保存到原始文件中 (sed)

## 414

## 每行仅进行一次替换 (sed)

## 415

## 更改分隔符 (sed)

## 416

## 从行中移除（删除）字符串 (sed, R.E.)

## 417




# 选择性替换或删除

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用特殊字符

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在搜索或替换字符串中使用 Shell 变量

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 不要替换 0 次或多次出现 (sed)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 在替换字符串中使用通配符匹配的内容 (sed)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 删除但保留搜索模式 (sed)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 规则：正则表达式通配符匹配最长跨度

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用 Perl 替换或删除字符串

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 如何匹配尽可能短跨度 (perl)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 扩展模式以提高可读性 (perl)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 替换不包含在更大单词中的单词 (perl)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 替换字符串或另一个 (perl)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在匹配正则表达式模式时忽略大小写

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 选择性替换或删除

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用 awk 替换或删除字符串

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 基于字段的替换或删除

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 只显示字段 (awk)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 条件替换特定值 (awk)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 将字段格式化为整齐的列 (awk)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 按列位置删除字符 (cut)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 从 UNIX 命令中提取字段





# 在文件或管道中替换/删除字符 (tr)

## 确定你的 UNIX 系统上是哪种 tr

## 将大写字母转换为小写字母或反之 (tr)

## 设置/清零每个字符的第八位 (tr)

## 删除选定的字符 (tr)

## 将大多数字符转换为单个字符 (tr)

## 替换/删除整行

## 替换整行 (sed)

## 删除包含正则表达式 R.E. 模式的行 (grep)

## 删除重复行 (uniq)

# 17 使用 vi 编辑文本文件

 介绍 vi 编辑器

## 如何启动 vi

## 创建用于 vi 练习的文件

## 仅需 10 条 vi 命令即可编辑任何内容

## 使用 h, j, l 移动

## 错误时的蜂报声

## 使用重复计数

## 使用 i 插入

## 使用 x 和 dd 删除

## 使用 j 合并行





# 使用 `:wq` 保存并退出

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 使用 `:q!` 放弃修改

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 为 vi 添加帮助功能

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 接下来学习这八 个 vi 命令

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 按 `Ctrl+L` `Ctrl+R` 重绘屏幕

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `u` 撤销修改

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `A` 在行尾添加文本

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `:w` 定期保存

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `:w File` 保存到不同的文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 处理写入权限失败

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `r` 替换一个字符

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `cW` 修改单词

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `1G/G` 跳转到文件开头/末尾

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `:f` 查看文件名、大小和当前位置

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 帮助使用 vi 的技巧

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `U` 恢复整行

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 `spell` 寻找拼写错误的单词

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 段落格式化

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 恢复丢失的编辑

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 以只读模式启动 vi

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 插入命令表

## 在 vi 中移动





## 分离单词、包含单词与非单词

## vi 移动命令表
### 通过搜索字符串移动
### 在行内移动到特定字符
### 查找匹配的括号符号
### 设置标记以便返回

## vi 删除文本命令表
### 恢复被删除的文本

## vi 修改文本命令表
### 替换文本

## 18 让 vi 编辑器为你你效力
### 跳过重复性编辑
### 使用 `.` 重复编辑操作
### 使用 `n` 和 `.` 搜索并选择性地重复编辑
### 将按键映射到常用的命令序列
### 防止 `J` 将你的文本变成一团糟
### 全局和局部文本替换
### 在整个文件中替换正则表达式（R.E.）模式
### 在文件的部分区域替换正则表达式（R.E.）模式
### 在 vi 中进行条件文本替换
### 修改行的缩进




# 在 vi 中移动/复制文本段

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 在同一文件中移动/复制文本

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 在不同文件之间移动/复制文本

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 设置插入文本的选项

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 设置 vi 始终显示输入模式

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 关闭行尾自动换行

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 行首自动缩进

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 使用缩写处理长字符串

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 行号显示

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 使用 / 或 ? 搜索时忽略大小写

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 在 .exrc 中保存选项

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 利用其他命令在 vi 中工作

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 在 vi 中期间检查其他命令

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 将其他 UNIX 命令的输出插入到文件中

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 排序文件或部分文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 删除匹配模式的行

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 加密/解密文件或部分文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 在文档中插入横幅标题

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 打印文件部分

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 统计文件部分的行数/单词数/字符数

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

# 编辑多个文件





# 19 Korn Shell 中的命令行编辑

## 调用命令行编辑选项
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 命令历史
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## vi 命令编辑模式
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 别名 (Alias)
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 介绍 emacs 编辑器
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 技术术语
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

##  emacs
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 打开/保存文件并退出 emacs
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用撤销功能
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 剪切与粘贴
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 自动备份
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 键键绑定
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 定义宏
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 重复宏
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 搜索与替换
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 增量搜索
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 普通搜索
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 普通搜索与替换
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 正则搜索与替换
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 编译匹配列表
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 搜索中的大小写
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





## 拼写检查 (526)

## 主模式与子模式 (528)

## 加载子模式 (529)

## 加载主模式 (530)

## 获取关于 emacs 的帮助 (531)

## Info (532)

## 继续使用 emacs (533)

## 额外的 emacs 软件包 (534)

## 文中未的实用 emacs 函数列表 (534)

## 第五部分与其他用户及系统通信

### 21 通过调制解调器访问其他 UNIX 系统 (539)

#### 调制解调器概述 (540)

#### UNIX 设备 (541)

#### 检查设备文件 (542)

#### 串口通信配置 (543)

#### 串口通信拨入配置 (543)

#### 用于拨出的串口 (545)

#### 在 `cu` 程序中登录 (547)

#### 配置 `cu` (549)

#### 使用 `cu` 程序 (552)

#### 通过 `uucp` 传输文件 (554)

#### 运行远程命令 (556)

页码 xi





# 查看 uucp 任务状态

## 取消 uucp 请求

## 通过调制解调器扩展网络 (PPP)

## 配置简单的 PPP 连接

## 停止 PPP 连接

## 注意

## 访问网络或互联网上的其他系统

## 网络概念

## 检查网络连接

## 检查 IP 地址

## 命名主机

## 使用 Ping 测试连接

## 检查域名服务正在运行

## 检查你已连接到互联网

## 通过网络登录 UNIX

## 使用 Telnet 登录

## 当 `rlogin` 优于 Telnet

## 配置 `hosts` 和 `.rhosts`

## 跨网络传输文件

## 使用 FTP 传输多个文件

## 使用 `rcp` 传输文件





# 在网络中的另一个系统上执行命令

## 结语

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 23 从 Windows 访问 UNIX

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### Windows 和 TCP/IP

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 Ping 测试连接

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 查看本地 TCP/IP 设置

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 ftp 在 UNIX 之间传输文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用 telnet 登录 UNIX

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 拨号上网

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 通过互联网访问 UNIX 主机

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 通过终端连接访问 UNIX 主机

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 与远程主机之间传输文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在 Windows 上通过 Netscape 收发邮件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 24 UNIX 与互联网

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 从 UNIX 浏览网页

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 从互联网下载软件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 下载 Lynx

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在 Lynx 上运行 make

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 使用字符浏览器 (Lynx)

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### UNIX 厂商网站

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 访问 UNIX 技术支持

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 访问免费（非支持）软件





![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查补丁/更新 627

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查安全公告 628

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查 2000 年问题 628

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 阅读 UNIX 新闻 629

## 第六部分 编程

### Bourne Shell 脚本 25

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 编写/执行简单脚本 637

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 创建/使用自定义的变量 638

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 使用反引号设置变量 639

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 与用户交互 641

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 显示标题和提示符 (`echo`) 643

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 将用户输入获取到 Shell 变量 (`read`) 643

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 在命令行上提供脚本输入 (`$1`) 645

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 根据测试结果执行代码 (`if`) 647

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查类型、大小或权限 648

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查变量内容 652

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查命令结果 654

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 进行算术计算 (`expr/bc`) 656

### 特殊变量 658

检查命令行参数数量 (`$#`) 658

检查上一个命令的状态 (`$?`) 658

使用不冲突的临时文件 (`$$`) 659





# 将所有参数传递给另一个命令 ($*)

# 退出脚本并设置退出状态 (exit)

# 提供适当的 UNIX 使用错误提示

# 循环遍历每个命令行参数 (for)

# 调试你的脚本

# 循环遍历列表 (for)

# 处理目录中的文件

# 处理目录树中的文件

# 从项目菜单中选择 (case)

# 编写 awk 脚本

# 何时何时使用 awk

# awk 的特性

# awk 的基础知识

# 从命令行使用 awk

# 处理（模式与动作）

# 正则表达式模式

# 比较运算符与模式

# 复合模式运算符

# 运算符

# 处理输入

# 编写你的程序

# 动作




# 变量
682
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 定义变量
684
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 字符串
687
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 字符串常量
688
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 字符串运算符
688
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 特殊常量
692
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 数组
692
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 数组函数
693
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 多维数组
694
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 内置数值函数
695
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 算术运算符
695
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 流程控制
696
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 空语句
697
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 条件运算符
697
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 循环
698
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### do 语句
698
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 循环控制 (break 和 continue)
698
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### for 语句
698
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### while 语句
700
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 高级输入输出
700
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 输入
701
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 下一个和退出





# 701
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
`getline`

# 701
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 从文件输入

# 702
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 从命令输入

# 702
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 结束文件或命令输入

# 702
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 输出

# 703
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 格式化 (`printf`)

# 703
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 输出到文件

# 706
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 输出到命令

# 706
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 关闭输出文件或管道

# 706
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 函数

# 707
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 定义

# 707
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 参数

# 708
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 函数的显式返回 (`return` 语句)

# 709
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 编写报告

# 710
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 复杂报告

# 710
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 提取数据

# 710
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 临时命令

# 711
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 一个内置函数: `system`

# 713
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 结语

# 714
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 27 编写 Perl 程序

# 717
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 编写/执行简单的 Perl 脚本

# 718
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
## 关于终止的快速说明

# 720





### 与用户交互

### 字面量

### 变量

### 代码引用

### 文件句柄

### 这里

### 特殊变量

### 作为参数提供输入

### 在命令行上提供输入

### 控制结构

### 什么是真？

### 根据结果执行代码 (`if`)

### 决策判断 (`if-else`)

### 遍历每个命令行参数 (`for`)

### 遍历整个对象 (`foreach`)

### Perl 中常用的函数

### 数组操作

### Pop 和 Push

### Shift 和 Unshift

### Splice

### 文件操作

### 关闭





## 739 Open
## 740 哈希值操作
## 741 each
## 741 keys
## 742 values
## 742 系统操作
## 742 time
## 742 localtime
## 743 system
## 744 变量
## 745 split
## 746 join
## 747 chomp
## 747 调试你的脚本 (`-d`)
## 748 列出代码 (`l`)
## 749 列出代码 (`l`)
## 750 执行一行代码 (`n`)
## 750 打印变量值
## 750 断点
## 751 结语
## 754 附录 A UNIX 命令
## 757 术语表
## 805 索引
## 823 页 xiv
## 关于作者




# 作者

DTR Business Systems（本书的编写公司）已销售、集成、安装、配置并目前支持跨越整个大陆的数千 UNIX 系统。

Steve Mor Moritsugu（实际撰作者）在 `Caltech` 获得 `B.S.` 学位，并在 20 多年中专注于计算机操作系统。他是一位高级软件工程师，也是 `DTR` 的支持主管。他曾多次在世界各计算机会议上担任演讲嘉宾，并为各种计算机杂志撰写文章。此外，Mor 还在南加利福尼亚州的 `Santa Ana College` 教授 `UNIX` 操作系统、`System Administration` 和 `Shell Script Programming`。他曾尝试将多本 `UNIX` 书作为其课程的教材，因此对于如何编写一本有效的 `UNIX` 书具有独特的见解。

James Edwards 是一位 IT 专业人士，在北美和欧洲的数据通信、网络集成和系统设计方面拥有丰富经验。他拥有伦敦大学（University of London）的信息技术 `M.S.` 学位和英国米德尔塞克斯大学（Middlesex University）的 `B.A. (Hons)` 学位。James 目前住在加拿大多伦多，在 `Deloitte & Touche Consulting Group` 担任经理。他的空余时间花在女儿 Denise、Lauren 和 Poppy 身上。

Sanjiv Guha 有 15 年管理和开发金融、银行和其他应用系统的经验。他擅长在各种硬件平台上进行 `Visual C++`、`C` 和 `COBOL` 开发，包括 `RISC 60000 AIX`、`IBM ES9000 MVS`、`VAX 3400` 和 `Windows 95`。他曾合著过其他本 `UNIX` 书。他正在培养 `Java` 和 `Windows NT` 技能。Sanjiv 拥有印度新德里理工学院（Indian Institute of Technology）的技术硕士学位（Master of Technology Degree）。他目前与妻子 Misty 和四岁的儿子 Saptarsi 住在特拉华州。

David B. Horvath, `CCP` 是宾夕法尼亚州费城地区的高级顾问。他担任顾问已超过 12 年，并是当地学院的兼职副教授，教授 `C Programming`、`UNIX` 和 `Database Techniques` 等课题。他目前正在宾夕法尼亚大学（University of Pennsylvania）攻读 `Dynamics of Organization` 的 `M.S.` 学位。他在国际范围内为专业协会和公司提供研讨会和工作坊。David 是 *UNIX for the Mainframer* (Prentice-Hall/PTR) 的作者，《UNIX Unleashed, Second Edition: System Administration Edition and Internet Edition* 系列的贡献作者（封面贡献），*Red Hat Linux, Second Edition* 的贡献作者，并撰写过大量杂志文章。不在键盘前时，他会在花园里忙碌或泡热水浴。他已结婚超过 10 年，有几只狗和猫。如果你对这本书有任何问题，可以通过 `usu@cobs.com` 联系他（请勿发送垃圾邮件！）。

T. Gordon Marler 从 1987 年开始在运行 `Ultrix` 的 `DECStation` 上接触 `UNIX`，之后从未停止。他毕业于路易斯安州数学、科学与艺术学校（Louisiana School for Math, Science, and the Arts），并在德克萨斯大学阿灵顿分校（University of Texas at Arlington）获得 `Computer Science Engineering` 的 `B.S.` 学位。他的第一份大型 `UNIX` 系统管理工作是在超导对撞加速器（Superconducting Super Collider）粒子加速实验室，作为六人小组的一员负责约 750 台工作站及支持它们的服务器。Gordon 在华盛顿州雷蒙德的 `AT&T Wireless` 担任 `Lead System Administrator`。可以通过 `gordon.marler@attws.com` 联系他。

1998 年 9 月，Jesper Kjær Pedersen 将在丹麦奥登大学（Odense University）完成计算机科学论文。他认为他迄今为止最重要的事情是开发 `Dotfile`。他还为 `Linux Journal` 撰过文章，进行过关于 `UNIX` 的演讲，并在奥登大学负责过 `UNIX` 系统。完成论文后，他想出国（去英国或美国）几年。空余时间他练空道，并与可爱的女朋友 Anne 享受生活。

David Pitts 是 `BEST Consulting` 的高级顾问，该公司是密西比河以西的顶级公司之一，目前正派往 `The Boeing Company` 担任系统管理员、程序员、网站管理员和作者。他住在华盛顿州埃弗特，与优秀的妻子 Dana 在一起。埃弗特就像住在明信片上，西边是普吉特湾，东边是雪后的喀斯奇山脉。David 最喜欢的引言来自方济各圣：传演福音，必要时要使用语言。可以通过 `dpitts@mk.net` 或 `dpitts@bestnet.com` 联系他。

Daniel Wilson 是 `Oracle Corporation` 印第安波利斯处的首席顾问。他的背景包括 `SMP` 和 `Clustered` 环境下的 `UNIX Systems Administration` 和 `Oracle Database Administration`。他曾使用 `C`、`C++` 和 `SQL` 进行编程。他于 1984 年毕业于印第安州芒西的鲍尔州大学（Ball State University）。他目前住在印第安波利斯郊，与妻子 Angela 和两个孩子 Tim 和 Emily。

# 致谢

我要感谢 `DTR` 的同事和管理层为我编写这本书提供时间和资源支持；感谢 `DTR` 的客户提供不断的问题和技术挑战；感谢 `Santa Ana college` 的学生对本书提供的反馈和帮助；感谢我的朋友和家人的爱与理解；最重要的是，感谢所有在我遇到困难时帮助我的 `UNIX` 专家们。

Steve Mor Moritsugu

告诉我们你的想法！





作为麦民计算机出版社操作系统团队的执行编辑，我欢迎您的反馈。您可以通过传真、电子邮件或直接写信与我，告诉您对这本书的喜欢或不喜欢之处，以及我们可以做哪些来提高书的质量。

请注意，我无法帮助您解决与本书主题相关的技术问题，而且由于收到的邮件数量很大，我可能无法回复每一条信息。

在您写信时，请务必包含本书的书名和作者，以及您的姓名和电话或传真号码。我将仔细审查您的意见，并将其与参与本书的作者及编辑分享。

**传真：** 317-581-4663
**电子邮件：** opsys@mcp.com
**邮寄：**
Executive Editor Operating Systems
Macmillan Computer Publishing
201 West 103rd Street
Indianapolis, IN 46290 USA

第 1 页

# 引言

欢迎使用 UNIX。UNIX 系统因其卓越的可靠性而深受。它们通常运行数月或多年而不出现任何系统问题或崩溃。在任何计算机配置中，UNIX 系统通常都能提供最佳的性能、最高的吞吐量以及最大的并发用户支持。UNIX 提供了无与伦比的扩展性，允许计算机系统既可以作为单用户工作站，也可以作为支持数百并发用户访问公共数据库的服务器。UNIX 提供了丰富的实用程序、网络和编程工具，以及适用于几乎每个业务和行业的定制应用程序。UNIX 通过为您提供快捷方式来提高生产力，并回报您投入的时间和精力，并通过揭示其秘密，让您能够深入内部发现并修复错误，并根据您的喜好定制系统。随着新 CPU 芯片的开发，UNIX 卓越的可移植性将允许您在迁移到更新、更快的机器时，保留您的软件投资。

UNIX 命令具有如 `ls`、`mv`、`awk`、`grep` 和 `sed` 等名称，通过这些命令，UNIX 专家可以用几行代码完成其他情况下可能需要数小时工作或通过特殊编程才能实现的任务。事实上，微软刚刚发布了 Windows NT 的 UNIX 服务附加包，其中其他功能允许允许 25 多个 UNIX 命令和 Korn shell 在 Windows NT 下运行。

第 2 页

另一方面，也有人喜欢 UNIX 但认为它晦涩、简洁且不友好。UNIX 假设你清楚自己在做什么，如果你输入了无意义的命令，它通常不会发出任何警告。初学者经常会在此卡壳并不得不寻求帮助。每个命令都像一个独立的王国，有它们自己的语言、习俗和传说。

# 本书简介

如果您是 UNIX 初学者，这本书将帮助您避开大多数初学者都会会掉入的陷阱。它将帮助您理解底层概念和命令，使它们变得易懂并让您记忆得更好。本书不需要 MS-DOS 背景，但如果您熟悉 MS-DOS，您会发现某些内容是相似的。

如果您已经使用 UNIX 多年，现在准备好提高精通程度，这本书将为您提供帮助。它基于我在南加利州教授 UNIX 的多年经验。特别是第 9 章以及第 15 章和第 16 章，阐述了复杂的主题，我将这些主题组织成了层层递进的内容。

如果您是 Linux 用户，本系列中有一本名为 *Using Linux* 的书，您可以在那里找到比本书更关于 Linux 使用和设置的特定信息。然而，由于任何书中都有大量内容涵盖了安装以及设置用户、磁盘、打印机、调制解调器、网络、`tcp/ip`、Web 服务器、DNS 等，您可能会发现 Linux 下提供的标准 UNIX 概念和命令覆盖范围没有本书如此详尽。

第 3 页





多位作者为本书编写了章节，以帮助我们赶上出版截止日期，我非常感谢他们的帮助。作为主作者，我很乐意听取读者对本书的意见或问题。我的电子邮件地址是 `mori@dtrbus.com`。

我计划为本书列出一份更错修订列表，希望它能足够优秀并达到出版第二版的标准。我正在与出版商讨论制作一本配合此本书的练习题和答案练习册。如果读者们愿意购买此类练习册，请告诉我。

我工作的公司 DTR Business Systems 为我担任本书的主作者提供了职能支持。DTR 在全国范围内支持一个 UNIX 增值转销商网络。遗憾的是，我无法通过电子邮件提供免费的 UNIX 支持，但我确定，如果您需要商业级 UNIX 产品或服务，我们可以为您推荐相关资源。

# 本书内容

## 第一部分：什么是 UNIX？

### 第 1 章：UNIX 和 Shell 导论
讨论了什么是 UNIX、它的历史以及为什么会有这么多不同的版本。本章通过最近发布的 64 位 `SVR5` 将历史更新到了最新状态。它涵盖了您在书中其余部分需要的某些基础但基本的 UNIX 概念。

### 第 2 章：UNIX 目录与路径名
展示了如何访问 UNIX 目录和文件。本章涵盖了绝对路径与相对路径，这在构建 UNIX 文件命令至关重要。

### 第 3 章：显示系统信息
展示了您在登录新系统时可以运行的命令，提供有关您的登录和工作站、其他用户、系统及其文件系统和进程的信息。

### 第 4 章：输入 UNIX 命令的规则
解释了命令语法，让您知道哪些空格是必须的，哪些是非法的。它描述了 `man` 命令，该命令允许您查询命令用法和选项。展示了命令行中常见的错误以及如何解释常见的 UNIX 响应。它描述了当工作站卡住时该怎么办。告诉您如何将命令的输出或错误保存到文件中。

### 第 5 章：UNIX 用户界面 (GUI)
描述了 `X Window` 系统，该系统允许您使用鼠标和图形图标。它以 `Solaris` 为例。它涵盖了在许多类型的 UNIX 系统中常见的桌面环境（CDE），包括作为文本编辑器、文件管理器和电子邮件处理程序的图形化应用程序。

## 第二部分：与 UNIX 文件操作

### 第 6 章：列出、查找、显示或打印文件
涵盖了使用 `ls` 列出文件、使用 `find` 查找文件、使用 `cat`、`pg`、`less`、`nl`、`od`、`strings`、`banner` 和 `col` 显示文件。还涵盖了打印文件、检查队列、移动打印作业以及使用 `pr` 格式化输出。

### 第 7 章：复制、移动、重命名或删除文件
涵盖了如何通过简单示例执行不同目录执行这些操作。还涵盖了创建硬链接和软链接。

### 第 8 章：修改、合并和分割文件
涵盖了如何排序文件；如何仅文件的开头或结尾；以及对文件进行加密、压缩和编码为可打印文本格式。涵盖了如何使用 `sort`、`paste` 和 `join` 合并文件。涵盖了如何使用 `split` 和 `csplit` 分割文件。

### 第 9 章：生成和使用文件列表
涵盖了如何使用文件名生成通配符，为可以操作多个文件的 UNIX 命令生成所需的文件列表。它还描述了如何使用反引号和 `xargs` 处理文件列表，特别是当匹配的文件过多导致通配符无法处理时。

### 第 10 章：按日期、大小或内容比较文件
展示了如何使用 `ls` 命令按照最后访问、最后修改或文件大小列出文件。展示了如何使用 `find` 列出在给定时间范围内修改或访问的或特定大小的文件。展示了如何以及何时使用 `diff`、`sdiff`、`diff3`、`comm`、`cmp` 和 `sum` 比较文件内容。

## 第三部分：用户与系统管理

### 第 11 章：文件权限与系统安全
讨论和密码安全，以及如何在 UNIX 下设置用户和组以共享某些文件和目录，同时限制其他内容。涵盖了文件和目录权限以及数字和符号模式下的 `chmod` 命令。涵盖了 `umask` 如何影响分配给新文件和目录的权限。讨论了 `SUID` 和 `SGID` 位的安全影响。

### 第 12 章：启动、关闭和作业管理
涵盖了如何启动和关闭 UNIX 系统。讨论了用户和系统管理员如何在系统启动、登录以及预定义时间或周期性间隔自动作业。涵盖了作业优先级以及如何设置和更改优先级。讨论了作业控制以及如何暂停、恢复和杀死后台作业。

### 第 13 章：使用 tar 和 cpio 保存和恢复文件
涵盖了 UNIX 设备名称，特别是磁带和磁盘。涵盖了如何使用 `tar` 备份目录或选定文件、列出备份内容以及恢复文件的策略和注意事项。然后针对 `cpio` 涵盖了相同的内容。





# 第 14 章，管理系统资源
涵盖了文件系统和磁盘配额。

## 第四部分：UNIX 文本处理

### 第 15 章，在文件或管道中搜索行
描述了如何使用 `grep` 显示包含模式的行。它涵盖了正则表达式，这是一个极其重要但困难的话题，并将其分解为系列分层的课程。它涵盖了 `egrep` 中的扩展正则表达式。它涵盖了从命令行使用 `perl` 和 `awk` 来提供搜索模式的额外功能。

### 第 16 章，在文件或管道中替换或删除文本
描述了如何使用 `sed` 利用正则表达式的力量来修改行。它涵盖了从命令行使用 `perl` 和 `awk` 为替换和删除文本提供额外功能。它还涵盖了使用 `cut`、`tr` 和 `uniq` 修改或删除行或字符。

### 第 17 章，使用 vi 编辑文本文件
展示了学习所有基础编辑所需的前 10 条 `vi` 命令。它涵盖了接下来要学习的八条命令。它列出了各种用于插入文本和移动光标的 `vi` 命令，引入了分离单词与包含单词及非单词的概念。它列出了用于删除和更改文本的 `vi` 命令。

### 第 18 章，让 vi 编辑器为你工作
展示了 `vi` 在快速处理任何重复性编辑任务中的威力。它并没有学习独立的 `vi` 内置命令，而是展示了如何调用 `sed` 和 `awk` 进行搜索和替换操作，使用 `sort` 进行排序，使用 `grep -v` 选择性地删除行、加密部分、插入横幅、打印部分以及统计部分内的行数。它展示了如何 `cut`、粘贴以及设置所需的 `vi` 选项。

### 第 19 章，Korn Shell 中的命令行编辑
展示了如何召回之前的命令、修改并执行它们。这一章的简易性掩盖了它的实用性，因为它让 UNIX 专家能够分阶段地构建出优雅的命令行结构。

### 第 20 章，介绍 emacs 编辑器
描述了另一个具有强大功能和灵活性的 UNIX 编辑器。许多用户倾向于这种 `vi` 的替代方案。

## 第五部分：与其他用户和系统通信

### 第 21 章，通过调制解调器访问其他系统
描述了如何使用 `write` 和 `talk` 与另一个用户进行在线对话。它涵盖了如何向另一个用户发送电子邮件以及读取任何邮件。它提到了 `wall` 向所有用户广播。

### 第 22 章，在网络或互联网上访问其他系统
涵盖了 TCP/IP 基础、如何使用 `telnet` 和 `rlogin` 登录网络中的另一个系统、如何使用 `ftp` 和 `rc` 传输文件，以及如何使用 `rsh`（某些 UNIX 系统上称为 `cmd`）执行命令。

### 第 23 章，从 Windows 访问 UNIX
展示了如何在 Windows 上设置 TCP/IP，如何使用 Windows `ftp` 在 UNIX 和之间之间传输文件，如何使用 Windows `telnet` 登录 UNIX，如何将你的 Windows 连接到互联网，然后在那里使用 `telnet` 和 `ftp` 连接到互联网上的任何 UNIX 服务器。它还涵盖了如何在 Windows 上使用调制解调器，以及如何使用 `Netscape` 读取邮件和发送回复。

### 第 24 章，UNIX 与互联网
展示了如何从 UNIX 浏览互联网；如何使用 Web 浏览器下载软件；如何下载并使用 `Lynx`（一种在 UNIX 终端上用于互联网浏览的字符界面浏览器）；如何使用 `make` 编译软件；如何在互联网上访问 UNIX 供应商并获取帮助（例如，UNIX 需要的 2000 年补丁）；如何访问安全公告；以及如何在 UNIX 上阅读网络新闻。

## 第六部分：Shell 编程

### 第 25 章，编写 Bourne Shell 脚本
涵盖了使用 Bourne Shell 脚本语言编写程序。它描述了 shell 变量、提示符、用户输入、命令行参数、`if` 测试、检查命令结果、计算、特殊变量、用法错误、循环处理命令行参数、调试、循环处理一组文件，以及 `case` 语句。

### 第 26 章，编写 awk 脚本
涵盖了使用 `awk` 语言进行编程，该语言与 C 语言语法相似。它包含了变量、字符串、操作符、内置函数、数组、数组函数、`if` 语句、循环、获取输入的 `getline`、用于格式化输出的 `printf`、自定义函数以及执行 UNIX 命令的 `system` 命令。

### 第 27 章，编写 Perl 程序
涵盖了使用 `perl` 进行编程，它通常用于 UNIX 和 Windows 上查找和显示网站信息。本章涵盖了内置变量、`if` 语句、循环、函数、数组、文件访问、哈希数组、字符串和调试。它没有涵盖 CGI 编程，但本章中的所有元素在 CGI 编程中都是用。

## 第一部分 什么是 UNIX？

### 1 UNIX 和 Shell 简介
### 2 UNIX 目录与路径名
### 3 显示系统信息
### 4 输入 UNIX 命令的规则
## 5 UNIX 图形用户界面 (GUI)





# 第 1 章 UNIX 与 Shell 简介
作者 Steve Mor Moritsugu

## 基础硬件与软件术语

### 什么是 UNIX
### UNIX 的历史
### 不同类型的 UNIX
### UNIX 对比 Windows
### UNIX 的结构
## UNIX Shell
### 标准输入、输出和错误
## 管道与过滤器
### UNIX 之道

## UNIX 是一种操作系统
为了解释 UNIX 是什么，我将首先介绍一些关于计算机硬件、软件，以及应用程序与操作系统的非常基础术语。如果你已经了解了这些内容，请随时跳过接下来两个关于计算机硬件和软件概述的章节。

### 计算机硬件概览
计算机硬件是指你可以触碰的物理元件。例如，大多数计算机都有一个用于打字的键盘，以及一个用于查看输出的显示器或屏幕。安置计算机的箱子（其机箱）将包含更多硬件，例如一个或多个硬盘驱动器，这些设备允许你存储数据。你可能听过容量高达 500 兆字节（MB）或吉字节（GB）的驱动器。`Mega` 代表百万，`giga` 代表十亿。`Byte`（字节）是计算机单位，相当于文档中的一个字符。因此，一个 `500MB` 的磁盘可以存储 500 份各包含一百万字符的文档。一个 `2GB` 的磁盘容量是 `500MB` 磁盘的四倍。另一个硬件组件是内存或 `RAM`。内存容量通常是 2 的幂，例如 `32MB` 或 `256MB`。某些非常强大且昂贵的计算机拥有 GB 内存。内存是计算机的工作空间，因此更大的内存允许计算机更好地运行。`CPU`（中央处理器）是一个至关重要的硬件元件。它是计算机的大脑，允许它遵循一组程序指令进行计算，并处理存储在内存或硬盘驱动器中的信息。你可能听过英特尔处理器，例如奔腾芯片，但也存在其他与英特尔完全不同的 `CPU` 类型，例如 RISC 处理器（精简指令集计算机），如 PowerPC。某些计算机拥有多个 `CPUs` 以提高性能。

计算机还可以包含其他系统组件，例如一个或多个磁带驱动器、软磁盘驱动器或 CD-ROM 驱动器。这些组件也可以称为外围设备和辅助设备，但这些术语通常留给连接设备，如终端、打印机和调制解调器。

### 计算机软件概览
计算机的一组指令被称为程序。程序存储在硬盘上，从 `RAM` 运行，控制 `CPUs` 并使用外围设备。为了将这种编程与计算机的硬件部分区分来，被称为软件。计算机软件可以分为以下几类：

- **应用程序**：应用程序是设计为为用户提供特定功能的程序。例如，文字处理程序允许用户输入、修改文档并将其打印出来。应用程序涵盖了业务的几乎每个方面，如会计、工资单、库存、销售点管理和预约调度。应用程序也存在用于科学或财务计算、个人及家庭使用以及游戏。使用应用程序的人被称为终端用户。
- **语言**：计算机语言是让被称为“程序员”的人能够创建计算机程序的软件程序。诸如 `BASIC`、`FORTRAN` 和 `COBOL` 等计算机语言已经存在多年，且仍在使用。新计算机语言的开发是为了为程序员编写程序提供更好的工具。例如，`Visual BASIC` 提供了图形工具，用于编写在 Windows 下运行的程序。`Java` 为运行在万维网上的应用程序提供了图形工具。`C` 语言是一种古老、多用途且高效的语言，如今仍然非常受欢迎，此外还有 `C++`，`C++` 是 `C` 的修订版本，支持更新的面向对象编程方法，使得编写复杂程序变得更容易。
- **操作系统**
- **实用程序**





# 操作系统

操作系统是整个计算机的核心控制程序，负责控制正在运行的任务。它还将将硬盘组织成文件，文件是磁盘块的集合，用于存储我们想要保留在一起的信息。操作系统允许为每个文件赋予一个名称，称为文件名，以便人类能够告诉计算机访问哪些磁盘块。文件可以被组入目录，而目录又可以分组成更大、更具包容性的目录。

操作系统使用户户能够运行应用程序并执行系统功能，如创建目录和复制文件。操作系统负责调度和运行计算机上的所有任务。它允许用户登录并使用系统。它控制所有系统资源，如内存、磁盘文件、磁带驱动器、CD-ROM 驱动器、调制解调器、打印机、终端和网络连接。UNIX、MS-DOS、Windows 95、Windows NT 和 Apple Macintosh 都是今天常用的不同操作系统的示例。UNIX 是一个操作系统而不是应用程序，因此不要期望在 Windows 系统上找到它作为一个程序。

许多用户对可用应用程序的了解远比对可用操作系统及其功能的了解深入。当你首次启动系统时，在运行任何应用程序之前，必须启动操作系统。这个启动操作系统的过程被称为“唤起系统”（bringing up the system）；也称为“启动”（booting up）。在启动过程中，操作系统会初始化所有设备，这意味着它向它们发送任何所需的指令，以便它们准备好使用。系统启动后，操作系统对大部分或所有系统硬件具有完全控制权——尤其是磁盘驱动器。当应用程序想要访问或在磁盘驱动器上创建文件时，它们并不这样做。相反，它们请求操作系统代它们完成。多个应用程序可以同时访问不同的文件。操作系统跟踪哪些程序在使用哪些文件。如果多个程序同时请求访问磁盘，操作系统将决定优先处理哪个请求。操作系统还会确定用户是否有权限访问某个文件，如果没有权限则阻止访问。

## 工具程序

工具程序（Utilities）是较小的、独立的程序，通常范围较窄，提供单一能力或单一功能领域，例如备份工具。工具程序可能与操作系统或应用程序强耦合，意味着它们是必不可少、不可替代的一部分。工具程序也可能是松耦合的，例如该工具是可选的、需要额外付费的、共享软件或免费软件、必须从互联网下载，或者由与提供操作系统或应用程序的不同的公司销售。

## UNIX 的历史

20 世纪 60 年代后期，开发了一种使用计算机的新方法，称为分时系统。在分时系统中，计算机可以通过给每个任务分配有限的时间来同时运行任务。分时系统使用户能够能够直接与计算机交互。计算机可以立即向他们显示程序中的任何错误，他们修正错误并重新运行任务而无需长时间等待。贝尔实验室联合电气（GE）和麻理工学院（MIT）开发了一个名为 Multics 的分时系统。然而，在 1969 年被取消了，因为 Multics 太复杂且太困难。汤森（Thompson）、里奇（Ritchie）和其他贝尔实验室的人继续开发他们自己的分时系统。

当时开发了许多其他计算机操作系统。更快、更强大的计算机正在开发中。在那个时代，每台新计算机都有自己独特的操作系统。每当计算机制造商开发一台新计算机时，它也必须提供一个运行在该计算机上的操作系统。它还会提供运行在该操作系统上的新工具程序和应用程序。这些被称为“专有系统”（proprietary systems），因为计算机制造商拥有在该计算机上运行的唯一操作系统。用户被锁定在该供应商处，由其为该机器提供基础且必要的软件。

UNIX 故事中的一个关键事实是，当时 AT&T 由于法律限制无法扩展到计算机业务。因此，AT&T 没有开发和销售自己的计算机系统。他们从其他公司购买计算机。因为他们在越来越多的多的计算机上使用 UNIX，他们想找到一种方法，将其轻松移动到他们可能购买的不同计算机上运行。




大多数操作系统，包括早期的 `UNIX`，都是用汇语言编写的。汇语言被称为低级计算机语言，因为每条指令都是计算机硬件的基本操作。低级语言通过寄存器和内存访问工作，而这些构成了计算机的基础操作。因此，汇语言程序员可以编写出非常紧凑且高效的循环——这对于反复使用的操作系统代码至关重要。诸如 `BASIC`、`FORTRAN` 和 `COBOL` 等高级语言则与机器级相去甚。它们提供的编程工具和概念使得编写程序变得容易得多，但产生的代码没有汇语言代码那样高效。

汤普（Thompson）和其他人意识到，随着新计算机的出现，能够将 `UNIX` 移植到这些计算机上运行是极其重要的。他们还意识到，如果继续用汇语言编写 `UNIX`，那么将整个系统移植到新计算机将花费过多的精力。汤普开发了一种名为 `B` 的语言，里奇（Ritchie）对其进行了改进并将其命名为 `C`。到 1973 年，他们已经用这种新的、级 `C` 编程语言重写了几乎所有的 `UNIX`，而这种语言在编写操作系统代码时仍然非常高效。他们现在可以在几种不同类型的计算机上提供相同的操作系统。他们继续为 `UNIX` 添加新功能，撰写关于 `UNIX` 内部的论文，并将其提供给对设计概念以及能够在许多计算机上运行这一事实感兴趣的大学。大学和其他计算机公司开始使用并扩展 `UNIX` 以满足自身需求，提供了 `UNIX` 的新特性和变体。

我第一次在 20 世纪 80 年代中期遇到 `UNIX`。我是一个操作系统小组的成员，为 `Point 4` 微型计算机编写并支持一种专有操作系统。在当时，我们的整个专有操作系统和所有用户数据都可以放入一个 20MB 的磁盘驱动器中。它只需要 128KB 的内存即可运行。`UNIX` 对当时的专有系统并不构成威胁，因为 `UNIX` 需要更多的磁盘空间、内存和 CPU 功率；因此，它的性价比不高。所有计算机制造商都提供自己的高度优化的专有操作系统，这些系统可以在最小磁盘和最小内存下运行。这些专有时分系统仍然将计算机用户锁定在某一家公司的计算机产品中。这导致了高价格，因为这家公司必须承担所有的程序开发；因此几乎没有竞争。

到 1990 年，计算机格局发生了巨大的变化。`UNIX` 赢得了与专有系统的战斗。内存和磁盘的硬件成本下降了很多，使得 `UNIX` 需要的额外内存和磁盘不再是一个主要的考虑因素。`UNIX` 的大卖点在于它是一个开放系统，这意味着用户不再被锁定在专有系统中。由于 `UNIX` 是用高级语言编写的，它可以轻松地移植到其他类型的计算机上，在旧计算机上运行的所有应用程序也可以轻松地移植到新计算机上。开放 `UNIX` 系统的价格比专有系统有竞争力得多。同时，由于贝尔实验室（Bell Laboratories）、伯克利（Berkeley）等大学以及太阳微系统公司（Sun Microsystems）等公司的共同努力，`UNIX` 拥有一极其丰富的工具和功能。随着 `UNIX` 势头增长，编写新软件应用程序的公司选择为 `UNIX` 平台编写程序，以便他们的软件可以在各种硬件上运行，这再次加速了专有系统的终结。尽管某些计算机供应商仍提供或支持专有操作系统，但他们通常也提供一种替代的 `UNIX` 产品线。

### UNIX 如何构建互联网

互联网（`Internet`）起源于国防部（`DARPA`）的一个项目，旨在连接政府、军事和大学计算机。随着网络主机系统数量的增加，他们需要一种有效的方法将信息以包的形式从一个系统通过网络中的其他系统发送到目的地。随着网络的增长，他们需要动态路由来绕过糟糕的连接。开发的数据包路由协议被称为 `TCP/IP`，最早在加利福尼亚大学伯克利分校的 `UNIX` 中实现。`UNIX` 和 `TCP/IP` 成为互联网的骨干，将成千上万乃至数百万计算机连接在一起。`UNIX` 和互联网上的其他服务器通过万维网（`World Wide Web`）提供了大量的数据、研究、新闻、时事和人文类内容。通过这种方式，数百万在使用 `UNIX` 系统的人甚至根本不知道它的存在。

### 有哪些类型的 UNIX 系统？

当计算机供应商将 `UNIX` 移植到自己的机器上时，他们通常会给它一个独特的名称。下节提供了销售 `UNIX` 系统的计算机公司部分列表（无顺序）。此列表显示了供应商是否给 `UNIX` 起起了特殊名称，以及他们是否给所售的系统起起了特殊名称。

#### 表 1.1 部分销售 UNIX 的公司

| 计算机公司 | UNIX 操作系统 |
| :--- | :--- |
| AT&T | `UNIX SVR3` |
| AT&T | `UNIX SVR4` |
| 太阳微系统/SunSoft | `SunOS`（作为 `Solaris` 的组件） |
| 太阳微系统/SunSoft | `Interactive UNIX` |
| 惠普公司 (HP) | `HP-UX` |
| Data General (DG) | `DG-UX` |
| Novell | `UnixWare`（早期版本） |
| Santa Cruz Operation (SCO) | `UnixWare` |
| Santa Cruz Operation (SCO) | `OpenServer` |
| Santa Cruz Operation (SCO) | `XENIX` |
| 微软 | `XENIX`（早期版本） |
| IBM | `AIX` |
| 硅图形 (SGI) | `IRIX` |
| 数字设备公司 (DEC) | `ULTRIX` |
| 数字设备公司 (DEC) | `Digital UNIX` |




# NCR | NCR UNIX

| NCR | NCR UNIX |
| :--- | :--- |
| 西门子数字信 (SNI) | Reliant UNIX |
| Caldera | Caldera OpenLinux |
| RedHat Software | RedHat Linux |
| 非商业来源 | UNIX o/s |
| 加州伯克利大学 | BSD (伯克利软件发行版) |
| FreeBSD 项目 | FreeBSD |
| 自由软件基金会 | GNU/Linux |
| Linus Torvalds | Linux kernel |
| Debian | Debian GNU/Linux |

列表并非完整。例如，Bull 和摩托罗达等其他公司销售使用 `AIX` 操作系统的计算机系统。Unisys 销售运行 `UnixWare` 的计算机。其他备受尊敬的公司也销售 UNIX 和 Linux 系统。列出的某些产品可能是已被新产品取代的老产品。列出的某些公司可能不再销售所列的特定 UNIX 产品。

### 非 AT&T UNIX

当你观察 UNIX 系统首次通电时，你可能会看到一长系列版权声明，感谢多年来为 UNIX 贡献软件的各种公司和组织。你可能看到的版权声明之一来自加州大学摄政委员会，感谢他们在伯克利大学在 UNIX 上所做的大量工作。在该大学产生的 UNIX 被称为 `BSD`，即伯克利软件发行版。

第 21 页

许多 BSD 工具已成为所有 UNIX 软件包的标准。FreeBSD 是 BSD 的扩展，其中受版权保护的 AT&T UNIX 代码已被删除或重写，以便其可以在没有通常 UNIX 版税和源代码限制的情况下发行。有关更多完整信息，请参阅网络上的 `www.freebsd.org`。

Linus Torvalds 编写了自己的 UNIX 内核，这是操作系统的主要执行部分。他将内核命名为 `Linux`；尽管它模拟了 UNIX 的主要功能，但它没有使用任何限制的代码。他的内核与自由软件基金会的 `GNU` 项目工具一起发行，该项目代表 `GNUs` 而非 UNIX。该项目的目标是创建一个自由的 UNIX 系统。它创建了许多重要的自由软件工具，如 `GNU C Compiler` 和 `GNU emacs` 文本编辑器。将 `Linux` 内核与 `GNU` 工具结合，最终创建了一个完全没有 AT&T UNIX 版权和版税的完整类 UNIX 系统。此版本的 UNIX 可用于商业目的。它受名为 `GPL` 的特殊许可限制，该许可防止操作系统的源代码受到限制或版权化。有关更多完整信息，请参阅 `www.gnu.org` 和 `www.linux.org`。

商业 UNIX 系统通常运行在支持大量用户的昂贵计算机上。它们通常由计算机操作人员维护。普通用户甚至看不到 UNIX 机器，只能看到连接在上面的终端。所有的系统管理功能都由计算机人员完成。普通用户甚至无法查看大多数系统配置文件。相反，这些自由的非 AT&T UNIX 系统允许 UNIX 加载到家用计算机上。用户可以安装并管理自己的个人 UNIX 系统。事实上，他们通常没有选择，因为家庭很少有自己的数据处理部门。这些自由 UNIX 系统可以作为 Web 服务器、电子邮件处理器或 `DNS` 服务器连接到互联网。一些公司为自由 UNIX 添加新模块，使其与新硬件同步。一些公司提供商业支持。

第 22 页

尽管如此，在大型企业中使用自由 UNIX 仍然存在犹豫情绪。尽管如此，这种 UNIX 在 UNIX 的演变中起着重要作用。

### UNIX 如何区别 MS-DOS/Windows

从一开始开始，UNIX 被设计为一种多用户、分时操作系统，可以高效处理多个用户。个人电脑（或 PC）是沿着完全不同的路径开发的。PC 有一个键盘、一个屏幕和一个鼠标；因此它们仅适应单用户。在 MS-DOS 或 Windows 下支持单用户的同一处理器，在 UNIX 下可能可以支持 100 个用户。

Windows 软件的外观和感受与传统的基于字符的 UNIX 软件非常不同。如果 Windows 用户启动任务，处理器通常会有大量的剩余功率；因此，Windows 用户习惯了忙碌的屏幕和以图形方式显示任务进展的彩色指示。相比之下，传统的 UNIX 在任务完成之前输出的消息很少。请记住，当 UNIX 运行你的任务时，它可能同时运行着其他 100 个任务。任何浪费的努力或输出都会减慢他人的速度。

今天，UNIX 和 Windows 之间的差异不再那么明显了。许多 UNIX 系统是单用户工作站，用户利用鼠标点击图标并操纵窗口。某些 Windows 系统直接为从串口或另一台 Windows PC 登录的用户运行任务。某些 Windows NT 和 UNIX 服务器完全没有直接用户。它们为网络提供服务，如打印共享、文件共享、电子邮件或互联网访问。许多 UNIX 系统可以运行 Windows 程序（例如，通过 `WABI`）。许多 Windows 系统可以运行 UNIX 工具，如 `vi`、`awk` 和 `shell`（通过 `MKS` 工具）。

第 23 页




UNIX 和 Windows 之间的一个主要区别是用户从哪里获取系统应用程序。在本地 PC 商店，可以获得广泛的通用实用程序。无论你从事什么行业，文字处理、电子表格和支票簿对账等程序通常都是实用的。相反，你很少能在 PC 商店找到任何 UNIX 应用程序。UNIX 的强大之处之一是它是为特定行业编写自定义软件的极佳平台。UNIX 支持许多编程语言、数据库和程序开发工具。它是一个开放系统，因此可以运行在许多不同的硬件系统上。UNIX 开发人员通常研究某一个行业，例如牙科诊、木材店、汽车配件店或花店。他们创建一系列应用程序，将该特定业务所需的所有功能计算机化，并使用所需的术语、特殊规章、表格和会计方法。我们可以将这些称为**垂直应用**：针对一个目标业务的完整应用集；而 PC 商店通常销售的是**水平应用**，即一个应用程序具有足够的通用性，适用于广泛的业务。软件开发者使用 UNIX 创建一个交钥匙系统，即终端用户只需转动钥匙开启系统，然后使用提供的自定义程序来运行其业务。

如今，Windows 系统正在相互联网，以提供 UNIX 提供的多用户功能。软件开发者正在创建 Windows 图形多用户程序，其视觉效果和体验比传统的 UNIX 字符应用程序更时尚。UNIX 可以通过特殊的 X Windows 工作站支持图形应用程序；然而，这些工作站无法运行 PC 商店的 Windows 软件。在太阳科技（Sun Microsystems）及其对 Java 语言的支持下，人们正努力利用万维网的成功提供多用户图形 Web 应用程序。通过 Web 浏览器运行应用程序提供传统 UNIX 字符应用程序所缺乏的时尚图形视觉效果的一种方法。这些应用程序可以在局域网上运行，也可以在互联网上运行。它们可以在低成本的网络计算机上运行，这些是专门为运行浏览器应用程序而设计的最小计算机站。主机服务器可以是 Windows 或 UNIX；这对于软件开发公司非常有吸引力。基于浏览器的应用程序会成为新的应用标准吗？只有时间能给出答案……

## UNIX 标准与修订

表 1.1 列出了许多修改 UNIX 并以 UNIX 以外的名称发行操作系统的公司，例如 `HP-UX` 或 `SunOS`。在书中，你有时会看到完成某项任务的两种或三种方法，因为某些类型的 UNIX 计算机只能以第一种方式完成，某些只能用第二种，而某些只能用第三种。在一家公司里，你可能经常使用几种不同类型的 UNIX 服务器，其命令存在此类差异。如果你连接到互联网等广域网，你会遇到更多 UNIX 主机，其 UNIX 与你习惯的略有不同。起初你可能会发现这种多样性令人困惑。

作为回答，让我描述一下 UNIX 就像汽车收音机。所有的汽车收音机都可以播放音乐、调节音量和换台。然而，它们在旋钮、按钮或滑块的位置和使用上有很大差异。音量控制并不总在左侧。但如果你租了一辆车，通常仍然可以让收音机工作。人们习惯于拨弄控制装置，直到实现他们想要的功能。同样，当你在一个命令与你习惯的 UNIX 略有不同的系统上工作时，不需要恐慌。在了解主要变体后，如果命令以某种方式不起作用，你只需尝试其他标准方法。

标准化 UNIX 的努力随处可见，试图在不同的硬件和供应商平台上统一命令。`POSIX` 是来自一个名为 `IEEE` 的组织的标准，许多类型的 UNIX 都遵循该标准。国际组织 `X/Open` 提供了 `X3`、`X4` 和 `Spec11` 等 UNIX 标准。许多公司如 `IBM`、`HP` 和 `Sun` 采用了通用桌面环境 (`CDE`) 来为 UNIX 提供统一的外观和体验。`SVID`（System V Definition）是另一种让 UNIX 更统一的标准。它有助于了解 UNIX 如何演进，以预判在未知系统中可能会出现哪些变化。

最初，UNIX 是在 AT&T 贝尔实验室开发的，他们将这些名称赋予 AT&T UNIX 的连续修订版本：
- 第六版 (Sixth edition)
- 第七版 (Seventh edition)
- `System III`（他们跳过了 `System IV`）
- `System V`（罗马数字五）
- `System V, Release 2`（缩写为 `SVR2`）
- `System V, Release 3` (`SVR3`）
- `System V, Release 4` (`SVR4`）

`SVID` 描述了基于 AT&T `System V UNIX` 的 UNIX 标准。

在 AT&T 开发的同时，加州大学伯克利分校正在修改 UNIX 的早期版本。他们的 UNIX 版本是 `BSD`，代表伯克利软件发行（Berkeley Software Distribution）。`BSD` 为 UNIX 增加了许多重要功能，但其中一些功能与 AT&T 添加的新功能重叠。今天，所有 UNIX 系统都可以根据它们基于 System V UNIX 还是 BSD UNIX 的程度进行分类。目录 `/etc/rc2.d` 的存在表示基于 System V 的 UNIX，而该目录的缺失通常表示基于 BSD 的 UNIX。以下是某些 System V 和 BSD 之间特定命令差异的示例：





# System V 与 BSD 打印

| System V | BSD |
| :--- | :--- |
| `shutdown -g3 -i0 -y` | `shutdown -h +3` |
| `lp -dlaser2 -n2 acme` | `lpr -Plaser2 -#2 acme` |

如果你的系统不支持用于打印的 System V `lp` 命令，它可能使用的是 BSD 的 `lpr` 命令。某些系统同时支持这两个打印命令。例如，SunOS rev 4 是一个 BSD UNIX 变体。其下一个主要版本 SunOS rev 5 从 BSD 切换到了 SVR4，该版本结合了 (System V) SVR3、XENIX、BSD 和 Sun 的特性。SunOS rev 5 仍然支持 rev 4 BSD 版本的工具作为可选替代方案。SunOS rev 5 的用户可以自定义他们的 UNIX 会话，以便默认使用 System V、BSD 或 XPG4 版本的工具。（这是通过更改 `PATH` 变量来实现。）

## 另请参考
- *关于 `PATH` 变量的更多信息，请参阅第 97 页*

## AT&T 之后的 UNIX
最初，AT&T 开发并许可了 UNIX，控制着限制性的源代码，并向销售 UNIX 的公司收取版税。1991 年左右，AT&T 创建了一家名为 UNIX System Laboratories 的公司负责此。1993 年左右，Novell 从 AT&T 手购买了 UNIX。Novell 整合了部分 NetWare 技术并创建了基于 SVR4 的 UnixWare。Novell 将 UNIX 商标转给了 X/Open Company Ltd.，该公司发布标准并认证某个 UNIX 版本是否符合标准。Novell 保留了许可 UNIX System V 源代码的权利。1995 年左右，Santa Cruz Operation (SCO) 从 Novell 手购买了 UNIX。随后，SCO 有两个主要的 UNIX 支持分支：它自己的 OpenServer 和 UnixWare。今年（1998 年），SCO 与若干主要的 UNIX 供应商联合发布 UnixWare 7，该版本包含了 UNIX 的下一个主要版本：SVR5，这是一个 64 位 UNIX 操作系统。这并不是唯一的 64 位 UNIX 操作系统，因此 UNIX 市场仍然存在着良性竞争。

## 你必须掌握的重要 UNIX 概念
以下章节涵盖了你需要理解的 UNIX 系统的基本特性。

### 内核 (Kernel)
在图 1.1 中，你可以看到 UNIX 系统表示为三个同心圆。最内层的圆被称为内核，指的是操作系统的核心。内核是操作系统中最隐藏的部分。它包含了被称为驱动程序的代码；这些程序允许系统控制所有硬件、磁盘等。

![UNIX kernel, utilities, and shell](img/8bf015b4f90d6fffa18dc.gif)

下一个圆代表系统工具和命令。当你运行像 `vi` 这样的命令时，它使用内核内部的程序在你的屏幕上显示输出、从键盘获取输入并在磁盘上保存文件。

### UNIX 外壳 (Shell)
最外层的圆代表 UNIX Shell。Shell 是一个接受用户命令并启动所请求命令的程序。Shell 是用户看到的 UNIX 操作系统的全部——就像你观察鸡蛋或坚果时，你看到的只是外层，而看不到内部的复杂性。Shell 不仅仅是传递你输入的命令。Shell 允许用户在后台运行命令；这意味着在命令运行时用户的工作站不会被占用。Shell 允许用户使用通配符来指示应该处理哪些文件。Shell 实际上支持一种完整的编程语言，允许根据其他命令的结果执行条件执行命令，并使用循环来重复命令序列。

UNIX 上实际上有许多 Shell 程序，不同的用户可以同时使用他们偏好的、不同的 Shell。下表中的前三个 Shell 通常在大多数商用 UNIX 系统上可用。

### 表 1.2 可用的 UNIX Shell

| Shell 名称 | 命令 |  |
| :--- | :--- | :--- |
| Bourne shell | `sh` | 在所有 UNIX 系统上可用 |
| C shell | `csh` | 类似于 C 语言的语法 |
| Korn shell | `ksh` | Bourne shell 的超集 |
| Bash shell | `bash` | 包含 C shell 和 Korn shell 的特性 |
| tcsh shell | `tcsh` | 类似于 C shell |

由于每个 Shell 都是系统工具，你只需要输入表 1.2 所示的命令即可开始使用特定的 Shell。




尽管 C shell 在用户便利性方面比 Bourne shell 有所改进，但它的某些语法与 Bourne shell 不兼容。由于 Bourne shell 脚本非常常见，C shell 用户必须学习这两种 shell 的语法并避免混淆它们。

Korn shell 提供了与 C shell 相似的用户便利性。它具有强大的命令行编辑能力（这是 C shell 并不具备的），可以使用 `vi` 或 `emacs` 编辑命令，这允许你检索之前的命令、对它们进行编辑并执行。Korn shell 是 Bourne shell 的超集，因此它们之间没有语法冲突。Korn shell 比 Bourne shell 提供了更强大的编程结构。然而，如果你需要在未提供 Korn shell 的旧版 UNIX 系统上运行程序，则应避免使用这些结构。

## Shell 提示符

要使用 UNIX 系统，系统管理员（称为 `root`）必须为你创建一个供使用的账户。UNIX 会话的开始看起来大致如下：

```
acme login: fred Password:
TERM = (vt100)
$ _
```

在登录提示符处，你必须识别身份并输入密码（出于安全考虑，输入时将不会显示）。美元符号（`$`）是 shell 提示符，表示 UNIX 已准备好让你输入命令。美元符号（`$`）后面的下划线字符（`_`）代表等待输入的光标。以下是标准的 shell 提示符：

- Bourne shell 或 Korn shell：`$`
- C shell：`%`
- 无论什么 shell 的 root 登录：`#`

shell 提示符可以自定义包含你的系统名称、当前目录或其他字符。以下是你可能会遇到的一些 shell 提示符：

```
acme$ _ /usr/fred> _
[acme] _
```

你必须处于 shell 提示符处才能输入命令。你也可以像第 5 章描述的通过图形界面（GUI）使用 UNIX。警告：`root` 登录是全能系统管理员。如果你是新手，请远离 `root` 登录。如果你以根身份出错，可能会崩溃或损坏你的 UNIX。

## Shell 变量

shell 支持变量。单词、短语和其他信息可以保存到命名变量并在以后使用。某些变量对 shell 有特殊含义，并控制系统的运行。例如，`TERM` 变量应该设置为你正在使用的终端类型；否则，屏幕输出可能包含乱码。许多 shell 变量使用全大写字母，以避免与 UNIX 命令（通常为小写）混淆。

## 标准输出、标准错误、标准输入

UNIX 下程序程序不会直接将消息显示在屏幕上。相反，它们调用一个特殊的输出程序，称为标准输出（简称 `stdout`）。`stdout` 通常设置为输出到你的屏幕，但 `stdout` 可以轻松重定向到打印机等设备或磁盘文件。这是 UNIX 真正优雅的元素之一。程序和工具将其输出到 `stdout`，因此它们不知道输出实际上去了哪里。shell 可以根据需要将 `stdout` 重定向到设备或文件。

```
cal
$ cal > /dev/lp0
$ cal > /usr/year
```

在第一个示例中，`cal` 将日历输出到 `stdout`。在第二个示例中，大于号（`>`）将 `stdout` 重定向到打印机设备（`/dev/lp0`）。在第三个示例中，`stdout` 被重定向到磁盘文件（`/usr/year`）。

还有一个用于显示错误消息的特殊程序。这被称为标准错误（简称 `stderr`）。`stderr` 通常发送到你的屏幕，以便你可以看到任何错误消息。但同样，shell 可以轻松地将 `stderr` 重定向到设备或文件，而不受 `stdout` 的影响。

有一个用于执行输入的特殊程序。这被称为标准输入（简称 `stdin`）。如果程序从 `stdin` 获取输入，shell 可以通过从设备或磁盘文件重定向来提供这些输入。例如，如果一个工具在开始运行之前总是问三个问题，你可以将问题的答案放入磁盘文件，然后重定向该磁盘文件以提供输入，这样你就不需要自己输入内容了。

## 管道与过滤器

一个命令的 `stdout` 可以被重定向为另一个命令的 `stdin`，创建从一个命令到另一个命令的直接管道。我们称这种操作为*管道*，并使用竖线（`|`）作为管道符号。

```
ls | pg
```



在前面的示例中，`ls` 是列出当前文件的 UNIX 命令。如果你单独运行 `ls` 且文件超过 25 个，某些名称会在你读到它们之前就超出屏幕。`pg` 是一个逐页显示输出的 UNIX 命令。它在显示下一页之前会等待用户输入。我们可以将 `ls` 的输出直接管道传输到 `pg`，这样我们就可以一次查看一个文件名了。

某些 UNIX 命令显示的信息非常多，以至于我们正在寻找的行会丢失。`grep` 是一个只显示包含所需模式的行的 UNIX 命令，如下例所示：

```bash
ls | grep acme
```

在前面的示例中，`ls` 将输出所有文件。这些文件不会直接显示在屏幕上，而是被管道传输到 `grep`。`grep` 只显示名称中某个包含 `acme` 的文件名。`grep` 就像一个咖啡过滤器。热水和咖啡渣都进入过滤器。过滤器过滤掉我们不需要的东西（咖啡渣），并让我们需要的东西（咖啡液）通过。同样地，`grep` 过滤器过滤掉了我们不需要的行，并只通过包含所需模式的行。*过滤器*一词可以用于任何可以在管道中使用并按需修改输出的 UNIX 工具。

## 用户与组

UNIX 是一个多用户系统。通常，每个用户必须使用唯一的登录名称登录，以便系统知道是谁刚刚登录了。该系统会跟踪该用户的文件和邮件。

组是用户的集合。用户可以属于多个组。每个组都有一个组名。每个文件都有所有者：拥有该文件的用户。每个文件属于属于组，该组通常是创建文件用户的主组。第 11 章“文件权限与系统安全”将更详细讨论用户、组和权限。

## 获取 UNIX 访问

商业 UNIX 往往运行在数据处理部门昂贵的计算机上。公司和机构可能提供供你登录 UNIX 服务器的终端。然而，在使用 UNIX 系统之前，你必须获得一个 UNIX 账户。

Linux/GNU 和 FreeBSD 是非 AT&T 的 UNIX，它们通过杂志、电脑交易市场、PC 商店、技术商店、订购以及互联网销售。你可以通过互联网从 `www.sco.com` 获取免费的 SCO 许可。你还可以以低廉的价格订购安装媒体。此优惠仅用于非商业用途。Sun 还为 Intel 计算机提供了其操作系统的成本非商业版本，称为 Solaris x86。这些 UNIX 系统可以加载到家用计算机上。然而，这个过程需要一个可用的分区，并且不适合初（Linux 可以加载到 DOS 系统或直接从 CD-ROM 运行）。如果你在同一台计算机上运行 Windows，除非你有信心在万一出错时恢复 Windows 和所有文件，否则不要加载 UNIX！如果你加载了自己的系统，你将学习到关于 UNIX 和计算机的大知识。

## 遵循 UNIX 之道

以下是一些帮助你适应 UNIX 的通用规则。

## 没有消息就是好消息

由于一个命令的输出通常作为输入管道传输到另一个 UNIX 命令，因此命令不会输出不必要的消息。如果命令执行成功，它会直接返回 shell 提示符而没有任何其他输出。不要期待完成消息或状态消息。另一方面，如果产生了任何输出，这就是引起警报的原因。仔细研究任何输出，因为这可能是出现错误的指示。

## 命令是构建块

许多 UNIX 命令看起来是原始的或未完成的。将它们想象成原始的构建块。你可以通过在管道中放置一系列命令来创建你自己的命令。大多数命令没有打印选项，因为你可以将输出管道传输到打印机。大多数命令没有排序选项，因为你可以将输出管道传输到 `sort`。

### 最少按键

UNIX 允许熟练的用户使用最少的按键完成奇迹。你可以在常用命令中看到这种减少按键的趋势：
- `ls`（列出文件）
- `rm`（删除文件）
- `cp`（复制文件）
- `mv`（移动文件）
- `cd`（切换目录）
- `pg`（分页显示输出）




# 第 2 章：UNIX 目录与路径
作者 Steve Mor Moritsugu

## UNIX 目录树结构

### 标准 UNIX 目录
###绝对路径和相对路径切换目录
### 切换到主目录
### 切换到父目录
### 创建和删除目录
### 快速访问常用目录

## 介绍 UNIX 目录树结构

UNIX 在一个或多个磁盘驱动器上存储用户数据等信息。每个磁盘驱动器的容量通常以兆字节（MB）为单位，每兆字节等于一百万个字符。例如，一个 500 MB 的硬盘可以存储 50,000 份文档，每份文档有 10,000 个字符。某些磁盘驱动器的容量以千字节（`1 GB = 1000 MB = 1,000,000,000 字符`）甚至太字节（`1 TB = 1000 GB = 1,000,000,000,000 字符`）为单位。![ad91af06ad96c57f0a338bded4c42f0e.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif)

### 变化速度有多快
当我开始接触计算机时，我的系统只有 10 MB 的磁盘空间。今天，一个名为 UnixWare 7 的新 UNIX 版本规格说明它支持 76,800 TB 的磁盘空间。这比我旧的 10 MB 硬盘大了 76 亿倍。太惊人了！

由于有这么多数据需要跟踪，所有这些信息都被分成了相关信息的集合，称为文件。如果你写一封信给亲戚，这封信的内容将全部存储为一个文件。文件在系统中可以发挥不同的功能。有些文件是文档，有些是程序，有些是数据文件或其他类型。UNIX 下每个文件都有一个名为 inode 号（参见术语表）的数字，UNIX 用它来访问文件。为了方便人类操作文件，每个文件也可以通过名称进行访问。

旧版本 UNIX 的文件名只能包含 14 个字符。大多数现代 UNIX 系统允许更长的文件名，有时可达数百个字符。文件名可以开头或包含任何字母、数字、标点符号或空格，但在实践中，应避免在文件名中使用空格和大多数标点符号，因为这会让它们在命令行中难以使用。

UNIX 系统可能有成上万万甚至更多文件需要跟踪。为了简化这一点，文件被分组为相关文件的集合，称为目录。将目录想象成文件夹或容器，你可以将相关文件放入其中。例如，如果你给你的阿姨 Alice 写了 20 封信，你可以将这 20 个文件放在一个名为“阿姨信”的目录中。我可能会将目录命名为 `auntAlice`，因为我不希望在文件或目录名称中包含空格。同样，目录可以组合在一起并放入更大的目录中。例如，我可以创建一个名为 `correspondence` 的目录，其中包含 `auntAlice` 目录。

### 根目录包含所有其他目录
根目录始终由单个斜杠 `/` 表示。每当你看到 `/` 符号时，请将这个 `/` 想象成生长在地下的树根，固定着我们的树形结构。

### 寻找名称的路径（全路径）
图 2.1 显示了三个从根目录 (`/`) 出的文件：
- `report`
- `usr`
- `tmp`

图 2.1 UNIX 目录树结构。

有关 `PATH` 变量的更多信息，请参阅第 97 页。




我们说这三个文件位于根目录下。在真实的 UNIX 系统中，根目录下会有更多文件，因此图 2.1 仅向你展示了示例 UNIX 目录树的一部分。

`usr` 和 `tmp` 目录包含图 2.1 所示的其他目录和文件。在 UNIX 中，目录以文件的形式存在于磁盘上，该文件负责跟踪该目录的内容。因此，目录是一种特殊类型的文件。

还有其他类型的文件。例如，字符设备节点和块设备节点文件允许 UNIX 访问系统中的硬件设备。UNIX 系统上的大部分文件被称为普通文件，即包含文本、数据或程序的文件。次于常见的文件类型是目录。所有其他类型的文件（如设备节点文件）都很少遇到。

在图 2.2 中，显示 `tmp` 目录包含一个名为 `report7` 的普通文件。注意，根目录（`/`）也包含一个名为 `report7` 的普通文件。事实上，我们的树示例显示了位于不同目录下的四个 `report7` 文件。只要位于不同的目录，UNIX 允许不同内容拥有相同的文件名。

在任何一个目录下，所有文件名必须是唯一的。无论该文件是否为目录都是如此。出于这个原因，我无法在根目录下同时拥有一个名为 `usr` 的普通文件和一个名为 `usr` 的目录。

不要将 UNIX 目录名与 DOS 目录名混淆。

DOS 使用类似的目录树，也从根目录开始增长。然而，DOS 使用反斜杠（`\`）作为根目录和分隔目录名的符号，而 UNIX 使用斜杠（`/`），它也被称为正斜杠（`/`）。

图 2.3 突出了我们树中的其中一个 `report7` 文件。文件的完整名称包含了为了获取所需文件而必须经过的所有目录。你可以看到，这一系列被高亮显示为链的目录形成了一条穿过树的路径，通向你想要的文件，因此我们称这种名称为全路径。有了全路径，就不必担心有人误认为你指的是树中的其他某个 `report7` 文件。全路径也被称为绝对路径。

图 2.3 全路径 `/usr/fred/report7`。

UNIX 中的目录

在大多数 UNIX 系统上，你都会遇到一些标准目录名。我已经提到过，所有的 UNIX 系统都会有一个根目录（`/`）。

标准 UNIX 目录名

`/tmp` 和 `/usr/tmp` 目录被系统用于存储临时文件。用户也可以在那里存储临时文件，但要小心，系统可能会定期清理（或删除）`tmp` 目录中的旧文件，且无任何警告。文件会在 `/tmp` 中保留多久呢？系统经常会删除 `/tmp` 或其子目录下 7 或 14 天未被访问的文件。有时，系统管理员在面临磁盘空间突然不足时，会不分时间地删除 `/tmp` 中的所有文件。

`/dev` 是根目录下的一个目录，包含访问硬件（如磁带驱动器软磁盘）的特殊节点。这些设备节点可以存在任何地方，但按照惯例被存放在 `/dev` 或其子目录下，以提醒我们处理的是设备而不是普通文件。

`/bin` 是根目录下的一个目录，存放系统实用程序，例如 `ls` 命令。`bin` 是二进制可执行文件的缩写。今天，`bin` 术语也可以用于命名其他可执行文件目录，无论它们是二进制文件还是文本文件，例如 `/usr/bin`。

`/usr` 是根目录下的一个目录，存放用户文件以及支持用户程序所需的系统实用程序。例如，`/bin` 存放基本系统运行所需的实用程序，而 `/usr/bin` 存放用户和用户程序所需的系统实用程序。`/usr/lib` 存放有用系统表和子程序的库。`/usr/spool` 存放置池文件，这些是排队打印文件的临时副本，一直保留到打印完成。`/usr/spool` 还存放许多其他系统进程（如 uucp）持有的临时文件。`/usr/bin`、`/usr/lib` 和 `/usr/spool` 是操作系统的重要部分，将 `/usr` 专门用于系统并将实际的用户数据和程序放在其他目录中通常是明智之举。




### SVR4 (Solaris) 中的新目录

`lost+found` 是根目录及其他目录下的一个目录，当系统崩溃导致文件名丢失时，系统会将文件数据存储在这里。如果你在系统崩溃后丢失了重要数据，可能会在这里找到它们。

`/home` 是一个专门用于用户主目录的目录，用户可以在其中存储个人文件。（请参阅下文关于主目录的章节。）

`/sbin` 和 `/usr/sbin` 包含专门用于系统管理和系统操作的可执行文件。

`/stand` 是某些 SVR4 系统（但不是 Solaris）上的特殊目录，专门用于存放 UNIX 内核和启动文件。

`/var` 包含系统变量信息文件，即内容随时间变化的临时文件和日志。`/var` 取了旧的 `/usr/spool` 目录。

# 切换到另一个目录

能够在 UNIX 目录树中自由移动对于 UNIX 用户来说是一项非常重要的技能。

### 切换目录并查看其内容 (cd, ls)

如果你每次引用文件都必须指定完整路径，那么 UNIX 将变得非常难用。一如既往，UNIX 有一种快捷方式来减少输入量。你可以指定一个目录作为我们的当前目录，这允许我们在不提供完整路径的情况下引用该目录中的文件名。当前目录充当默认目录，因为当你没有指定使用哪个目录时，系统就会使用它。

当前目录的其他名称为：
- 工作目录 (working directory)
- 当前目录 (present directory)
- 当前工作目录 (present working directory)
- 默认目录 (default directory)

想象一下，我们已经开始从根目录沿着 UNIX 树行走，并决定某处停下来，看看从那个角度可以看到什么。想象你正坐在树的某个分支上。你只能坐在目录里，而不能坐在文件中。你所在的目录被称为你的当前目录。我们可以使用 `cd` 命令加上想要切换的目录名称来更改当前目录。在图 2.1 中，如果我执行：

```
cd /usr/fred
```

那么我的当前目录将变为 `/usr/fred`。通过切换到 `/usr/fred`，你可以轻松访问该目录中的任何文件。你可以在 shell 提示符（此处用美元符号 `$` 表示）处输入 `ls` 命令列出当前目录下的所有文件。以下示例显示了如果你的文件与图 2.1 相同，你会看到的输出：

```
cd /usr/fred
ls
docs
reports
```

如果 `report7` 是你当前目录中的一个普通文件，你可以直接通过 `report7` 访问它。你不需要指定哪个目录下的 `report7` 文件，因为当你没有提供完整路径时，系统会认为你指的是当前目录。

## 使用 basenames 和 dirnames

文件名通常包含一个目录部分（我将其称为 `dirname`）和一个最后的基准名称（我将其称为 `basename`）。这个 `basename` 不包含任何斜杠 (`/`)，因此也不包含任何目录名。`basename` 可能表示普通文件也可能表示目录。`dirname` 指明了如何到达所需的 `basename`。如果提供的路径仅为基名称，则你用点 (`.`) 来指示它的 `dirname`，你稍后会看到点是一个代表当前目录的符号。例如：

表 2.1 一些示例的 `dirnames` 和 `basenames`。

| full pathname | --dirname | --basename |
| :--- | :--- | :--- |
| `/usr/fred/report7` | `/usr/fred` | `report7` |
| `/usr/fred/docs` | `/usr/fred` | `docs` |
| `report7` | `.` | `report7` |

## 显示你的当前目录名称

要显示当前目录的名称，请输入：

```
pwd
```




当你使用 `cd` 命令且不指定目录时，它会将你带到主目录，也就是说，你的主目录变成了你的当前目录。

主目录的名称可能因系统而异，但它通常包含你的登录用户名。例如，如果你以用户 `jane` 的身份登录，在某个 UNIX 系统上你的主目录可能是 `/usr/jane`。在另一个 UNIX 系统上（特别是 SVR4，例如 Solaris）它可能是 `/home/jane` 甚至是其他内容。要显示你的主目录名称，请输入：

```bash
$ cd $pwd
/home/fred
```

即使你不知道主目录的名字，`cd` 命令也会带你回到主目录。随后，`pwd` 命令会告诉你你到达了哪里，即你主目录的名称。在上面的示例中，`/home/fred` 就是该用户的主目录。

### 切换到绝对目录

正如我们之前看到的，我们可以通过带有绝对路径（即完整路径）的 `cd` 命令来设置当前目录。如果你不知道完整路径的确切拼写，请使用后文“切换到目录”章节中描述的方法。如果你知道确切的拼写，可以通过 `cd` 命令直接切换到该目录。确保你的目录以开头的 `/` 起始。

例如，要切换到 `/usr/fred/reports`，输入：

```bash
cd /usr/fred/reports
```

要切换到根目录，输入：

```bash
cd /
```

### 切换到当前目录的子目录（相对）

如果我们想切换到当前目录的子目录，我们可以使用另一个快捷方法。我们可以指定一个相对路径，显示如何从我们所在的位置到达目标位置。例如，在图 2.1 中，假设以下情况成立：`/usr/fred` 是我们的当前目录，`/usr/fred/docs/98sales` 是我们想要切换到的目录。

我们可以通过完整路径到达那里：

```bash
cd /usr/fred/docs/98sales
```

然而，由于 `/usr/fred` 是当前目录，使用如下相对路径会更简单：

```bash
cd docs/98sales
```

注意，相对路径不以斜杠 `/` 开头，因为它们没有指示返回根目录的路径。因此，相对路径被称为部分路径。它们之所以被称为相对，是因为它们基于我们的当前目录。例如，下表显示了相对路径随当前目录变化的情况：

表 2.2. 根据当前目录到达 `/usr/fred/docs/98sales` 的相对路径

| 当前目录 | 命令 | 结果 |
| :--- | :--- | :--- |
| `/usr/fred` | `cd docs/98sales` | `/usr/fred/docs/98sales` |
| `/usr/fred/docs` | `cd 98sales` | `/usr/fred/docs/98sales` |
| `/usr/fred` | `cd docs/98sales` | `/usr/fred/docs/98sales` |
| `/usr` | `cd fred/docs/98sales` | `/usr/fred/docs/98sales` |
| `/` | `cd usr/fred/docs/98sales` | `/usr/fred/docs/98sales` |

### 分步切换到目录

有时，你对目标目录有一个模糊的想法，但不知道具体如何到达那里，或者不知道每个中间目录的确切拼写。有时你认为自己知道这些信息，但你的 `cd` 命令执行失败并报错：No such file or directory（没有此类文件或目录）。这里有一个可以帮助你的方法：提示：起始斜杠 `/` 意味着从根目录 `/` 开始。学会注意路径的第一个字符。如果它以斜杠 `/` 开始，那么它就是绝对路径，包含了回到根目录 `/`的所有目录。

分步切换到目录

1. 在脑海中确定通往目的地必须到达的第一个目录。如果你想使用相对路径，第一个目录将是你当前目录的子目录。如果你想使用绝对路径，那么第一个目录就是根目录 `/`。如果你不确定，在脑海中计划从根目录开始。
2. 如果你使用相对路径，跳过此步进入第 3 步。如果你使用绝对路径或决定从根目录开始，请执行第 2 步。输入：

```bash
cd /
```

在这一步以及此过程中的每一步之后按下回车键。现在你处于根目录。
3. 如果你不确定下一步要去哪个目录，或者不确定其拼写，输入：



```
ls -CF
```

在此步骤以及此过程中的每一步之后，请按回车键。`ls`（参见附录）将向你显示从这里可以到达的所有文件和目录名称。`ls` 的 `-C` 选项将以列显示输出。`ls` 的 `-F` 选项将在目录名称末尾添加斜杠（`/`），以便你将其与普通文件区分来。

如果文件太多导致输出超出了屏幕，你可以通过输入以下命令之一来逐页查看输出：

```
ls -CF | pg ls -CF | more
ls -CF | less
```

`pg`、`more` 和 `less` 是用于逐页查看输出的实用。如果你的系统没有这些工具之一，你将立即看到错误：Command not found（未找到命令）。在这种情况下，请尝试显示的其他替代方案。要进入下一页，请按回车键或空格键。若要在结束前退出，请输入 `q`。

### 4. 在确定要进入的下一个目录的正确名称后，按照如下方式切换到该目录：

```
cd nextdir
```

将 `nextdir` 替换为你所需的目录名。注意，在此 `cd` 命令中不要输入任何斜杠（`/`）。如果此命令 get No such file（无此类文件）错误，请重复上面的步骤 3 并双检你的拼写。如果你 get permission error（权限错误），你可能没有切换到该目录的权限。

### 5. 如果步骤 4 中的 `cd` 命令执行成功，我们现在离目标又近了一个目录。反复重复步骤 3 和 4，直到你到达所需的目录。

#### 另另
- ![arrow.gif](img/arrow.gif) 有更多关于列表的信息，请参第 15 页
- ![arrow.gif](img/arrow.gif) 有更多关于逐页查看的信息，请参第 16 页

### 访问当前目录 (.)
#### 返回上一级父目录 (..)




```bash
cd ../reports/acme
```

如果你不确定需要返回多少级目录（`..`），可以使用“小步步进”的方法，例如：

```bash
cd ..
ls -CF
```

第 49 页

```bash
cd reports
ls -CF
cd acme
```

每个 `ls` 命令都会列出当前目录的内容，因此你可以看到可以进入的可用目录。记住，在任何小步步进的过程中，不要以斜杠（`/`）开头任何目录名称，因为那将带你直接回到根目录。

*返回上一个目录。*

Korn shell 中的 `cd` 命令有一个 Bourne shell 中不具备的额外选项：

```bash
cd -
```

它会将你带回上一次所在的目录。该命令也可以轻松地在两个目录之间来回切换，例如所示：

```bash
cd /data
# 现在在 /data 中做一些工作
cd /usr/fred
# 现在在 /usr/fred 中做一些工作
cd -
# 现在你回 /data
cd -
# 现在你回到了 /usr/fred
cd -
# 现在你回到了 /data
# 等等
```

### 如何构建文件的相对路径

在本书中，指令经常会指定输入目标文件的绝对路径或相对路径。绝对路径包含了一直到根目录的所有父目录。这很容易理解，但需要大量的键盘输入。

如果你的当前目录就是包含目标文件的目录，你只需通过其基名（`basename`，参见术语表）即可访问该文件，这比输入绝对路径要短得多。

第 50 页

`basename` 是相对路径的一个示例，因为获取文件的路径是从你的当前目录开始的。不要在 `basename` 前加斜杠（`/`），因为那将表示绝对路径，告诉系统在根目录中查找该 `basename`，而不是在当前目录中。

要使用相对路径访问当前目录的子目录（即子目录）中的文件，请输入此相对路径：

```
child-dir/filename
```

将 `child-dir` 替换为目标子目录的名称。再次注意，相对路径不能以斜杠（`/`）开头。例如，如果当前目录下有一个名为 `reports` 的子目录，而你想访问该目录下的 `acme` 文件，则相对路径为：

```
reports/acme
```

要访问隔了多级子目录的文件，请输入如下相对路径：

```
sub-dir/its-sub-dir/its-sub-dir/filename
```

这种路径的优势在于，你不需要指定回到根目录的每一个目录。

要访问当前目录的父目录中的文件，请输入此相对路径：

```
../filename
```

正如你在本章较早之前看到的那样，点-点（`..`）表示父目录。

通过使用多个点-点（`..`）条目，可以使用相对路径访问整个系统中的任何其他文件或目录，例如：

```bash
../../../..//usr/jane/accounts/progs/acme
```

在实践中，多个点-点条目难以理解且并不常见。相对路径的使用频率比绝对路径高得多，因为减少了打字工作量。

### 创建新目录 (mkdir)

创建新目录有三种方法：

1. 进入你想创建新目录的父目录。你可以指定绝对路径或相对路径到达那里。输入：
2. 留在原地并创建它
3. 同时创建所有中间目录。

### 进入父目录并创建新目录

1. cd 进入你想创建新目录的父目录。你可以指定绝对路径或相对路径到达那里。输入：





# mkdir

`mkdir new-dir`

将 `new-dir` 替换为你想要创建的新目录名称。不要在 `new-dir` 中包含任何斜杠 (`/`)。`mkdir` 将创建所需的目录目录。

若要停留在当前目录并在其他地方创建新目录，请输入 `mkdir` 命令，后跟要创建的新目录的完整路径或相对路径。如果中间的任何目录不存在，`mkdir` 将执行失败并显示错误信息。

## 创建新目录及所有中间父目录

1. 输入：
```
mkdir -p
```
（在接到指示前不要按回车键。）

2. 输入一个空格，然后输入要创建的新目录的完整路径或相对路径。然后按回车键完成此命令。`mkdir` 的 `-p` 选项会使其创建路径中任何不存在的父目录以及给定路径中的最终目录。

### 删除现有目录 (`rmdir`)

1. 输入：
```bash
cd dir-name
```
将 `dir-name` 替换为要删除目录的绝对路径或相对路径。

2. 输入：
```bash
ls -aF
```
查看当前目录下的所有文件，包括文件名以点 (`.`) 开头的文件。要删除目录，该目录下不能包含点 (`.`) 和双点 (`..`) 以外的任何文件。

3. 如果第 2 步列出了大量文件，请确保你确实想删除所有这些文件及其所在的目录。如果你确定，请进入下一个程序“删除整个子树”。如果第 2 步仅显示少量文件或目录，请继续执行此程序的第 4 步。

4. 第 2 步中 `ls` 的 `-F` 选项会导致 `ls` 在文件名后添加斜杠 (`/`) 以表示目录。如果要删除的目录中有子目录，必须通过从头开始对每个子目录及其子目录的子目录执行此程序来先删除它们。

5. 在删除目录之前，必须删除该目录中的所有普通文件。要删除当前目录下的文件，请输入：
```bash
rm file-name
```
将 `file-name` 替换为要删除的文件。`rm` 是删除（即移除）文件的 UNIX 命令。

6. 一旦目录中除了点 (`.`) 和双点 (`..`) 之外没有所有普通文件和子目录，输入：
```bash
cd ..
```
移动到要删除目录的父目录。你无法在目录内部时删除它。

7. 输入以下命令删除目录：
```bash
rmdir dir-name
```
将 `dir-name` 替换为要删除的空目录的相对路径或绝对路径。`rmdir` 是删除（即移除）空目录的 UNIX 命令。

## 删除目录子树

可以使用一条命令删除目录及其所有存在的文件和子目录（即整个目录子树）。然而，此命令非常强大，因此非常危险，必须非常小心地输入以避免悲剧。

1. 确保你知道要删除目录的准确拼写和完整路径。使用 `cd` 和 `ls` 命令切换到该目录，并列出其内容以及任何子目录的内容。确保你想要删除所有这些文件和子目录。确保你删除的是用户创建的目录，而不是系统所需的目录，特别是当你以 root 身份登录时。

2. 输入：
```bash
cd parent-name
```
将 `parent-name` 替换为要删除目录的父目录的绝对路径或相对路径。





输入 `pwd` 以确认你已到达正确的目录。

### 4. 输入：
```bash
ls -dF dir-name
```
将 `dir-name` 替换为要删除的目录。此命令应该显示相同的 `dir-name`，后面跟着一个斜杠 (`/`)。如果你看到错误信息：No such file（无此类文件），说明出了问题。返回此步骤的第 1 。

### 5. 输入：
```bash
rm -rf dir-name
```
将 `dir-name` 替换为要删除的目录。此命令非常危险。在按下回车键之前，请双检拼写是否正确。`rm` 命令通常只删除普通文件而不删除目录。`rm` 的 `-r` 选项会导致 `rm` 递归删除指定的目录及其文件，以及所有的子目录及其文件、所有的子目录及其文件，以此类推。没有撤销选项。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

在以 root 身份运行时，避免使用 `rm -r`。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

指定的 `dir-name` 出现错误或拼写错误（例如错误的空格或斜杠 (`/`)），可能会抹除 UNIX 系统的重要部分并使其完全无法运行。没有撤销选项。为了更安全，如果你的 shell 允许，可以将 `rm` 别名为 `rm -i`。

### 提高访问目录的效率

在长目录名之间切换可能会变得疲惫且沮丧。这里是一些可以帮助你的技巧。

### 为常访问的目录设置 CDPATH

在第一章中，我们看到了如何设置 shell 变量来定制系统如何为运行。Bourne shell 和 Korn shell 都有一个名为 `CDPATH` 的变量，只要这些目录具有独特的名称，你就可以轻松地进入最常用的目录。一旦设置了 `CDPATH`，你就可以 `cd` 进入常用目录的基名（basename），就像你坐在这些目录的父目录中一样。

### 设置和使用 CDPATH

1. 列出你最常 `cd` 进入的目录的完整路径列表。列表可以存在脑海中、草稿纸上、文件中等。如果这些目录的基名大部分是唯一的，这个过程将对你有所帮助。
2. 为最常访问目录的父目录创建一个新的完整路径列表。我将其称为 `CDPATH` 列表。
3. 将 `CDPATH` 列表排序，使得你最常 `cd` 进入的目录的父目录排在前面。
4. 如果任何你常 `cd` 的目录具有相同的基名，将最常使用基名的父目录放在最少使用基名的父目录之前。此过程将允许你仅访问其父目录在列表中排靠前的那个相同基名。其他目录中的其他相同基名必须使用完整路径或相对路径访问。
5. 决定是在检查 `CDPATH` 中的所有目录之前还是之后检查当前目录中的给定基名。如果在之前，则当前目录覆盖或优先级高于 `CDPATH` 目录；如果在之后，则 `CDPATH` 覆盖或优先级高于当前目录。

例如，假设你输入：
```bash
cd docs
```
假设 `docs` 目录既是当前目录的子目录，也是 `CDPATH` 中某个目录的子目录。我们可以通过控制当前目录的优先级是高于还是低于 `CDPATH` 目录，因此我们可以控制最终进入哪个 `docs` 目录。

6. 输入：
```bash
CDPATH=
```
在接到指示之前不要按回车键。在 `=` 符号周围不要留任何空格。
7. 如果希望当前目录的优先级高于 `CDPATH` 目录，输入：
```bash
.:
``` （即点加冒号）且没有空格。
8. 输入你 `CDPATH` 列表中的所有完整路径，使用冒号 (`:`) 分隔每个项目。不要以冒号 (`:`) 结束列表。不要输入任何空格。




`:`（即冒号）且没有空格。

10. 按回车键完成你的命令。这里是一个完整命令的示例：

```bash
CDPATH=.:/usr/fred/reports:/data/acme
```

11. 现在，每当你 `cd` 到一个 `basename` 时，shell 都会按照顺序搜索 `CDPATH` 中的每个目录，直到找到给定的 `basename` 成为 `CDPATH` 中某一个父目录的子目录。然后，它将带你进入该目录。

12. 除非你在 `.profile` 中设置了此 shell 变量定义，否则你每次登录都必须重新输入整个 `CDPATH=` 行内容。

### 另需参考

- 有关如何在 `.profile` 中设置 shell 变量定义以便在每次登录时自动执行的配置，请参阅第 307 页。
- 有关不同 shell 的更多信息，请参阅第 27 页。

### 保存/访问常用目录名称

有时，你会发现有些目录是你想要多次返回的，但频率又没高到需要更新 `CDPATH`。你可以创建并使用自己的临时 shell 变量，以便方便返回这些目录。

#### 保存/访问常用目录名称

1. `cd` 进入一个你知道自己多次返回的目录。
2. 输入：
```bash
D1=`pwd`
```
请确保你输入的是反引号（`` ``）而不是单引号（''）。不要在该命令中输入任何空格。此命令会将当前目录的完整路径保存到变量 `D1` 中。
3. 要返回到 `D1` 中的目录，输入：
```bash
cd $D1
```
注意，你必须在变量前加上 `$` 符号才能使用其内容，但在设置内容时不需要。
4. 遵循步骤 1 到 3，你可以设置并使用其他变量（如 `D2` 或 `D3`）来记住并在几个目录之间轻松地切换。
5. 你可以选择更具描述性的变量名，例如：
```bash
CUSTS=`pwd` REPORTS=`pwd`
```
在执行上述命令之前，你必须位于目标目录中。你不能选择已存在的 shell 变量名。输入：
```bash
env
```
查看现有变量列表。
6. 如果你忘记了变量存储的是哪个目录，可以使用 `echo` 命令显示其内容，例如：
```bash
echo $D1
```
7. 如果你想让某些变量永久化，这样就无需每次登录都重新设置，请按照上述过程所述，在 `.profile` 中进行设置。

### 显示系统信息

作为 UNIX 系统上的新用户，你可能最想做的事情之一就是查看系统内部的真实样貌。UNIX 系统维护着关于你是谁、你的当前环境如何以及你正在做什么的详细信息。这些信息中的大部分可以通过简单的命令或更深入的 shell 编程语言获取。




请记住，存在许多版本的 UNIX，你的输出结果可能与此处看到的并不完全相同，请务必根据你自己的系统文档检查你在此处使用的命令。好好的消息是，在学习了这些命令后，你几乎可以坐在任何一台 UNIX 机器上并开始工作。让我们通过几个实用的命令，看看你可以获取关于你系统的哪些信息。

# 显示关于你和你的系统的信息

让我们先让 UNIX 告诉它对你当前会话的了解。这些信息非常重要，因为你在系统中的身份决定了你能够执行的许多命令和程序。你要知道，一个 `userid`（ `uid` ）拥有所有程序，而 UNIX 命令本质上就是一种程序，并且它为这些程序和命令赋予了特定的权限。现在，让我们来看几条可以告诉你当前登录会话相关信息的命令。

## whoami 命令

第一个要探索的命令是 `whoami` 命令。

1. 在 shell 提示符下，输入 `whoami`。
2. 根据你的系统不同，你应该在一一行中看到你的 `userid`，并在下方看到 shell 提示符：
```
$ whoami
nick_humes
```
3. 我们可以通过输入 `who i` 来稍微修改此命令以查看更多信息。
1. 在 shell 提示符下，输入 `who i`。
2. 你应该看到类似的信息：
```
$ who i
nick_humes tty1 Mar 18 12:12
```
3. 如你所示，此命令提供了更多信息；它返回了你的用户名、终端以及你登录系统的初始日期和时间。

## id 命令

另一个你会发现频繁使用的有用命令是 `id` 命令。

1. 在 shell 提示符下，输入 `id`。
2. 你应该看到系统返回的以下信息：
```
$ id
uid=101(nick_humes) gid=20(users)
```
该命令返回了你的用户 ID (`uid`) 和组 ID (`gid`)。这些信息非常有用，因为它告诉你当前在系统中的身份。你需要了解这一点，这是 UNIX 的强大功能之一：只要你有有效的密码，就可以切换到另一个用户。你也可以更改当前的用户组所属关系。这些功能非常有价值，因为你可能需要以与登录时不同的用户和用户组身份运行程序。

## tty 命令

另一个你应该检查的命令是 `tty` 命令。此命令告诉你你所使用的终端，或者如果你是通过网络登录的，则告诉你你连接的伪终端（pseudo-terminal）。伪终端意味着你不是通过物理连接直接到机器；而是通过网络连接。让我们来看一个例子。

1. 在 shell 提示符下，输入 `tty`。
2. 你应该看到类似下面的内容：
```
$ tty /dev/ttyp1
```
3. 系统返回你的终端用于连接到系统的设备名称。请注意输出 `/dev/ttyp1` 在设备号之前有一个 `p`。这表示该设备是一个伪终端。如果你直接通过系统控制台登录机器，你将看到以下内容：
```
$ tty /dev/console
```

## 变量

环境变量 `$TERM` 告诉系统你想要模拟的终端类型。根据你所处的系统和终端，你可以模拟字符终端（character terminal）或 X-Windows 终端（X-Windows terminal）。X-Windows 类型终端赋予你图形能力，而基于字符的终端则没有。你可以在登录机器后立即通过检查你的系统来确定你的环境变量是否已经激活。看看如何查看你的 `$TERM` 设置以及在需要时如何更改它。

1. 在 shell 提示符下，输入 `echo $TERM`。
2. 系统会将 `TERM` 的值回到屏幕：
```
$ echo $TERM
100
```
3. 如果你使用的是 `ksh` (Korn shell) 或 `sh` (posix shell) 并且想要更改 `TERM` 的值，你需要执行以下步骤：
1. 在 shell 提示符下，输入 `TERM=vt220;export $TERM`。
2. 要检查 `TERM` 是否已更改，你需要输入 `echo $TERM`。
3. 你会看到 TERM 被设置为 vt220。





在 `csh` (C shell) 中，你可以通过以下步骤来更改 `TERM`：

1. 在 shell 提示符处，输入 `set term=vt220`。
2. 输入 `set` 来检查 `TERM` 是否更改。
   ```
   set
   ```
3. 你将看到所有的环境变量设置。在输出中，你应该能看到类似下面这一行的内容：
   ```
   term    vt100
   ```

`stty` 命令用于设置或显示终端当前的 I/O 选项设置。你使用 `stty` 来设置有用的功能，例如退格键（backspace）或进程中断键。让我们来看例子：

1. 在提示符处，输入 `stty -a`。
   ```
$ stty -a 
   speed 9600 baud; line = 0;
   rows = 0; columns = 0
   min = 4; time = 0;
   intr = ^C; quit = ^^\; erase <undef>; kill = ^U
   eof = ^D; eol = ^@; eol2 <undef>; swtch <undef>
   stop = ^S; start = ^Q; susp <undef>; dsusp <undef>
   werase <undef>; lnext <undef>
   parenb -parodd cs7 -cstopb hupcl -cread -clocal
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif) -loblk -crts
   -ignbrk brkint ignpar -parmrk -inpck istrip -inlcr
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-igncr icrnl -iuclc
   ixon -ixany ixoff -imaxbel -rtsxoff -ctsxon -ienak
   ig-icanon -iext-case echo eechok-echon
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-nofsh
   -echoctl-echop-echoke-flus-pend
   opost-olconcr-ocr-onret-ofill-del
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-tost
$
   ```
2. 从前面的输出中，你可以看到有很多设置。大多数情况下，你只需要修改其中几个。注意输出输出中 `erase` 设置是未定义的（`<undef>`）。将其设置以使其对退格键（`<Backspace>`）起工作。`CTRL-H` 是 Control 键和 H 键的组合。`CNTR-H` 是退格键的默认值。你使用 `stty` 命令告诉系统使用此按键序列来执行退格功能。
   在 shell 提示符处，输入 `stty erase ^H`。
   ```
$ stty erase ^H
   ```
3. 现在查看输入 `stty -a` 的结果：
   ```
$ stty -a 
   speed 9600 baud; line = 0;
   rows = 0; columns = 0
   min = 4; time = 0;
   intr = ^C; quit = ^^\; erase = ^H; kill = ^U
   eof = ^D; eol = ^@; eol2 <undef>; swtch <undef>
   stop = ^S; start = ^Q; susp <undef>; dsusp <undef>
   werase = ^K; lnext <undef>
   parenb -parodd cs7 -cstopb hupcl -cread -clocal -loblk
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-crts
   -ignbrk brkint ignpar -parmrk -inpck istrip -inlcr
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-igncr icrnl -iuclc
   ixon -ixany ixoff -imaxbel -rtsxoff -ctsxon -ienak
   ig-icanon -iext-case echo eechok-echon
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-nofsh
   -echoctl-echop-echoke-flus-pend
   opost-olconcr-ocr-onret-ofill-del
   ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)-tost
$
   ```
如你所见，退格键已设置。

### 显示关于用户的信息
你已经准备好学习有关登录系统的其他用户的命令了。首先通过 `who` 命令查看谁登录了系统。

   在 shell 提示符处，输入 `who`。
   ```
$ who   Tim_Wilson      ttyp1   Mar 19 18:27
   Emily_Wilson    tty10   Mar 19 18:30
   oracle          ttyp2   Mar 19 15:27
   Taylor_Klausner  typd5  Mar 19 10:20
   Marissa_Klausner ttypd1  Mar 18 06:00
   BPierce         ttyp7   Mar 19 19:17
   BWood           ttyp47  Mar 19 14:00
   CSarjent        ttyp10  Mar 19 11:27
   singleton       ttyp19  Mar 19 08:27
   Zach_Wilson      ttyp15  Mar 19 09:27
   Travis_Wilson   ttyp17  Mar 19 12:27
   Berglund         ttyp21  Mar 19 12:12
   Ed_Lewis        ttyp35  Mar 19 12:13
   Tony_Amico      console Mar 19 12:00
$
   ```
从输出可以看出，有很多用户在系统中。注意某些用户是直接连接的（tty ID），而其他用户是通过网络连接（ttyp ID）。还要注意 `ttyp1` 和 `ttyp5` 与其他不同，因为这些用户是通过调制解调器登录的。你还可以看到管理员之外的人员登录了系统控制台。这具有潜在的危险，因为在系统中通过登录系统控制台更容易获得特权。你可以使用这个简单的命令来查看谁登录了系统、他们是如何进入系统的以及何时登录的。

让我们看看 `who` 命令的另一个用法。这次我们将用该命令显示有关你的 UNIX 机器的一些信息。
   ```
$ who -b
   system boot  Oct 28 13:35
   ```



上述输出告诉我们机器启动（或重启）的日期时间。如果你在下班前启动了一个任务，第二天回来发现计算机崩溃了，那么知道这个信息会有用。在与系统管理员交流之前，你找到的任何信息都将有助于解决你遇到的任何问题。

另一个显示有关用户和系统信息的命令是 `uptime` 命令。以下是它的用法示例：

在 shell 提示符下，输入 `uptime`。

```bash
$ uptime 8:00pm up 142 days, 6:25, 2 users, load average: 0.51, 0.52, 0.52
```

输出告诉我们当前时间是晚上 8:00，系统已运行了 142 天 6 小时 25 分钟。当前有两个用户登录到系统。系统管理员使用平均负载（load average）来帮助评估系统性能。

现在让我们来看看如何通过特殊选项使用 `uptime` 命令，以获得与 `w` 命令相同的输出。

在 shell 提示符下，输入 `uptime -w`。

```bash
$ uptime -w 7:55pm up 142 days, 6:20, 2 users, load average: 0.51, 0.52, 0.52
User tty login@ idle JCPU PCPU what
dwilson tty1 6:27pm 3 uptime -w
root tty2 7:53pm sh
```

现在输入 `w` 命令。

在 shell 提示符下，输入 `w`。

```bash
$ w 7:55pm up 142 days, 6:21, 2 users, load average: 0.51, 0.52, 0.52
User tty login@ idle JCPU PCPU what
dwilson tty1 6:27pm 3
root tty2 7:53pm sh
```

如你所见，两个命令产生了相同的输出。然而，使用 `w` 命令比记住 `uptime` 命令的选项要简单一点。

你 world 使用的另一个命令是 `finger` 命令。该命令显示以下内容：

-   登录名。
-   用户的全名（如果列在密码文件中）。
-   终端状态（`write` 命令允许用户通过终端直接相互通信）。
-   用户的空闲时间。
-   用户的登录时间。
-   任何存放在用户 `.plan` 文件中的计划信息。该文件位于用户的家目录下。
-   任何存放在用户 `.project` 文件中的项目信息。该文件也位于用户的家目录下。
-   用户的办公室信息（如密码文件列所示）。
-   用户的电话号码（如密码文件列所示）。

你可以使用 `finger` 命令显示注册在系统上的其他用户信息。请记住，即使这些用户没有登录，你也可以看到关于他们的信息。在这个示例中，显示了用户 `<laLaurie>`；请替换为你你想要使用 `finger` 命令的用户。

在 shell 提示符下，输入 `finger laurie`。

```bash
$ finger laurie
Login: Laurie
Directory: /home/laLaurie
Office: 101
Phone: 555-1234
Idle: 0.01
Login: Mon 8:00
```

`mesg` 命令控制这种与终端交互的能力。`mesg` 命令返回你的终端接收其他用户消息当前当前（超级用户始终可以向另一个用户发送消息）。

假设在以下示例中 `mesg` 设置为 `y`：

```bash
$ mesg
y
```

现在将此设置更改为 `n`。

```bash
$ mesg n
```

在 shell 提示符下，输入 `mesg`。

```bash
$ mesg
n
```



$mesg is n

现在让我们来看看当用户能够接收消息时，`finger` 命令的输出看起来是所示所示：

```
$ finger llarie
Login name: llarie In real life: Linda Laurie
Bldg: Indy, Work phone: 317.555.7180
Directory: /home/llaurie Shell: /usr/bin/sh
On since Mar 21 14:59:15 on ttyp1 from Hydra.
Plan: Oracle 8.1 Web Server
```

注意，（messages off）输出已经不再出现。你现在可以通过如 `write` 等程序与该用户进行交互。

# 显示有关 UNIX 密码文件的信息

与大多数安全系统一样，UNIX 要求用户不仅要在系统中注册，还必须通过提供用户 ID 和密码来验证其登录。不过，这并非万无一失，因为用户有时会将密码与他人共享，或者有人会使用其他用户的密码。

首先，查看 UNIX 密码文件（`passwd`）。以下是位于 `/etc` 目录下的密码文件示例。

```
root:Thisisasecret:0:3::/:/sbin/sh daemon:*:1:5::/:/sbin/sh
bin:*:2:2::/usr/bin:/sbin/sh
sys:*:3:3::/:
adm:*:4:4::/var/adm:/sbin/sh
uucp:*:5:3::/var/spool/uucppublic:/usr/lbin/uucp/uucico
lp:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:11:11::/var/spool/uucppublic:/usr/lbin/uucp/uucico
hpdb:*:20:1:ALLBASE:/:/sbin/sh
nobody:*:-2:-24::/:
oracle:BJXXXX3HTWSls:201:200:,,,:/home/oracle:/usr/bin/sh
cfliss:XXXXXXXXXXXXX:100:200:,,,:/home/cfliss:/usr/bin/sh
dwilson:Can'tguessme!:101:200:DanWilson,Indy,317.555.5555,:/home/dwilson:/usr/bin/sh own
```

`passwd` 文件中的每一行都标识系统中的单个用户。每个字段由冒号（`:`）分隔。你可以按照如下方式分解每个条目：

- 登录名
- 加密后的密码
- 数字用户标识符
- 数字组标识符
- 用户信息字段
- 用户主目录
- 登录时使用的 Shell 程序

在上述 `passwd` 示例中，你会注意到某些账户的加密密码字段中有一个星号（`*`）。这会指示操作系统防止任何人直接登录这些账户。

## 修改用户信息

如果你想更改用户字段中的信息，请尝试以下操作：

1. 在 shell 提示符下，输入 `chfn dwilson`。默认值打印在 `[]` 中。如要接受默认值，输入 `<return>`。若要留空，请输入单词 `none`。
Name [Daniel Wilson]: Daniel Wilson Location (Ex: St Paul) [Chicago]: Carmel Office (Ex: 1234) [317.555.555]: 800.555.5555 Home Phone (Ex: 555555) []

2. 查看你的更改，请执行以下步骤：
   . 在 shell 提示符下，输入 `grep -i dwilson /etc/passwd`。

```bash
$ grep -i dwilson /etc/passwd
```



大多数 UNIX 版本都支持影子密码（shadow passwords）。正如你在上面的 `passwd` 文件示例中所看到的，你可以看到每个设置了密码的用户的加密密码（虽然创建没有密码的用户账户是可能的，但不建议这样做）。这在某种程度上是一个安全问题，因为其他用户可以使用这些信息来破解其他用户的密码。为了防止这种情况，UNIX 厂商开始实施影子密码系统。该系统将加密密码信息放在另一个目录下的特殊影子密码文件中，该目录只有特权用户才能访问。某些系统拥有一个 `/etc/shadow` 文件，只有特权用户可以访问。无论哪种方式，目标都是防止普通用户读取加密密码。

# 更新用户信息

你可以使用此命令在不涉及系统管理员的情况下更新你的用户信息。请检查你的系统手册或帮助页（man pages），以查看你的 UNIX 版本是否支持此命令。

# 组文件

另一个值得的系统文件是组文件。该文件也位于 `/etc` 目录下，维护了你所属的主组和关联组列表。让我们来看一个组文件的示例，并识别组成它的组件。

```
root::0:root other::1:root,hpdb
bin::2:root,bin
sys::3:root,uucp
adm::4:root,adm
daemon::5:root,daemon
mail::6:root
lp::7:root,lp
tty::10:
developer::99:dwilson,ssmith,cfliss
nuucp::11:nuucp
users::20:root,dwilson,ssmith,cfliss
nogroup:*:-2:
dba::200:oracle,dwilson,ssmith,cfliss
```

注意，一个用户可以存在于多个组中。你在 `passwd` 文件中的条目决定了你的主组身份。cfliss 账户的主组是 200 (dba)。但她也是 developer (99) 和 users (20) 组的成员。

现在是查看如何使用 `passwd` 命令更改密码的好时机。

在 shell 提示符下，输入 `passwd`。

```
$ passwd Changing password for msch
Old password: <Old Password>
New password: <New Password>
Re-enter new password: <New Password>
```

`passwd` 命令会以交互方式引导你完成密码更改。

### 显示系统信息

UNIX 系统为用户提供了许多命令，使其能够获取有关系统的信息。普通用户可以执行各种命令，从告诉他们日期和时间的命令到提供有关 UNIX 系统当前状态详细信息的命令不等。在本节中，你将学习普通用户如何利用可用命令从系统中获取信息。

### 获取日期 (date)

让我们先学习如何显示系统的日期和时间。在 shell 提示符下，输入 `date`。

```
$ date Sun Mar 22 10:25:28 CST 1998
```

你还可以添加格式选项来更改日期的显示方式。以下是几个示例。

在 shell 提示符下，输入 `date %+j`。

```
$ date %+j 081
```
上面的示例打印了儒略日（Julian date），这是一年中当前数的数的表示。

在 shell 提示符下，输入 `date %+D`。

```
$ date %+D 03/22/98
```
上面的示例使 `date` 命令以 mm/dd/yy 格式打印日期。

输入 `date %+I:%M%p`。

```
$ date %+I:%M%p 11:20AM
```
这个示例提供了带有 am 或 pm 显示的时间。

在 shell 提示符下，输入 `date "+%A %B %e %Y"`。

```
$ date "+%A %B %e %Y" Sunday March 22 1998
```
这个示例显示了如何显示完整的星期几名称、完整的月份名称、日期以及完整的四位年份。正如你从每个示例中看到的，带有格式选项的 `date` 命令允许用户以几乎任何格式格式显示日期。

### 获取系统名称信息 (uname)

现在让我们看看如何显示系统的正式名称。执行此操作的命令是 `uname` 命令。




# 系统信息

在 shell 提示符下输入 `uname -a`。

```bash
$ uname -a HP-UX Hydra B.10.20 E 9000/890 7047254010 unlimited user
```

该输出可以分解为以下组件：
- 操作系统名称
- 用于标识系统的网络系统名称
- 操作系统发行版本
- 操作系统版本
- 机器及型号数字
- 机器 ID 号
- 操作系统许可证

请检查您的系统手册以获取适用于您机器的详细说明。如果您使用的是惠普（Hewlett-Packard）系统，上述示例适用。*理解 UNIX 文件系统*。

# UNIX 文件系统

UNIX 环境支持所谓的层次文件系统和文件/目录结构。这意味着您的文件系统（以及目录）呈现出倒置树状。人们有时将这种结构称为树。这种目录结构类似于更熟悉的 MS-DOS 布局。树的顶端被称为根目录。根目录之下是所有其他目录。

所有目录都维护在 UNIX 文件系统中。这种文件管理方法更容易将文件分区到磁盘上。另一个好处是，如果系统丢失了非系统磁盘驱动器，系统只需只需更换驱动器并从备份中恢复数据。层次文件系统通过使数据的实际位置对您透明化，为分配文件空间提供了灵活性。作为用户，您无需关心数据是位于物理驱动器 A 还是 B。将文件和目录逻辑地映射到物理驱动器的工作完全由管理员负责。作为用户，您可能没有权限更改文件系统的配置。

# 磁盘使用

现在查看 `df` 命令。通过此命令，您可以查看文件系统及其大小。在 shell 提示符下输入 `df -k`。

```
/data1(/dev/vg01/lvol1): 1803132 total allocated Kb 162443 free allocated Kb 1640689 used allocated Kb 90% allocation
/data2(/dev/vg02/lvol1): 901556 total allocated Kb 387825 free allocated Kb 513731 used allocated Kb 56% allocation
/data3(/dev/vg03/lvol1): 40513 total allocated Kb 30087 free allocated Kb 10426 used allocated Kb 75% allocation
/data4(/dev/vg04/lvol1): 90156 total allocated Kb 184337 free allocated Kb 71219 used allocated Kb 79% allocation
/data5(/dev/vg01/lvol2): 2704904 total allocated Kb 351091 free allocated Kb 2358813 used allocated  87%
/datadata6devdevvg033lvol2): 2254018 total allocated Kb 173082 free allocated Kb 2080936 used allocated Kb 92% allocation
/data7(/dev/vg02/lvol2): 254018 total allocated Kb 206370 free allocated Kb 27648 allocated allocated Kb 10% allocation
/data8(/dev/vg04/lvol2): 1803132 total allocated Kb 166125 free allocated Kb 37007 used allocated Kb 18% allocation
/data9(/dev/vg04/lvol3): 2704904 total allocated Kb 225131 free allocated Kb 453373 used allocated Kb 16% allocation
/home(/dev/vg00/lvol5): 17874 total allocated Kb 16586 free allocated Kb 1288 used allocated Kb 7% allocation
/opt(/dev/vg00/lvol6): 58982 total allocated Kb 524 free allocated Kb 53758 used allocated Kb 98% allocation
/tmp(/dev/vg00/lvol7): 42306 total allocated Kb 28873 free allocated Kb 3433 used allocated Kb 0% allocation
/usr(/dev/vg00/lvol8): 598200 total allocated Kb 283706 free allocated Kb 314494 used allocated Kb 52% allocation
/var(/dev/vg00/lvol9): 259341 total allocated Kb 68893 free allocated Kb 190448 used allocated Kb 73% allocation
/stand(/dev/vg00/lvol1): 43046 total allocated Kb 28522 free allocated Kb 14524 used allocated Kb 33% allocation
/(/dev/vg00/lvol3): 75359 total allocated Kb 53928 free allocated Kb
```





## 磁盘使用与管理

```
21431 used allocated Kb
28 % allocation used | | | |
```

上述输出来自一个生产系统。`df -k` 命令报告了文件系统中可用的千字节数，以及分配给该文件系统的总千字节数。输出还显示了已使用的千字节以及文件系统使用的百分比。这些信息非常有用，因为你可以此确定系统空闲空间在哪里，以及有多少空间可用于额外的存储。

请记住，并非所有空闲空间对标准用户都是可用的。UNIX 要求文件系统和目录留有足够的空间以保证它们能够增长。你的系统管理员经常使用 `df` 命令作为其工具套件的一部分来管理系统。根据经验，当文件系统的空闲空间低于 10% 百时，就是时候开始归档并删除旧的未用文件以释放空间了。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 注意

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

再次强调，请务必阅读你特定系统的文档；惠尔-惠提到有一个更好的命令 `bdf`。

`df` 命令的输出引出了另一个有趣的点。注意文件系统名称后面的 `/dev/vgxx/lvolxx`（例如 `/usr (/dev/vg00/lvol8`）。这表明文件系统正由卷管理器管理，更具体说是惠尔-惠的逻辑卷管理器（LVM）。简而言之，这意味着当文件系统装满时，只需向组成该文件系统的磁盘池中添加另一个硬盘驱动器。

## 进程

本章以讨论 UNIX 进程结束。`process`（进程）简单来说就是正在执行的程序。你到目前见过的每个命令实际上都是某人编写的用于执行有用功能的程序。UNIX 系统设计成能够同时处理许多程序的执行。这背后的思想是虚拟机。简单来说，虚拟机意味着每个人似乎都独立拥有机器的全部权限。每个用户都可以执行命令或程序，而不必担心其他用户在做什么。在大多数情况下，这种自主性是真实的。然而，如果另一个用户正在运行一个占用机器大部分资源的程序，其他用户就会知道，因为他们的程序和命令运行得比正常慢。这时你的系统管理员就会介入进行性能调优。系统管理员可能会增加内存、磁盘或 CPU 来解决问题。他可能会要求所有的 `hog` 程序在特定小时内运行，以免影响其他用户。无论他们做出什么选择，目标都是让用户社区工作尽可能高效且经济。看看你可以如何查看机器上正在运行的进程。在 shell 提示符处，输入 `ps -ef`。

```
UID      PID    PPID   C  STIME       TTY     TIME  COMMAND
root       0      0  0  Oct 28      ?       1:05   swapper
root       1      0  0  Oct 28      ?       0:00   init
root       2      0  0  Oct 28      ?       0:36   vhand
root       3      0  0  Oct 28      ?       308:2   daemon
root       4      0  0  Oct 28      ?       8:7    ash
root       7      0  0  Oct 28      ?       356:35  isr
root      70     0  0  Oct 28      ?       0:0    lvmkd
root       1      0  0  Oct 28      ?       0:0    lvmkd
root       2      0  0  Oct 28      ?       0:0    lvmkd
root      13      0  0  Oct 28      ?      26:35   vx_sched_thread
root      14      0  0  Oct 28      ?       5:16   vx_iflush_thread
root      15      0  0  Oct 28      ?       5:24   vx_ifree_thread
root      16      0  0  Oct 28      ?       5:45   vx_inactive_cache
root      17      0  0  Oct 28      ?       1:35   vx_delxwri_thread
root      18      0  0  Oct 28      ?       1:18   vx_logflush_thread
root      19      0  0  Oct 28      ?       0:07   vx_attrsync_thread
root      20      0  0  Oct 28      ?       0:17   vx_inactive_thread
root      21      0  0  Oct 28      ?       0:0    vx_inactive_thread
root     2194      0  0  Oct 28      ?      14:0   ora_dbwr
root     2192      0  0  Oct 28      ?       0:0    ora_smon
root     2503      0  0  Oct 28      ?      48:0   ora_pmon
root     2519      0  0  Oct 28      ?       9:46   ora_lgwr
root     8735      0  0  Oct 28      ?      20:32   sh
root     8765      0  0  Oct 28      ?      22:26   sh
```

现在让我们看看输出。你从标题中注意到几列源于此输出；你只需要理解对此项重要的几列。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





#进程信息

- `UID`: 进程所有者的用户 ID。
- `PID`: 进程的进程 ID。
- `PPID`: 父进程的进程 ID。
- `STIME`: 进程的启动时间。如果超过 24 小时，则显示启动日期。
- `TTY`: 进程的控制终端。
- `TIME`: 进程的累计执行时间。
- `COMMAND`: 正在执行的命令。

注意，我们简写输出的最后一条显示了执行 `ps -ef` 命令的进程。还要注意它正方的进程——这是该命令的父进程。通过查看此类报告，我们可以看到 UNIX 如何在特定时间点执行系统中运行的命令和程序。如果我们再次执行 `ps -ef` 命令，我们将看到新旧进程的混合。这是因为某些程序在机器的整个生命周期内一直留留在系统中。这些程序属于操作系统，并执行必要的资源管理以保持系统正常运行。

在完成这一切之后，你仅仅触及了 UNIX 计算能力方面的冰一角。正如我在章节开头说的，即使是知识最丰富的 UNIX 专家，起初也和你现在一样。你学习得越多、对 UNIX 操作系统及其工具越熟悉，你指尖的计算能力就越大。

## 第 4 章：输入 UNIX 命令的规则
作者 Steve Moritsugu
第 81 页

## 识别 UNIX Shell 提示符
### 理解命令、选项和参数，并在它们之间添加必要的空格
### 为命令添加注释
### 从 Man 页面（帮助页）获取帮助
### 从重排索引（Permuted Index）获取帮助
### 命令未找到错误
### 设置目录的路径

## Shell 提示符回顾
让我们看看当我登录到 UNIX 系统时发生了什么：

```
login: mor
Password:
Last login: Fri Mar 13 17:33:22 from :0 Sun Microsystems Inc. SunOS 5.6 Generic
$ _
```

登录时出现的消息会因系统而异。在前面的示例中，在登录信息完成后，系统显示一个美元符号（`$`），光标停在它旁边等待输入。美元符号被称为 `prompt`（提示符），因为它提示用户输入命令。

生成美元符号提示符的程序是 `shell`（外壳）。shell 程序是一个命令行解释器，允许用户输入命令。本章的目的是介绍向 shell 输入 UNIX 命令的规则。主要有三种 shell 程序，它们在大多数商业 UNIX 系统上都可用：
- Bourne shell
- C shell
- Korn shell

Korn shell 的语法是 Bourne shell 的超集，因此两者非常兼容。Bourne shell 和 Korn shell 都使用美元符号提示符。该规则的唯一例外是当你以系统管理员 `root` 身份登录时。由于 root 账户共同拥有所有文件和目录，它可以无视文件或目录权限进行更改。当你以 `root` 登录时，系统会显示特殊的 shell 提示符——井号（`#`），提醒你这是一个全能账户，你必须小心不要犯任何错误，或者不要离开终端让任何人访问。

### Root 注意事项
为系统管理员一个普通的 UNIX 账户并在大多数时间使用是一个好主意。仅在需要时使用 `su` 命令变为 `root`。

如果你看到百分号（`%`）作为 shell 提示符，你可能处于 C shell 中。C shell 的语法和规则与 Bourne 及 Korn shell 不同，因此它为普通用户显示不同的提示符。如果你以 `root` 登录，C shell 将像 Bourne 和 Korn shell 一样使用井号提示符。

第 82 - 83 页




你可能会遇到的其他 shell（特别是在 Linux 下）包括 `tcsh`（它类似于 C shell）以及 `bash`（后者又称为 GNU Bourne-Again Shell，它结合了 C shell 和 Korn shell 的有用功能）。

可以为特定用户自定义 shell 提示符（prompt）。如果你处于网络环境中，有时会看到你的 shell 提示符包含你的系统名称。例如：

```
sparcster$ _
```

这是一个非常有用的提示符，因为网络允许你登录到各种 UNIX 主机，有时你可能会混淆自己当前正在访问哪种系统。shell 提示符并不一定以通常的 shell 提示符字符结束，如下面的示例所示：

```
[sparcster] _
```

在 Korn shell 中（但 Bourne shell 不行），可以将当前目录作为 shell 提示符的一部分。请看以下示例：

```bash
/usr/fred > cd /tmp
/tmp > cd /usr/jane/reports
/usr/jane/reports > cd acme/fiscal97/glaccounts
/usr/jane/reports/acme/fiscal97/glaccounts > ls
acme
report6
report7
/usr/jane/reports/acme/fiscal97/glaccounts > _
```

在这里，shell 提示符包含了当前目录，并以大于号（`>`）结束。你的当前目录从 `/usr/fred` 开始。当你切换到 `/tmp` 时，你可以看到 shell 提示符会自动跟踪我们的当前目录。请注意，当前目录可能包含许多子目录并变得很长，留给你输入命令的空间非常小。你仍然可以输入长命令，因为命令会自动换到下一行并继续显示你的输入。然而，当你想要查看之前的命令时，这可能会难以阅读。

正如你所看到的，shell 提示符可以以许多不同的形式出现。当你第一次登录时，请花一点时间看看你的 shell 提示符在该系统中是如何显示的，这样你以后就能识别出它。正如你在本章中看到的，使用 UNIX 必须掌握的技能之一就是识别你何时处于 shell 提示符状态，何时进入了某种意外情况。有关 UNIX shell 的更多信息，请参阅第 27 页。

### UNIX 命令行选项、参数和注释

在 shell 提示符处，你需要向 UNIX 输入命令。一个 UNIX 命令可以是一个简单的单词：

```bash
exit
```

在这里，`exit` 命令允许你结束 shell 并返回登录提示符。如果 `exit` 不起作用，尝试 `logout` 命令或使用 `Ctrl+D`。

```
date Sun Mar 15 07:30:49 PST 1998
```

### 大小写敏感

大小写敏感——单词是大写、小写还是两者的组合——非常取决于具体情况。在 UNIX 中，你必须警惕大写和小写。许多命令需要参数（也称为参数），参数是告诉命令要操作对象的单词。

```bash
rm acme pegasus
```

在这个示例中，`acme` 和 `pegasus` 是 `rm` 命令的参数。`rm` 是删除文件的命令。注意多个参数之间用空格分隔，而不是逗号。

```bash
cd /tmp
```

在这个示例中，`/tmp` 是 `cd` 命令的参数，它允许你更改当前目录。注意在 UNIX 中，没有消息就是好消息。在这个示例中，你知道 `cd` 命令执行成功了，因为 shell 提示符在下一行重新出现，且没有错误信息。

```bash
cd /tmp
```

在命令和任何参数之间加上一个空格是非常重要的。在接下来的示例中，你可以看到某些消息可能是坏消息：

```
cd/tmp
cd/tmp: not found
```



在这里，`cd` 命令后不小心漏掉了空格。首先注意，在出现下一个 shell 提示符之前，你收到了一条消息。你必须仔细阅读任何消息，因为它们通常意味着你的命令执行失败了（否则 UNIX 根本不会生成任何消息）。初学者往往会输入一系列命令，忽略这些消息，然后纳闷为什么程序不起作用。

在在上一个示例中，你可能认为 `cd` 命令失败是因为系统找不到 `/tmp` 目录。这是不对的。更仔细地观察错误信息：`cd/tmp` 未被找到。UNIX 下的大多数命令实际上是编译好的程序或脚本工具，它们存在于单独的磁盘文件中。系统正在告诉你，`cd/tmp` 不是一个有效的命令，也就是说，磁盘上没有名为该名称的系统实用程序。

让我总结一下到目前为止的要点：

1. 在 shell 提示符处，你输入的第一个单词必须是一个 UNIX 命令。
2. 大多数 UNIX 命令必须以小写输入（但也有例外）。
3. 如果命令需要后续接参数，你必须在命令后输入一个空格。
4. 然后，你可以根据该命令需要输入一个或多个参数。多个参数必须用空格分隔。
5. 你必须为命令、参数以及命令行上的所有单词输入正确的大小写字母。

### 另另

- 关于 `date` 命令的更多信息，请参阅第 72 页
- 关于 `rm` 命令的更多信息，请参阅第 191 页
- 关于 `cd` 命令的更多信息，请参阅第 42 页

### 在命令行中添加注释

在后续的一些示例中，我将为命令行添加注释，因此现在让我向你介绍注释。`comment`（也称为 `remark`）包含供人类读者的解释性文字。在 UNIX shell 中，任何以井号（`#`）开头的单词都被视为注释的开始。注释一直持续到行尾。

```
rm amet # no longer needed so free up the disk
```

在这个示例中，`rm` 命令后面跟着一个注释。shell 将忽略从井号（`#`）到行尾的所有内容。注释主要用于脚本编程，即把 UNIX 命令保存在文本文件中。如果你想让井号开始一段注释，必须在它前面加一个空格。否则，它只是一个普通字符（尽管我建议不要在文件名中使用它）。

### 空格分隔符

UNIX 允许使用一个或多个空格或制表符任意组合来分隔命令、选项和参数。这些分隔符简称为 `white spaces`（空白）。

```
rm amet # no longer needed so free up the disk
```

### 为命令输入选项

大多数 UNIX 命令允许在命令行指定选项，以修改命令的操作方式。看下面的示例：

```
ls -l /tmp
```

文件名特意以井号（`#`）开头，这样你就必须在处理文件之前停下来思考。shell 无法访问 `#acme`，因为它是一个注释，但它可以访问 `./#acme`。

在这里，`ls` 是你之前见过的用于列出目录文件的命令。`-l` 是 `ls` 命令的一个选项，导致它以长格式列出，显示文件的详细信息以及文件名。注意命令后有一个空格，这是要求的。注意使用破折号（`-`）来表示区分选项和参数。在这个示例中，`-l` 是修改 `ls` 运行方式的选项。`/tmp` 是 `ls` 命令的一个参数，告诉 `ls` 要列出哪个目录。选项必须紧跟命令之后，并在命令的任何参数之前。还要注意我们处于 C shell 中，因为我们使用的是百分号（`%`）shell 提示符。

```
ls -l -a /tmp # case 1
ls -a -l /tmp # case 2
ls -la /tmp # case 3
ls -al /tmp # case 4
```



在这些示例中，你可以看到 UNIX 在输入多个（简单）选项时展现了极大的灵活性。`-a` 是 `ls` 的另一个选项（如果你对 `ls` 的所有功能感兴趣，请参阅附录 A，“UNIX 命令”以获取更多信息）。

上述四种情况都是实现同一目的的不同且有效的方法。注意，我在每行开头都使用了井号（#）来开始注释，正如我们在前一节中讨论的那样。Shell 会忽略从井号到行尾的所有文本，这允许我添加解释性文字，以便让你们知道我指的是哪一行。

在情况 1 中，我指定了每个选项，并在前面加了连字符。注意每个选项和参数之间需要一个空格。在情况 2 中，注意选项的顺序并不重要。在情况 3 中，注意简单的单字母选项可以组合成复合选项，并在前面加一个连字符。在情况 4 中，注意选项可以以任何顺序组合在复合选项中。

注意，选项并不是通用的。一个命令的 `-v` 在与另一个命令配合时可能意味着完全不同的意思。你可能会发现某些命令的某个选项具有相同的含义，但其他命令的该选项字母却具有完全不同的含义。还要注意，某些选项在某些 UNIX 版本上可能不支持，或者该选项在另一个 UNIX 版本上可能会导致完全的结果。

如果选项不是单字母，它们就无法组合成复合选项，如下：

```bash
$ find / -mount -print
```

在这里，调用 `find` 命令时带了两个选项：`-mount` 和 `-print`。这两个选项不能组合成复合选项。此外，`find` 是一个选项顺序会产生差异的命令示例。

某些 UNIX 命令并不总是要求在其选项前使用连字符：

```bash
$ tar tv
```

`t` 和 `v` 是 `tar` 命令的选项。由于历史原因，这是通常不使用连字符的命令。大多数现代 UNIX 版本（包括 SCO 和 Solaris）允许在 `tar` 选项前加连字符，因此在指定选项时它不需要与其他命令有所不同，例如：

```bash
$ tar-tv
```

记住，必须按照以下顺序输入命令并用空格分隔：

1. 命令名称。
2. 任何所需的选项，前面加一个连字符。
3. 任何所需的参数。
4. 任何所需的注释。在注释开头加一个空格和一个井号。

另需参考
- 关于 `ls` 命令的更多信息，请参阅第 151 页。
- 关于 `find` 命令的更多信息，请参阅第 153 页。
- 关于 `tar` 命令的更多信息，请参阅第 340 页。

### 选项参数

某些选项需要自己的参数，例如：

```bash
$ lp -dn3 laser 
```

`lp` 是打印文件的命令。`-d` 是 `lp` 的选项，允许你指定使用哪个打印机。同样，`-n` 是 `lp` 的选项，用于指定每个文件的打印副本数。`laser` 是 `lp` 命令的参数，用于指定要打印的文件。

大多数命令允许或要求在选项及其参数之间留空格。我通常首先尝试使用空格，因为这样整个命令更具可读性。如果遇到错误，会在不留空格的情况下重试命令。提示：使用命令行编辑可以方便地编辑和提交之前的命令。

当你第一次学习英语语法时，将句子拆分为主语、谓语、介词和介词宾语有助于你提高阅读能力并构建正确的句子。同样，将 UNIX 命令行分析为命令、选项、选项参数和命令参数，有助于你更好地理解你所遇的命令，也有助于你构建正确的 UNIX 命令。

### 在哪里可以获得帮助？(*man*)




有 100 多个标准的 UNIX 命令和实用程序。每个命令可能有选项；某些命令可能有 15 个或更多选项。这些选项并不是通用的，那么你到底如何记住所有命令的所有选项呢？幸运的是，你不需要这样做。UNIX 维护了一套在线手册，提供了关于每个命令及其选项的信息。

# 从 man 页（帮助页）获取帮助

你使用 `man` 命令来访问这些信息：

```bash
$ man ls
```

此命令将向你显示如何使用 `ls` 命令的在线手册页。这个过程被称为查看 `ls` 的 man 页。大多数商用 UNIX 系统都有类似的 man 页。让我们看看我的 Solaris 系统上 `ls` 的 man 页：

```text
User Commands                   ls(1) 

NAME
    ls - 列出目录内容 

SYNOPSIS
    /usr/bin/ls [ -aAbcCdfFgilLmnopqrRstux1 ] [ file... ]
    /usr/xpg4/bin/ls [ -aAbcCdfFgilLmnopqrRstux1 ] [ file... ]
```

`SYNOPSIS`（概要）部分在其他系统上有时被称为 `SYNTAX` 或 `USAGE`。它显示了组合此命令所需的格式。方括号 (`[]`) 中的条目是可选的。注意，`ls` 命令支持大量的命令选项。它允许将一个或多个文件名作为 `ls` 命令的参数。这个示例显示 Solaris 支持两种形式的 `ls` 命令。在 man 页的后面，它会指出两种形式之间的差异。

```text
DESCRIPTION 对于每个目录文件，ls 会列出目录
    的内容；对于每个普通文件，ls 会重复其名称
    以及请求的任何其他信息。输出默认按字母顺序排序。当没有参数时 ...
```

`DESCRIPTION`（描述）部分内容很长，所以让我跳过这里，向你展示介绍命令行选项的地方：

```text
OPTIONS 支持以下选项：
    -a 列出所有条目，包括以点 (.) 开头的条目，这些通常不会被列出。
    -A 列出所有条目，包括以点 (.) 开头的条目，但工作目录 (.) 和父目录 (..) 除外。
    -b 强制将不可打印字符以八进制 \ddd 符号打印。
```

由于 `ls` 有许多可用选项，这一部分也很长。事实上，如果你打印 `ls` 的 man 部分，大约会有七页长。在某些 UNIX 系统上，man 页的文本太多，以至于在你读完之前它就已经超出了屏幕。在这种情况下，你必须将 `man` 的输出通过管道交给分页实用程序：

```bash
$ man ls | pg
```

在其他系统上，man 页会在每页结束时自动暂停，但你必须确定你使用的是哪种分页器，并输入正确的命令来移动和结束会话。我将在第 6 章“列出、查找、显示或打印文件”中的“每次显示一个文件/管道”节中介绍如何执行操作。以下是无论你使用哪种分页器都能让你进行操作的基础知识：

- 要跳到下一页，请按 Enter 键或空格键。
- 要结束 man 会话，请按 `Q` 键。你可能还需要按 Enter 键。

有关 `man` 命令本身的更多信息，请输入此命令：

```bash
$ man man
```

### 另请
更多关于每次显示一个文件的信息，请参阅第 160 页

# 识别系统子程序的 man 页
等等，更多关于每次显示一个文件的信息，请参阅第 160 页

# 识别系统子程序的 man 页

man 页按节划分，涵盖了用户从 shell 运行的命令、系统管理命令、文件格式、在 UNIX 下编写 C 程序时可用的系统子程序等。某些命令（例如 `kill` 命令）也是 C 语言子程序的名称。

### 设置 man 分页器 PAGER

如果你系统上的 `man` 没有对输出进行分页，或者你不喜欢它调用的分页器，请将 `PAGER` 设置为你喜欢的分页器（例如：`PAGER=pg`），然后执行 `export PAGER`。

### 系统调用

```text
System Calls                   kill(2)

NAME
    kill - 向进程或进程组发送信号

SYNOPSIS
    #include <sys/types.h>
    #include <signal.h>

    int kill(pid_t pid, int sig);

DESCRIPTION
    kill() 向进程或进程组发送信号。 ...
```



在本示例中，注意名称 `kill` 后面跟着括号内的 man 章节编号。同样请注意 SYNOPSIS（概要）部分中的 `#include` 语句。`#include` 始终表示你正在查看一个 C 语言子程序，而不是你可以在 shell 提示符下输入的命令。执行 `man man` 可以查看如何指定 man 章节的搜索顺序。如果你不编写 C 语言程序，可能希望设置 `man`，使其在检查系统子程序之前先检查帮助页的命令章节。

`man` 命令只会显示它遇到的第一个章节的帮助页。使用 `man` 命令的 `-a` 选项可以搜索所有章节。如果第一个帮助页是系统子程序，那么显示的第二个帮助页可能来自你感兴趣的命令章节。通常有一个 `man` 选项可以告诉它你感兴趣哪个 man 章节，这样它将只搜索该章节。

### 快速在帮助页中查找信息

UNIX 初学者会一页一页地阅读帮助页，这很困难，因为每个命令都包含大量信息需要处理。通过快速扫描页面，你还可能会漏掉重要的参考。

中级 UNIX 用户知道如何使用斜杠 (`/`) 命令快速将光标移动到所需信息。例如，如果我正在查看 `df` 命令的帮助页，我想知道块的尺寸是基于 512 字节块还是 1024 字节块。与其一页一页地查看，我可能会输入此命令：

```bash
/512
```
此命令告诉分页实用将光标移动到它找到的请求字符串（在这种情况下为 `512`）的下一个位置。要找到相同字符串的下一次出现，输入：

```bash
/
```
高级 UNIX 用户知道，由于帮助页可能包含格式化输出的特殊控制字符，帮助页中的斜杠命令可能找不到指定的字符串，尽管你在视觉上可以在几页之后找到该字符串。我将在第 6 章的“清理帮助页 (`col`)” (Cleaning up Man Pages (`col`)) 节中解释这一问题及其解决方案。以下是高级 UNIX 用户启动 `man` 命令的方式，以便斜杠命令能够正确地找到所有字符串：

```bash
$ man ls -bx pg
```
你可以用你喜欢的分页器替换 `pg`。有关清理帮助页的更多信息，请参见第 168 页的“另参见”（SEE ALSO）。

### 如果不知道命令，如何找到所需的 man 页面

要使用 `man` 命令，你必须提供拼写正确的 UNIX 命令。但如果你不知道该命令该怎么办？例如，假设我想将当前一个队列中的打印作业移动到另一个打印机。我该如何查找执行此操作的命令？

要查找特定主题的 UNIX 命令，请使用 `man` 的 `-k` 选项。例如：

```bash
$ man -k print
```
`accept(1m)` - 接受或拒绝打印请求
`acctcom(1)` - 搜索并打印进程计数文件
`asa(1)` - 将 FORTRAN 回车控制输出转换为可打印格式
`cancel(1)` - 取消打印请求
`curs_printw(3x)` - 在 curses 中打印格式化输出
`devinfo(1m)` - 打印设备信息

`-k` 选项告诉 man 搜索每个命令的描述，查看它是否与给定的参数（在本例中为 `print`）有关。这里显示的输出是 Solaris 的。该输出包含了超过 100 个描述中包含单词 print 的命令。

在第 15 章“搜索文件或管道”（Searching for a File or Pipeline）中，你将看到如何使用 `grep` 命令过滤掉你不想要的行并留下你需要的行。在下面的示例中，我使用 `grep` 来查找这 100 多行中是否有任何可以将打印请求从一个打印机移动到另一个打印机的命令：

```bash
$ man -k print | grep lpmove
```
`lpmove(1m)` - 移动打印请求
`lprm(1b)` - 从打印队列删除打印请求

啊！有一个移动打印请求的命令，叫做 `lpmove`。为了了解更多关于 `lpmove` 的信息，我现在可以执行此命令：

```bash
$ man lpmove
```
当然，你可能不像我在示例中那样容易地找到你寻找的命令。你通常需要搜索各种相关的关键词并尝试不同的过滤词才能获得成功。例如，如果我查找的是 transfer（传输）而不是 move（移动），我就找到了我在找的命令。

如果你的系统不支持 `man` 的 `-?` 选项，请尝试 `apropos` 命令：




# $ apropos print

有时 `man-k` 或 `apropos` 命令会失败，并给出错误信息，说明在运行之前必须创建 `whatis` 数据库。通常该信息会建议运行 `catman-w` 来创建此数据库。SCO UNIX 使用了不同的命令 `makewhatis` 来创建此数据库。请参阅 `man` 帮助页获取适用于你系统的信息。创建此数据库通常需要 root 权限。

## 参见

* 有关 `grep` 命令的更多信息，请参见第 380 页

### 使用置换索引 (Permuted Index)

置换索引是某些 UNIX 系统自带的一本书，提供了查找感兴趣主题的其他方法。为了帮助你理解置换索引，我创建了一个包含两个条目的置换索引：一个针对 `lpmove`，另一个针对 `lprm`：

```
lpmove(1m) - move print requests
lprm(1b) - remove print request from the print queue
lpmove(1m)-move print requests
lpmove(1m)-move print requests
lprm(1b)-remove print requests from the print queue
lprm(1b)-remove print requests from the print queue
lpmove(1m)-moveprint requests
```

第 96 页

每个条目都会被置于置换索引中多次，对应该行中的每个重要单词。请注意，所有条目的中间都有一个间隔。置换索引根据紧随间隔之后的单词按字母顺序排列。每个条目都包含多次，以便其每个关键词都能紧跟在间隔之后。当你想要通过关键词查找条目时，请按字母顺序在间隔之后找到你想要的词汇。然后查看整个条目，看它是否是你感兴趣的内容。

## 错误

要执行 UNIX 命令、实用或 shell 脚本，只需在 shell 提示符输入命令名称，包括命令所需的任何选项和参数。某些命令是内置在 shell 中的，但大多数标准命令是存储在 `/bin`、`/usr/bin/`、`/etc/`、`/usr/local/bin`、`/sbin` 等目录下的程序文件。如果你尝试运行命令，可能会得到这样的错误：

```
$ myscript: not found
$ ./myscript
```

在你开始编写自己的 shell 脚本时，看到这种 notfound（未找到）错误是很常见的。如果脚本在当前目录下，请通过 `./scriptname` 运行文件。这可能会解决问题。如果你仍然得到 `command` notfound 错误，请检查命令拼写是否正确、是否使用了正确的大小（大写、小写或混合大小写），以及命令后是否留有空格以与任何选项或参数分开。检查该命令的帮助页。如果帮助页没有说明，可能是你系统上的 UNIX 版本不支持该命令。

某些 UNIX 系统提供系列分层产品（额外付费软件）。为了使用某些命令，你必须购买包含该命令的额外软件包。现在 UNIX C 编译器已是一项额外付费的项目。因此，在你尝试运行 `cc` 命令或 `make` 命令时，会收到 `command` notfound 错误，直到你购买并安装了该软件。有时可以从网上下载免费软件替代品，以提供相同或类似的功能。许多主要 UNIX 供应商的网站都有此类免费软件的链接。

## 参见

* 有关编写脚本的更多信息，请参见第 25 章，第 67 页

### 设置命令的路径

当你运行 `ls`、`cp` 和 `rm` 等命令时，你不需要担心它们是在 `/bin` 还是 `/usr/bin`。这是因为 `PATH` 变量使得运行命令变得简单。你可以使用 `echo` 命令显示 `PATH` 变量当前的内容：

```
$ echo $PATH
/usr/bin:/usr/ucb:/etc:.
```

shell 前前的美元符号 ($) 表示我们正在引用该变量的内容。`PATH` 包含一系列由冒号 (:) 分隔的目录名称。必须指定每个目录的完整路径。目录的顺序很重要，因为它决定了 shell 如何查找你输入的命令。

第 98 页

让我们看看当你向 shell 输入 UNIX 命令时会发生什么。





Shell 首先检查命令名称是否包含斜杠 (`/`)。如果名称包含斜杠，shell 将使用该名称作为路径名并尝试执行该文件。以下是一些包含斜杠的命令示例：

```bash
$ /usr/fred/bin/myscript -p acme
$ ./yourscript file1 file2
```

如果命令名称不包含斜杠，shell 将检查 `PATH` 中的每个目录，寻找具有正确名称的可执行文件，并尝试尝试运行找到的第一个。例如，假设 `PATH` 包含：

```bash
/bin:/usr/bin:/usr/local/bin
```

```bash
$ ls /usr/fred
```

这个命令字是 `ls`，它不包含斜杠。因此，shell 将检查 `PATH` 中的第一个目录，在我们的示例中是 `/bin`。如果 `/bin/ls` 是可执行文件，shell 将尝试运行该程序且不再检查 `PATH` 中的任何其他目录。如果 `/bin/ls` 不存在、不是普通文件或不可执行，shell 将移动到下一个目录，在我们的示例中是 `/usr/bin`。如果 `/usr/bin/ls` 是可执行文件，shell 将尝试运行它且不再检查 `PATH` 中的任何其他目录。一旦 shell 尝试了 `PATH` 中的所有目录均未找到可执行文件，它将给出一个 *command not found* 错误。

### 将当前目录添加到 PATH

如果你的 UNIX 命令不包含斜杠，则只会检查 `PATH` 中的目录。有些人人还希望检查当前目录。这通常只在你编写自己的 shell 脚本并希望在处于脚本所在目录时方便地运行它们时才有用。

要将当前目录包含在 `PATH` 变量中，请添加点目录（.）或空目录。我更倾向于添加点目录，因为这是指示当前目录的常用方法。然而，你应该能够识别 `PATH` 中的空目录，因为这涉及到安全问题（我们稍会介绍）。

以下是在 Bourne shell 或 Korn shell 中使用点 (`.`) 将当前目录添加到 `PATH` 的示例：

```bash
PATH=/bin:/usr/bin:.:/usr/local/bin
```

在这里，我们设置了 `PATH`，在 `/bin` 和 `/usr/bin` 之后、`/usr/local/bin` 之前搜索当前目录。这里是更多使用点的示例：

```bash
PATH=/bin:/usr/bin:/usr/local/bin:.  # 情况 1
PATH=.:/bin:/usr/bin:/usr/local/bin   # 情况 2
PATH=$PATH:.                         # 情况 3
```

在情况 1 中，只有当在前三个目录中未找到时，我们才会搜索当前目录。在情况 2 中，我们在其他目录之前搜索当前目录。在情况 3 中，我们保留 `PATH` 的默认值，并将当前目录指定为最后一个搜索目录。

作为简便方法，你可以使用空目录来表示当前目录。空目录就像点一样，但不要放点，只放额外的冒号 (`:`)。例如：

```bash
PATH=/bin:/usr/bin::/usr/local/bin  # 情况 1
PATH=:/bin:/usr/bin:/usr/local/bin   # 情况 2
PATH=/bin:/usr/bin:/usr/local/bin:     # 情况 3
PATH=$PATH:                          # 情况 4
```

在情况 1 中，在 `/usr/bin` 之后搜索当前目录。在情况 2 中，在其他目录之前搜索。在情况 3 和 4 中，在 `PATH` 中的其他目录之后搜索。

### PATH 的安全影响



通常情况下，你不应该在 `PATH` 的开头指定当前目录。出于安全考虑，如果你要将当前目录添加到 `PATH`，请将其添加到末尾。否则，黑客可以在 `/tmp` 或其他常用目录中创建名为 `cp` 或 `ls` 等常用命令名称的文件。如果你在该目录下执行该命令，你运行的是黑客程序而不是系统程序。出于同样的原因，`PATH` 中的任何目录都不应对用户具有写权限。

### 软件包

如果你向系统添加了新软件包，该软件包可能希望你将其可执行目录添加到 `PATH`。软件包的安装脚本可能会修改 `/etc/profile`。以 root 添加软件包后，重新登录并检查你的 `PATH`。确保目录顺序是合理的，特别是如果通过添加操作进行了修改。

### 命令在哪里？(type, whence)

有时知道你运行的命令的完整路径是有用的，特别是当它们运行不正常且你想调查原因时。`PATH` 可能包含许多目录，因此幸好有一些命令可以检查 `PATH` 并告诉你命令的完整路径。这些命令中最用的是 `type` 命令，它在 Bourne shell 和 Korn shell 中都可以工作：

```bash
$ type ls
/usr/bin/ls
...
ls is a tracked alias for /usr/bin/ls
```




在这里，`type` 会接收你输入的命令并确定该命令的完整路径。

如果你的系统不支持 `type` 命令，请使用 `which` 命令或 `whence` 命令来获取命令的完整路径：

```bash
$ which ls
$ whence ls
```

通常，`which` 命令仅在 Bourne shell 中有效。通常，`whence` 命令仅在 Korn shell 中有效。

### 用户在输入 UNIX 命令时常见的错误

UNIX 对初学者来说可能非常令人沮丧。起初，UNIX 似乎非常挑剔，并且对你输入的每一个内容都反对意见。我在这里列出了初学者常犯的错误，以帮助你避免它们。

### 错误的大小写

在 UNIX 下，以下文件名将指向不同的文件：

* `acme`
* `aCme`
* `acMe`
* `acmE`
* `ACME`
* `acME`
* `aCMe`
* `AcMe`
* `AcMe`
* `AcmE`
* `Acme`
* `aCME`
* `AcME`
* `acME`

所有这些文件可能同时在同一个目录中运行，因为在 UNIX 下，字母是大写还是小写至关重要。起初，你的眼睛可能注意不到本该小写却写成大写的字母，反之亦然。要小心手写的 UNIX 命令指令，因为人们在书写时往往不注意大小写。

### 错误的空格

正如本章前面提到的，命令、选项和参数不能一起运行。它们必须通过空格隔开。在命令或路径中间插入空格同样是无效的。

### 误用方向键、Insert、Page Up 等

避免使用键盘上的特殊键，例如方向键、`Insert` 键、`Home` 键、`End` 键以及 `Page Up` 和 `Page Down` 键。Linux 是良好整合这些键的 UNIX 变体。对于大多数其他类型的 UNIX 系统，使用这些特殊键会在文件、电子邮件甚至文件名中插入插入序列。一旦你插入了这些垃圾内容，想要删除它们会非常困难。

如果你在文本文档、电子邮件或文件名中发现这样的垃圾：

```
^A^B^C^D
```
这是由于用户尝试使用方向键重新定位光标来纠正拼写错误导致的。

要显示文件名中的控制字符，请使用 `ls-b` 选项：

```bash
$ ls acme
acme
$ ls -b
acme
abm^M
```

在这里，`ls` 似乎显示同一目录下有两个名为 `acme` 的文件，我们知道这是不可能的。通过给 `ls` 添加 `-b` 选项，我们可以看到第二个文件名中的控制字符。该文件名是由用户创建的，他想将输出重定向到 `acme` 但误输入了 `abm`。他按了两次左方向键，并在 `bm` 之上输入了 `cme`，以便命令行显示为 `acme`。用户从未意识到自己犯了错误，因为一切看起来都很正常。

### 使用 Backspace VS Delete 修正错误

你应该如何退回并纠正输入错误？这取决于情况。退回和纠正错误的方法有两种：

1. 使用 `Backspace` 键或 `Ctrl+H`。
2. 使用 `Delete` 键或 `Ctrl+?`。

之所以变得复杂的原因是，在某些键盘上，`Delete` 键发送的是 ASCII DEL (127) 字符。在其他键盘上，它发送的是一个 ESC 序列。`Backspace` 键会发送 `Ctrl+H` 或 ASCII DEL。有时 `Backspace` 是可编程的，特别是当你使用 PC 登录 UNIX 时。有时 `Backspace` 会发送 `Ctrl+H`，而 `Shift+Backspace` 会发送 DEL，反之亦然。

为了消除困惑，请输入此命令：




```bash
$ stty -a speed 38400 baud
eucw 1:0:0:0, scrw 1:0:0:0
intr = ^c; quit = ^\; erase = ^?; kill = ^u;
eof = ^d; eol = <undef>; eol2 = <undef>; swtch = <undef>;
start = ^q; stop = ^s; susp = ^z; dsusp = ^y;
rprnt = ^r; flush = ^o; werase = ^w; lnext = ^v;
-parenb -parodd cs8 -cstopb -hupcl creadad -clocal -loblk
-crtscts -crtsxoff -parext
-ignbrk brkint ignpar -parmrk -inpck istrip -inlcr -igncr
icrnl -iuclc
ixon -ixany -ixoff imaxbel
isig icanon -xcase echo echoe echok -echonl -noflsh
-tostop echoctl -echoprt echoke -defecho -flusho -pendin
iexten
opost -olcuc onlcr -ocrnl -onocr -onlret -ofill -ofdel tab3
```

### 删除字符 (Erase Character)

第四行告诉你是系统是如何期望你删除字符的。你会看到 `erase` 被设置为 `^H`、`^?` 或 `DEL`。

要测试删除键，请输入此命令：
```bash
$ datex
```
删除字母 `x` 并按回车键。如果你看到了系统日期和时间，说明你使用了正确的键来删除字母 `x`。尝试分别使用 `Ctrl+H`、`Delete`、`Backspace` 和 `Shift+Backspace`，看看其中哪一个可以成功删除字母 `x`。希望你能够找到一个与当前设置兼容的删除字符。

如果没有，请按照如下方式将你的删除字符更改为 `Ctrl+H`：
```bash
$ stty erase Ctrl+H
```
在这里，通过按住 `Ctrl` 键然后按 `H` 键来输入 `Ctrl+H`。不要按 `C` 再按 `R` 再按 `L` 最后按 `H`。现在你应该能够使用 `Ctrl+H` 来退格输入了。如果你希望此更改永久，可以将此 `stty` 命令添加到你的 `.profile` 中。

### 使用三种引号类型

UNIX 使用所有不同的引号字符：
- `"` 引号，我称之为双引号。
- `'` 撇点键，我称之为单引号。
- `` `` 反引号，我称之为反引号（back quote）。

这些引号键在 UNIX 下下各有不同的用途，因此你必须根据不同情况使用正确的键。为了在一个参数中包含空格，请使用双引号或单引号包裹该参数：
```bash
$ mail -s'Meeting next week' fred jane Harvey
```
在这里，`mail` 命令允许使用 `-s` 选项来指定发送邮件的主题。`-s` 选项接受该选项的参数，即主题文本。单引号使 `Meeting next week` 短语成为一个完整的参数。

以下是错误的做法：
```bash
$ mail -s Meeting next week fred jane Harvey
```
在这里，单单词 `Meeting` 是邮件的主题，而短语 `next week` 是接收此邮件的用户列表的一部分。稍后你会收到一封邮件，提示系统无法交付给名为 next 和 week 的用户。

当你想要包含 shell 变量时，使用双引号：
```bash
$ mail -s "$PROJECT" fred jane Harvey
```
在这里，邮件的主题将包含两个词：shell 变量 `$PROJECT` 的内容和单词 `proposal`。

当你想要使用 shell 替换时，使用反引号。这允许你获取一个命令的输出并将其作为另一个命令中的文本：
```bash
lp `cat flist`
```
在这里，反引号内的命令将首先运行，显示文件 `flist` 的内容。该输出随后将替换原始命令中反引号内的单词。因此，`lp` 命令将紧跟一个 `flist` 文件中包含的文件名列表。随后将执行 `lp` 命令将这些文件打印到默认系统打印机。

#### 另参 (SEE ALSO)
- 有更多关于反引号和命令替换的信息，请参第 245 页
- 有更多关于正则表达式模式的引号的信息，请参第 393 页

### UNIX 在告诉我什么？ (What Is UNIX Telling Me?)

某些 UNIX 消息非常晦涩。本节告诉你如何解释常见的错误指示，以便你快速轻松地纠正错误。

#### 用法错误 (Usage Errors)

当你输入 UNIX 命令时，可能会收到的错误类型是用法错误：





# cp 用

```bash
cp [-fip] source_file target_file
cp [-r|-R][-fip] source_file... target_file
```

## 错误信息概述

记住“没有消消息就是好消息”，这个错误意味着出现了一些问题，你的命令没有执行成功。在这种情况下，错误信息意味着以下所有内容：

- 命令没有执行，是因为你犯了错误。
- 你误用了此命令。
- 这里是正确的用法（语法），希望你能够重新正确输入。

此用法错误是在告诉你 `cp` 同时需要 `source_file` 和 `target_file`，但你没有在命令行中同时输入这两个参数。用法说明还显示了可能的有效选项。由于它们显示在方括号中，因此不是必需的（是可选的）。

## > 符号 (PS2 提示符)

大于号（`>`）被称为 PS2 提示符。它出现在如下情况下：

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 用法意味着误用

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

我见过很多初学者忽略用法信息，并奇怪为什么不起作用。每当你看到用法信息时，请记住它是一个错误信息。你搞乱了命令，所以它没有正常运行。

```bash
$ mail -s"tomorrow jane fred" > quit
> exit:q!
```

当 UNIX 认为你正在输入一个多行命令时，就会出现 PS2 提示符。shell 在下一行使用这个独特的 PS2 提示符来警告你，你输入的内容是上一行开始的命令的一部分。在前面的示例中，注意到 mail 命令缺少闭合的双引号，因此命令是不完整的。PS2 提示符出现在下一行。在这种情况下，用户没有识别出 PS2 提示符并感到困惑，因为系统停止了对其命令的响应。他无法退出到 shell 提示符或重新登录。他应该使用 `Ctrl+C` 或 Delete 键终止该命令并重新输入整个命令。

某些情况下 PS2 提示符是有效的。例如：

```bash
$ lpstat -t |
> grep '^p104-' |
> awk '{print $1}' |
> while read $RR
> do
> cancel $RR
> done
```

## 管道命令

如果一行以管道符号（`|`）结束，这向 shell 表示该管道命令的剩余部分将在下一行输入。如果一个管道由多个命令组成，将每个命令放在单独的一行可以提高可读性。注意 PS2 提示符出现了，确认了我们正在输入一个长多语句命令。

如果你误触发了 PS2 提示符，请按 `Ctrl+C`、`Delete` 或 `Shift+Backspace` 来终止命令并返回 shell 提示符。参见后文关于中断键（intr key）的讨论。

## 换到下一行

与许多命令一样，`grep` 可以在指定了要在文件中查找的模式后接受文件名列表。如果没有提供文件，`grep` 将从标准输入读取要处理的行。这并不会将任何输出管道到 grep，因此它只是在等待键盘输入。

```bash
$ grep 'acme'
```

光标停留在第二行。如果你识别出了问题，你可能会让命令运行一会儿，认为它很快就会完成。但如果没有输入，它永远不会完成。

## 无法获取文件名状态 (Can't Stat)

`stat` 子程序是 UNIX 工具确定文件或目录信息的一种方式。如果命令无法 stat 文件名，就无法获取该信息。请检查确保你已正确输入了命令，并正确拼写了命令中的任何文件名或目录。还要检查预期的文件是否存在以及类型是否正确（例如目录文件与普通文件）。

## 当你的会话似乎挂起时该怎么办





如果你正处于 `vi` 中，你可能仍然处于插入模式。在这种情况下，你输入的所有命令都会显示在屏幕上，但不会被执行。按下 `Esc` 键退出插入模式。尝试现在是否可以使用普通的 `vi` 命令来检查你的文件，然后保存并退出，或者在不保存更改的情况下退出。如果这不能解决问题，请尝试下一个建议。

如果你在一个分页程序（pager program）中，输入会显示在屏幕上但不会被处理。按下 `Q` 键然后按 `Enter` 键，查看是否会终止分页程序并将你带回 shell 提示符。如果这不能解决问题，请尝试下一个建议。

尝试终止你正在运行的任何命令。按下 `Ctrl+C`、`Delete`、`Backspace`、`Shift+Backspace` 和 `Ctrl+\`，看看是否有任何一个可以将你带回 shell 提示符。如果这不能解决问题，请尝试下一个建议。

你的某些终端设置可能被干扰了。输入以下内容，但不要按下 `Enter` 键：

```bash
Ctrl+J stty sane
```

现在回到建议列表的开头，再次尝试这些建议。如果这不能解决问题，请尝试下一个建议。

如果你正在使用 Windows PC 或通过网络连接到 UNIX 的终端，可能是 UNIX 窗口没有焦点。点击窗口内部以选择它。一旦被选中，窗口的轮廓应该变得更深。在输入上述代码行后，回到建议列表的开头并再次尝试。如果这不能解决问题，请尝试下一个建议。

确保连接你到 UNIX 系统的电缆连接稳固。通常电缆应该紧紧拧好以避免连接问题。如果你发现电缆松动并纠正了它，请回到列表开头并再次尝试这些建议。如果这不能解决问题，请尝试下一个建议。

你的终端或 Windows PC 可能丢失了正确的设置。你应该记录如何设置你的终端或 Windows PC 以及如何检查设置是否正确。如果你从未这样做过，请使用相同的终端或 PC 程序检查附近的另一站，并将其设置与你的进行比较。如果你发现设置错误并进行了纠正，请回到列表开头并再次尝试这些建议。如果这不能解决问题，请尝试下一个建议。

某些网络或设备问题可能需要 10 分钟才会超时并将控制权交还你的工作站。如果你只卡住了几分钟，请总共等待 10 分钟，然后回到列表开头并再次尝试这些建议。如果这不能解决问题，请尝试下一个建议。

如果你通过终端连接，尝试关闭终端电源，数到 20，然后重新开启终端。这可能允许你再次与 UNIX 通信。警告：不要关闭 UNIX 系统本身。如果你不确定其中的区别，请不要继续。向你的系统管理员寻求帮助。

如果你通过 Windows PC 连接，请启动另一个到 UNIX 的连接并查看是否可以登录。如果成功，请终止无响应的窗口，并在新窗口中工作。

UNIX 系统本身可能宕机了，或者网络可能断了。询问其他用户是否也遇到了相同的问题。如果是，请向系统或网络管理员报告此情况。

作为最后手段，如果你在终端而非 Windows 工作站上，你可能需要杀死你的进程，看看新的登录提示符是否允许你通过以下程序登录：

### 如何杀死进程以获取新登录

1. 如果你在 Windows 工作站上，关闭 UNIX 窗口以结束该会话。启动一个新的 UNIX 窗口开始另一个会话。
2. 如果你处于挂挂的终端上，前往另一个终端或工作站并使用相同的 ID 登录。
3. 输入此命令，将 `fred` 替换为你的登录 ID：
```bash
who -u | grep fred
```
你应该看到类似这样的输出：
```
fred term/a Mar 15 19:12 . 9476 (10.1.1.7) fred pts/1 Mar 15 20:30 . 0302 (10.1.1.1)
```
4. 使用 `tty` 命令确定你当前的工作端口。例如：
```bash
$ tty /dev/term/a
```
5. 在 `who-u` 输出中找到对应挂起会话的行。`tty` 不匹配你当前的工作会话。寻找行末尾或附近的 PID 数字。在前面的示例中，PID `9476` 是工作会话的，因此 PID `0302` 必须是挂起的会话。如果你的结果不明，请寻求帮助。不要继续。
6. 如果你确定了挂起会话的 PID，通过输入以下两个 kill 命令来杀死该会话，将 `1032` 替换为挂起会话的 PID：
```bash
$ kill 1032
$ kill -9 1032
```




## 7. 转到挂起的会话并检查是否出现了新的登录提示符。如果是，请继续登录。如果没有，请向系统管理员寻求帮助。

### 另请参考
- 关于从 Windows 访问 UNIX 的更多信息，请参阅第 589 页。
- 关于 X 终端的更多信息，请参阅第 120 页。
- 关于 `ps` 和进程的更多信息，请参阅第 316 页。
- 关于杀死进程的更多信息，请参阅第 320 页。

### 预检你的 Intr 和删除键 (`stty`)
在本章前面的部分，我们讨论了如何确定你的删除字符以及必要时如何更改它。你可以使用相似的过程测试你的字符并在必要时进行更改。输入此命令：

```bash
$ date
```

不要按回车键。按下 `Ctrl+C`、`Delete`、`Backspace` 和 `Shift+Backspace`，看看这些键是否有哪个能让你回到 shell 提示符。如果是，输入 `date`（但不要按回车键）并再次尝试同一个键。如果它让你回到了 shell 提示符，那么它就是你的 `intr` 键。记录下该工作站对应的按键，因为它连接到了 UNIX。如果没有任何键或组合键有效，请按回车键进入一个新的 shell 提示符。输入此命令：

```bash
$ stty intr Ctrl+C
```

按住 `Ctrl` 键然后按 `C` 键输入 `Ctrl+C`。不要先按 `C` 然后 `R` 然后 `L` 最后按 `C`。现在你可以使用 `Ctrl+C` 来中断并终止当前作业。如果你想让此更改永久生效，可以将 `stty` 命令添加到你的 `.profile` 中。

### 将输出或错误保存到文件中
每个 UNIX 命令都可以访问三个功能：
- 标准输入 (`stdin`)
- 标准输出 (`stdout`)
- 标准错误 (`stderr`)

通常，所有的 UNIX 命令都使用系统提供的标准输出例程来显示其结果。命令使用标准错误例程显示任何错误信息。这些标准输出和标准错误例程的编写方式使得 shell 很容易将输出重定向到文件或管道而不是屏幕。命令使用了标准输出或标准错误例程，但它们并不知道输出实际上发送到了屏幕、文件，还是通过管道交给另一个 UNIX 命令。

并不是所有命令输出都进入标准输出或标准错误。某些错误信息会发送到系统控制台，因此不会通过标准错误，所以它们无法被重定向或保存到文件中。同样，某些命令输出可以直接发送到物理设备（例如用户的终端）。在这种情况下，输出无法被重定向或保存到文件中。然而，大多数命令输出都去往标准输出，大多数命令错误都指向标准错误。

- 关于标准输出或错误的更多信息，请参阅第 30 页。

### 将命令输出保存到文件 (>)
在 Bourne shell 或 Korn shell 中，使用大于号 (`>`) 将标准输出重定向到文件而不是屏幕：

```bash
$ cal 1998 > thisyear
```

在这里，`cal` 命令的输出将被存入一个名为 `thisyear` 的文件中，且不会显示在屏幕上。重定向输出到文件会在文件不存在时创建它。要将输出保存到当前目录，请使用基作为文件名。要将输出保存到不同的目录，请使用绝对或相对路径来指定文件。

shell 在实际执行命令之前会设置重定向。然后，shell 会从命令中移除所有重定向符号和文件，因此命令在运行时永远不会看到它们。以下操作与刚才的 `cal` 命令等效：

```bash
$ cal > thisyear 1998
$ > thisyear cal 1998
```

因此，在命令的任何位置指定重定向都没有区别。如果你在 Bourne shell 或 Korn shell 中，要创建一个空文件，请输入以下内容：

```bash
$ > filename
```

如果此命令给你返回 `Invalidnullcommand` 错误，说明你处于 C shell 中，该命令在那里不起作用。`>` 是 `1` 的简写。它们是等价的；因此，这两个命令是等效的。





```bash
$ cal 1998 > thisyear
$ cal 1998 1> thisyear
```

标准输出是通道 1，这解释了 `1>` 中的 `1`。

在较旧的 UNIX 系统上，你必须创建一个空文件，如下所示：

```bash
$ cat /dev/null filename # 旧方法，不再使用
```

如果你准备覆盖一个已存在的文件，shell 不给出任何警告。因此，在将输出重定向到该文件之前，你应该确保你的目标文件没有包含重要数据。

### 另另

有关重定向的更多信息，请参阅第 30 页。

### Korn Shell 中的 noclobber 选项

Korn shell 有名为 `noclobber` 的选项，它可以防止你重定向到已存在的文件：

```bash
$ date > junk # step 1
$ date > junk # step 2
$ set -o noclobber # step 3
$ date > junk # step 4
ksh: junk: file already exists
$ date >| junk # step 5
$ date > junk # step 6
ksh: junk: file already exists
$ set +o noclobber # step 7
$ date > junk # step 8
```

在步骤 1 中，我们通过将 `date` 命令的输出重定向来创建一个名为 `junk` 的文件。在步骤 2 中，我们用新信息覆盖旧的 `junk` 文件。注意没有产生错误。在步骤 3 中，我们在 Korn shell 中开启了 `noclobber` 选项。在步骤 4 中，我们再次尝试重定向到 `junk` 文件，但操作失败，并提示文件已存在。在步骤 5 中，注意即使开启了 `noclobber`，我们也可以使用大于符号（`>|`）来覆盖存在的文件。在步骤 6 中，注意对于普通重定向，`noclobber` 仍然有效。在步骤 7 中，我们使用 `+o` 取消 `noclobber`。在步骤 8 中，注意我们可以进行重定向。

### 输入文件不能同时作为输出文件

由于 shell 在命令开始之前会初始化输出文件，你不能将同一个文件同时用 UNIX 命令或管道的源和目标。

```bash
$ grep -v discontinued pricelist > pricelist # 不行
```

在这个示例中，我们想要删除文件 `pricelist` 中所有包含 `discontinued` 单词的行，并将结果保存到同一个文件中。在 `grep` 命令开始之前，`pricelist` 文件被初始化为空文件用于输出。因此，它找到了一个空源并立即结束，导致目标文件为空。使用管道时也是如此：

```bash
$ sort acme | grep -v discontinued > acme # 不行
```

实现此目的的方法是使用一个临时中间文件：

```bash
$ sort acme | grep -v discontinued > /tmp/tmp$$ # step 1
$ mv /tmp/tmp$$ acme # step 2
```

在这里，我们将管道或 UNIX 命令的输出保存到临时文件中，如果磁盘空间足够，通常放在 `/tmp` 中。我建议你使用以 `$` 结尾的文件。这会在文件末尾附加一个唯一数字，这样同时运行执行相同代码的其他用户就不会干扰我们。在步骤 2 中，我们获取临时文件并覆盖原始文件，完成操作。

## 保存到文件 (2>)

你可以独立于保存输出来保存错误信息。由于标准错误是通道 `2`，因此使用 `2>` 将错误保存到文件中：

```bash
$ anycommand 2> anycommand.err # case 1
$ anycommand > log 2> errs # case 2
$ anycommand 2> errs > log # case 3
$ anycommand > log # case 4
```

在情况 1 中，标准输出没有被重定向，因此它显示在屏幕上，而任何错误都会进入名为 `anycommand.err` 的文件，因此不会在屏幕上显示。在情况 2 中，标准输出到一个文件，标准错误去往另一个文件。在情况 3 中，在标准输出之前重定向标准错误或反之，没有区别。在情况 4 中，标准输出被重定向到一个文件。标准错误没有被重定向，因此任何错误将出现在屏幕上。

## 将输出或错误追加到文件 (>>)

使用双大于符号（`>>`）将标准输出或标准错误追加到文件中。*追加*（append）意味着保留文件中当前信息，并将新信息添加到文件末尾。如果文件不存在，此命令将创建它。

```bash
$ anycommand >> outlog 2>> errlog
```

由于标准输出和标准错误是独立的，你可以根据需要只追加到其中一个文件而不是另一个：

```bash
$ anycommand 2>> errlog > anycommand.out
```





# 将输出和错误保存到同一个文件 (2>&1)

要将标准输出和标准错误保存到同一个文件中，请使用 `2>&1` 重定向标准错误：

```bash
anycommand > anycommand.out 2>&1
```

你不能在 `2>&1` 内部放置任何空格，但在 `2` 之前必须有一个空格。在命令行中，`2>&1` 必须在重定向标准输出之后。`2>&1` 表示将标准错误重定向到与标准输出相同的地方。

### 将输出复制到文件和屏幕 (tee)

`tee` 管道的名称源于一个流过液体的管道图像，它随后呈 T 形分形成两根管道，使得一半液体流向一个方向，另一半流向另一个方向。对于 UNIX，`tee` 实际上会将重复的信息发送到两个不同的地方：标准输出和一个文件：

```bash
anycommand | tee filename
```

在这里，`anycommand` 的输出被存储在指定的 `filename` 中。相同的信息也会发送到标准输出，由于它没有被重定向，因此将显示在你的屏幕上。

```bash
anycommand | tee file1 | grep -v discontinued | tee file2 | pg
```

这个示例展示了在一个管道中使用两个 `tee` 管道。第一个 `tee` 管道将 `anycommand` 的输出保存到 `file1` 中。相同的信息进入标准输出，并传递给 `grep`，后者会删除任何包含 `discontinued` 单词的行。`grep` 的输出随后保存到 `file2` 中，并逐页显示在屏幕上。

`tee` 命令的 `-a` 允许将输出追加到指定的 `filename`：

```bash
anycommand | tee -a filename
```

# 第 5 章 UNIX 用户界面 (GUI)

### 介绍 GUI 和 X Windows

UNIX 可以运行在廉价的字符 ASCII 终端上，这些终端通常被限于 80 列 24 行文本或有限的图形字符。UNIX 还可以利用更贵的位图显示器，显示器可以显示图片、图像和图形，并使用鼠标与用户进行交互。第二种交互方式被称为 GUI，即图形用户界面。

GUI 屏幕看起来非常像 PC 上的 Windows 屏幕，带有被称为图标的小图片，代表程序和功能。与 Windows 一样，GUI 也使用鼠标使用户户通过指向图标并点击或双击来做出选择。UNIX GUI 通常还提供滚动条、按钮、对话框和菜单。这些元素可以让 UNIX 变得易用得多，特别是对于偶尔使用 UNIX 的 Windows 用户，他们可能记得输入 UNIX shell 命令所需的命令、选项和语法。即使对于经验丰富的 UNIX 用户来说，GUI 图标和图形通常也能对正在发生的情况提供更清晰的视图。由于 GUI 允许你在屏幕的窗口中启动 shell 命令行会话，它兼顾了两种者的优点。事实上，GUI 允许多个命令行窗口同时运行，每个窗口都相互独立运行。用户可以使用鼠标与这些不同的 shell 窗口交互，甚至从一个窗口剪切并粘贴文本到另一个。

### X Windows

大多数 UNIX GUI 实现都基于在 MIT 开发的 X Window 系统（也称为 `X11`），并由构成 X 联盟的各个公司进一步增强。`X11` 提供了一个图形例程库，可用于创建使用图形显示元素和鼠标输入的应用程序。尽管许多 UNIX GUI 实现运行在 UNIX 系统自身的控制台上，但 `X11` 也允许图形程序运行在通过以太网连接到主机 UNIX 系统的站上。`X11` 软件也可用于连接到 UNIX 系统的 Windows PC 和 Macintosh 系统运行图形程序。

## UNIX 系统的通用环境 (CDE)

（提供的文本列出了 CDE 相关主题的目录）：
- 在 UNIX 下使用图标 (GUI)
- 作者：steve Moritsu
- 在 UNIX 下使用鼠标 (GUI)
- 什么是 X Windows 和 Motif？
- 包含 Solaris UNIX 和两个 GUI
- UNIX 系统的通用环境 (CDE)
- 如何使用 CDE
- 从 CDE 运行 UNIX 命令
- 从 CDE 编辑文本文件
- CDE 文件管理器
- 通过 CDE 邮件处理程序发送和读取邮件





还有被称为 X 终端（X Terminals）的低成本工作站，它们是带有图形显示器和鼠标的极简计算机站。它们拥有 CPU 和内存，但通常没有硬盘。它们通过网络连接到 UNIX 主机，并可以运行 X11 应用程序。UNIX 主机负责高层程序计算，而 X 终端负责低层图形处理。这减轻了 UNIX 主机的开销，并允许在无需完整 PC 成本的情况下运行图形应用程序。

### 窗口管理器

窗口管理器是一种利用 X 窗口系统在图形屏幕上的窗口中启动任务、更改窗口大小、将窗口最小化为图标、将窗口最大化为全屏等的软件。其中最常见之一是由开放软件基金会（OSF，一家公司组成的联盟）开发的 Motif 窗口管理器。

### 控制台 GUI

大多数 UNIX 系统都有一个被称为系统控制台（system console）的特殊工作站。通常，这是一个带有鼠标和键盘的位图显示器，非常靠近计算机系统本身。控制台是显示任何意外系统警告的地方。控制台通常在计算机首次启动或关机时与计算机交互。在大型公司中，UNIX 计算机及其控制台通常被锁在计算机部门内部，普通用户永远见不到它们。另一方面，还有专门供主用户使用的 UNIX 工作站，该用户坐在控制台前运行 CAD（计算机辅助设计）或动画等应用程序。

现在的许多 UNIX 系统都提供了可以在系统控制台上运行的 GUI。在某些 UNIX 系统上，除了 GUI 控制台外，所有终端都是基于字符的，此时 GUI 控制台是唯一可以运行图形应用程序和显示图像的工作站。如果你的系统连接到互联网，UNIX GUI 控制台可能支持 Web 浏览器以便上网。如果你的系统有如 WABI 等应用程序，UNIX GUI 控制台可以运行 Windows 应用程序。如果你的系统网络包含运行 X11 的 X 终端或 PC，它们可能也能运行与图形 UNIX 控制台相同的应用程序。

### Solaris 桌面

Solaris 是来自 SunSoft Inc.（Sun Microsystems Inc. 的子公司）的操作系统。Solaris 的底层是 Sun 版本的 UNIX，称为 SunOS（目前为 5.6，基于 SVR4）。由于之前的 SunOS 4.x 版本基于 BSD UNIX，因此当前的 SunOS 尽管是 System V (SVR4) 类型的 UNIX，但仍然提供许多 BSD 工具。Solaris 还包含了 Sun 对 UNIX 的网络扩展，并包含了登录系统控制台时可以选择的两种不同的 GUI。这些在后续关于 OpenWindows 和 CDE 的章节中描述。与大多数 UNIX GUI 一样，它们提供了图形控制应用程序，用于编辑文本文件、操作文件和目录、读取/发送电子邮件以及执行系统管理。除了这些标准应用程序外，Solaris 还提供了许多其他。实际上，Solaris 为大多数应用程序提供了两个版本：OpenWindows 版本和 CDE 版本。有关 BSD 和 SVR4 的更多信息，请参阅第 19 页。

### Solaris GUI: OpenWindows

旧版本的 Solaris 提供了一个名为 OpenWindows 的 GUI，基于 Open Look Manager。图 5.1 显示了该 GUI 在一个屏幕上打开两个窗口示例：

1. 一个 UNIX 命令行窗口（称为 `cmdtool`）
2. 文件管理器窗口

![8227-0123a.gif](img/7b05f7fad269af1e56393d7e915798b.gif) 图 5.1 Solaris 旧版 GUI：OpenWindows。

注意每个窗口的左上角都有一个三角形。如果你单击该三角形，将看到以下选项。（双击没有效果）。括号 () 中的文字是选项含义的描述

- 关闭（Close）
- 最小化（Minimize，最小化为图标）
- 全屏（Full Size，还原）
- 切换（Toggle）
- 移动（Move，允许移动整个窗口）
- 调整大小（Resize，允许更改窗口大小）
- 后置（Back，将窗口移至其他窗口后面）
- 刷新（Refresh）
- 退出（Quit，终止并关闭此窗口）




如果你将光标移动到背景的空白区域并点击右键，将看到这些选项：

### 程序
- **属性**：（设置配色方案。）
- **工作站信息 . . .**：（系统名称和 IP 地址、内存、版本。）
- **帮助 . . .**
- **退出 . . .**：（注销。）

### 工具
如果你选择“工具”，将看到这些选项：
- **刷新**
- **重置**
- **功能键**
- **窗口控制**
- **保存工作区**：（登录时自定义。）
- **锁定屏幕**：（输入密码解锁。）
- **挂起**
- **控制台**：（启动命令会话以接收系统错误。）

如果你选择“程序”而不是“工具”，你将看到这些选项：
- **文件管理器**：（创建目录、复制文件、重命名、删除、磁盘。）
- **电源管理器**：（设置空闲时自动关机。）
- **文本编辑器**：（使用鼠标编辑文件。）
- **邮件工具**：（发送/接收邮件。）
- **日历管理器**：（安排预约、会议。）
- **命令工具**：（历史记录、命令与文件之间的剪切/粘贴。）
- **Shell 工具**：（简单的 tty 命令行。）
- **时钟**
- **计算器**
- **性能计数器**：（监控 CPU 使用率、磁盘等。）
- **打印**：（管理打印队列。）
- **音频工具**：（录制/播放声音。）
- **磁带工具**：（保存/恢复/列出磁带文件。）
- **图像工具**：（查看/保存 GIF, JPEG, PostScript, TIFF, . . .）
- **截图**：（保存 GUI 屏幕图像。）




# GUI 组件

- **图标编辑器 (Icon Editor)**：（创建您自己的图标。）
- **绑定器 (Binder)**：（将文件类型与图标、应用程序等连接。）
- **AnswerBook2**：（在线文档。）
- **演示 (Demos)**：（如何运行各种应用程序。）

## OpenWindows 文本编辑器

OpenWindows 文本编辑器提供了一个独特的分屏选项，允许您在同一个文件的两个部分之间进行编辑或剪切粘贴。请注意，本章稍后描述的名为 `CDE` 的其他 Solaris GUI 自带的文本编辑器并不具备此功能。然而，大多数 OpenWindows 程序都可以从 `CDE` 应用程序器的 OpenWindows 部分运行。相反，OpenWindows 无法运行较新的 `CDE` 应用程序。

OpenWindows 有一项功能，可以防止您指定的窗口在在使用后立即消失。在某些 OpenWindows 菜单或窗口中，左上角会出现一个小图钉图标。如果您点击图钉，它将固定您的窗口或菜单，使其在您做出选择后不会消失。您稍后可以从该窗口或菜单进行其他选择。如果您不再需要从该窗口或菜单进行任何选择，请点击图钉取消固定并允许其关闭。

这种较旧的 OpenWindows GUI 仍然适用于当前的 Solaris 系统，供那些不想切换到后续章节讨论的名为 `CDE` 的新 GUI 用户使用。

## Common 桌面环境 (CDE)

Solaris 包含一个名为通用桌面环境 (`CDE`) 的第二个 GUI，它基于 `X Window System` 和 `Motif Window Manager`。惠尔特-帕洛洛德、IBM 和 Sun 共同贡献了 `CDE` 的开发，因此这种相同的 GUI 现在出现在它们的 UNIX 版本中：`HP-UX`、`AIX` 和 `Solaris`。

SCO UNIX 采用了 `CDE` 标准。在它最新的发行版本 `UnixWare 7` 中，SCO UNIX 将 CDE GUI 作为默认设置。学习了这个 GUI 后，你将会发现在许多 UNIX 平台上找到它。

在 `CDE` 登录屏幕上，有一个标记为 `Options` 的按钮。可用选项之一是“安全会话 (`Failsafe Session`)”，这在您错误配置了显卡或屏幕分辨率时非常有用。登录 Solaris GUI 时，您可以在较旧的 OpenWindows 和较新的 `CDE` 之间进行选择。在 SCO `UnixWare 7` 上，您可以在较新的 `CDE` GUI 和旧版 SCO 系统上的 `Panorama GUI` 之间进行选择。

### 图 5.2：Solaris 2.x 上 CDE 的主面板

图 5.2 显示了 Solaris 2.x 上 `CDE` 的主面板。以下是标记数字的说明：

1. 点击此栏操作 `CDE` 主面板：移动（其位置）、最小化（将主面板最小为图标）、置底（将主面板置于任何重叠窗口下方）、刷新、注销。
2. 显示当前时间。
3. 显示当前的和日期。
4. 点击此三角形查看“文件夹 (Folders)”：`Home`（访问主目录）、`Floppy`（访问磁盘）、`CD-ROM`（访问 CD-ROM）。
5. 点击此三角形查看“个人应用程序 (Personal Applications)”：`Text Editor`（文本编辑器）、`Terminal`（UNIX 命令行）、`Web browser`（网络浏览器）。
6. `邮件应用程序 (Mailer application)`（发送/接收电子邮件）。
7. `锁定此工作站 (Lock this station)`（提示 UNIX 解锁）。
8. 四个独立的桌面区域可以打开窗口。
9. `EXIT`（注销 UNIX）。
10. 闪烁的 LED 表示 GUI 正在忙。
11. 点击此三角形查看“打印机 (Printers)”选项。
12. `样式管理器 (Style Manager)`（配置颜色、字体、背景、键盘、鼠标、蜂鸣声、屏幕、窗口、启动）。
13. 点击此三角形查看“应用程序 (Applications)”选项。
14. 点击此三角形查看“帮助 (Help)”选项（在线文档）。
15. `垃圾桶 (Trash Can)` 图标（将项目拖到此图标处即可删除）。双击此图标可查看可用文件：`Put Back`（还原）、`Shred`（永久删除）。
16. 点击此处最小化主面板。





## 图 5.2 CDE 的主面板。

在图 5.2 中，数字 4、5、11、13 和 14 指向三角形。当你点击三角形时，会打开一组选项。当选项打开时，三角形会翻转并指向下方，提醒你如果再次点击三角形，选项将会消失。每个三角形下方是该区域选项中的一个图标。它是一个快速启动图标，因为你可以点击该图标并直接从主面板启动它，而无需点击三角形并打开所有选项。

要更改主面板中三角形下方的快速启动图标，请遵循以下步骤：

1. 点击三角形以打开选项。
2. 将光标置于所需的图标上。
3. 右键点击一次。
4. 选择“复制到主面板”（`Copy to Main Panel`）。
5. 点击三角形以关闭选项。现在，你所需的图标应该已经出现在主面板中了。

在图 5.3 中，我们已经点击了“个人应用程序”（Personal Applications）三角形来打开那些选择。以下是图中标记数字的说明：

17. 点击此栏可获得这些选项：移动（Move，将此菜单保留在桌面上以便访问）、降低（Lower，将此菜单置于任何重叠窗口之下）、关闭（Close，关闭此菜单）。
18. 安装图标（Install Icon，将程序或文件图标拖到此处添加到此菜单。如果你想从菜单中删除它，请右键点击该菜单项）。
19. 文本编辑器（Text Editor，点击此处进入图形文本编辑器）。
20. 终端（Terminal，点击此处进入命令行窗口）。
21. 网页浏览器（Web Browser，点击此处启动 Java 浏览器）。
22. 菜单按钮（Menu button，点击此向下三角形可关闭菜单。三角形将指向向上，表示它可以用于打开菜单）。
23. 主面板快速访问图标（Main Panel quick access icon，这允许快速访问菜单中的一个项目。在示例中，它目前被设置为终端应用程序，但可以像之前描述那样轻松更改）。

图 5.3 个人应用程序。使用 Motif 窗口。

在图 5.4 中，我们使用 CDE 主面板启动了一个应用程序。使用 Motif 窗口管理器的 CDE 以及我们启动的每个应用程序都将在各自的 Motif 窗口中运行。图 5.4 显示了所有 Motif 窗口应用程序可用的窗口控件。

为什么不能使用垃圾箱？如果你在 CDE 中删除文件，可以从垃圾箱中恢复文件。然而，你无法从命令行这样做。使用 `rm` 命令时要小心，因为没有撤销删除的操作。

24. 点击此菜单按钮可获得这些选项：移动（Move，移动此窗口）、大小（Size，调整窗口大小）、最小化（Minimize，将窗口缩小为图标）、最大化（Maximize，将窗口放大为全屏，从此菜单恢复以撤销此操作）、降低（Lower，将此窗口置于任何重叠窗口之下）、关闭（Close，终止应用程序并关闭窗口）。切换菜单栏（Toggle Menu Bar，移除或恢复下方项目 29）。双击此菜单按钮作为调用关闭的快捷方法。
25. 标题栏（Title bar），在此点击并拖动可移动整个窗口
26. 此窗口中运行的应用程序名称
27. 最小化按钮（Minimize button，将窗口缩小为图标
28. 最大化按钮（Maximize button，将窗口放大为全屏）（再次点击此处可撤销此操作）。
29. 菜单栏（Menu bar，选项取决于应用程序）
30. 滚动条（Scrollbars）将根据需要出现在右侧或底部。

图 5.4 窗口控件。




如果你启动了多个应用程序，每个程序都将有自己的窗口。在向该应用程序输入文本之前，你必须先点击窗口内的任何位置来选择该窗口。这被称为激活该窗口或赋予该窗口焦点。活动窗口的边框颜色会变得更深。选择一个窗口将自动取消选择其他窗口。当窗口未被选中时，其边框将变为中性灰色。

在 `CDE Style Manager` 的 `Window` 部分中，你可以选择以下项之一：

- `点击窗口内位置以激活`(Point in Window to Make Active)
- `点击窗口以激活（默认）`(Click in Window to Make Active)

选择 `Point in Window to Make Active` 允许你只需将鼠标移动到该窗口即可选择它。我个人不喜欢这个设置，因为当我需要在屏幕的一端移动到另一端时，所有的窗口都会跳动，但不同的用户可以对此选项有不同的设置。

你可以通过之前列出的菜单按钮更改窗口大小（调整尺寸），或者通过将光标置在窗口的一个角上并拖动来放大或缩小窗口。

你可以通过之前列出的菜单按钮重新定位窗口在屏幕上的位置（即移动它），或者通过将光标置于标题栏内并拖动窗口到其新位置。

如果一个窗口在另一个窗口后面，你可以通过之前列出的菜单按钮将上方窗口降低（即将其放在另一个窗口后面）。或者，你可以点击下层窗口的任何可见部分，使其全部在前景中显示。

### 在窗口之间传输文本

Motif 允许你轻松地在两个窗口之间传输文本。窗口可能运行不同的应用程序；例如，你可以将文本从电子邮件传输到文本编辑器，或者将文本从帮助文档传输到 `UNIX` shell 命令中。传输文本有一种简单的方法，以及一种方法允许相同文本被记住并多次输入的长期方法。

#### 如何单次传输

1. 将光标移动到目标文本处选中所需的文本，按住鼠标左键并将光标拖动到文本末尾。然后释放左键。
2. 将鼠标光标移动到你想放置文本的地方，无论是在同一个窗口还是不同的窗口。如果该窗口正在运行 `UNIX vi` 命令，请使用 `vi` 命令定位 `vi` 光标，如果你还没有在该窗口中执行操作，则输入 `insert` 或 `append` 命令。
3. 点击鼠标中键或右键以插入文本。

#### 如何保存文本并粘贴一次或多次

1. 将光标移动到目标文本处选中所需的文本，按住鼠标左键并将光标拖动到文本末尾。然后释放左键。如果你有一只三键鼠标，现在可以通过移动鼠标指针并点击中键来粘贴选中的文本。如果你有一只双键鼠标，则必须执行以下步骤。
2. 在菜单栏中，点击 `Edit` 然后点击 `Copy` 以保存选中的文本。或者，如果 `Edit` 也显示 `Cut` 命令，你可以使用它保存文本并将其从当前应用程序中移除。
3. 将鼠标光标移动到你想放置文本的地方，无论是在同一个窗口还是不同的窗口。点击一次设置文本光标。如果该窗口正在运行 `UNIX vi` 命令，请使用 `vi` 命令定位 `vi` 光标，如果你还没有在该窗口中执行操作，则输入 `insert` 或 `append` 命令。
4. 在菜单栏中，点击 `Edit` 然后点击 `Paste` 在光标处插入保存的文本。如果你处于 `vi` 中，现在手动按 `Esc` 键退出 `Insert` 模式。

### CDE 支持什么？

CDE 可用于 `HP-UX`、`AIX`、`Solaris` 等。这些版本中的通常都支持基础 CDE 应用程序，例如：

- `File Manager`（创建、复制、删除文件和目录）
- `Text Editor`（编辑文本文件）
- `Terminal`（运行 shell 命令）
- `Mailer`（发送和读取电子邮件）
- `Print Manager`（查看 `UNIX` 打印队列）
- `Help`（查看此系统的在线文档）

某些系统（如 `Solaris`）增加了许多可以从 CDE 调用的其他应用程序，这些在其他系统中是找不到的。在 Solaris 下，你可以通过将光标移动到屏幕的空白部分、点击右键然后点击 `Programs` 来访问这些额外应用程序。Solaris 2.6 程序：




# CDE 应用概述

- **文件管理器**:（创建、拷贝、移动、删除文件和目录）
- **文本编辑器**:（用于编辑 UNIX 文本文件）
- **邮件服务器**:（发送和读取电子邮件）
- **日历**:（安排预约、会议）
- **网络浏览器**:（HotJava）
- **终端**:（运行 UNIX shell 命令）
- **控制台**:（类似于终端，但接收系统控制台错误）
- **时钟**:（可以放置在桌面上的图形时钟）
- **计算器**:（科学和财务图形化计算器）
- **性能仪表**:（图形化显示随时间变化的系统占用）
- **打印管理器**:（查看 UNIX 打印队列）
- **音频**:（录制和播放音频文件）
- **查看器**:（查看/保存 GIF, JPEG, PostScript, TIFF 等）
- **截图**:（保存 GUI 屏幕图像）
- **图标编辑器**:（创建自己的图标）
- **样式管理器**:（自定义 CDE 的外观）
- **应用管理器**:（访问更多程序）
- **桌面应用**:（程序以及 CDE 程序开发工具 App Builder）
- **桌面控制**:（样式管理器和无障碍访问）
- **桌面工具**:（格式化软盘、压缩文件等实用程序）

## 信息

- **信息**:（Readme 文件和 Answerbook2）
- **OpenWindows**:（来自旧版 OpenWindows GUI 的应用）
- **系统管理**:（Admintool，电源管理器等）
- **帮助**:（CDE 信息）
- **AnswerBook2**:（Solaris 和 SunOS 信息）

### CDE 中的详尽帮助

图 5.5 显示了 CDE 文本编辑器应用程序中的部分帮助目录。每个 CDE 应用都包含关于该程序屏幕和选项的有用信息。帮助文档使用了超文本链接（类似于网页），点击带有下划线的短语即可直接跳转到特定文档。超文本文档非常出色，因为它能向你展示章节中每个主题的概述，并让你快速进入到选择的主题和相关主题。

![8227-0134a.gif](img/34157b46b8bd3cf942d91a78eb7ee60c.gif)

图 5.5 CDE 中的详尽帮助。

##在 CDE 中运行 Shell 命令

`Terminal` 应用程序创建一个 CDE 窗口，你可以在其中输入 shell 命令，就像在字符终端上一样。你可以在多个窗口中运行此 `Terminal` 应用，因此同时运行并观察多个 UNIX 命令。你甚至可以如前节所述，在两个 UNIX Terminal 会话之间或 CDE 应用与 UNIX Terminal 会话之间剪切粘贴文本。

要启动 `Terminal` 应用，请点击图 5.3 所示的 `Terminal` 图标。在 Solaris CDE 下，你也可以通过移动到屏幕空白区域、右键点击然后选择 `Terminal` 来启动此应用。

在图 5.4 中，我们启动了 `Terminal` 命令行。以下图中标记的特定 `Terminal` 应用数字的说明：

1. **窗口 (Window)**：点击此处获取选项：新建会话，关闭/终止此窗口。
2. **编辑 (Edit)**：点击此处获取选项：拷贝高亮文本，粘贴已保存文本。
3. **选项 (Options)**：点击此处获取选项：终端特性（例如，允许 132 列，允许换行），窗口大小，字体大小。

当你启动 `Terminal` 窗口时，你不需要登录，因为你在 CDE 会话开始时已经登录了。如果你在 `Terminal` 窗口中输入 `exit`，将结束该窗口但不会结束 CDE 会话。要结束 CDE 会话，请点击 `EXIT` 单词（如图 5.2 所示）。

## 在 CDE 中编辑文本文件

`Text Editor` 是一个 CDE 窗口应用程序，你可以在其中创建和修改 UNIX 文本文件和系统文件。你也可以如之前所述，在此编辑器与其他 CDE 应用（如 UNIX Terminal 会话）之间剪切粘贴文本。

要启动 `Text Editor` 应用，请点击图 5.3 所示的 `Text Editor` 图标。在 Solaris CDE 下，你也可以通过移动到屏幕空白区域、右键点击、选择 `Programs` 然后选择 `Text Editor` 来启动此应用。

### CDE 文本编辑器--打开文件

在 `Text Editor` 中，你必须首先打开想要编辑的任何文件。点击 `File`, `Open`。你会看到一个图 5.6 所示的对话框。以下是图中标记数字的说明：

1. **文件 (Files)**：该框显示了可以通过双击文件名来打开的文件。
2. **过滤器 (Filter)**：该框显示了一个正则表达式模式，用于隐藏 Files 框中的某些名称。`[^.]*` 是默认值，用于隐藏隐藏文件（即以点开头的文件）。`^*` 将显示所有文件（隐藏和非隐藏），`a^*` 将仅显示以字母 a 开头的文件。
3. **路径或文件夹 (Path or folder)**：该框显示 Files 框中所示文件的 UNIX 目录。它初始为你的当前目录，但你可以将其改为任何所需的目录。点击右侧的三角形获取你可以选择的之前或其他目录的列表。
4. **文件夹 (Folders)**：该框显示路径框中目录的子目录。双击其中任何一个，该新目录的内容将显示在 Files 框中。你也可以点击 `..` 返回上一级父目录。




5. 在 `Filename` 框中，你可以输入所需文件的完整路径，而无需设置其他任何框。在此处按 Enter 键打开该文件。
6. 点击 `OK` 打开文件名框中显示的文件。
7. 点击 `Update` 更新 `Files` 和 `Folders` 框中的内容，包括任何最近更改。
8. 点击 `Cancel` 终止打开文件的尝试。

![8227-0137a.gif](img/6b23f4b003f9e7fbe60e89ffe4e11425.gif)
图 5.6 CDE 文本编辑器--打开文件。

**另另**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *有关正则表达式通配符的更多信息，请参阅第 388 页*

*CDE 文本编辑器--基础编辑*

你可以使用滚动条或 `Page Up` 和 `Page Down` 键在文件中移动。你可以使用 `Home` 键回到行首，使用 `End` 键移动到行尾。

你有两种输入文本模式。在 `Insert` 模式下，光标将是一条细线，你在行中间输入的任何字符都会将行的其余部分向右推。你可以通过按下 `Insert` 键切换到 `Overstrike` 模式，或者点击 `Options` 然后点击 `Overstrike`。光标将变为一个方块，你在行中间输入的任何文本将覆盖该处的现有文本。你可以通过再次按下 `Insert` 键或再次点击 `Options` 和 `Overstrike` 来切换模式。

`Backspace` 键将删除光标左侧的字符。如果光标是一个块，`delete` 键将删除光标下的字符。如果光标是一条线，`delete` 将删除光标右侧的字符。你可以通过拖动一段文本来显示它，然后按 `Delete` 键来删除该文本。

你可以在本文内部或窗口之间进行剪切粘贴或复制粘贴。请参见上一节关于在窗口之间传输文本的介绍。这是一个文本编辑器，而不是文字处理器。没有字体类型或大小选项。

### CDE 文本编辑器--检查拼写

要检查当前文件的拼写，点击 `Edit, Check Spelling`。这将打开一个如图 5 所示的对话框。以下是图中标记数字的解释：

1. Word（单词）是在你的文件中发现的问题。
2. Suggestion（建议）是拼写检查器找到的最佳替代方案。
3. 显示其他有效单词。你可以双击其中一个来替换你的单词。
4. 显示文件有多大比例已通过拼写检查。
5. `Change` 表示将 Word 替换为 Suggestion 一次。
6. `Change All` 表示在整个文件中将 Word 替换为 Suggestion。
7. `Skip` 表示忽略此 Word，但稍后如果发现相同的 Word 仍会标记。
8. `Skip All` 表示在整个文件中忽略此 Word。
9. `Learn Word` 将此词添加到你的个人字典中作为有效单词，这样在你对任何文件运行拼写检查时，它都不会再被质疑。
10. `Options` 允许你查看并从个人字典中删除单词。
11. `Stop` 停止拼写检查，但保持拼写检查对话框打开以便轻松重新启动。
12. `Close` 关闭拼写检查对话框。

![8227-0139.gif](img/4c59a23469972588bbb480ca.gif)
图 5.7 CDE 文本编辑器--检查拼写。

### CDE 文本编辑器--格式化段落

在 UNIX `vi` 命令中，格式化段落可能困难。这可能会导致某些文件的段落某些行太短，某些行太长。你可以使用 CDE 文本编辑器编辑这些文件并格式化问题的段落。启动 CDE 文本编辑器并打开所需的文件。将光标移动到问题的段落。点击 `Format`，然后点击 `Settings`。你会看到如图 5.8 所示的对话框。在此框中，设置左右边界的列数。然后选择你所需的段落对齐方式：`Left`（左对齐）、`Right`（右对齐）或 `Center`（居中对齐）。




你也可以选择 `Justify`（两端对齐）同时进行左右对齐，这会让你的段落看起来是整齐的块状。你可以点击 `Paragraph` 仅格式化当前段落，或点击 `All` 格式化整个文档。定义好设置后，下次需要格式化时，点击 `Format`，然后点击 `Paragraph` 或 `All`。

![8227-0140a.gif](img/a6f1aee29ddc0a67ac579c60b2515d4c.gif)
图 5.8 CDE 文本编辑器格式化段落。

# 通过 CDE 文件管理器复制和移动文件/目录

图 5.9 显示了如何从 CDE 主面板启动文件管理器。点击溢出文件的文件夹图标。在 Solaris 上，它被标记为 `Home Folder`（主目录），因为它会开始向你显示你的主目录。

图 5.10 显示了文件管理器窗口。以下是图中标记数字的说明：

1. 显示你所选目录的深度。带有斜杠的铅笔表示你对该目录没有写权限。你可以双击这些图标之一切换到该目录。

![8227-0141a.gif](img/cebca3a2256fbf5ddf03ba83c8a1d0c2.gif)
图 5.9 启动 CDE 文件管理器。

2. 显示每个目录的名称
3. 显示你所选目录的完整路径。你可以使用鼠标编辑此处并切换到不同的目录。
4. 显示你所选目录中的文件和子目录。你可以双击任何子目录切换到该目录。
5. 你可以点击 `..` 回到上一级。
6. 要重命名文件或目录，点击它并按需要替换名称。要将文件移动到子目录，将它的图标拖到该目录。要复制文件，按住 `Control` 键然后拖动文件。要将文件移动或复制到不同的目录，点击 `View`，然后点击 `New View`，这将启动另一个文件管理器窗口。在该窗口中选择目标目录并将文件拖到该目录。要创建符号链接，按住 `Shift` 和 `Control` 然后拖动文件图标。

![8227-0142a.gif](img/251a2488d75cd8ef81bf320852abf5.gif)
图 5.10 CDE 文件管理器。

要删除文件，将其拖动到 `Trash Can`（垃圾桶）图标处。要永久删除文件（称为粉碎），双击 `Trash Can`，选择所需文件，点击 `File`，然后点击 `Shred`。你可以不点击 `Shred` 而点击 `Put Back`（还原），这将撤销文件的删除。你可以将文件或文件夹拖到桌面以便于访问。

# 使用 CDE 邮件程序读取/发送电子邮件

UNIX 的 `mail` 和 `mailx` 工具对于 UNIX 新手来说非常困难。图形化的 CDE Mailer 应用程序让发送和接收电子邮件变得简单得多。它还可以处理附件，这是 `mail` 和 `mailx` 工具无法处理的。启动 CDE Mailer，点击主面板中的 `Mail` 图标（见图 5.9 中的数字 6）。随后你将看到如图 5.11 所示的 Mailer 窗口。以下是图中标记数字的说明：

1. 菜单栏
2. 此窗口显示信箱中每个邮件项目占的一行。行开头的 `N` 表示该项目从未被读过。菱形表示该项目包含一个或多个附件。
3. 此窗口显示窗口 1 中当前选中邮件项的正文。
4. 只有在存在附件时此窗口才会出现。
5. 删除当前邮件项。
6. 跳转并显示下一个邮件项。
7. 跳转并显示上上一个邮件项。
8. 点击此处回复发送者。这会将收到的邮件文本添加到回复中。
9. 点击此处将此邮件项副本转发给另一个用户。
10. 点击此处编写并发送新邮件。你也可以包含附件。
11. 打印邮件项。

![8227-0143a.gif](img/ada6bf14363f36cfb77d5d103072314a.gif)
图 5.11 CDE Mailer。




# 第二部分：与 UNIX 文件操作

CDE 邮件器允许你设置自己的邮件别名。如果你经常向一组固定的人员发送邮件，此功能将非常有用。点击 `Options`，然后点击 `Aliases`。为该组创建一个别名名称，例如 `salesteam`。在 `Addresses` 下输入人员列表。然后点击 `Add` 添加此别名。现在，你可以向 `salesteam` 发送一封邮件，该邮件将发送给组内的每位成员。

还有许多其他功能。你可以创建一个包含有用且具个人标识文本的签名，并将其添加到发出的邮件中。你可以设置 `Vacation Message`（休假回复），在指定的指定的日期内自动对收到的邮件进行回信。你可以在撰写邮件时检查拼写。你可以为邮件消息创建模板。你可以创建其他邮箱，以按项目分离和归档信函。所有这些及更多内容在“帮助”部分都有介绍，并带有超链接，可以帮助你快速到达所需的章节。

# 第 6 章列出、查找、显示或打印文件
作者 Steve Moritsugu

## 确定文件类型和文件内容类型

### 列出和查找文件

### 分页显示文件

### 添加行号和处理控制字符

### 使用标题

### 打印文件和管道

### 检查打印队列

### 取消作业

### 为打印格式化输出

## 介绍文件

我们从第 2 章“目录和路径名”中已经了解许多关于 UNIX 知识。从那一章，我们了解到 UNIX 通过称为 `inode`（索引节点）的数字来访问文件。人类则通过文件名访问文件，文件名可以包含任何字母、数字或标点符号，现代 UNIX 系统允许文件名包含数百个字符。所有文件都组织在树形目录系统中。然后我们可以通过`绝对`路径或`相对`路径访问任何文件。

### 如何确定文件类型 (ls)

UNIX 下最常见的文件类型称为`regular file`（普通文件）。程序、数据文件、文档、文本文件、系统实用程序和系统配置表都是普通文件。`COBOL` 或 `BASIC` 等应用程序语言可以在 UNIX 下创建顺序文件（从头到尾按顺序读取）或索引文件（包含键字段，可快速访问所需数据）。对于 UNIX 来说，这些都是普通文件。

UNIX 不支持连续文件（即连续文件的所有块分配在磁盘的一个区域内相邻）。由于 UNIX 是一个`多用户、多任务`操作系统，磁盘服务来自多个用户和多个作业请求，将一个文件的所有块聚集在一起的好处有限。

`Directories`（目录）是 UNIX 下第二常见的文件类型。它们包含该目录内的文件名列表以及每个文件的 inode 号。每个目录都是 UNIX 文件，因此它也有一个 inode 号。

另一种重要的文件类型是`device file`（设备文件），也称为`device node`（设备节点）。对硬件设备（如磁带驱动器或软磁盘）的所有访问都是通过访问该设备节点文件完成的。存在两种设备节点：用于原始访问设备的字符设备节点，和用于经过处理后访问设备的块设备节点。某些设备可以通过字符节点和设备节点同时进行访问。设备节点也被称为`special files`（特殊文件）。

另一种重要的文件类型是`symbolic link`（符号链接），它是指向系统中另一个文件的指针。

还有几种其他 UNIX 文件类型由系统使用，但普通用户永远不需要了解它们。

### 如何确定文件类型

1. 输入 `ls -l`。在接到指示前不要按回车。`ls` 的 `-l` 选项将显示每个文件的详细信息，包括文件类型。




2. 输入一个空格，然后输入要列出的文件或文件。你可以指定当前目录下的 `basename`，也可以指定指向另一个目录的绝对路径或相对路径。如果你在此输入一个目录名称，`ls` 将显示该目录中每个文件的信息。
3. 按回车键执行你的命令。输出每行开头的字符将根据下表告诉你该文件的 UNIX 文件类型：

### 表 6.1 `ls -l` 使用的文件类型字母。

| 文件类型字母 | 描述 |
| :--- | :--- |
| - | 普通文件 |
| d | 目录 |
| l | 符号链接或软链接 |
| b | 块设备节点文件 |
| c | 字符特殊设备节点文件 |
| p,s,m | 你可能会遇到的其他类型 |

以下是上述步骤的示例，显示了各种文件类型。`ls` 命令是一个系统命令，`passwd` 是文本文件，`fd0` 是软驱的设备节点，`tmp` 是目录，而 `uncompress` 是指向压缩程序的符号链接。

```
ls -ld /bin/ls /etc/passwd /tmp /dev/fd0 /dev/rfd0 /usr/bin/uncompress
-r-xr-xr-t   1 bin      bin           43296  May 13  1997
/bin/ls
brw-rw-rw-   2 bin      bin           2, 64  Feb 13 10:11
/dev/fd0
crw-rw-rw-   2 bin      bin           2, 64  Feb 13 10:11
/dev/rfd0
-rw-rw-r     1 bin      auth          3001  Feb 16 16:01
/etc/passwd
drwxrwxrwt   7 sys      sys           3072  Feb 20 11:16  /tmp
lrwxrwxrwx   1 root     root            40  Feb 13 10:02
/usr/bin/uncompress -> /usr/bin/compress
```

在前面的示例中，我们使用 `ls` 的 `-l` 选项产生包含每个文件详细信息的长列表。我们使用 `-d` 选项是为了让 `ls` 显示目录本身的信息，而不是按照它的习惯显示目录的内容。关于符号链接的更多信息，请参见第 197 页

### 确定文件内容的类型

要确定文件内容的类型，请使用 `file` 命令。为命令提供你想确定类型的文件名：

```
file /bin/ls: ELF 32-bit MSB executable SPARC Version 1, dynamically linked, stripped
```

在前面的示例中，我们看到 `/bin/ls` 文件是一个系统程序，它被编译为为运行 Solaris 的 SPARC 系统产生执行代码。在下一个示例中，我们使用星号（`*`）文件名通配符来确定当前目录下所有非隐藏文件的类型：

```
file * acmetab: ascii text
report7: English text
report8: empty file
rpio: executable shell script
cpiofile: ASCII cpio archive
```

在前面的示例中，`file` 命令会对文件内容的类型做出最佳猜测，通常仅基于分析文件的开头。在某些情况下，该命令会使用文件中嵌入的魔数（magic number），并在魔数表中查找内容类型（通常在 `file /etc/magic` 中找到）。

### 使用 `ls` 列出文件

我们可以使用 `ls` 命令列出当前目录或不同目录下的文件名。

1. 在 shell 提示符下，输入 `ls`。在接到指示之前不要按回车。
2. 输入一个空格，然后输入任何所需的选项（请参附录中 `ls` 下的可能选项列表及其含义）。如果存在多个选项，可以像示例所示逐个输入：
```
ls -l -a -L
```
选项也可以组合成一组，如下所示：
```
ls -la
```
3. 输入空格，然后输入一个或多个要列出的目录或文件。在输入的每个目录或文件之间输入空格。输入目录会导致 `ls` 的输出出该目录的内容（除非指定了 `-d` 选项）。此文件和目录列表也可以包含由文件名通配符模式生成的文件列表。如果文件名或目录位于当前目录，只需输入其 `basename`。否则，输入该文件或目录的绝对路径或相对路径。
4. 如果你想一次显示一次 `ls` 的输出（这样行在你可以阅读之前不会离开屏幕），输入一个空格。然后输入此行：
```
pg
```

### 理解坏数字错误




如果你遇到此 UNIX 错误，意味着该程序正在检查文件中的一个特殊标记（即魔数，magic number），以确认该文件具有预期的内容类型。如果文件的魔数错误，则它要么是损坏了，要么是错误的文件。

你可以将 `pg` 替换为 `more` 命令或 `less` 命令，取决于你的 UNIX 系统支持哪种分页器工具以及你最喜欢的分页器工具。这些内容在本章的稍后部分会有更详细介绍。

5. 除了执行第 4 步，你还可以选择将 `ls` 的输出保存到文件中。输入一个空格，然后输入此行：
```bash
> filename
```
将 `filename` 替换为你想要保存结果的文件的绝对或相对路径。

6. 除了执行上述第 4 或第 5 步，你还可以选择一次性完成这两个步骤——即将结果保存到文件中，并同时逐页查看结果。输入一个空格，然后输入此行：
```bash
tee filename pg
```
将 `filename` 替换为你想要保存结果的文件的绝对或相对路径。你可以将 `pg` 替换为 `more` 命令或 `less` 命令，取决于你的 UNIX 系统支持哪种分页器工具以及你最喜欢的分页器工具。这些内容在本章的稍后部分会有更详细介绍。

7. 按回车执行你的命令。

以下是一个 `ls` 命令示例：
```bash
ls -l pg
```
1 2 4 4

在前例和接后的示例中，命令的每个单词下方都出现了生成该单词的步骤编号。在前例中，我们以长格式列出当前目录下的所有非隐藏文件，以查看每个文件的详细信息。我们使用 `pg` 工具逐页显示结果。

这是另一个 `ls` 命令示例：
```bash
ls -aid /usr/reports /usr/jane/* > ls.save
```
1 2 3 5 5

在这个示例中，`-a` 选项向我们显示非隐藏文件和隐藏文件。`-i` 选项显示文件的 `inode number` 及其名称。`-d` 选项显示列出的任何目录本身而非其内容。接下来，我们指定要列出的文件。第一个是 `/usr/reports`。如果这是一个目录，由于 `-d` 选项的作用，我们将看到该目录的信息（而不是该目录的内容）。在此示例中，该文件被指定为绝对路径。第二个要列出的文件是 `/usr/jane/*`，这是一个文件名通配符（Filename Wildcard）。shell 会将此模式单词替换为 `/usr/jane` 中所有非隐藏文件的列表。然后 `ls` 命令对所有这些文件名进行操作，就像我们逐个输入它们而不是输入通配符模式一样。该命令的结果不会显示在屏幕上，而是进入当前目录下的 `ls.save` 文件中。

另请参考
关于重定向和管道的更多信息，请参阅第 26 页。
关于文件名通配符的更多信息，请参阅第 23 页。

### 如何通过名称查找文件

`find` 命令可以轻松遍历 UNIX 树的全部或部分，并向你显示它找到基名（basename）的位置。在每天处理几十个文件时，很容易丢失路径。`find` 可以帮助你根据各种标准定位文件。

### 根据名称查找文件

如果你只知道目标文件的基名，但不知道其路径，可以使用 `find`。当你只知道基名的一部分时，甚至可以使用文件名通配符（第 9 章介绍）。

1. 在 shell 提示符下，输入 `find`。在接到指示前不要按回车。
2. 输入一个空格，然后输入你想开始搜索的目录。像它是当前目录的子目录一样输入目录。否则，输入目录的绝对或相对路径。要搜索整个系统，请输入此行作为根目录：
```bash
/
```




若仅搜索当前目录及其子目录，请输入点（`.`）；这表示当前目录。`find` 命令会搜索起始目录的所有子目录（除非在下方第 5 步中提供了 `-mount` 选项）。

如果系统中有很多文件，`find` 完成可能需要很长时间。如果你能指定根目录（`/`，即整个系统）以外的起始目录，那么 `find` 命令将执行得快得多。

3. 输入一个空格，然后输入 `-name`。

4. 输入一个空格，然后输入你正在查找的文件名。如果你只知道名称的一部分，请使用此标符号输入该名称部分：
```
'*partname*'
```
例如，如果您要找的文件名包含 acme，请输入：
```
'*acme*'
```
在读过文件列表和文件名生成通配符（第 9 章）之后，你可以使用任何这些通配符来指定你正在查找的文件。记住将通配符模式放在单引号内。

5. 如果需要，你现在可以输入任何其他搜索标准，以便只查看特定大小、所有者、权限等的文件。请参阅附录中 `find` 条目获取此类选项列表。例如，你现在可以添加 `-mount` 选项，防止 `find` 挂载点进入其他文件系统（即其他磁盘驱动器）。

6. 输入一个空格，然后输入：`-print`。
按 Enter 完成你的 `find` 命令。你也可以执行下方更有挑战性的第 7 步来代替第 6 步。

7. 输入一个空格，然后输入：`-exec ls -l {}`。这是第 6 步的替代方案。它向你显示与 `ls -l` 相同的文件信息。如果需要，你也可以输入 `-exec` 后跟不同的命令，以便对选定的每个文件执行某些操作。有关 `-exec` 的更多信息，请参阅附 `find`。

8. 如果你想逐页查看 `find` 命令的输出（这样行在你阅读它们之前就不会离开屏幕），请输入一个空格。然后输入此行：
```
pg
```
你可以将 `pg` 替换为 `more` 或 `less`，取决于你的 UNIX 支持哪种分页器以及你最喜欢的分页器。这些内容在本章稍后的部分会有详细介绍。

9. 与执行第 8 步相比，你也可以选择将 `find` 的结果保存到文件中。输入一个空格，然后输入此行：
```
> filename
```
将 `filename` 替换为想要保存结果的文件的绝对或相对路径。

10. 与执行第 8 步或第 9 步相比，你也可以选择同时完成这两件事；即你可以将结果保存到文件中并逐页查看结果。输入一个空格，然后输入此行：
```
tee filename pg
```
将 `filename` 替换为想要保存结果的文件的绝对或相对路径。你可以将 `pg` 替换为 `more` 命令或 `less` 命令，取决于你的 UNIX 系统支持哪种分页器以及你最喜欢的分页器。这些内容在本章稍后的部分会有详细介绍。

11. 按 Enter 执行你的命令。

12. `find` 命令的输出是一个路径列表。每个路径都从你在第 2 步中指定的目录开始。如果你在第 2 步中指定了绝对路径，所有生成的文件都是绝对的。如果你在第 2 步中指定了相对路径，则所有文件都是相对的。这是一个 find 命令示例，每个单词下方是生成该单词的程序步骤：
```
find /usr/fred -name report7 -print
```
在前面的示例中，起始目录是一个绝对路径，因为它以 `/` 开头。因此，该 `find` 命令生成的所有路径也是绝对路径。以下是上述 `find` 命令的一些可能输出：
```
/usr/fred/report7
/usr/fred/acme/reports/report7
/usr/fred/pegasus/report7
```
这是另一个 find 命令示例，再次显示了生成命令每个单词的程序步骤。该 find 命令的起始目录是点（`.`），它表示当前目录。该命令在当前目录及其子目录中找到包含部分名称 `report27` 的所有文件名。`-user` 选项告诉 `find` 考虑...



仅包含用户 `Fred` 拥有的文件。此 `find` 命令的结果同时输出到名为 `/tmp/findlog` 的文件和屏幕上，逐页显示。

```
find . -name '*report27*' -user fred -print | tee /tmp/findlog | pg
```

前一个命令的起始目录是一个相对路径，命令的输出也是以点（`.`）开头的相对路径。以下是前一个命令的可能输出：

```
./casereport273a ./1998/reports/acme.report27-2-98
```

### 延伸
关于后台运行作业更多信息，请参第 319 页。

关于使用 `find` 根据最后访问日期或最后修改日期查找文件的更多信息，请参第 153 页。

### find 选项对比 find 操作 (*find*)

`find` 命令有许多选项，包括 `-name` 和 `-user`，它们允许我们指定文件被 `find` 命令选取时必须满足的条件。`-type` 是另一个 find ，允许我们指定文件类型（例如目录或普通文件）。不满足 find 条件的文件不会被选取。（参见附录中 `find` 的条目获取可能的 find 选项列表。另见 `find` 的帮助页。）这些 find 选项可以以任何组合和顺序使用。

在指定所有所需的选项后，你应该用一个或多个操作来结束你的 `find` 命令。`-print` 选项是最常用的操作，因为它只需指示系统显示找到的文件。如果你忘记包含操作，某些系统将默认假设为 `-print`。但在其他系统上，`find` 将花费所需的时间来定位文件，但由于你忘记输入操作，它将不会显示任何内容。始终指定操作是一个好习惯。

另一个实用的操作是 `-exec`，它允许我们指定一个在每个找到的文件上运行的 UNIX 命令。在命令中使用 `{}` 来指定插入文件名的位置。该命令必须以空格后跟 `\;` 结尾。。以下是一个 `find -exec` 命令的示例，它查找任何基名为 `core` 的文件并将其从系统中删除。`rm` 的 `-f` 选项意味着如果你对被删除的文件没有写权限，则不需要确认；也就是说，它对所有删除操作都给予强制确认。

```
find / -name core -print -exec rm -f {} \;
```

注意上述命令中发生了两个操作：`-print` 显示找到的 core 的路径，以及`-exec` 删除它们。以下是一个重命名当前目录及其子目录下所有普通文件的 find 命令示例。该命令为所有普通文件名添加了 `.old`。

```
find . -type f -exec mv {} {}.old \;
```

### 如何查找内容包含某个单词的文件 (*find,grep*)

有时你对文件名一无所知，但你知道文件中包含某个独特的单词。你可以像这个例中一样找到所有此类文件：

```
find / -exec grep {} /dev/null \;
```

将 `WORD` 替换为你想要搜索的单词。你可以在 `WORD` 中包含正则表达式通配符（在第 15 章“搜索文件或管道中的行”中介绍），但此时你应该将 `WORD` 括在单引号中。在前面的示例中，`find` 命令调用 `grep` 命令检查系统中的每个文件，查看其是否包含给定单词。包含第二个空文件（`/dev/null`）会导致 `grep` 显示文件名以及包含该单词的行。

前面的示例让你对如何使用 `find` 和 `-exec` 有了概念，但也要意识到这种方法效率低下，需要很长时间才能完成，因为它调用了多次 `grep` 命令。这里是实现相同功能的更高效的方法：

```
find / -print | xargs grep WORD /dev/null
```

`xargs` 的用法在第 9 章中描述。这种方法更高效，因为 `xargs` 对每组文件只调用一次 `grep`。

### 延伸
关于 `xargs` 的更多信息，请参第 247 页。

### 在 find 选项中使用逻辑 AND、OR 和 NOT

每当你指定多个 find 选项时，所有选项都必须通过，文件才能被选取。这在实际上是逻辑与（AND）的情况。

```
find / -name acme -user fred -type d -print
```



上一个示例包含三个选项和一个操作。文件必须通过所有三个选项才能执行该操作。在这种情况下，基名（basename）必须是 `acme`，且所有者必须是 `fred`，并且它必须是一个目录。

可以使用 `-o` 命令来表示逻辑或（OR），并可以使用*转义*的括号进行分组，如下例所示：

```bash
find / \( -name acme -o -user fred \) -type d -print
```

在上述示例中，我们正在寻找基名为 `acme` 或所有者为 `fred` 的文件。无论哪种情况，如果让 `find` 选择并显示这些文件，它们必须是目录。请注意，转义括号周围必须有空格。

为什么要使用转义括号？

通常情况下，我们使用括号是为了告诉 shell 在子壳中运行括起来的命令。我们对括号进行转义（即在前面加一个反斜杠 `\`），是为了告诉 shell 忽略它们并将它们传递给 `find` 命令。

感叹号（`!`）可以用于反转或否定某个条件，如下例所示：

```bash
find / ! -user fred -print
```

在上述示例中，`find` 显示所有所有者不是 `fred` 的文件。请注意，感叹号（`!`）周围必须有空格。

### 显示文件

以下是 UNIX 环境下显示文件的命令和选项的概述。

## 显示小文件

显示小文件的标准方法是使用 `cat` 命令：

```bash
cat filename
```

在 UNIX 中，`cat` 一词与“显示”是同义词，因此指令可能会让你 `cat` 一个文件，或者提到 `catting` 一个文件。

## 分页显示文件/管道

UNIX 命令没有一次显示一屏（即一页）结果的选项。这是因为你始终可以将输出管道到你喜喜欢的分页器（pager）工具，并让它一页页显示输出。UNIX 下有三种常用的分页器：`pg`、`more` 和 `less`。

遗憾的是，你不能只学习其中一个，因为某一个在某些类型的 UNIX 系统上可能不存在。每个分页器都有一套略有不同的命令。某些工具（如 man 页面）会自动调用这些分页器之一，这让初学者感到很困难，因为现在你必须弄清楚你处于哪种分页器中以及如何让它工作。

通常，商业 UNIX 系统提供 `pg` 和 `more`。`pg` 选项的功能最全，但 `more` 通常是默认分页器。商业 UNIX 系统通常不提供 `less` 分页器。Linux/GNU 提供 `less` 分页器，但通常不提供 `pg` 或 `more`。

这些分页器都有两种用法：

1. 在命令行上指定一个或多个文件，如下例：
```bash
pg file1 file2
more file1 file2
less file1 file2
```

2. 你可以将输出管道（`|`）到这些任何一个分页器。这将一次显示 `ls -l` 的输出：
```bash
ls -l | pg
ls -l | more
ls -l | less
```

如果你既将输出管道到分页器，又给分页器提供了文件列表，分页器将显示文件列表并忽略管道数据。

如何识别你处于哪种分页器中：
如果每个屏幕的底部看起来像这样，那么你正在运行 `pg` 工具：
```
--More--(34%)
```
如果看起来像这样，你正在运行 `more`：
```
Filename (34%)
```
如果看起来像这样，你正在运行 `less`：
```
--More--
stdin
```

如何跳转到下一页：
- `pg`: 按下 `ENTER` 键
- `more`: 按下空格键
- `less`: 按下空格键

如何跳转到上一页：
- `pg`: 按减号 (`-`）
- `more`: 按 `Ctrl+B`
- `less`: 按 `Ctrl+B`

如何跳转到 `STRING` 的下一次出现处：
- `pg`: 按下 `/`
- `more`: 按下 `/`
- `less`: 按下 `/`

如何跳转到文件末尾：
- `pg`: 按下 `$`
- `more`: 按下 `G`
- `less`: 按下 `G`

如何回到文件开头：
- `pg`: 按下 `1`
- `more`: 按下 `1G`
- `less`: 按下 `1G`

如何重新显示当前页：
- `pg`: 按下 `.`
- `more`: 按下 `Ctrl+L`
- `less`: 按下 `Ctrl+L`

如何显示分页器中可用命令的帮助菜单
- `pg`: 按下 `h`
- `more`: 按下 `h`
- `less`: 按下 `h`





# 如何向下滚动半页
(当你对屏幕底部的内容感兴趣并想查看周围行时，这非常有用)

- `pg`: `d`
- `more`: `d`
- `less`: `d`

## 即使不在文件末尾如何退出分页器
- `pg`: `q`
- `more`: `q`
- `less`: `q`

## 比较商业 UNIX 系统上的 pg、`more` 和 `less`

商业 UNIX 系统通常不提供 `less`。`less` 拥有 `pg` 的所有功能，并且 `more` 命令的一致超集。`more` 的功能非常有限——通常没有方法跳到末尾或向后移动。当你通过管道 (`|`) 使用 `more` 时，情况尤为如此。

`pg` 比 `more` 更用，因为它可以后移动、跳转到文件结尾、跳转到文件开头等。遗憾的是，无法通过 `pg` 确定你处于文件的什么位置。

在巨大的管道中使用 `pg` 时要小心。当你显示管道输出并使用 `pg` $ 命令时，可能需要很长时间才能完成，因为系统会将遇到的所有文本保存在临时文件中，以便你根据需要返回第一页。某些系统没有足够的临时空间来存储大文件，当空间耗尽时，所有用户任务都可能被中断，系统可能会崩溃。`pg` 有一个功能在你想要定位文件中某个单词的所有出现处时非常有用。通常这很难，因为查找单词的斜杠 (`/`) 命令从当前屏幕的末尾开始搜索。如果一个屏幕上有多个出现处，你可能会漏掉一些。“巨大”到底有多大？你什么时候需要开始担心使用管道会导致系统崩溃？分页器通常在 `/tmp` 中构建临时文件。使用 `df` 命令检查 `/tmp` 中有多少空闲块，或者如果 `df` 未显示 `/tmp` 则检查根目录。该空闲块计数就是你的限制，但为了安全起见，你不应该达到那个程度。

## 使用 `pg` 查找字符串的所有出现处

1. 使用 `pg` 查看文件或管道。
2. 在运行 `pg` 时，输入此行：`/string/b`
   - 将 `string` 替换为你要查找的文本。如果没有 `/b`，找到的字符串将放在屏幕的第一行。`/b` 告诉 `pg` 将本次及以后搜索找到的行放在屏幕底部。
3. 要查找 Find 相同字符串的下一个出现处，输入此行：`/`
   - 系统将使用上一个字符串。因为第 2 步中给了 `/b`，字符串的下一个出现处将位于底行。如果没有第 2 步中的 `/b`，你可能会漏掉某些出现处，因为 `/` 假设你已经在当前屏幕的任何地方找到了所有匹配项，并从屏幕底部开始搜索。
4. 根据需要重复步骤 3 直到文件末尾。

### 另外
关于 `df` 命令和文件系统可用块更多信息，请参见第 93 页

### 在文件显示中添加行号 (`nl`,`cat`)
你可以使用 `nl`（编号行）或 `cat -n` 为文件或管道的显示添加行号，例如所示：

```
$ cal | nl     1 February 1998
      2 S M Tu W Th F S
      3  1 2 3 4 5 6 7
      4  8 9 10 11 12 13 14
      5 15 16 17 18 19 20 21
      6 22 23 24 25 26 27 28

$ cal | cat -n
      1     February 1998
      2  S M Tu W Th F S
      3  1 2 3 4 5 6 7
      4  8 9 10 11 12 13 14
      5 15 16 17 18 19 20 21
      6 22 23 24 25 26 27 28
      7  8
```

在前面的示例中，我们取了一个月的日历并将其通过化，以便每行都编号。请注意 `cat -n` 会为所有行编号。`nl` 命令则不对空行编号。然而，某些选项可以改变这种行为。

- 要对所有行（包括空行）编号，输入此行：`cat -n nl -ba`
- 要仅对非空行编号，输入此行：`cat -nb nl`





`cat` 和 `nl` 都接受命令行上的文件列表。如果没有提供任何文件，它们将从标准输入读取内容，这样你就可以将数据管道传输这些命令。某些 UNIX 系统可能并不同时支持这两个命令，因此了解这两个命令是否都可用是很有用的。

## 显示包含控制字符的文件 (cat, od, strings)

文本文件仅包含打印字符，而二进制文件可以包含所有可能的字符值，包括我们所说的*控制字符*的范围。如果你将二进制文件显示在屏幕上，文件中的控制字符可能会为你的终端设置不必要的模式，导致后续所有输出显示为乱码或无意义，甚至可能让你的终端完全停止响应。

在显示未知文件之前，请使用本章开头讨论的 `file` 命令来查看它是否为文本文件。如果不是文本文件，那么简单地将其显示在屏幕上是不安全的。确实有一些安全的方法可以查看二进制文件的文本，正如我们将在本节中看到的那样。

`od` 命令代表 octal dump（八进制转储）。该命令以八进制（即使用 8 计数法）显示文件或管道中的每个字，如下例所示：

```bash
# od /bin/ls | head -5
0000000 077505 046106 000402 000400 000000 000000 000000 000000
0000020 000002 000002 000000 000001 000001 007374 000000 000064
0000040 000000 040140 000000 000000 000064 000040 000005
```

`od` 的 `-b` 选项将每个字拆分为 2 个字节或字符，如下例所示：

```bash
# od -b /bin/ls | head -5
0000000 177 105 114 106 001 002 001 000 000 000 000 000
0000020 000 002 000 002 000 000 001 000 001 016 374 000
0000040 000 000 100 140 000 000 000 000 064 000 040 000 00
```

`od` 的 `-c` 选项向你显示输出中的任何打印字符，如下例所示：

```bash
# od -c /bin/ls | head -5
0000000 177 105 114 106 001 002 001 000 000 000 000 000
0000020 000 002 000 002 000 000 001 000 001 016 374 000
0000040 000 000 100 140 000 000 000 000 064 000 040 000 00
```

在这里，`strings` 命令显示任何长度约为四个字符或更长的打印字符字符串。注意在在上一个示例中，打印字母 `ELF` 出现在文件开头附近，但 `strings` 并没有报告它，因为在该部分不存在四个打印字符。

```bash
# strings /bin/ls | head -5
```

你可以使用 `strings` 的 `-n` 选项设置显示字符串的最小长度。

## 使用大字体显示文本 (banner)

`banner` 命令可以用于大字母显示短消息，如下例所示：

```text
# banner hello
#  #  ######  ######  ######  ####
#  #  #      #      #      ####
#  #  #      #      #      ####
#  #  #      #      #      ####
#  #  #      #      #      ####
#  #  #      #      #      ####
#  #  ######  ######  ######  ####
```

## 在二进制文件中寻找文本线索

在二进制程序中寻找打印文本在解决程序无法运行的问题时非常有用。有时，二进制文件中包含的文本错误消息、用法信息以及文件和目录名称可以提供启动程序所需的线索。

这种技术在打印作业之间创建分隔页时非常有用，因为它生成的文本易读且突出。当你需要将输出到文件中时，可以重定向 `banner` 的输出。





`banner` 命令将不同的单词放在不同的行上。如果你希望将这些单词放在同一行，请在每个空格前加上反斜杠（`\`）来转义任何空格，或者像此例所示，将任何空格包含在单引号或双引号中：

```
banner "Acme Corp."
```

`banner` 的最大行长度为 10 个字符。该命令会截断超出长度的任何字符。

### 显示 DOS 文件 (*col*)

DOS/Windows 下的文本文件每行都以回车符（carriage return）和换行符（linefeed）结束。UNIX 文本文件仅以换行符结束，UNIX 称为 `newline character`。如果你将一个 DOS 文本文件引入 UNIX 并尝试用 `vi` 编辑它，可能会看到文件显示如下：

```
 |
|
Page 168

这是一个来自 DOS^M 系统、通过磁盘或通过^M 网络下载的文本文件^M。^M
```

每段每行末尾的 `Ctrl+M` 是回车符。有多种方法可以使用 `col` 命令来移除 `Ctrl+M`，`col` 是一个过滤控制字符的实用程序。

要从现有 DOS 文本文件创建 UNIX 文本文件，请输入此行：

```
col -bx < dosfile > unixfile
```

如果你在 `vi` 中发现每行都以 `^M` 结尾，请输入此行：

```vi
%! col -bx
```

前面的命令使 `vi` 对每一行应用 `col -bx`，从而移除每行末尾的 `^M`。你现在可以继续编辑。

### 清理 man Pages (*col*)

如果你将帮助页（man page）保存到文件中，你可能会发现单词中间夹杂着 `^H` 或退格键字符。`^H` 是给打印机的指令，要求返回并再次加粗打印该字符，或为该字符加下划线。以下是一个显示 `^H` 的保存帮助页示例：

```
NAME    ls-list contents of directory
SYNOIS
    /usr/bin/ls [-aAbcCdfFgilLmnopqrRux1] [file...]
    /usr/xpg4/bin/ls [-aAbcCdfFgilLmnopqrRux1] [file...]
DESCRIPTION
    For each file that is a directory, ls lists the contents of the directory; for each file that is an ordinary file, ls repeats its name and any other information requested.
```

你可以像上一节所示，从命令行或在 `vi` 中运行 `col -bx`。以下是运行 `col -bx` 后相同的帮助页文件：

```
NAME    ls-list contents of directory
SYNOPS
    /usr/bin/ls [-aAbcCdfFgilLmnopqrRux1] [file...]
    /usr/xpg4/bin/ls [-aAbcCdfFgilLmnopqrRux1] [file...]
DESCRIPTION
    For each file that is a directory, ls lists the contents of the directory; for each file that is an ordinary file, ls repeats its name and any other information requested.
```

这也解释了为什么在帮助页中，你使用 `/` 搜索字符串时，man 却说它不存在，但你随后在帮助页的后面找到了该字符串。为什么之前没找到？答案可能是因为它是一个重要词汇，因此包含了一些 `Hs`。你可以通过如下方式输入 man 命令来提高搜索帮助页的能力：

```
ls col -bx
```

`col -bx` 移除了关键字中的 `Hs`，使得 `/` 能够在搜索中找到它们。

另参 *更多关于帮助页的信息，请参阅第 90 页*

### 打印文件

通常 UNIX 系统上存在一个或多个打印机。系统管理员为每台打印机命名，以便用户指定希望输出输出的打印机或打印机组。用户使用 `lp` 或 `lpr` 命令打印到指定的打印机。

### 介绍 UNIX 打印系统

实际发生的情况是，打印的文本被保存在一个系统磁盘文件中，称为 *spool file*。每个不同的打印作业都有自己的 spool 文件。`lp/lpr` 命令实际上执行得非常快，因为将所有文本保存到磁盘文件中并不花费长时间。这个过程被称为打印请求排队。在后台运行的打印调度程序会等待指定的打印机变得可用，然后打印该打印机队列中的下一个作业。





假打印（Spooling）提供了许多优势。通过假打印，打印机在打印你的作业时不会占用你的工作站（对于大型打印作业，这可能是一个缓慢的过程）。所有作业都通过一个打印机调度程序进行，因此不存在两个用户同时向同一台打印机打印会导致输出相互交错的危险。

假打印也有一些缺点。在假打印程序终止之前，假打印作业不会开始打印。这一事实提供了一个明显的优势，即打印机可以始终以全速运行，因为它不需要等待程序计算和磁盘访问来生成下一行打印输出。当一个作业需要长时间（例如六小时）来生成输出时，缺点就显现了。在六小时的任务完成后，打印才会开始，因此用户必须等待更长时间才能获得打印输出。

应用程序可以打开并直接输出到打印机设备。对于前段文字中的示例，直接打印机允许在整个六小时的程序运行期间进行打印，因此当假打印打印机刚开始输出时，直接打印机已经完成了大部分打印工作。

当你在打印机上有支票和表单，并希望从应用程序控制表单的正确居中时，直接打印机也更有用。应用程序通常会打印一些测试表单，并要求用户在打印批量表单之前检查表单对齐。除非应用程序关闭输出通道，否则假打印机无法打印测试表单，这会导致打印机处于开启状态，从而浪费已经加载的表单。

直接打印机很难防止用户的输出相互交错。应用程序通常会在打印机在使用期间锁定打印机，迫使所有其他用户等待作业完成。不同的应用程序通常使用不同的锁定机制，因此一个应用程序的输出可能会与另一个应用程序的输出交错。如果有多个应用程序使用同一台打印机，通常需要假打印来防止输出交错。

每当 UNIX 文档提到打印时，它通常指的是打印队列/假打印系统。本节的其余部分也均指打印队列/假打印系统。

### 如何确定你的系统打印机名称 (`lpstat`)

要获取系统上的打印机名称列表，请输入此行：

```
lpstat -p -D
```

`lpstat` 命令显示打印机状态。`lpstat` 的 `-p` 选项将输出限制为显示打印机及其可用性。`lpstat` 的 `-D` 选项显示该打印机的描述（如果有的话）。你应该会看到类似下面的输出：

p104 idle enabled since Sat Aug 23 16:32:49 available
p108 idle enabled since Thu Aug 21 16:28:28 available: Laser III by copy room
p206 idle enabled since Feb 14 16:50:49 available: LaserJet in Accounting

前面的示例显示三个可用的打印机名称：`p104`、`p108` 和 `p206`。它们目前都处于空闲状态，这意味着它们没有在打印任何作业。没有被禁用（例如，没有正在维修）。但无法确定打印机 `p104` 位于建筑的哪里；它可能在 104 室，但也可能是起始于 104 室但后来移动到 237 室的打印机。

### 如何打印文件或管道 (`lp`, `lpr`)

UNIX 下有两个通用命令处理文件或管道打印：

UNIX 假打印也适用于网络打印机。可以使用本节中的相同命令向网络上的打印机打印。系统管理员必须配置配置打印机，以便它们出现在 `lpstat` 中。`lp`（系统实用程序）或 `lpr`（BSD 实用程序）。你应该学习这两种打印命令，以便在仅提供其中一种的 UNIX 系统上工作。以下步骤描述了如何打印一个或多个文件。

#### 如何打印文件或管道输出

1. 如果你正在打印一个或多个文件，请跳到第 2 步。否则，在 shell 提示符处，输入你想打印其输出的 UNIX 命令。以管道符号 `|` 结束命令。`|` 符号周围的空格是的。在接到指示前不要按回车。现在转到第 3 步。
2. 如果你正在打印一个或多个文件，请先使用 `file` 命令检查它们，如本章开头所示。确保这些是文本文件。如果你不小心打印了二进制文件，可能会浪费大量的打印纸，并让其他人对你生气。
3. 输入 `lp` 或 `lpr`。





1. 输入你的系统支持的任何命令。如果你不确定，可以尝试一个。如果你选择的命令不支持，运行该命令时将得到“找不到命令”（command not found）的错误。

4. 如果你想指定去哪个打印机，请遵循以下指令：
   - 对于 `lp`，输入一个空格然后输入 `-d`。
   - 对于 `lpr`，输入一个空格然后输入 `-P`。
   - 输入所需的打印机名称。
   如果你跳过此步骤，输出将发送到系统默认打印机；如果不存在默认系统打印机，你的命令将产生错误。

5. 如果你想指定打印份数，请遵循以下指令：
   - 对于 `lp`，输入一个空格然后输入 `-n`。
   - 对于 `lpr`，输入一个空格然后输入 `-#`。
   - 输入要打印的份数。

6. 如果你想打印一个或多个文件，输入一个空格然后列出每个文件，并用空格分隔。如果文件在当前目录下，只需列出其文件名（basename）。否则，输入每个文件的绝对路径或相对路径。你也可以使用一个或多个文件名生成通配符模式（Filename Generation Wildcard）来生成文件列表。

7. 按回车执行你的命令并队列输出。你应该能看到输出显示了一个请求 ID（request id），以便跟踪任务是否已经打印，从而中止打印，例如：
```
$ ls -l lp request is hp-85 (standard input)
```

### 检查打印队列 (`lpstat`)
在 System V 上，你可以通过输入不带选项的 `lpstat` 来检查打印队列中的请求，例如：
```
$ lpstat hp-85 mori 11946 Feb 23
hp-86 fred 203 Feb 23
```
`lpstat` 输出的每行都以打印任务请求 ID 开头，以打印机名称开头。在前例中，fred 和 mori 都在大约相同时间为打印机 `hp` 排了打印任务。mori 先到达，他的任务目前正在 `hp` 上打印。尽管 fred 的任务很小（只有 203 个字符），但在 mori 的任务完成之前，他的任务将不会打印。

如果你的系统不支持 `lpstat`，请尝试使用 `lpq` 获取排队打印任务列表，例如：
```
$ lpq -P printer-name -l
```
如果你的系统中没有 `lpq`，请尝试 `lpc`。进入 `lpc` 后，有用的命令是 `help` 和 `quit`。

### 取消打印任务 (`cancel`, `lprm`, `q`)
在 System V 上，你可以通过请求 ID 取消打印任务。使用上一节所示 `lpstat`、`lpq` 或 `lpc` 来确定你想取消哪个当前请求，例如：
```
$ lpstat hp-85 mori 11946 Feb 23
hp-86 fred 203 Feb 23
$ cancel hp-85
request "hp-85" canceled
$ lpstat
hp-86 fred 203 Feb 23
```
在 BSD UNIX 上，使用带有任务号的 `lprm` 来移除（即取消）当前的打印请求。在 AIX UNIX 上，使用 `qcan` 取消打印请求，例如：
```
$ qcan -P printer -x jobid
```
在所有所有系统中，非 root 用户都可以取消他们提交的任务；root 可以取消任何打印任务。

字体 从故障打印机上移动打印请求 (`lmove`)
如果打印机出现故障，系统管理员（root）可以使用 `lmove` 命令将该打印机的部分或全部待处理打印请求移动到另一个打印机。
要将一个或多个特定的打印任务移动到另一台打印机，root 可以此语法：
```
$ lmove list-of-req-ids new-printer
```
要显示指定打印机的所有用户的待处理打印任务请求 ID，root 可以输入此语法：
```
$ lpstat -p printer-name
```




移动打印作业

要将所有打印作业从损坏的打印机移动到另一台打印机，`root` 可以进入语法：

```
lpmove broken-printer new-printer
```

这将损坏的打印机移出服务，使其不再接受新的打印作业。

# 如何为打印格式化输出

如果你在针式连续进纸打印机上打印输出，输出最令人不满意的部分将是打印在每页的顶部和底部没有留出任何边距。如果你在激光打印机上打印输出，你会发现所有输出都从最左侧边距开始，并为你留出了装订页面或打三孔的空间。这类问题可以在打印之前通过 `pr` 命令对输出进行处理来解决。

默认情况下，`pr` 会在每页的顶部和底部添加一个五行的页眉和页脚。页眉包含页码、日期/时间和文件名（如果不是通过管道传递的话）。`pr` 命令接受命令行上的文件列表。如果没有给出文件列表，你可以将输出通过管道传给 `pr`。然后，你可以直接将 `pr` 的输出重定向到打印机，如下两个示例所示：

```
pr file1 acme* | lp prog2 | pr | lpr -Paccting
```

使用 `pr` 的主要问题是确定打印机每页的行数。在这里，`pr` 假设每页 66 行，这在许多打印打印机上并不适用，会导致页面中间出现分页。要设置每页行数，使用长度选项 `-l`，如下示例所示：

```
pr -l60 file
```

由于 `pr` 通常不在每页结束时发送分页符，你必须将长度设置为所需的精确值，否则你会在输出的后续页面中间发现分页。在本章之前，讨论过如何为输出的每行编号。打印带行号的输出将帮助你确定你的打印机要使用的值。至少打印 10 页输出以确保你使用的是正确的值。

你可以使用 `-f` 选项告诉 `pr` 在每页结束时发送分页符，如下示例所示：

```
pr -f file
```

如果在非常长的输出的页面上出现分页问题，这种方法会非常有用。如果你在标准尺寸的纸上每页只打印少数行，这种方法会更有效。如果输出是到你的屏幕上（也就是说，如果没有重定向），那么 `-f` 将导致蜂鸣声并等待你在第一页开头按 `Enter` 键。如果你在终端上运行非常有用，因为你可以调整表单顶部。如果你在进纸式终端上运行，请对 `pr` 使用 `-p` 选项，这样它会在每页开始时蜂鸣并等待 `Enter` 键。

要为输出设置左边距，使用 `-o` 选项偏移打印，如下示例所示：

```
pr -o5 file
```

在在上述示例中，`pr` 在每行输出的开头打印五个空格。默认（如果没有给出 `-o` 选项）偏移为 0。

要在每页顶部设置自定义标题而不是文件名，请使用 `-h` 选项。要在新页眉中包含空格，请将整个页眉包含在双引号或单引号中。警告：你必须在 `-h` 后面包含空格，否则你的整个输出将是乱码，如下示例所示：

```
pr -h "    Acme Proposal    " acmeprop | lp
```

要使输出双倍行间距，对 `pr` 使用 `-d` 选项。

要为输出的每行编号，使用 `-n` 选项。在 `-n` 之后跟随一个可选的用于行号的字符数。如果没有给出值，默认为 5 个字符，如下示例所示：

```
pr -n file -n4 file
```

虽然 `pr` 会为正文中所有的行（甚至是空行）编号，但它不会为每页页眉和页脚中的行编号。行号从 1 开始并在整个文档中增加，也就是说，它永远回到 1。

要将输出中的制表符扩展相应数量的空格，使用 `-e` 选项。要将默认的制表设置从八列更改，请在 `-e` 之后跟随新值，如下示例所示：

```
pr -e file -e8 file
```

在打印大于八个字符的制表符列时，这非常有用。

然后 `pr` 可以按列显示你的输出，如下示例所示：

```
pr -3 file
```

在上述示例中，`-3` 告诉 `pr` 将输出跨页面组成三个等大小的列。注意，`pr` 不会将普通的行长度输出转换为列。你必须先手动组合你的输出，使没有一行超过列宽（三列为页面的 1/3，四列为页面的 1/4，依此类推）。任何长列宽的文本将被截断——也就是说会丢失。





# 第 7 章 复制、移动、重命名或删除文件
作者 Steve Moritsugu

## 使用相对路径

### 复制文件
### 移动文件
### 重命名文件
### 删除文件
### 为同一文件创建多个名称

## 选择目标路径

在本章中，`absolute`（绝对路径）和 `relative pathnames`（相对路径）的概念非常重要。如果需要的话，你可以在第 2 章“UNIX 目录与路径”中复习它们。该章节还讨论了大多数 UNIX 系统上的标准目录。在那个讨论中，`/tmp` 被提到作为临时文件的目录。当用户想要创建一些小型临时文件（也称为 `scratch files`）时，这是一个非常适合用户使用的目录。

由于所有用户都可以在 `/tmp` 中创建文件，请为你的文件选择一个不太可能被其他用户使用的名称——例如，将你的登录 ID 作为名称的一部分。我通常会在此类文件中添加 `junk` 或 `tmp` 单词。每当我以后遇到创建的带有 `junk` 或 `tmp` 字样的文件时，都可以自由地删除它们，而无需花时间去评估它们的内容。

第 2 章还提到了每个用户都有一个家目录（home directory）。某些系统会让一组用户共享同一个家目录，但通常你有一个独有的家目录。因此，这是存储你想要保留一段时间的文件的好地方。

在你的家目录下创建子目录是一个好主意，这样你就可以组织文件。组织文件的传统方法之一是按文件类型或功能。例如，你可以为文本文件创建一个目录，为可执行程序创建另一个目录（可执行文件会被放在 `bin` 目录中）。拥有一个 `bin` 目录的优势是，你可以将其添加到你的 `PATH` 中，这样无论你当前在哪个目录，都可以轻松执行该目录中的任何程序。

我建议按项目来组织你的家目录。为每个项目创建一个目录，并将与该项目相关的所有文件放入该目录。如果是一个复杂项目，你可以创建子目录。这种组织方式的好处在你需要清理不需要的文件以清理磁盘空间时就会体现出来。许多项目在几个月或一年后就不再需要了。按项目组织让你能够轻松地删除与该项目相关的所有文件。

如果你需要创建任何大文件或创建数千个文件，你应该咨询系统管理员。如果你用尽了文件系统中的磁盘空间或 `inodes`，可能会导致严重问题。`df` 命令可以显示每个文件系统中的可用磁盘空间和可用 `inodes`。如果你需要大量的磁盘空间，系统管理员可能会在另一个文件系统中为你创建一个供使用的目录。

另：
- 绝对路径和相对路径，第 42 页
- 标准目录，第 40 页
- 家目录，第 44 页

## 处理权限拒绝（Permission-Denied）错误

要在目录内创建文件和子目录，你需要该目录的写入权限。如果你创建了该目录，你通常拥有该目录的写入权限。如果该目录属于别人，你可能需要请求他/她开放该目录的写入权限。他/她可能不愿意对所有人开放写入权限。传统的 UNIX 方法为需要共享文件和目录的用户创建一个新组，将这些文件和目录分配给该组，并允许组员拥有写入权限但不允许所有人。然后你必须请求 `root`（系统管理员）将你加入该组。

另：
- 权限，第 273 页

### 在当前目录内复制、移动或重命名 (*cp,mv*)




要重命名文件，我们使用 UNIX 的 `mv` 命令将其移动到新名称。这不会发生实际的数据传输（除非我们将其移动到不同的文件系统）。如果我们复制文件，则会创建一个不同名称的新文件，并将源文件的所有内容复制到新文件中。

### 如何在目录内复制/移动/重命名文件

1.  确保你处于目标目录。如果你不确定当前在哪个目录，可以使用此命令显示当前目录：
```bash
pwd
```

2.  在 shell 提示符下，如果你想移动（即重命名）文件，请输入以下内容：
```bash
mv
```
如果你想复制文件，请输入此：
```bash
cp
```
在接到指示之前，不要按回车键。注意，该命令只有两个字母，而不是整个单词。

3.  输入一个空格，然后输入 `-i`。这是现代 UNIX 系统上一个实用的选项，但在旧的 UNIX 系统中不可用。如果你准备覆盖一个现有文件，它将发出警告。

4.  某些 UNIX 系统（如 Solaris 或 Linux）允许为 `cp` 命令使用 `-p` 选项，这可以在复制时保留文件的所有者、组和权限。（你可以在你系统的 `cp` 手页中检查此。）如果你以 root（系统管理员）身份运行，此选项效果最好。如果你要在 `cp` 中包含此选项，请输入空格然后输入 `-p`。

5.  输入一个空格，然后输入要移动或复制的现有文件名。输入 `basename`，因为它位于当前目录下。此文件必须已经存在，因此有时被称为现有文件或源文件。

6.  输入一个空格，然后输入要创建的新文件名。这被称为目标文件。以 `basename` 输入此目标文件。此 `basename` 不能与当前目录中的任何其他文件或子目录匹配。你的新文件名可以开头并包含任何大小写字母、数字、下划线（`_`）、横线（`-`）或点（`.`）。旧的 UNIX 系统限制为 14 个字符，但现代 UNIX 系统允许 `basename` 超过 100 个字符（但请不要取得那么长）。除非你想让它成为隐藏文件，否则不要以点开头你的新文件名，让它与你的普通文件分开。

7.  按回车键执行你的命令。

8.  如果你收到 Usage 错误并提示 `-i` 不是有效选项，说明你的 UNIX 系统不支持该选项。请不要带上 `-i` 选项重新输入整个命令。如果 `-i` 选项在你的系统上不起，你必须在执行任何 `mv` 或 `cp` 命令之前手动检查目标是否存在。

9.  如果你收到 Permission Denied（拒绝访问）类型的错误，要么是你没有权限读取源文件，要么是你没有权限向目录写入并在那里创建新文件。请参见上一节关于处理拒绝访问错误的说明。

10. 如果你收到此消息：`overwrite dest-file?`，`-i` 选项正在提醒你所选择的目标文件已存在。你现在可以选择输入 `y` 并覆盖文件，或输入 `n` 取消复制或移动。如果你不确定，输入 `n` 然后显示目标文件的内容（参见上一章）以查看你是否需要保留它。

11. 没有消息就是好消息。如果没有生成任何消息并且直接返回到 shell 提示符，说明你的复制或移动成功了。

### 复制、移动或重命名到不同的目录

本节假设你已经阅读了之前关于执行复制操作的章节。本节讨论了当源文件和目标文件位于不同目录时如何使用复制或移动。

-i 选项和自动大灯

在 C shell 和 Korn shell 下，可以为你的登录 ID 设置别名（alias），这样 `-i` 选项就会自动添加到你输入的任何 `cp` 和 `mv` 命令中。我个人没有这样做，原因和我不不喜欢自动关闭的车灯的原因相同——它会养成你驾驶其他汽车、在其他登录名下或在其他 UNIX 系统上工作的坏习惯。

选项 #1 是对复制或移动的源和目标都使用绝对路径。这样无论你当前目录在哪里都不重要。这种方法的缺点是需要输入大量内容，因此很少被使用。




# 为两个目录设置 Shell 变量

选项 #2 是执行命令时处于源目录中（这意味着它是是当前工作目录）。此时你可以使用基名（basename）来指定源文件。你必须使用绝对路径或相对路径来指定目标文件。当你需要在源目录中执行后续命令时，此选项非常有用。

选项 #3 是处于目标目录中，使用绝对路径或相对路径指定源文件，并使用基名（basename）指定目标文件。当你需要在目标目录中执行后续命令时，此选项非常有用。

选项 #4 是处于某个可以方便访问源目录和目标目录的附近目录。例如考虑此拷贝命令：

```bash
cp -i /usr/fred/reports/acme/report7 /usr/fred/reports/98Jan/report7
```

注意，`/usr/fred/reports` 是源目录和目标目录共有的，因此你可以待在那里，并使用此处所示的方便相对路径访问文件：

```bash
cd /usr/fred/reports
cp acme/report7 98Jan/report7
```

选项 #5 是当你需要像下文那样在同一个两个目录之间拷贝多个不同文件时，使用你自己的 Shell 变量。

## 步骤

1. `cd` 进入源目录。
2. 输入：`SD=`pwd``。在前面的命令中，你获取 `pwd` 报告的当前目录，并使用反引号将该目录名称保存到变量 `SD` 中。你可以选择自己的变量名。我选择大写的 `SD` 代表源目录，以免与通常小写的 UNIX 命令混淆。
3. `cd` 进入目标目录。
4. 输入：`DD=`pwd``。
5. 现在在两个目录之间拷贝或移动文件变得简单。`SD` 和 `DD` 包含绝对路径，因此当前目录是什么并不重要。要从源目录拷贝文件到目标目录，输入以下命令：

```bash
cp -i $SD/filename $DD/.
```

注意，如果目标文件名与源文件名相同，则不需要指定目标文件名。注意下文所述，我在目录名称后面添加了斜杠点（`.`）。有关变量的更多信息，请参见第 30 页

## 确定文件的去向 (cp, mv)

并不总是容易预测 `cp` 或 `mv` 将创建哪个目标文件。这是因为结果取决于目标是否已存在的目录。例如：

```bash
mv /usr/jane/acme /usr/fred/reports
```

如果 `reports`（在 `/usr/fred` 中）是一个目录，`mv`（或 `cp`）将把源文件 `acme` 移动（或拷贝）到 `reports` 目录中。因此，结果文件名将为：`/usr/fred/reports/acme`。

注意，在这种情况下，源目录 `/usr/jane` 仅告诉我们去哪里寻找源基名。被移动或拷贝的只是源基名。源目录中的任何目录都不会被带走。

如果指定的路径 `/usr/fred/reports` 不存在，`mv`（或 `cp`）将创建它并将 `acme` 的内容放入其中。因此，结果将是一个名为 `/usr/fred/reports` 的普通文件。

如果 `reports` 在 `/usr/fred` 中作为一个普通文件存在，我们将得到相同的结果。旧的 `reports` 文件将丢失，文件 `acme` 的内容将放在它的位置。不会有关于 `reports` 旧内容被覆盖的警告，因为在这个示例中我们没有使用 `-i` 选项。每当你将文件拷贝或移动到目录时，我建议在目录名称后加上斜杠点（`.`）。例如：

```bash
mv acme /usr/fred/reports/
```

斜杠点（`.`）告诉系统我预期 `/usr/fred/reports` 是一个目录，并将 `acme` 文件移动到该目录。如果 `reports` 不是已存在的目录，命令将失败并显示错误信息，我会收到出问题的提示。如果 `reports` 恰好是一个已存在的文件，在前面的命令中添加斜杠点（`.`）可以防止覆盖 `reports` 文件并丢失其数据。




我不建议仅仅添加斜杠（`/`），因为这在许多 UNIX 系统上是非合法的语法。

以下是一个示例，使用斜杠点（`/..`）可以防止数据丢失：

```
mv file1 /usr/fred/reports
mv file2 /usr/fred/reports
mv acme /usr/fred/reports
```

在上述述示例中，用户预期 `/usr/fred/reports` 是一个存在的目录；然而，事实并非如此。因此，第一条命令在 `/usr/fred` 中创建了一个名为 `reports` 的普通文件，其中包含了 `file1` 的所有数据。第二条命令用 `file2` 的内容覆盖了 `reports` 文件。`file1` 的内容现在已完全从系统中消失且无法找回。（注意，在这里使用 `-i` 选项会提供一个救命的警告。）第三条命令将再次覆盖 `reports`，因此 `file2` 的内容也将丢失且无法找回。以下是我推荐的相同操作序列：

```bash
mv -i file1 /usr/fred/reports/.
mv -i file2 /usr/fred/reports/.
mv -i acme /usr/fred/reports/.
```

如果 `/usr/fred/reports` 不是一个目录，第一条命令将报错并失败。在目标目录后添加斜杠点（`/.`）也更容易理解 `mv` 或 `cp` 的预期结果。这对于编写操作说明以及我们在 shell 脚本中插入命令时（将在稍后的章节中介绍）都是如此。

### 将文件列表复制/移动到目录 (cp, mv)

如果 `cp` 或 `mv` 的目标是一个目录，则源可以包含一个或多个普通文件；即文件列表。例如：

```bash
cp -i file1 file2 file3 /data/acme/.
```

在例例中，`file1`、`file2` 和 `file3` 将复制到 `/data/acme` 目录。如果有两个或多个源文件，目标必须是一个目录；否则你将得到错误。在随后的章节中，你将看到可以使用文件名通配符创建文件列表，这些列表可以用于 `cp` 和 `mv`。例如：

```bash
cp -i acme /usr/fred/ac/.
```

另参：文件名通配符，见第 232 页

### 处理确认请求

如果 `mv` 或 `rm` 正准备覆盖或删除一个已存在的文件，这些命令将检查你是否有权限写入该文件。如果没有，它将像如下所示请求确认：

```
mv: dest-file: override protection 400 (yes/no)?
```

在某些系统上，确认信息非常简短。例如：

```
400?
```

对于此确认信息，`mv` 正准备覆盖另一个用户的文件，且该用户没有给你写入或修改此文件的权限。然而，你对该目录拥有管理员权限，因此你可以覆盖权限。该文件的三个权限数字为 XXX（上例中为 `400`）。你是否仍然想覆盖此文件？请输入 `y` 表示是，或输入 `n` 表示否。

### 移动/重命名目录 (mv)

你可以使用 `mv` 命令移动或重命名目录。通过这种方式，可以将目录从 UNIX 目录结构中移除，并重新连接到树的不同部分。该目录的所有子目录将随之移动。假设该文件存在于系统中：`/usr/fred/reports/compsys/pegasus`。

注意 `pegasus` 位于 `compsys` 目录。现在假设我们执行这条命令：

```bash
mv /usr/fred/reports/compsys /usr/fred
```

对于 `mv` 和 `cp`，如果指定的目标是一个已存在的目录，目标将在该目录下创建。在本例中，我们知道 `/usr/fred` 是一个目录。根据本章前面的部分，我们知道 `mv`（以及 `cp`）只取源文件名并将其放入现有的目标目录。因此，`compsys` 的新绝对路径如下：`/usr/fred/compsys`。

`pegasus` 文件的新绝对路径将是：`/usr/fred/compsys/pegasus`。

在示例中，`mv` 命令从 UNIX 目录树结构中移除了目录 `compsys` 及其所有文件和子目录，并将 `compsys` 及其所有文件和子目录重新连接到了新位置。




旧版本的 UNIX 如果你尝试将目录移动到不同的文件系统，它会报错并终止。许多现代 UNIX 系统可以毫无问题地完成此操作。

## 复制整个目录子树 (`cpio`)

有时，你可能想要将一个目录及其所有的子目录和文件复制到目标目录。某些 UNIX 系统提供了一个 `copy` 命令（拼写为 `copy`），如果你使用 `-r` 选项就可以实现此操作，该选项意味着*递归地*复制子目录；即：无论嵌套多少层，都复制所有的子目录。其他 UNIX 系统可能为 `cp` 提供 `-r` 选项以允许对目录进行递归。然而，某些 UNIX 系统（尤其是较旧的）并不提供任何递归复制或 `cp` 选项。

有一种使用 `cpio` 命令递归复制目录子树的方法，它在旧版 UNIX 系统和新系统上都适用。你只需要为所有系统学习一种技术，而且它比其他方法更具灵活性。

### 复制整个目录子树

1. 如果源目录包含多个用户拥的文件，且你希望目标目录能够准确镜像源目录的所有权和权限，则你必须以 `root` 身份登录以执行此操作。
2. 确定源目录的精确绝对路径。源目录的每个文件和子目录都将被复制到目标目录。
3. 确定目标目录的精确绝对路径。目标目录将为源目录（及其子目录）的每个子目录和文件创建一个副本。
4. `cd` 进入源目录。
5. 输入 `pwd` 确保你正处于源目录。
6. 输入：
```
find . -print | cpio -pvum dest-dir
```
将 `dest-dir` 替换为目标目录。你可以使用绝对路径或相对路径表示 `dest-dir`。当你运行此命令时，`cpio` 会在复制整个目录时显示每一个文件名。
7. 在步骤 6 中，以下 `cpio` 选项是可选的，可以根据需要添加或省略一个或多个：
    - `-a`: 将每个文件的最后访问日期/时间重置为 `cpio` 访问该文件之前。如果包含了 `-m` 选项，则无法使用此选项。
    - `-d`:根据需要创建目标目录。
    - `-L`:跟随软链接（见下一节），以便复制所指向的文件而非指针文件。
    - `-m`: 保持每个目标文件的最后修改日期/时间与源目录相同。如果包含了 `-a` 选项，则无法使用此选项。
    - `-u`: 无条件覆盖任何现的目标文件，否则较旧的文件不会覆盖较新的文件。
    - `-v`: 详细输出，在复制每个文件时列出它。

关于 `cpio` 的更多信息，请参阅第 355 页。`tar` 也可以复制目录树。我之所以讨论如何使用 `cpio` 复制目录树，是因为旧版本的 `tar` 无法恢复空目录或设备文件，无法保留目录的所有者、组或权限。如果你使用 `cpio`，就不需要担心这些旧版 `tar` 的局限性。

## 删除文件 (`rm`)

在许多情况下你必须删除文件和目录，根据文件所在的位置，你采取的每种操作都有特殊的注意事项。UNIX 有许多用于这些过程的命令和选项。以下章节将详细介绍可用的命令和选项。

### 删除当前目录下的文件 (`rm`)

#### 如何删除当前目录下的文件

1. 确保你处于目标目录中。如果你不知道当前在哪个目录，请使用此命令显示当前目录：
```
pwd
```




## 使用 rm 命令

2. 在 shell 提示符下，输入：
```
rm
```
在接到指示之前，不要按回车键。要删除文件，我们使用 `remove` 命令。注意，该命令只有两个字母，而不是整个单词。

3. 之前我们讨论过 `rm` 和 `mv` 的确认请求。如果你想在删除你没有权限修改的其他用户的文件时，防止出现确认请求，请输入一个空格，然后输入以下内容：
```
rm -f
```
这个强制删除或替换的选项当你确定要删除某组确定的文件时非常有用。

4. 如果你正在删除一组文件，可以通过输入一个空格然后输入以下内容，让 `rm` 对其中的每一个文件都请求确认：
```
rm -i
```
这个交互式选项在你使用通配符模式指定要删除的文件列表时非常有用，可以确保你不会删除比预预期更多的文件。

5. 输入一个空格，然后输入一个或多个要删除的文件名，并用空格分隔。每个文件名都作为基名（basename）输入，因为它们位于当前目录下。

6. 请仔细检查你的命令，因为如果你操作错误，并没有 `undelete` 命令可以使用。按回车键执行你的命令。

7. 没有消息就是好消息。如果没有生成任何消息并直接返回到 shell，说明你的删除操作成功了。

### 在不同目录中删除文件
单个 `rm` 命令可以删除多个目录中的文件。在 `rm` 命令的文件列表中，只需包含目标文件或文件的绝对路径或相对路径即可。请复习本章中关于如何构建路径的上一一节。

### 删除文件列表
`rm` 命令允许指定文件列表。该列表可以通过文件名通配符生成（见第 9 章）。例如：
```
rm acme/*
```

### 删除整个目录子树
要删除一个目录，它必须是完全空的，除了点 (`.`) 和双点 (`..`) 条目外。的。如果你确定要删除一个目录及其所有的文件、子目录，以及它们所有的子目录，可以通过一个简单的命令来实现。在使用此命令时必须非常小心，因为如果操作错误，没有办法将文件找回来。删除整个目录及其内容的步骤在第 7 章（关于目录）和路径部分已介绍过。

### 另需参考
有关删除整个目录树的更多信息，请参见第 53 页

### 为同一文件创建多个名称 (ln)
目录是一种具有两个的文件：
1. 跟踪该目录中包含的文件名和子目录。
2. 跟踪这些文件名中每个对应的 inode 号。

当你在 UNIX 下访问一个文件名时，系统会根据该文件名的目录条目确定使用哪个 inode 条目。UNIX 允许多个文件名引用给定的 inode 号，这在实际上允许同一个文件拥有多个名称。由于文件名不是 inode 信息的一部分，因此一个文件的每个名称都是同等有效的。哪个名称先出现并不重要。将这些名称视为文件的副本是不正确的，因为只引用了同一个 inode。这意味着如果你使用一个名称更改了文件，那么当你通过该文件的其他名称访问它时，该更改将是可见的。

当你为同一个文件拥有多个名称时，每个名称被称为指向该文件的硬链接（hard link）。在 UNIX 的分级目录系统中，当你想要将同一个文件放在两个不同的目录时，允许一个文件有多个名称或硬链接是有用的。例如，假设我有一个客户目录……




为我的每个客户准备一个文件，其中包含他们的名称、地址、电话号码和交易历史。假设我还有一个供应商目录，用于存储我购买产品的的公司，供应商目录中的每个文件都包含供应商名称、地址、电话号码和交易历史。

现在，假设有些公司从我这里购买物品，因此它们应该在客户目录中；但我也从他们那里购买物品，所以它们应该在供应商目录中。我可以通过创建两个硬链接来解决这个问题。也就是说，我可以在客户目录中创建一个文件，同时将该文件放在供应商目录中。通过使用硬链接，这些文件并不是彼此的副本；它们是同一个文件的两个名称。因此，如果我在客户目录中更新了该公司的电话，该更改将自动反映在供应商目录中的该公司上。

如果有一个大文件，硬链接占用的空间比复制文件要少得多。无论有多少个硬链接，文件只有一份。

### 另另

- 关于 UNIX 目录的更多信息，请参阅第 36 页
- *使用硬链接创建多个名称 (ln)*

### 为现有文件创建硬链接

现在你已经了解了硬链接以及它们的优势，以下是为文件创建额外硬链接（即为访问特定文件创建另一个名称）的步骤。

1. 确保你知道现有文件的完整路径，以及想要赋予该现有文件的新硬链接的名称。现有文件必须是普通文件，不能是目录。硬链接文件名不能已经作为文件、目录、链接等被占用。
2. 要创建的新硬链接必须与现有文件位于同一个文件系统中。如果你不确定你的文件系统边界在哪里，请输入此命令：
```bash
df
```
你可能会看到如下的输出：
```
/          724074 blocks
/boot      13780 blocks
/u         601622 blocks
/data      1776032 blocks
/u/tmp     42302 blocks
```
在上述 `df` 的输出中，左列显示文件系统的目录名称。要确定两个绝对路径是否位于同一个文件系统中，请将路径的开头部分与 `df` 输出中最长的匹配文件系统目录匹配。如果两个文件匹配到同一行 `df` 输出，则它们在同一个文件系统中。例如，`/u/tmp/reports` 将位于 `/u/tmp` 文件系统（因为我们取最长匹配项）。`/u/reports/acme` 将位于 `/u` 文件系统。因为它们在不同的文件系统中，它们不能是同一个文件的硬链接。另一个例子是，`/usr/fred/reports` 位于 `/` 文件系统。`/acme/Jan23` 也位于 `/` 文件系统。因此，它可以为 `/usr/fred/reports` 创建硬链接。
3. 在 shell 提示符处，输入 `ln`。在接到指示前不要按回车键。
4. 输入空格，然后输入现有文件的名称。你可以以绝对或相对路径的形式输入。
5. 输入空格，然后输入你想要为现有文件创建的硬链接名称。你可以以绝对或相对路径的形式输入新链接。
6. 按回车键完成命令。

### 查找文件的所有链接 (ls)

要确定一个文件有多少个硬链接，请输入以下命令：
```bash
ls -l filename
```
以下是一个示例输出：
```
-r-xr-xr-x 3 bin bin 15176 Jul 15 1997 compress
```
在权限之后、所有者和组之前，有一个字段称为链接数（link count），在前面的示例中数字为 3。这意味着 `compress` 命令（位于 `/bin` 目录）共有三个名称来引用同一个文件。其中一个名称是 `compress`，所以该文件还有两个我们未知的名称。

要确定同一目录下是否对该文件有更多硬链接，请输入以下命令：
```bash
ls -li sort
```
以下是一个示例输出：
```
-r-xr-xr-x 1 bin bin 10832 Jul 15 1997 col
-r-xr-xr-x 1 bin bin 6344 Jul 15 col
```





```text
5529 -r-xr-xr-x  3 bin     bin           15176 Jul 15
5529 -r-xr-xr-x  3 bin     bin           15176 Jul 15
5529 -r-xr-xr-x  3 bin     bin           15176 Jul 15
5530 -r-xr-xr-x  1 bin     bin           30596 Jul 15
5531 -r-xr-xr-x  1 bin     bin           39916 Jul 15
```

`ls` 命令的 `-i` 选项会导致 `ls` 在行开头显示 inode 编号，这非常适合应用 `sort` 命令，使得以相同 inode 编号开头的行将排列在一起。注意上一个例子，`compress`、`uncompress` 和 `zcat` 都具有相同的 inode 编号（`5529`）、相同的权限（`r-xr-xr-x`）、相同的所有者、组、大小（`15176`）以及最后修改日期。因为它们具有相同的 inode 编号且处于同一个目录下，所以它们是指向同一个文件的硬链接——即同一个文件的不同名称。

如果没有找到所有的硬链接，那么其中某些必须存在于其他目录。要找到所有匹配给定 inode 编号的文件名，请输入以下命令：

```bash
find /STARTDIR -inum INODE -print
```

将 `INODE` 替换为你要查询的 inode 编号。将 `/STARTDIR` 替换为从 `df` 命令中获取的文件系统目录（正如你在第 2 步中所看到的）。例如：

```bash
find /-inum 1724836-print /usr/fred/acme /usr/jane/acme/project/data/pegasus
```

在上述步骤的第 2 步中，你了解了如何确定路径是否在同一个文件系统中。Inode 编号会在其他文件系统中重用用于其他不相关的文件。只有当具有相同 inode 的文件位于同一个文件系统时，它们才是指向同一个文件的硬链接。利用这一知识可以忽略 `Find` 报告的非正确文件系统中的。

### 另类
- 有关 `ls` 命令的更多信息，请参阅第 15 页。
- 有关文件系统的更多信息，请参阅第 72 页。

### 删除硬链接 (`rm`)
如果一个文件有多个硬链接，它就有多个名称。如果你使用 `rm` 命令删除这些名称之一，其余名称和文件内容将不受影响，只是文件的总链接计数会减 1。如果你删除一个链接数为 1 的文件名，该 inode 的链接计数将变为 0，这意味着没有名称可以访问该文件了。一旦链接计数归零，该文件将从系统中被删除。文件被删除后，无法将其找回。

### 使用软链接/符号链接创建指针 (`ln`)
还有另一种为同一个文件创建多个名称的方法。你可以为现有文件创建一个软链接，也称为符号链接。与硬链接相比，软链接有两个优势：

1. 你可以为目录软链接。
2. 你可以为另一个文件系统的文件或目录创建软链接。

软链接是一个小文件，在 `ls -l` 的输出中用箭头 (`->`) 表示。例如：

```text
ls -l /usr/spool lrwxrwxrwx 1 root root 10 Feb 13 09:19 /usr/spool -> /var/spool
```

在上例中，`/usr/spool` 是指向 `/var/spool` 的软链接。SVR 引入的更改之一是将 spool 目录从 `/usr` 移动到 `/var`。SVR 通常创建 `/usr/spool` 为指向 `/var/spool` 的软链接。这使得用户和程序能够继续访问 `/usr/spool`，软链接会导致他们实际访问 `/var/spool`。在上例中，注意 `/usr/spool` 是一个大小只有 10 个字符的文件；也就是说它的内容是 `/var/spool`，长度为 10 个字符。注意行开头的类型为 `l`，表示软链接。注意所有用户的权限均为 `rwx`。这允许所有用户访问该软链接。然而，读/写/执行权限将由被指向的文件决定。

### 创建软链接/符号链接
1. 确定所需的软链接以及你希望它指向的文件的绝对路径。在创建链接时，被指向的文件不必存在。被指向的文件可以是目录，且可以位于与软链接不同的文件系统中。软链接文件名不能已已占用。
2. 在 shell 提示符下，输入 `ln -s`。在接到指示前不要按回键。
3. 输入一个空格，然后输入被指向文件的完整路径。
4. 输入一个空格，然后输入要创建的软链接文件名。可以是绝对路径也可以是相对路径。通常首选绝对路径。




5. 按回车键完成您的命令。旧的 UNIX 系统不支持软链接（soft links）。某些 UNIX 系统仅允许 root（系统管理员）创建软链接。

## 确定命令是否遵循软链接

使用硬链接时，文件的每个名称与其他文件的任何名称都没有区别。相反，软链接与它指向的文件完全不同。大多数命令都会遵循软链接，这意味着当你要求它们访问软链接时，它们实际上会访问软链接所指向的文件。

### 避免将目录链接到自身

像下面的命令可以将目录链接到自身：

```
ln -s dir2 dir2
```

现代 UNIX 系统上的 `cd` 命令会检测到此错误并立即报告“Bad Directory”（目录错误）。通常情况下，对被指向的文件使用绝对路径是最安全的。

例如，如果你使用 `vi` 编辑软链接，它将编辑软链接所指向的文件。如果该文件不存在，你就拥有了一个过期的软链接（stale soft link），一个指向空处的链接。在这种情况下，`vi` 会给出“No Such File”（找不到文件）错误，尽管软链接确实存在。

某些 UNIX 命令不会遵循软链接，这意味着它们对软链接本身进行操作。例如，`mv` 和 `rm` 不遵循链接，这允许你重命名或删除软链接。请检查各个命令的帮助页（man pages），以查看它们是否遵循软链接并对指向的文件进行操作。

以下是 Solaris 系统上 `rm` 的节录：如果文件是符号链接，将删除链接，但它所指向的文件或目录不会被删除。用户删除符号链接不需要写入权限，只要他们在该目录下具有写入权限。前面的节录告诉我们 `rm` 不遵循链接。它对软链接本身进行操作。

以下是 Solaris 系统上 `ls` 的节录：-L 如果参数是符号链接，则列出链接引用的文件或目录而不是链接本身。这个节录告诉我们 `ls` 通常不遵循链接。它提供关于软链接的信息。如果我们为 `ls` 添加 `-L` 选项，它将遵循链接并显示指向的文件。

以下是 Solaris 系统上 `file` 的节录：如果文件是符号链接，默认会遵循该链接并对符号链接指向的文件进行测试。

有关 `man` 命令的更多信息，请参阅第 89 页。

## 第 8 章 修改、合并和分割文件
作者：Steve Moritsugu

- 对文件、多个文件或管道中的行进行排序
- 显示文件或管道的第一行或最后一行
- 加密文件以便只有你才可以解密
- 压缩/解压缩文件
- 将二进制文件转换为简单文本格式
- 对一组文件进行排序
- 连续连接文件
- 粘贴文件使对应行并排显示



`sort` 将所有指定的文件合并到其工作区，对工作区进行排序，然后将结果显示在标准输出（除非你将输出重定向到文件或将其传递给另一个命令）。

`sort` 命令也可以作为典型的 UNIX 过滤器在管道中使用，如下所示：

```bash
ls acme* *.c | sort | uniq
```

在 във述示例中，`sort` 从标准输入读取由 `ls` 命令生成的行。然后，`sort` 将这些行按字母顺序排列，并将它们传递给标准输出。在 във述示例中，来自 `sort` 的标准输出被传递给 `uniq` 命令，以删除任何重复行。

如果你在 `sort` 命令之后指定了任何文件名，它将从这些文件获取输入，而不是从标准输入获取。以下是 `sort` 的错误用法：

```bash
ls acme* *.c | sort acme* | uniq # incorrect sort usage
```

上述示例是错误的，因为在 `sort` 命令之后指定了一个或多个文件名，因此 `sort` 将不会从标准输入读取，并且会忽略由 `ls` 命令生成的输出。

### 另请

- 有更多关于管道（piping）的信息，请参阅第 31 页。
- 有更多关于文件名生成通配符（Filename Generation Wildcards）的信息，请参阅第 232 页。

### 为什么 UNIX 命令内置排序或分页选项？

如果用户希望从任何 UNIX 命令获得排序输出、分页输出或一次一页的排序输出，用户只需管道到 `sort` 或管道到 `pg`，或者先管道到 `sort` 再管道到 `pg`。通过这种方式，UNIX 工具更加高效。

### 确定行的排序方式 (ASCII)

`sort` 根据行内字符的 ASCII 值排列行。你通常可以通过输入此命令查询 ASCII 序列：

```bash
man ascii
```

以下是 Solaris 系统的示例输出：

| 000 | NUL | 001 | SOH | 002 | STX | 003 | ETX | 004 | EOT | 005 | ENQ | 006 | ACK | 007 | BEL |
| 010 | BS | 011 | HT | 012 | NL | 013 | VT | 014 | NP | 015 | CR | 016 | SO | 017 | SI |
| 020 | DLE | 021 | DC1 | 022 | DC2 | 023 | DC3 | 024 | DC4 | 025 | NAK | 026 | SYN | 027 | ETB |
| 030 | CAN | 031 | EM | 032 | SUB | 033 | ESC | 034 | FS | 035 | GS | 036 | RS | 037 | US |
| 040 | SP | 041 | ! | 042 | " | 043 | # | 044 | $ | 045 | % | 046 | & | 047 | ' |
| 050 | ( | 051 | ) | 052 | * | 053 | + | 054 | , | 055 | - | 056 | . |
| 057 | / | 060 | 0 | 061 | 1 | 062 | 2 | 063 | 3 | 064 | 4 | 065 | 5 | 066 | 6 |
| 067 | 7 | 070 | 8 | 071 | 9 | 072 | : | 073 | ; | 074 | < | 075 | = | 076 | > |
| 077 | ? |
| 100 | @ | 101 | A | 102 | B | 103 | C | 104 | D | 105 | E | 106 | F |
| 107 | G | 110 | H | 111 | I | 112 | J | 113 | K | 114 | L | 115 | M |
| 116 | N | 117 | O | 120 | P | 121 | Q | 122 | R | 123 | S | 124 | T | 125 | U |
| 126 | V | 127 | W | 130 | X | 131 | Y | 132 | Z | 133 | [ | 134 | \ | 135 | ] |
| 136 | ^ | 137 | _ | 140 | ' | 141 | a | 142 | b | 143 | c | 144 | d | 145 | e |
| 146 | f | 147 | g | 150 | h | 151 | i | 152 | j | 153 | k | 154 | l | 155 | m |
| 156 | n | 157 | o | 120 | p | 121 | q | 122 | r | 123 | s | 124 | t | 125 | u |
| 126 | v | 127 | w | 130 | x | 131 | y | 132 | z | 133 | { | 134 | | | 135 | } |
| 176 | ~ |
| 177 | DEL |




有时你会发现标题以感叹号（`!`）开头，这样即使对输出结果进行排序，它们仍然位于输出的开头。

字符排序的顺序被称为*排序序*（collation sequence）。尽管 `ASCII` 是美国标准的排序顺序，但其他国家有时会有特殊的键盘和字母表。因此，你可能会遇到不同的排序序。

### 另参

有关帮助页（man pages）的更多信息，请参第 90 页。

### 排序时忽略开头空格 (sort -b)

如果行以相同的字符开头，它们的顺序将由行第一个不同的字符决定。例如，开头有许多空格的长行将排在开头较少或没有空格的长之前，因为根据 ASCII 表，空格的排序顺序在任何非空格字符之前。例如：

```bash
$ sort tstfile      zebra
    monkey
  apple
```

要在排序时忽略行开头的空格，请使用 `-b` 选项，如下：

```bash
$ sort -b tstfile   apple
    monkey
      zebra
```

### 按数值大小排序 (sort -n)

这种从左到右的原则也适用于以数字开头的行。例如：

```text
|
|
```
```bash
$ sort numfile 10oranges
5apples
66grapes
```

前面的行之所以被排序，是因为 1 在 5 之前。若要根据行首数字的数值大小对行进行排序，请使用下所示的 `-n` 选项：

```bash
$ sort -n numfile 5apples
10oranges
66grapes
```

`-n` 选项也能处理负数和分数。例如：

```bash
$ sort -n numfile3 -30bananas
-2pineapples
5.44apples
5.5apples
10oranges
66grapes
```

在下一个示例中，数字是右对齐的，这意味着数字可能从不同的列开始，但它们结束于同一列。

```bash
$ cat numfile2    5pencils
   2032crayons
   153erasers
```

在上述情况下，以及每当你有以右对齐数字头的行时，都不需要 `-n`，因为普通排序将按数值大小排列它们，如下：

```bash
$ sort numfile2    5pencils
   153erasers
   2032crayons
```

使用 `-n` 选项时，它会忽略行开头所有的空格，就像同时也提供了 `-b` 选项一样。如果任何行不以数字开头，`-n` 将这些行视为零值，并将它们排在以数字开头的行之前。

### 将结果保存回原始文件

`sort` 将排序后的行输出到标准输出。这意味着输出将显示在你的屏幕上，原始文件不会受到影响。要将结果保存到文件中，你可以将标准输出重定向到不同的文件，如下：

```bash
sort file1 > file2
```

在上述命令中，排序后的输出将放入 `file2` 而不会显示在你的屏幕上。如果你想修改一个文件使其所有行都处于排序状态，请使用临时文件，如下：

```bash
sort acme > tmpfile$$ && mv tmpfile$$ acme
```

在第一行中，我将排序输出保存到名为 `tmpfile$$` 的临时文件中。`$$` 是一个特殊的 shell 变量，可以提供我的进程号。我在 `tmpfile` 名称中添加 `$$` 是为了使其唯一，即：避免在我在使用该文件名时，其他用户可能也在使用 `tmpfile` 名称。第二行使用 `mv` 删除旧的未排序的 `acme` 文件，并将其替换为排序后的 `acme` 文件。

注意，你不能在管道中将同一个文件既作为输入文件又作为输出文件。例如：

```bash
sort acme > acme # 这是错误的
```

上述命令会失败，因为 shell 会首先设置重定向指向一个空的 `acme` 文件。然后 shell 将启动 sort 进程，该进程会发现 `acme` 是空的，从而产生一个空的输出文件。`acme` 的内容现在丢失且无法恢复。

### 合并忽略大小写排序 (sort -f)




在 ASCII 序列中，所有以大写字母开头的行都会在任何以小写字母开头的行之前排序。要忽略大小写进行排序，请为 `sort` 添加 `-f` 选项。这被称为将大写和小写字母合并。例如：

```bash
$ sort tstfile APPLE
APPLE
Orange
banana
grape

$ sort -f tstfile
APPLE
banana
grape
Orange
```

### 忽略排序结果 -o 选项
`sort` 命令实际上有一个 `-o` 选项，它允许你仅使用一个命令将排序后的结果保存到原始文件上。其他 UNIX 命令没有此选项，因此我向你展示了一种保存排序结果的方法，该方法适用于任何向标准输出写入内容的 UNIX 命令。

```bash
$ ls -s total
660
15 acme
625 pegasus
20 report7
```

### 反逆排序 (sort -r)
要按反序对行进行排序，请为 `sort` 添加 `-r` 选项。这与 `-n` 选项配合使用时特别有用，当你想先看到最大值时。例如，`ls -s` 将列出当前目录下的文件，并以文件块大小在前面。（你可以查看附录中的 `ls` 命令。）

```bash
$ ls -s total
660
15 acme
625 pegasus
20 report7
```

当文件很多时，很难在视觉上识别出大文件。我们可以将输出通过给 `sort`，让 `sort` 按从大到小排列文件。

```bash
$ ls -s | sort -rn
```
在此示例中，请注意我们是如何结合 `-r` 和 `-n` 选项的。实际上，排序的 `-n` 选项并不是真正需要的，因为数字是右对齐的。注意 `total` 行出现在了最后。因为它不是以数字开头的，`-n` 将其视为零值。在上一个示例中，为什么 `total` 行中的 `660` 出现在最后？答案是：`-n` 在寻找行首的数字（任何前导空格之后）。任何以非字母开头的行（如 `total` 行）都被视为具有零值。

### 排序时忽略标点符号 (sort -d)
如你所见，标点符号遍布于整个 ASCII 表格，因此会影响以标点符号开头的行的排序顺序，如下：

```bash
$ sort tstfile "orange"
'grape'
<apple>
melon
{banana}
```

要忽略标点符号并仅对字母、数字、空格和制表符进行排序，请使用 `-d` 选项按字典顺序排序如下：

```bash
$ sort -d tstfile <apple>
{banana}
'grape'
melon
"orange"
```

排序选项 `-d` 不能与 `-n` 选项结合，因此如果行以标点符号开头，仅使用 `sort` 选项无法按大小对数字排序。

### 根据行内的字段排序 (sort +n)
`sort` 命令将任何空格或制表符序列视为新字段。例如，在 `ls -l` 最后一行的每一列下方，我标注了它所在的字段编号。假设我们想按第 5 字段（字节大小）对此输出进行排序。

```bash
$ ls -l total
-rw-r-- 1 mori users 17157 Feb 11:31 acme
-rw-r-- 1 janepf accounting 1972 Feb 11:31
-rw-r-- 1 mori users 196484 Feb 11:33
```

注意字段 4 和字段 5 在每行的起始列位置不同。要让 `sort` 忽略或跳过行中的某些字段，请使用 `+n` 选项（其中 `n` 是跳过的字段数）。

```bash
$ ls -l | sort +4 # 这不是我们想要的 total
-rw-r-- 1 mori users 17157 Feb 11:31 acme
-rw-r-- 1 mori users 196484 Feb 11:33
-rw-r-- 1 janepf accounting 1972 Feb 11:31
```

在之前的示例中，`sort +4` 表示跳过 4 个字段并从第 5 字段开始排序，该字段文件的字节大小。然而，第 5 字段从该字段的前导空格开始。当你跳过前 4 个字段时，剩余行的排序如下：

```
   17157 Feb 1 11:31 acme
196484 Feb 1 11:33
1972 Feb 1 11:31
```

注意，当你跳过前 4 个字段时，数字并不是右对齐的。因为我们想按大小排序行，且第 5 字段没有右对齐，我们将添加 `-n` 选项来获取我们想要的输出：

```bash
$ ls -l | sort -n +4 total
-rw-r-- 1 janepf accounting 1972 Feb 11:31
```





```
-rw-r--r--  1 mori      users       17157 Feb  1 11:31 acme
-rw-r--r--  1 mori      users       196484 Feb  1 11:33
```

![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)
report07

当使用 `+n` 选项跳过字段排序时，字段开头的空格数量会影响排序。如果我们想要排序的字段包含数字，使用 `-n` 选项按大小排序，并忽略该字段开头的空格。如果我们想要排序的字段包含文本，使用 `-b` 选项排序以忽略该字段开头的空格。如果我们想要排序的字段包含开头空格，且文本有需要忽略的开头标点，则使用 `-bd` 同时忽略开头空格和开头标点，如下所示：

```bash
sort -bd +3 report8
```

### 基于主键和次键的排序 (`sort +m -n`)

假设我们有一个朋友文件，列出了几个朋友的名字、中间名首字母、姓氏和城市。注意按姓氏排序时会发生什么：

```bash
sort +2 friends     # 这不是我们想要的
William A.  Smith, St. Louis
James B. Nguyen, Los Angeles
Henry H. Nguyen, Yuba City
Mary K. Zornan, Cleveland
Mary A. Zornan, Pittsburgh
```

注意到 Smith 排在最前面，是因为该条目中 Smith 之前恰好有两个空格，而“空格-空格”在“空格-字母”之前，就像 `aa` 在 `ab` 之前一样。我们可以通过添加 `-b` 选项来忽略开头空格，如下：

```bash
sort -b +2 friends     # 这更接近我们的想要
James B. Nguyen, Los Angeles
Henry H. Nguyen, Yuba City
William A.  Smith, St. Louis
Mary K. Zornan, Cleveland
Mary A. Zornan, Pittsburgh
```

现在注意到两个 Nguyen 条目是按城市排序的。这是可以理解的，因为我们跳过了前两个字段并对行的剩余部分进行了排序。如果我们想先按姓氏排序，如果姓氏相同，再按名字排序呢？我们将此过程称为使用主排序键和次排序键。在这个例子中，姓氏为主排序键。名字和中间名首字母是次排序键，当两行具有相同的主排序键时使用它。你甚至可以指定使用更多级别的排序键，前提是所有更高层级的排序键都相同。你可以指定忽略主键中的开头空格但不忽略次键中的。你可以指定按正常顺序对主键排序，但如果主键相同，则按反向顺序对次键排序。你可以指定忽略主键或次键的一个或多个字符。你可以按大小对主键排序而按文本对次键排序。

### 使用主字段和次字段

1. 如果你准备将内容传递给 `sort`，请输入生成待排序输出的命令。接着输入管道符号 (`|`)。管道符号 (`|`) 周围的空格可选可选。在收到指令前不要按回车键。
2. 输入 `sort`。在收到指令前不要按回车键。
3. 如果你想让任何排序选项全局应用于主键、次键和所有排序键，请输入空格，然后输入一个连字符 (`-`)，紧接着输入此列表中所需的选项：
   - `b`: 忽略开头空格
   - `d`: 忽略开头标点（如果未指定 n）
   - `f`: 忽略大小写
   - `n`: 按大小排序数字并忽略开头空格
   - `r`: 反反顺序排序
4. 输入一个空格，然后输入 `+m`。将 `m` 替换为要跳过的字段数量，以到达主排序键的第一个字段。
5. 如果你想忽略主排序键开头的字符，输入 `.n`。将 `n` 替换为要忽略的起始字符数量。例如，`+3.2` 表示跳过三个字段，然后跳过两个字符，因此我们从第 4 个字段的第 3 个字符开始排序；即从字段 `m+1` 开始从第 `n+1` 个字符开始排序。因为对字段的部分进行排序很少见，所以通常省略 `.n`。
6. 现在你可以输入这些选项之一应用于此排序键：
   - `b`: 忽略开头空格
   - `d`: 忽略开头标点（如果未指定 n）
   - `f`: 忽略大小写
   - `n`: 按大小排序数字并忽略开头空格
   - `r`: 反向顺序排序
   例如，`+3.2bfr` 表示该排序键的找到方式是跳过三个字段，然后跳过两个字符并忽略开头空格、忽略大小写，且仅为此排序键按反向顺序排序。
7. 输入一个空格，然后指定主排序键的结束。使用符号 `-m.nOPTS`，其中：
   - `m` 是结束字段编号（不是跳过的字段数）
   - `n` 是第 `m` 个字段最后一个字符之后包含的字符数量





`OPTS` 可以是第 6 步描述的 `b`、`d`、`f`、`n` 或 `r`，但在实践中只有 `b` 用于定义排序字段的结束位置。因为很少会在排序字段的中间结束，所以通常会省略 `.nOPTS` `。如果完全省略了 `-m.nOPTS`，则排序键被认为延伸到行尾。

### 8. 由于前面的步骤较为复杂，让我们停下来，总结一下在正常情况下如何指定主排序键：

```
sort -GGG +xOPTS -y
```

其中：
- `GGG` 可以是排序选项 `b`、`d`、`f`、`n` 或 `r`，并将全局应用于主、次要以及所有的排序键。
- `+x` 表示跳过多少字段以到达主排序键。
- `OPTS` 可以是排序选项 `b`、`d`、`f`、`n` 或 `r`，并将仅应用于主排序键。
- `-y` 表示哪个字段结束了主排序键。

例如：
```
sort -f +2b -4
```
在上面的示例中，`-f`（忽略大小写）应用于所有的排序键。主键的起始通过跳过两个字段并忽略前导空格来找到。主排序键在字段 4 结束。因此，在这个示例中，字段 3 和 4 构成了主排序键。

### 9. 输入一个空格，然后以与指定主键相同的方式输入次排序键。例如：

```
sort -GGG +m.nOPTS -m.nOPTS +m.nOPTS -m.nOPTS          ppppppppppppppppp sssssssssssssss
```

在前面的格式中，重复的字母 `p` 表示指定主排序键开始和结束的位置。重复的字母 `s` 表示指定次排序键开始和结束的位置。

去掉较少使用的选项，这里是主键和次键的简化格式：
```
sort -GGG +xOPTS -y +xOPTS -y          ppppppp ssssss
```

### 10. 可以通过在命令中添加更多的起始和结束规范来添加更多的排序键。例如：
```
sort -GGG +xOPTS -y +xOPTS -y +xOPTS -y +xOPTS -y          ppppppp ssssss 3333333 4444444
```
记住，除非两行具有相同的主排序键，否则次排序键不会被使用。除非两行的主键和次键都相同，否则三级（第三阶）排序键不会被使用。

### 11. 如果你正在将内容传递给此 sort 命令并且已经输入了所有的排序字段规范，请按回车键完成命令。否则，你现在可以输入一个空格以及一个或多个要排序的文件名列表。如果你列出了多个文件名，请用空格分隔每个名称。列表可以包含文件名生成通配符模式。然后按回车键完成你的命令。

现在我们可以完成之前开始的示例，并按姓氏对 `friends` 文件进行排序。如果姓相同，则按名和中间名首字母排序。如果这些也相同，则按城市排序到行尾。这里是实现所有这些内容的 sort 命令：

```bash
$ sort -b +2 -3 +0 -2 +3 friends
Henry H. Nguyen, Yuba City
James B. Nguyen, Los Angeles
William A. Smith, St. Louis
Mary A. Zornan, Pittsburgh
Mary K. Zornan, Cleveland
$
```

有时你会遇到 `-k` 选项，它允许排序键。大多数系统都支持较新和旧的方法。以下是使用旧方法处理 `friends` 文件的等命令：
```
sort -k3,3 -k2,2 -k4,4 friends
```

简化格式为：
```
sort -kaOPTS,b
```
`aOPTS,b` 是此排序键的起始字段（不是跳过）。`OPTS` 可以是 `b`、`d`、`f`、`n` 或 `r`，并将仅应用于此键。`b` 是此键的结束字段。

### 显示文件的起始行 (*head, sed*)

 仅显示文件的前几行，请使用 `head` 命令，如下：
```bash
head groceries friends
```
`head` 接受命令行上的文件列表。当给出多个文件时，`head` 将用一个小小的横幅识别每个文件的起始，如下：
```
== groceries ==
5 apples
3 grapes
2 melons
== friends ==
James B. Nguyen, Los Angeles
Henry H. Nguyen, Yuba City
William A. Smith, St. Louis
Mary A. Zornan, Pittsburgh
Mary K. Zornan, Cleveland
```





`head` 通常显示最多 10 行输出。当你想要查看多个文件的某些行时，这非常有用。要显示更多或更少的行，请对 `head` 使用 `-n` 选项，如下所示：

```
ls -lt | head -20
```

在前面的示例中，`-20` 选项导致 `head` 最多显示 20 行。在前面的示例中，你还可以看到如果命令行上没有指定文件作为参数，`head` 将从标准输入读取，因此你可以在管道中使用它。在这个示例中，`ls -lt` 按最近修改的顺序显示文件，因此整个管道显示了最近修改的 20 个文件。

如果你的系统上没有 `head` 命令，你可以像这样使用 `sed` 命令：

```bash
sed nq filename
```

将 `n` 替换为要显示的起始行数，如下所示：

```bash
ls -lt | sed 5q
```

此示例仅显示前五行。前一个示例还说明了如果命令行上没有指定文件，`sed` 将从标准输入读取，因此它也可以用于管道。如果命令行上给了多个文件，`sed nq` 将显示这些文件的前 *n* 行，但它不会像 `head` 那样识别文件名。

**另参**：有关 `sed` 命令的更多信息，请参阅第 417 页

## 显示文件或管道的结束行

要仅显示文件的结束行，请使用 `tail` 命令，如下所示：

```
tail filename
```

`tail` 命令通常在命令行上接受一个文件名。`tail` 通常显示文件的最后 10 行。要指定显示最后几行，请对 `tail` 使用 `-n` 选项，如下所示：

```bash
ls -lt | tail -20
```

此示例仅显示来自 `ls` 命令的最后 20 行（你可以在附录中查看 `ls` 命令的选项）。前一个示例还说明，如果没有提供文件名，`tail` 将从标准输入读取，因此可以用于管道。

要从文件的第 `n` 行开始显示到文件末尾，请使用带有 `+n` 选项的 `tail`。例如：

```
tail +350 filename
```

警告：`tail` 输出是限制的。在许多 UNIX 版本上，`tail -n` 被限制为最多数百或几千行。`tail` 接受较大的 `-n` 值，但它不会显示那么多行。前一个示例将从文件的第 350 行开始并显示到文件末尾的所有行。要观察文件中添加的内容（例如日志文件），请输入：

```bash
tail -f filename
```

`tail` 将首先显示文件的最后 10 行。命令不会在那里停止。它将继续跟踪文件，随着新行被添加到文件末尾，`tail` 将把它们显示在你的屏幕上。这将一直持续直到你按下 `INTR` 键（通常是 `Ctrl+C` 或 `Delete`）。

## 加密文件或管道

如果你有机密文本信息或数据，可以使用 `crypt` 命令对信息进行加密或乱码，只有知道正确密码或密钥的人才能解密——即解乱信息并使用它。请注意，自 `crypt` 命令以来加密技术已经取得了进步，据报道今天有几种程序可以破解这种安全性。为了获得更好的加密，请研究来自某些 UNIX 供应商、技术书店以及互联网提供的 `pgp` 或 `des`。

### 如何使用 Crypt 加密文件

1. 确保你知道要加密文件的完整路径。该文件可以是文本文件也可以是数据文件。
2. `cd` 到包含要加密文件的目录。
3. 输入 `crypt < EXISTING-FILE > tmpfile`。将 `EXISTING-FILE` 替换为要加密的文件基名。`tmpfile$$` 是我们在此过程中使用的临时文件。按照所示所示输入该名称，但请注意 shell 将用某些数字替换 `$$` 以使名称唯一。




确保唯一性，以免当其他用户同时在同一目录下执行相同操作时发生冲突。

4. 在输入第 3 步中型命令后，你将看到此提示：
`Enter key:`

输入一个或多个字符或单词作为加密密钥。出于安全考虑，你输入的内容不会显示在屏幕上，因此请缓慢且仔细地输入密钥。

**警告**：你将需要知道此密钥的准确拼写，以便稍后解密并使用你的文件。该密钥没有后门，因此如果你忘记了该密钥，就无法解密你的文件。

5. 在第 4 步中输入密钥后，`tmpfile$$` 将存储加密后的信息。

6. 通过输入以下命令测试 `tmpfile$$`：
```bash
crypt < tmpfile$$ > tmp2$$
```
你将再次看到此提示：
`Enter key:`

输入与加密该文件相同的密钥。请注意，同一个密钥用于加密和解密信息。

7. 输入 `cmp EXISTING-FILE tmp2$$`。
将 `EXISTING-FILE` 替换为想要加密的原始文件名。此 `cmp` 命令应该直接返回 shell 提示符而没有任何输出，表示两个文件是相同的。如果不是，说明出了问题。请勿继续此操作。可能是你输入的密钥错误。尝试返回第 6 步。如果第 7 步显示文件不同，请按如下方式删除临时文件：
```bash
rm tmpfile$$ tmp2$$
```
并返回此操作的第 1 步。

8. 输入 `mv tmpfile$$ EXISTING_FILE`。
将 `EXISTING-FILE` 替换为想要加密的原始文件名。这将用加密版本替换原始文件。

9. 输入 `rm tmp2$$`。这删除了我们不再需要的另一个临时文件。

要解密文件，请输入以下：
```bash
crypt < ENCRYPTED-FILE > DECRYPTED-FILE
```
将 `ENCRYPTED-FILE` 替换为要解密的文件。将 `DECRYPTED-FILE` 替换为你想要创建的任何新。确保该名称已存在，因为该名称会被此命令覆盖。`crypt` 将输出此提示信息：
`Enter key:`

输入与加密文件相同的密钥。你也可以在命令行中提供密钥。例如：
```bash
crypt "Mary had a lamb" < file1 > file2
```
当你想在 shell 脚本中使用 `crypt` 而不想被提示从键盘输入密钥时，这非常有用。但请注意，任何读取 shell 脚本的人都能看到密钥是什么；这安全性不高。

加密软件通常不包含在你的 UNIX 系统中，因为美国政府有规定，将此类安全技术出口到国外。如果你的商业 UNIX 系统上没有加密功能，你可能会发现它在国内范围内是可用的。请咨询你的 UNIX 供应商。

 压缩文件 (*compress, gzip*)

压缩文件意味着对其内容进行编码，使其尺寸变小，并且在以后需要时可以恢复到原始大小和内容。文件可以压缩到多小取决于文件中的数据。包含许多重复字符的文本文件，压缩后的尺寸可以比包含随机数据的二进制文件小得多。

文件通常压缩有两个原因：
- 它们占用更少的磁盘空间。例如，你可能会压缩一组很少使用但必须保持可访问的归档文件。
- 可以在更短的时间内传输到另一个系统。如果你通过慢速调制调器下载文件，这可能是一个因素。

在 UNIX 下，你可以使用两个命令来压缩文件：





# compress 和 gzip

`compress` 在大多数 UNIX 系统上都可用。`gzip` 通常能提供更好的压缩效果——也就是说生成的压缩文件比 `compress` 命令更小。然而，`gzip` 通常不是标准 UNIX 发行版的一部分。

使用 `compress` 命令压缩文件，请输入以下命令：

```
compress FILENAME
```

将 `FILENAME` 替换为要压缩的文件。`compress` 会创建一个同名但后缀为 `.Z` 的压缩文件并删除原始文件。仅在 SCO UNIX OpenServer5 上，`compress` 有一个 `-H` 选项，它可以使用更好的压缩方法并生成更小的文件，且这些文件仍可以使用标准的 `uncompress` 进行解压。Solaris 2.6 未为 `compress` 提供此选项。

使用 `gzip` 压缩文件，请输入以下命令：

```
gzip FILENAME
```

将 `FILENAME` 替换为要压缩的文件。`gzip` 会创建一个同名但后缀为 `.gz` 的压缩文件并删除原始文件。

要在 `gzip` 中获得最佳压缩效果，请添加 `-9` 选项，如下所示：

```
gzip -9 FILENAME
```

共有从 `-1` 到 `-9` 的九个选项。如果你主要考虑的是快速完成压缩，即使文件不是尽可能小，请使用 `-1`。如果你主要考虑的是让结果尽可能小，请使用 `-9`，这将花费更多时间来完成。可以使用中间的任何数字作为速度与大小之间的权衡。如果未给出值，默认为 `-6`。

## 如何解压文件

1. 输入 `uncompress`。如果要解压的文件以 `.Z` 结尾，输入 `gunzip`。如果解压的文件以 `.gz` 结尾，在收到指令前不要按回车键。
2. 输入空格，然后输入要解压的文件名，该文件名必须以 `.Z` 或 `.gz` 结尾。
3. 按回车键执行此命令。文件将被解压，文件名中的 `.Z` 或 `.gz` 后缀将被移除。## 将文件编码为可传输的简单文本 (uuencode)

在邮件正文中发送信息时，信息必须是简单的、可的文本字符。当你从命令行使用 UNIX `mailx` 命令时，无法包含附件，因此任何要发送的二进制文件必须转换或编码为一段简单的文本字符。我们称此过程为 `uuencoding`，其中 `uu` 是用于 UNIX 到 UNIX 传输工具的标准 UNIX 前缀。

`gzip` 通常可以下载，但通常不随商业 UNIX 系统提供，通常可以通过专门提供你运行的 UNIX 平台共享软件或免费工具的互联网网站下载（例如 `www.sun.com`、`www.ibm.com` 或 `www.sco.com`）。

如果你拨入了另一个 UNIX 系统并想下载或上传二进制文件，`uuencoding` 也很有用。`cu` 中的 `~put` 和 `~take` 命令仅下载或上传文本文件。二进制文件可以先被 `uuencoded` 为文本文件。这些文件可以被传输，然后 `uudoded` 还原为原始二进制格式。

在 shell 提示符下 `uuencode` 一个文件，请输入：

```
uuencode BINFILE DESTFILE TEXTFILE
```

将 `BINFILE` 替换为要编码的二进制文件。将 `DESTFILE` 替换为要在目标系统上创建的文件名。将 `TEXTFILE` 替换为你系统中创建带有 `uuencoded` 信息的文件名。

要对另一个 UNIX 命令或管道的输出进行 `uuencode`，请输入：

```
CMD | uuencode DESTFILE TEXTFILE
```

将 `CMD` 替换为生成要 `uuencoded` 输出的 UNIX 命令或管道。

在 `TEXTFILE` 传输到另一个 UNIX 系统后，你可以输入以下内容将其还原为原始格式：

```
uudecode TEXTFILE
```

上述命令会创建二进制文件并将其命名为 `DESTFILE`，该名称是在运行 `uuencode` 时指定的。





要在运行 `uudecode` 之前确定 `DESTFILE` 是否会被创建，请输入：：

```
head TEXTFILE
begin 660 /usr/fred/acme M?T5,1@$! 0           (  P !    <)T$"#0   !0I@       #0  (  &
M "@ $@@ 0   8     T     -($"      #      P      4           P    /0
M             !,          !           !    -    #2 ! @     9'X
M &1^   %      !     $    "8?@  F X%"      #@)@  5$8    <      $
```

在第一行中，你可以看到当此文件被 `uudec` 解码时，它将创建一个名为 `/usr/fred/acme` 的文件。如果你想更改 `uudecode` 创建的目标文件，可以编辑此文件中的名称。这在于 UNIX 和 Windows 之间发送 uuencoded 文件时尤为有用。注意，其余行都以字母 `M` 开头。一个 `begin` 行后跟许多行 `M` 行通常表示这是一个 uuencoded 文件。

如果你在邮件中收到带有 uuencoded 文件的邮件，你可以保存此邮件并对其进行 `uudecode`，而无需删除 uuencoded 行前后的邮件行。

## 另此

关于使用 `cu` 的更多信息，请参见第 252 页。

## 合并文件

本节介绍了几个可以用于各种目的合并文件内容的命令。

### 邮件下的 uuencode/uudecode
Windows 下某些邮件程序支持 `uuencode/uudecode`。如果你想从 Windows 向 UNIX 发送二进制文件，这将非常有用。点击 `uuencode` 将二进制文件的文本版本直接插入你的邮件中。这不是附件！如果你在 Windows 邮件中收到 uuencoded 数据，请点击 `uudecode` 将数据保存到文件中。你可能需要调整 uuencoded 文本中的目标文件名。

### 对多个文件进行排序 (sort)
我们在本章开头介绍过 `sort`。如果在命令行上带有一个文件列表调用 `sort`，`sort` 将首先合并它们的内容，然后按排序顺序显示合并后的内容，如下：

```
sort file1 file2 file3 > bigsort
```

### 串联文件 (cat)
若要按顺序合并文件，请使用 `cat` 命令：

```
cat file1 file2 file3 > bigfile
```
`cat` 命令的名称源于 concatenation（连接）。

### 并排粘贴文件 (paste)
`cat` 命令是按顺序合并。`paste` 命令则是并排合并。`paste` 输出的第 1 行包含 `file1` 的第 1 行，然后是一个制表符，接着是 `file2` 的第 1 行，然后是制表符，最后是 `file3` 的第 1 行，此类推。同样，第 2 行包含每个文件的第 2 行。要以此种方式粘贴文件，请输入：

```
paste file1 file2 file3...
```

如果 `colors` 文件每行一种颜色，`fruits` 文件每行一个水果，将它们拼接将产生如下输出：

```
paste colors fruits
red   green apple
blue  banana
yellow melon
```

### 根据连接字段合并已排序的文件 (join)
`join` 命令允许你将一个文件中某行的数据与第二个文件中对应行的数据进行合并。相应的行是通过查找具有匹配 `join` 字段的行来指定的。两个文件都必须经过排序。你可以指定哪个字段为连接字段，且该字段在两个文件之间可以不同。你可以指定从每个文件中提取什么数据。以下是一个示例。

我的一个朋友正在研究股市。他加入了一个服务，该服务每天向他发送一个包含平均股票价格的文件。他想将这些小文件合并成一个大的历史文件，以便他一眼看出特定股票价值是在上涨还是下跌。以下是第 1 天的示例文件，它只包含三只股票：

```
ABC 2/8 DEF 24/8 GHI 6/8
```

这是第 2 天的文件：

```
ABC 3/3 BCD 12/2 DEF 22/8 GHI 5/5
```

这是第 3 天的文件：

```
ABC 5/5 BCD 14/3 DEF 22/5
```




你可以看到，在第 2 天我们获得了一只新股票 BCD。在第 3 天，我们丢失了股票 GHI。每个文件的第 3 行并不总是同一只股票；因此，我们无法使用 `paste` 命令来合并这些文件。这就是 UNIX `join` 命令用的任务。在这个示例中：

我们使用股票名称作为连接字段。

```bash
$ join -t'   ' -a1 -a2 day1 day2 ABC    2 1/8    2 3/8
BCD   12 2/8
DEF   24 5/8   22 7/8
GHI     6 3/8     6 5/8
```

在前面的示例中，`-t` 允许我们指定字段分隔符。在这种情况下，制表符（tab）将每个文件中的股票名称与其平均值隔开。因此，在 `-t` 选项之后指定了一个制表符进行连接。`-a1` 和 `-a2` 意味着包含文件 1 和文件 2 中的所有行。否则，将列出连接字段值在两个文件中都出现的行。在这个示例中，股票 BCD 仅出现在文件 2 中，因此如果没有指定 `-a2`，它将不会包含在连接输出中。

```bash
$ join -t'   ' -a1 -a2 day1 day2 | join -t'   ' -a1 -a2 - day3
ABC    2 1/8    2 3/8    2 5/8
BCD   12 2/8   14 3/8
DEF   24 5/8   22 7/8   22 5/8
GHI     6 3/8     6 5/8
```

在前面的示例中，`day1` 和 `day2` 的连接输出与 `day3` 相连接。注意一个 `join` 命令的输出如何通过管道到另一个 `join` 命令，如果该 `join` 命令将连字符（`-`）作为文件名之一表示标准输入。

要处理连接字段不是每行第一个字段的情况，请为 `join` 添加 `-j` 选项。在 `-j` 之后输入每个文件中连接字段的字段编号。例如：

```bash
$ join -j 3 file1 file2
```

要处理两个文件之间连接字段不是相同编号的情况，请使用 `-j` 后紧接 `nm`，其中 `n` 是 1 或 2（代表文件 1 或文件 2），`m` 是该文件中作为连接字段的字段，如下所示：

```bash
$ join -j 2 -j 4 file1 file2
```

在这个示例中，连接字段是文件 1 中的第 2 个字段，但在文件 2 中是第 4 个字段。要为 join 输出的每行仅显示某些特定字段，请使用 `-o` 选项，其后跟一个用空格分隔的 `n.m` 条目列表，其中 `n` 是 1 或 2（代表 `file1` 或 `file2`），`.m` 指定该文件中第 `m` 个字段，如下所示：

```bash
$ join -j 2 -j 4 -o 1.1 2.3 2.5 file1 file2
```

### join 有多用处？

一些 UNIX 籍暗示你可以通过 `join` 实现整个关系型数据库。其他的 UNIX 籍完全没有提到 `join`。我发现 `join` 在某些情况下合并来自不同文件的数据很有用。然而，由于 `join` 功能非常有限，我会使用 `awk` 或 `perl` 来对数据文件进行查询和编写报告。前面的示例将由 `-o` 选项控制每行显示三个字段：`1.1` 意味着首先显示 `file1` 中的第 1 字段，`2.3` 意味着接着显示 `file2` 中的第 3 字段，`2.5` 意味着最后显示 `file2` 中的第 5 字段。

### 将一个文件分成多个文件

有时，将一个文件分成较小文件是有用的。例如，如果一个文件无法放入磁盘，你可以将其分成多个可以放入磁盘的小文件。另一个例子是，当使用 `cu` 拨入另一个 UNIX 系统时，可以在系统之间传输文件。由于没有错误检查，干扰行可能会导致目标文件损坏。在这种情况下，我通过将文件分成几个较小文件然后分别传输获得了成功。使用 `cat` 命令，可以通过连接这些小文件来简单地恢复原始文件。

### 将文件分成等长度的片段 (*split*)

如何将文件分成等长度的段

1. 在 shell 提示符处，输入 `split`。在接到指示前不要按回车键。
2. 输入一个空格，然后输入 `-LINES`。将 `LINES` 替换为放入每个文件段的行数；例如，`-400` 表示创建每个长 400 行的小文件。如果省略此步，每个片段将创建为 1,000 行。
3. 输入一个空格，然后输入要拆分的文件。如果文件在当前目录下，只需输入其文件名。如果文件不在当前目录，请输入其绝对或相对路径。该文件不会受到此命令的影响。




4. 输入一个空格，然后输入分段前缀。第一个分段将以分段前缀后接 `aa` 开始。第二个段后面是 `ab`，然后是 `ac`，以此此类推。如果给定的前缀较小，例如，现有文件将被拆分为 `smallaa`、`smallab`、`smallac`、`smallad` 等的分段。如果跳过此步骤，分段前缀将为 `x`（即 `xaa`、`xab`、`xac` 等）。
5. 按回车键执行此命令。

要从分段重新创建原始文件，可以使用文件名生成通配符。例如：

```bash
cat small* > bigfile
```

`small*` 将匹配 `smallaa`、`smallab`、`smallac` 等。如果其他文件也以该前缀开头但不是大文件的分段，你可以使用更具体的通配符模式来规避它们。例如：

```bash
cat smalla[a-f] > bigfile
```

# 按章节标题分割文件 (*csplit*)

`csplit` 命令允许你根据文件内部的上下文将文件分割成段。

## 按重复的章节关键词分割文件

1. 确定一个出现在每个章节标题中的关键词。例如，如果每个关键章节标题都以单词 *Chapter,* 开头，那么 `Chapter` 就是关键词。如果没有单一关键词出现在每个章节标题中，则无法使用此方法。
2. 在 shell 提示符下，输入 `csplit -k`。在指示之前不要按回车键。
3. 输入一个空格，然后输入要分割的现有文件名称。
4. 输入一个空格，然后输入单引号（`'`）和斜杠（`/`）。
5. 输入章节关键词。
6. 输入斜杠（`/`），然后输入单引号（`'`）。
7. 输入一个空格，然后输入 `{}`。按回车键执行此命令。
8. 忽略错误信息：out of range（超出范围）。我们告诉它在必要时创建分段，但通常数量会少于该值。
9. 这将创建名为 `xx00`、`xx01`、`xx02` 等的文件。每个段将包含直到包含关键字行（如第 1 步所述但不包含）的所有行。如果 `Chapter` 是关键词，`xx00` 将包含到 Chapter 1 开始之前的所有行；`xx01` 将包含 Chapter 1 的所有行，直到但不包含 Chapter 2，以此此类推。

## 按唯一关键词分割文件

1. 当你能够识别出每个章节开头的唯一单词时，使用此方法。
2. 在 shell 提示符下，输入 `csplit`。在指示之前不要按回车键。
3. 输入一个空格，然后输入要分割的现有文件名称。
4. 输入一个空格，然后在斜杠（`/`）之间输入结束第一个段的关键词。包含该关键词的行将作为第二个段的开始。
5. 输入一个空格，然后在斜杠（`/`）之间输入结束第二个段的关键词。包含该关键词的行将作为第三个段的开始。
6. 继续在斜杠（`/`）之间输入关键词，直到定义所有段。按回车键执行你的命令。
7. 这将创建名为 `xx00`、`xx01`、`xx02` 等的文件。这是上述操作的示例：

```bash
csplit existing-file '/INSTRUCTIONS/' '/WARNINGS/' '/APPENDIX 1'
```

![arrow.gif](img/4505ed21b36ef4ebf4df520603bad.gif)

通过上述操作将创建四个分段文件：`xx00`、`xx01`、`xx02` 和 `xx03`。`xx00` 将包含直到包含 `INSTRUCTIONS` 的行之前的所有行。`xx01` 将从 `INSTRUCTIONS` 行开始，一直找到 `WARNINGS` 单词为止。`xx02` 将从包含 `WARNINGS` 单词的行开始。`xx03` 将从包含短语 `APPENDIX 1` 的行开始，并包含文件中其余的所有行。





# 使用文件名生成通配符 (*, ?, [...]) 创建文件列表

## 检查哪些命令允许文件列表

## 处理文件名通配符错误参数列表过长 (arg List Too Long)

## 使用反引号 ('') 创建文件列表

## 处理反引号错误空格 (No Space)

## 使用 `xargs` 处理极长的文件列表

# 使用文件名生成通配符

大多数文件命令都可以对一个或多个文件运行。例如，文件命令可以处理以下内容：
* 单个文件
* 几个文件
* 数百个文件
* 数万个文件（当然，这要困难得多。）

一如既往，UNIX 能够提高工作效率。在这种情况下，UNIX 通过提供一种方法，使用非常短的按键序列向命令输入一系列很长的文件名，来提高效率。用户可以在任何命令中输入一个或多个模式单词，shell 将把每个模式替换为匹配该模式的所有文件名列表。模式单词是指任何包含表 9.1 所示通配符字符之一的单词。

### 表 9.1 文件名生成通配符字符。

| 字符 | 描述 |
| :--- | :--- |
| `*` | 匹配零或多个任意字符 |
| `?` | 匹配任意单个字符 |
| `[...]` | 匹配括号内的任意一个备选项目 |
| `[!...]` | 匹配列出字符以外的任何字符 |

### 生成以模式开头、结尾或包含模式的名字 (*)

我们将从星号 (`*`) 通配符开始，因为它是所有通配符中最强大且最易理解的，因此也是最常用的。这里有一个例子：`rm report*` 是删除（即移除）一个或多个文件的 UNIX 命令。`report*` 是一个模式单词，因为它包含了表 9.1 给出的三个通配符字符之一。在命令开始执行之前，shell 将重新组合命令，将模式单词替换为匹配该模式的所有现有文件名列表。从表 9.1 可以看出，星号 (`*`) 匹配零或多个任意字符。因此，`report*` 是一个模式，匹配所有以 report 开头并后跟零或多个任意字符的现有文件名。

#### 表 9.2 使用 `rm report`。

会被 `rm report*` 删除的文件：
| Report |
| :--- |
| report2 |
| reports |
| 1reporters |
| Reportacme |
| report.acme |
| report-98.01.15 |

不会被 `rm report*` 删除的文件：
| Filename | 模式不适的原因 |
| :--- | :--- |
| Report | 大写 R 不匹配该模式 |
| 98report | 文件名不以 report 单词开头 |
| report.acme | 此名称中的 Report 拼写错误 |

### 删除所有以模式开头的文件

1. 输入 `rm`。我们使用 `rm` 作为示例，但该步骤适用于任何操作文件的命令。
2. 输入空格，然后输入模式。该模式定义了我们想要查找的前缀。
3. 输入星号 (`*`)，然后按回车键完成命令。
4. shell 将接受你的命令并对其重新组合，将模式单词替换为匹配该模式的所有现有文件名列表。然后 shell 将执行 `rm` 命令，其删除文件列表就像是你直接在命令行输入了这些文件一样。

我们可以修改上述过程，以删除所有以模式结尾或包含模式的文件。要像下表所示使用星号，你需要学习三个实用的短语。短语的措辞会告诉你星号 (`*`) 应该出现在模式之前、之后还是两侧。

#### 表 9.3 星号 (*) 文件名用用短语。

| 有用短语 | 示例 | 描述 |
| :--- | :--- | :--- |
| Start with ... (...开头) | `rm acme*` | 删除所有以 acme 单词开头的文件名 |
| End with ... (...结尾) | `rm *acme` | 删除所有以 acme 单词结尾的文件名 |
| Contain ... (包含...) | `rm *acme*` | 删除所有包含 acme 单词的文件名 |




Shell 会预处理并通所有文件名通配符模式展开为匹配的文件列表；然而，并非所有命令都能接受文件列表。例如：

### 通配符（wildcard）一词源于何？

在某些卡牌游戏（如扑克牌）中，王牌（Joker）是一种通配符，你可以将其用作牌组中需要的任何其他牌牌。星号 `*` 是一种极其强大的通配符，因为它可以代表零个或多个任意字符（噢，我的意思是字符）。我真希望下次玩扑克牌时能有一个星号 `*` 通配符。

```
pwd report*
```
这没有任何意义，因为 `pwd` 仅显示当前目录，不期望命令行中后续有任何参数。同样，

```bash
cd report*
```
如果有多个目录都以 `report` 单词开头，那么这个命令也是意义的，因为你一次只能切换到一个目录。

UNIX 的 `man` 命令（在线手册）为我们提供了关于如何使用每个 UNIX 命令的详尽信息，包括语法（即如何正确组合命令元素）。以下是几个命令的语法，用于说明 man 手页中是如何记录文件列表的。

#### 表 9.4 man 手页如何指示文件列表。

| 来自 man 的命令语法 | 我的描述（man 手页未包含） |
| :--- | :--- |
| `head [ -count ] [ file . . . ]` | 显示文件列表的开头行。 |
| `sort [-cmu] . . . [ files ]` | 对文件列表的内容进行排序。 |
| `tail [+/-number][lbc] [-f] [ file ]` | 显示给定单个文件的结束行。 |
| `tr -cds] [string1 string2]` | 将字符从标准输入输出。 |
| `cp file1 file2` | 将 `file1` 复制到 `file2`。 |
| `cp files directory` | 将文件列表复制到目录。 |

在前面的表格中，请忽略 `-count` 或 `-cmu` 等命令选项，现在关注如何为这些命令指定文件名。注意 `head` 和 `sort` 命令都允许指定文件列表；其中一个使用 `file . .`，另一个使用 `files` 来表示允许一个或多个文件。`tail` 命令仅允许单个文件。`tr` 命令不允许任何文件名。`cp` 命令有两种模式：第一种模式将单个文件复制到另一个，第二种模式将文件列表复制到目录。命令方面方面不同 UNIX 类型之间可能不同。因此，请检查你所在系统的 man 手页，以查看特定命令是允许文件列表、单个文件还是完全不允许文件。

参见第 89 页

本书的附录包含了如何使用每个命令的摘要，以及关于该命令各个方面的描述所在。从附录中，这里是 `sdiff` 和 `sort` 命令的前几行。注意 `sdiff` 不允许文件列表，因此我们不会在 `sdiff` 命令中使用通配符模式。注意 `sort` 允许文件列表，我们可以通过使用一个或多个通配符模式来组合它。`sort` 用法下的括号 `[...]` 告诉我们文件列表是可选的，意味着可以提供零或多个文件名。

重定向不允许文件名通配符。Shell 不会对任何用于重定向（即 `>`、`>>`）的文件名进行展开。当重定向到一个包含星号的文件名时（该名称通常是某个名称的快捷方式），如果该名称存在，你将创建一个包含星号的名称。



标准的 UNIX 文档通常极力避免使用 `wildcard`（通配符）一词。文档通常将其称为文件名生成模式字符、普通 shell 参数语法或 shell 模式元字符。我认为 `wildcard` 这个术语非常恰当且更容易理解，因此我在书中使用了它。

文中提到了以下文件：
- `inventory-after-special-order`
- `pricelist`
- `reports-in-old-format`
- `sales-Jan-1997-to-Dec-1997-adjusted-for-new-commission-structure`
- `security.memo`

如果我想删除销售文件，星号 `*` 通配符可以节省我大量的打字工作，如下所示：

```
rm sales*
```

然而，我不能将命令缩短为：

```
rm s*
```

这将删除不仅仅是销售文件的其他内容。

## 使用星号 (*) 作为快捷方式

1. 在你想要访问的文件中找到一个独特的模式，该模式在任何其他文件名中都不存在。这个独特模式可以是文件名的开头、结尾或中间任何位置。
2. 输入所需的 UNIX 命令，后跟适当的 `*` 通配符模式，以选择所需的文件而不选择任何其他文件。

### 文件列表中的目录

由星号 `*` 通配符（以及本章讨论的其他通配符）生成的文件列表可以包括普通文件（参见词表）、目录、设备文件等。无论文件类型如何，所有匹配模式的文件名都会在列表中。如果无法无法该类型的文件，它将对该文件报告错误并继续处理列表。

```
rm abc*
abc: directory
abc25: directory
```

在前面的示例中，星号生成的列表包含了两个目录名称。`rm` 确实删除了所有文件名匹配模式的普通文件。`rm` 也针对目录输出了错误信息，表明它没有处理它们。通常情况下，我会忽略这些目录错误，因为我通常使用通配符模式来处理一组文本或数据文件。错误信息的出现是一件好事，它告诉我哪些内容没有被处理，以便我在我想对它们采取进一步行动。

### 从多个模式生成一个文件列表

一个文件列表可以由多个通配符模式生成，如下所示：

```
rm acme* report*
```

在这个示例中，两个通配符模式由空格隔开，组成一个要删除的文件列表。任何以单词 `acme` 开头和任何以单词 `report` 开头的文件都位于同一个删除列表中。

请注意，多个列表可能会多次生成同一个文件名。例如：

```
rm acme* *.sav
```

在前面的示例中，任何以 `acme` 开头并以 `.sav` 结尾的文件将在列表中两次，因此会被打印两次。在本章稍后的部分中，你将学习如何解决这个问题。有关 `rm` 命令的更多信息，请参阅第 169 页。

### 在列表中包含隐藏文件

以点开头的文件名被称为隐藏文件，因为 `ls` 命令通常会隐藏它们（即忽略它们），除非为 `ls` 添加 `-a` 选项来显示所有文件。隐藏文件通常是系统文件，隐藏它们是为了防止在用户列出或处理数据和应用程序文件时它们不会被显示或受到影响。

通配符也遵循这一约定，忽略隐藏文件，除非在通配符模式中明确指定它们。例如：

```
rm *-sav
```

前面的命令将删除任何以 `-sav` 结尾的非隐藏文件。然而，`.acme-sav` 以 `-sav` 结尾，但不会被删除，因为开头的星号 `*` 无法匹配文件名开头的点。



要删除所有以 `-sav` 结尾的隐藏文件，请使用此命令：
```bash
rm .*-sav
```
此命令仅删除以点（`.`）开头并以 `-sav` 结尾的文件。要同时删除以 `-sav` 结尾的隐藏和隐藏文件，请使用此命令：
```bash
rm  *-sav  .*-sav
```
此命令使用两个通配符模式来创建一个待删除的文件列表。为了清晰起见，我额外添加了一些空格。

# 在其他目录生成文件列表

你已经看到星号（`*`）可以匹配除开头点以外的任意零或多个字符。还有第二个例外：星号不能匹配斜杠（`/`）目录分隔符。这是一个很好的规则。否则，像下面的命令：

```bash
rm *-sav
```

将会遍历整个系统寻找以 `-sav` 结尾的文件并进行删除。因为星号（`*`）不能匹配斜杠（`/`），列表仅限于当前目录中匹配模式的文件。

我们可以通过绝对路径或相对路径显式地生成当前目录以外目录中的文件名。例如：

### 表 9.5 使用不一定在当前目录的文件列表

| UNIX 命令 | 描述 |
| :--- | :--- |
| `rm *-sav` | 删除当前目录下任何以 `-sav` 结尾的文件 |
| `rm /tmp/*-sav` | 删除 `/tmp` 目录下任何以 `-sav` 结尾的文件 |
| `rm /tmp/*/*-sav` | 删除 `/tmp` 下任何子目录中任何以 `-sav` 结尾的文件 |
| `rm /*-sav` | 删除根目录下任何以 `-sav` 结尾的文件 |
| `rm */*-sav` | 删除当前目录下任何子目录中任何以 `-sav` 结尾的文件 |
| `rm *-sav */*-sav` | 删除当前目录或当前目录下任何子目录中任何以 `-sav` 结尾的文件 |

在本章稍后的部分，我们还会遇到其他通配符，如问号（`?`）和括号（`[]`），请记住它们也可以像星号（`*`）一样在其他目录生成文件列表。

## 在特定位置允许字符 (?)

问号（`?`）通配符匹配除开头点（`.`）或斜杠（`/）之外的任意单个字符。它允许我们精确指定在其他模式之前、之后或之间允许多少个字符位置。例如：

```bash
rm report-?
```
此命令删除任何以 `report-` 开头且后恰好接一个字符的文件名。

### 表 9.6 rm report-?

| 文件名 | 模式不匹配的原因 |
| :--- | :--- |
| `report` | `report` 后没有连字符（`-`） |
| `report-` | 连字符（`-`）后没有字符 |
| `report-33` | 连字符（`-`）后字符过多 |
| `acme.report-4` | 不以 `report` 开头 |

与星号（`*`）一样，`?` 通配符不能匹配开头点或斜杠（`/）。

## 指定固定长度的文件名

方括号（`[]`）允许你为文件名中的该位置指定一个范围范围，但开头的点或斜杠除外。当你想要访问所有长度完全相同的文件时，问号通配符也非常有用。例如：

```bash
rm report-??
```
此命令删除所有以 `report-` 开头且包含三个字符的文件名。

## 在特定位置允许字符 ([])

方括号（`[]`）允许你为文件名中的该位置指定字符备选，但开头的点或斜杠除外。假设，有二十多个文件名以 `report-` 开头，我们只想删除以下文件：

```bash
rm report-[1-5mv]
```
括号内两个字符之间的连字符（`-`）允许该闭区间范围内的所有字符。不要在括号内包含任何空格或逗号，除非它们本身就是文件名中的字符备选。



如果 `report-3` 不存在会怎样？没有问题，前面的命令不会生成任何错误信息。这些通配符模式从现有文件中选择匹配该通配符模式的文件名。

```
rm report-[4m51-3v]
```

上面的示例等同于上一个示例。以这种方式混杂备选项并不是好习惯。不过，它说明了选项可以以任何顺序列出。使用连字符（`-`）的范围必须按从低到高指定。例如，应指定 `b-g` 而不是 `g-b`。注意上一个示例中括号中的 `51` 意味着 `5` 和 `1` 都是文件名中该位置的备选项。该模式不会匹配 `report-51`，因为方括号只匹配备选项中的单个字符，而不是多个字符。

### 表 9.7：`rm report-[1-5mv]`

会被 `rm report-[1-5mv]` 删除的文件：
* report-1
* report-2
* report-3
* report-4
* report-5
* report-m
* report-v

不会被 `rm report-[1-5mv]` 删除的文件：
| 文件名 | 模式不匹配的原因 |
| :--- | :--- |
| report | report 后面没有连字符 (`-`)。 |
| report- | 连字符 (`-`) 后面没有字符。 |
| report-33 | 连字符 (`-`) 后面字符太多太多。 |
| report-6 | 6 不是允许的选项之一。 |
| report-x | x 不是允许的选项之一。 |
| acme.report-4 | 不以单词 report 开。 |

方括号内的星号（`*`）或问号（`?`）不会被视为通配符。然而，在文件名中包含星号或问号并不是好主意；因此，你通常不会在方括号内包含它们。

如果你想将连字符（`-`）作为备选项之一，请将其放在方括号内的第一个或最后一个字符。例如：

```
rm report-[a-g-]
```

### 表 9.8：`[...]` 通配符的更多示例

| 通配符模式 | 描述 |
| :--- | :--- |
| `report[0-9]` | 匹配 report 后跟一个数字 |
| `report[0-9][0-9]` | 匹配 report 后跟两个数字 |

| 通配符模式 | 描述 |
| :--- | :--- |
| `[A-Z]*` | 匹配所有以大写字母开头的文件 |
| `report[0-9][a-zA-Z]` | 匹配 report 后跟一个数字，再跟一个大写或小写字母 |

与星号一样，括号通配符无法匹配开头的点或斜杠。

#### 在模式 `[...]` 中指定不允许的字符

如果方括号内的字符列表以感叹号（`!`）开头，则任何一个字符都会匹配该通配符，括号列表内的字符除外。例如：

不要被“至少”这个词误导。`^(*[a-z][a-z])` 选择以至少两个字母结尾的文件名。这意味着星号可以在最后两个字母之前提供更多字母。创建以至少两个字母结尾的通配符模式是最简单的情况（如所示）。创建以恰好或仅两个字母结尾的模式则更困难。

```
rm acme[!2-5x].c
```

上面的示例删除了任何以 `acme` 开头、包含一个不是 `2`、`3`、`4`、`5` 或 `x` 的字符、并紧跟 `.c` 的现有文件。

### 表 9.9：`rm acme[!2-5x].c`

会被 `rm acme[!2-5x].c` 删除的文件：
* acme1.c
* acme6.c
* acme9.c
* acmea.c
* acmeb.c

不会被 `rm acme[!2-5x].c` 删除的文件：
| 文件名 | 模式不匹配的原因 |
| :--- | :--- |
| acme.c | acme 和 .c 之间需要一个字符。 |
| acme2.c | 2 被明确禁止。 |
| acme77.c | acme 和 .c 之间只允许一个字符。 |
| acmex.c | x 被不允许的，但 X（大写）是允许的。 |
| acmeb.m | 不以 .c 结尾。 |
| f-acme9.c | 不以 acme 开头。 |



Shell 在缓冲区中处理命令行，在较旧的 UNIX 系统上，该缓冲区有几百个字符，而在较新的 UNIX 系统上，它有几千个字符或更长。如果通配符模式生成的文件列表溢出了命令行缓冲区，执行此部分命令或使用部分文件名将是危险的，因此 shell 会立即终止操作，如下例所示：

```bash
$ rm report*
rm: arg list too long
```

UNIX 的准则是“没有消息就是好消息”。来自 `rm` 命令的提示信息表示存在问题。在前面的例中，以 `report` 开头的文件名太多，导致 shell 的命令行缓冲区溢出；因此，shell 不允许命令启动。某些用户错误地认为，可能 `rm` 命令在出现错误之前已经删除了一些以 `report` 开头的文件。他们不断重复执行相同的命令，希望列表会变得越来越小，直到命令最终成功，但事实是永远不会成功。

解决此问题的一种变通方法是将一个命令拆分为多个命令，每个命令指定一组较小文件组。例如：

```bash
rm report[a-m]*
rm report[n-z]*
rm report[!a-z]*
rm report
```

本章的剩余部分将讨论不使用文件名通配符的其他文件列表用法，因此当你遇到 `arg list too long` 错误时可以使用这些方法。

### 使用反引号（`` ``` ）生成文件列表

除了文件名生成通配符外，反引号（`` ```）是另一种我们可以用于许多目的的（且不同的）机制，包括为命令生成文件列表。反引号（`` ```）是另一种单引号，更准确的名称是重音（grave accent）。

使用反引号获取 UNIX 命令或命令序列的标准输出，并将该输出作为另一个命令的一部分。这种技术被称为命令替换。例如，如果我有一个名为 `flist` 的文件，其中包含我想删除的文件列表，我可以如下所示删除所有这些文件：

```bash
rm `cat flist`
```

在键盘上找到反引号（`` ```）：它通常与波浪号（`~`）位于同一个键上。反引号（`` ```）从左上到右下倾斜，但没有反斜杠（`\`）长。不要把它与单引号（`'`）混淆，单引号是从右上到左下倾斜，或者有时完全倾斜。

#### 使用反引号生成列表

1. 输入你将用于处理列表的 UNIX 命令。（在接到指示之前不要按回车键。）可以使用任何接受文件列表的 UNIX 命令，如 `rm`、`lp`、`sort` 等。
2. 输入一个空格，然后输入一个反引号（`` ```）。
3. 输入 UNIX 命令序列，该序列将在标准输出中生成所有你想处理的文件。该序列可以是管道中的一系列 UNIX 命令。如果文件都不在当前目录下，则此命令必须为每个文件生成正确的相对路径或绝对路径。多个文件名可以通过空格分隔，或者在不同的行输出，因为反引号会将每个换行符转换为空格。
4. 输入一个反引号（`` ``` ）并按回车键执行命令。

反引号还可以解决我们无法通过通配符模式解决的问题。假设你想打印所有以 `acme` 开头或以 `.c` 结尾的文件。使用通配符模式，例如 `lp acme *.c` 会导致重复打印。我们现在可以使用反引号来解决这个问题：

```bash
lp `echo acme *.c | sort | uniq`
```

在前面的例中，`echo` 命令生成了以 `acme` 开头或以 `.c` 结尾的文件列表。然后该列表通过管道传递给 `sort`，使得重复项彼此相邻。结果再次通过管道传递给 `uniq`，`uniq` 会忽略任何与之前行相同的行，即删除了重复行。随后，反引号使该列表成为 `lp` 命令的一部分，因此打印的文件将不会有重复。

与单纯的文件名通配符相比，反引号让我们对生成的文件列表进行更细粒度的控制。以下命令用于删除所有以 `acme` 开头的文件，但以 `-sav` 结尾的 `acme` 文件除外：

```bash
rm `echo acme* | grep -v '-sav$'`
```

让我为你分析一下这个命令的各个部分。




```bash
echo acme | grep -v '-sav$'
```
将生成所有以 `acme` 开头的文件列表。它使用正则表达式语法仅显示不以 `-sav` 结尾的行；因此，`grep` 会从我们的文件列表中删除任何以 `-sav` 结尾的文件。随后，反引号会将此生成的列表提供给 `remove` 命令。

另另参阅
有关 `cat` 命令的更多信息，请参阅第 160 页。
有关 `grep` 命令和正则表达式的更多信息，请参阅第 380 页。

### 处理反引号“无空间”错误

如果反引号生成的文件列表过长，命令可能会失败并显示如下的错误信息：

```
sh: no stack space
or
ksh: no space
```

较新版本的 UNIX 似乎能够处理比早期版本长得多的反引号列表。如果使用反引号出现 `list is too long` 错误，要解决此问题，请参阅本章中关于 `xargs` 的章节。

### 使用 `xargs` 处理文件列表

到本章为止，我们一直使用通配符在命令行上生成文件列表，但如果匹配模式的文件过多，该技术可能会失败。反引号可以从 UNIX 命令的管道中生成文件列表，从而让我们对列表中的文件有更多的控制权。然而，如果生成的文件名过多（特别是在旧版系统上），反引号可能会失效。我们可以在命令行级别使用另外一种技术来处理文件列表。它提供了对列表的控制，与反引号提供的程度相同，但它对可处理的文件数量没有限制。实现所有这一切的方法就是 `xargs` 命令。当你有成千上万甚至数百万个文件需要处理时，`xargs` 能够胜任这项工作。

1. 输入 UNIX 命令或管道，该命令将在标准输出上生成你想要处理的文件列表（在接到指示前不要按回车键）。如果文件不在当前目录，列表应包含每个文件正确的相对路径或绝对路径，而不仅仅是文件名。该命令可以简单的 `cat flist`，其中 `flist` 是一个包含要处理的文件名的文件。
2. 输入管道符号 (`|`)。管道符号前后的空格可选可选。
3. 输入 `xargs`。
4. 输入一个空格，然后输入将处理该文件列表的命令。随后跟上该命令所需的任何选项。
5. 按回车键执行此序列。第 1 步输入的命令将生成文件列表。第 2 步的管道将这些文件作为输入提供给 `xargs`。`xargs` 将使用其收到的子集构建并执行第 4 步输入的命令。`xargs` 会多次调用第 4 步的命令，直到处理所有文件。不存在参数列表过长的危险，因为它不会一次性处理整个列表。

以下是一个使用 `xargs` 的示例：

```bash
cd /usr
ls gl* | xargs chmod a+r
```

在这个示例中，我们想为 `/usr` 下所有以 `gl` 开头的文件添加所有人的读取权限。首先，我们尝试使用通配符 (`gl*`)。由于匹配模式的文件过多，我们得到了 `list too long` 错误。如果你在上述步骤在使用 `xargs` 时遇到 `list too long` 错误，请将 `xargs` 改为：

```bash
xargs -n 20
```

这会强制 `xargs` 发出多次命令，其中任何一个命令从标准输入中使用最多 20 个参数。UNIX 系统上的 `xargs` 通常不需要 `-n` 选项，因为 `xargs` 会自动调整命令行上的参数数量，以确保任何命令都不会遇到 `arg list too long` 错误。





a. 一个 UNIX 命令以及可能的选项。

b. 由文件名通配符生成的生成列表。

2. 输入一个使用正则表达式通配符生成相同列表的 UNIX 命令。（在指示之前不要按回车键。）例如，如果你使用此文件名通配符：
`abc*`
你可以使用以下命令生成相同的列表：
```
ls grep '^abc'
```
（见表 9.10）

3. 输入管道符号 (`|`)，然后输入 `xargs`。
管道符号周围的空格可选可选。

4. 输入一个空格，然后输入步骤 1.a 中的 UNIX 命令和选项。

5. 按回车执行你的命令。

### 表 9.10 文件名通配符到正则表达式通配符的转换。

| 文件名通配符 | 等效正则表达式序列 | 其它 |
| :--- | :--- | :--- |
| `abc*` | `ls grep '^abc'` | 有更多关于管道的信息，请参阅第 31 页 |
| `*abc` | `ls grep 'abc$'` | 有更多关于命令行参数的信息，请参阅第 84 页 |
| `*abc*` | `ls grep 'abc'` | |
| `abc[0-9]` | `ls grep '^abc[0-9]$'` | |
| `[!A-Z]?.c` | `ls grep '^[^A-Z]\.c'` | |

### 第 10 章 按日期、大小或内容比较文件。
作者 Steve Moritsugu

按最后修改日期或最后访问日期比较、列出或查找文件

按大小比较、列出或查找文件

显示文本文件中差异的方法

比较非文本文件

比较不同系统上的文件

查找同名的相同文件

### 按修改日期比较文件

UNIX 系统包含许多文件，有时一个项目中就有成千上万个甚至更多。有了这么多文件，用户通常需要以各种方式比较文件。我们可以按日期比较，查看哪些文件修改得最近，或者哪些文件长时间未被访问。我们可以按大小比较，哪些是占用磁盘空间最大的文件。我们经常想要按内容比较，找出重复文件（浪费磁盘空间）。有时我们需要比较两个不同系统之间的文件，查看哪个系统拥有程序的最新副本，或者两个系统是否具有相同的数据。如果你将文件从一个系统传输到另一个系统，比较它们的内容以确保传输成功是非常用的。这些类型的比较是本章的主题。

#### 按修改日期比较文件 (*ls*)

只需列出当前目录下的文件，请使用 `ls` 命令（有关 `ls` 及其选项的信息，请参阅附录）。以下是 `ls` 的一些典型输出：

```
total 4 -rw-------  1 lindap  group      552 Feb  1 08:48 acme.linda
-rw-r--r--  1 samw    prog      552 Aug 13 1996 acme.sam
-rw-r--r--  1 stevem  group      420 Feb  1 09:07 report.bak
-rw-r--r--  1 stevem  group      552 Jan 31 18:48 report.sav
```

查看此输出，我们看到有两个 report 文件。但哪一个是更新呢？有两个 acme 文件，但哪一个是最近被使用过的？

要确定文件最后修改的时间，请使用此命令：
```
ls -l
```

`ls` 的 `-l` 选项使其以长格式列出，这提供了关于每个文件的更多信息（包括最后修改日期/时间）。随后你应该会看到类似下面的输出：





现在我们可以看到 `report.bak` 最后修改时间是 2 月 1 日上午 09:07。我们知道这是在上午，因为 `ls` 会将晚上 9:07 显示为 21:07。注意，它没有显示年份。这可能是指的是前一年的 2 月吗？答案是否定的，因为 `ls` 遵循以下规则：如果事件发生于一年以内，它会显示时间而不是年份；如果事件发生在一年多以前，它会显示年份而不是时间。查看 `acme.sam` 所在的行，它是一个更旧日期的示例，它显示了年份而不是最后修改时间。

在这种情况下，`ls -l` 显示 `report.bak` 包含比 `report.sav` 更新的内容，而 `acme.linda` 比 `acme.sam` 新得多。

按最后修改时间比较文件的一种非常有用的方法是将它们从旧到新（或反之）全部列出来。

```
ls -lt
```

`-t` 选项导致 `ls` 按日期/时间列出文件，而不是按字母顺序排列。你应该看到按修改日期/时间从新到旧排列的文件，如下：

```
ls -lt total 4
-rw-r--r--  1 stevem  group          420 Feb  1 09:07 report.bak
-rw-------  1 lindap  group           552 Feb  1 08:48 acme.linda
-rw-r--r--  1 stevem  group          552 Jan 31 18:48 report.sav
-rw-------  1 samw    prog            552 Aug 13 1996 acme.sam
```

如果你最近更改了几个文件并想快速找到它们，这就会很有用。

要将从旧到新的顺序反过来，请使用此命令：

```
ls -ltr
```

`-r` 选项导致 `ls` 反转其正常顺序（无论是日期/时间还是字母顺序）。字母 `l`、`t` 和 `r` 可以以任何顺序指定。你现在看到的输出如下：

```
ls -ltr total 4
-rw-------  1 samw    prog            552 Aug 13 1996 acme.sam
-rw-r--r--  1 stevem  group          552 Jan 31 18:48 report.sav
-rw-------  1 lindap  group           552 Feb  1 08:48 acme.linda
-rw-r--r--  1 stevem  group          420 Feb  1 09:07 report.bak
```

这对于寻找长时间未更改的文件可能很有用。

### 按最后访问时间比较文件 (ls)

要确定文件最后一次访问的时间，请使用此命令：

```
ls -lu
```

`ls` 的 `-u` 选项将 `-l` 长格式输出更改为显示最后访问的日期和时间，而不是最后修改时间。访问可能意味着有人查看了文件、复制了它、打印了它等，但没有修改它。你应该看到类似下方的输出：

```
ls -lu total 4
-rw-------  1 lindap  group           552 Feb  1 08:48 acme.linda
-rw-------  1 samw    prog            552 Feb  3 10:14 acme.sam
-rw-r--r--  1 stevem  group          420 Feb  2 12:21 report.bak
-rw-r--r--  1 stevem  group          552 Jan 31 18:48 report.sav
```

由于这些文件都没有指定年份，我们知道所显示的日期都都在过去一年内。

UNIX 不跟踪文件的创建日期

UNIX 为每个文件维护了第三个日期和时间：最后 inode 更改时间，可以通过向 `ls -l` 添加 `-c` 选项来显示。我曾见过关于该选项显示文件创建日的错误引用。inode（见术语表）在文件创建时会更改，当你更改其所有者、组或权限时也会更改。

和以前一样，通过从最近访问到最久未访问列出文件来比较文件访问是非常用的。添加 `-t` 选项（`ls-t`）按日期/时间列出文件，而不是按名称，即从最近访问到最久未访问。添加 `-r` 选项（`ls -ltr`）反转顺序，使最先访问的文件首先列出。当你磁盘空间不足并想要归档和清理无人使用的文件时，这可能很有用。`ls` 命令的字母可以以任何顺序指定。

有关所有 `ls` 选项的摘要，请参见第 778 页。

### 比较并查找比给定文件更新的文件 (find)




在实践中，`ls` 命令允许我们比较仅存在于一个目录中的文件。可以使用 `find` 命令（参见附录）来比较目录子树（或整个系统）中的所有文件，并列出所有比给定文件修改更晚的文件。如果我们想确保给定文件包含最新信息，这将非常有用。

`find` 命令可以在一条命令中搜索系统上的许多目录或所有目录。以下是帮助你组合所需 `find` 命令的步骤。

### 列出比给定文件修改更晚的文件

1. 输入 `find`。
2. 在接到指示前，不要按回车键。
3. 输入一个空格，然后输入你想要开始搜索的目录。`find` 也会搜索该目录的所有子目录。要搜索整个系统，请输入 `/`。
4. 输入一个空格，然后输入 `-newer`。
5. 输入一个空格，然后输入给定的文件名。完成此命令输入后，`find` 将显示所有比该给定文件修改更晚的文件。如果文件在当前目录中，只需输入其名称。如果它在当前目录之外的目录，请输入其路径。
6. 如果需要，你现在可以输入任何其他搜索准则，例如只想查看特定大小、所有者、权限的文件。参见附录中关于 `find` 的条目获取此类选项列表。
7. 输入一个空格，然后输入 `-print`。按回车键，完成你的 `find` 命令。`find` 应当显示比给定文件修改更晚的文件列表。你也可以执行更具冒险性的步骤 7，而不是此第 6 步。
8. 输入一个空格，然后输入 `-exec ls -l \;`。按回车键，完成你的 find 命令。这是完成 find 命令的替代方案（替代步骤 6）。这将为你显示与 `ls` 相同的每个文件的详细信息。你也可以输入 `-exec` 后跟一个不同的命令，以便对选定的每个文件执行其他操作。

示例 1：
```
find /usr/fred -newer reports/acme -print
```
命令中每个单词下方对应的是生成该单词的步骤步骤。此 `find` 命令将搜索 `/usr/fred` 及其所有子目录，并显示任何比给定文件修改更晚的文件路径。给定文件是当前目录下 `reports` 子目录中的 `acme` 文件。

示例 2：
```
find / -newer acme -user fred -exec ls -l {} \;
```
这是另一个 `find` 命令。它将在整个系统中搜索任何比当前目录下 `acme` 文件修改更晚的文件。它将忽略任何所有者不是 `fred` 的文件。它将对满足两个条件的文件显示详细的 `ls` 输出。

`find` 的此 `-newer` 选项适用于增量备份，即你只想备份自上次备份以来更改的文件。你的备份脚本在备份时应该修改一个虚拟文件。使用 `find` 命令找到所有自该虚拟文件以来修改过的文件。然后使用 `cpio` 备份由该 `find` 生成的所有文件名。

**另参：**
在本章中，你已经了解了如何使用 `ls` 命令按日期列出文件来比较文件，这样你就可以轻松挑选出最近访问或最少访问的文件，以及最近修改或最少修改的文件。使用 `ls` 命令无法比较多个目录中的文件。

`find` 命令可以访问整个目录子树或整个系统。`find` 可以显示所有在 `x` 天前访问或修改的文件。以下是帮助你组合所需 `find` 命令的步骤。

### 列出访问/修改时间早于/晚 x 天的文件

1. 输入 `find`。
2. 在接到指示前，不要按回车键。
3. 输入一个空格，然后输入你想要开始搜索的目录。`find` 也会搜索该目录的所有子目录。要搜索整个系统，请输入 `/`。
4. 输入一个空格，然后输入 `-atime`、`-ctime` 或 `-mtime`。
   - `atime` 检查最后访问日期/时间。




## 文件属性

- `mtime` 检查最后修改日期/时间。
- `ctime` 检查最后索引节点（inode）更改日期/时间。

4. 输入空格，然后输入加号或减号，再输入要检查的天数。
   - `-atime +90` 意味着最后访问是在 90 天以前；即在过去的 90 天内没有被过。
   - `-mtime -7` 意味着最后修改是在 7 天内。
5. 如果需要，你现在可以输入任何其他所需的搜索标准，以便只查看特定大小、所有者、权限等的文件。参见附录中关于 `find` 的条目以获取此类选项列表。
6. 输入空格，然后输入 `-print`。
   按回车，完成你的 `find` 命令。此时 `find` 将显示比给定文件修改更晚的文件列表。你也可以选择更具挑战性的第 7 步，而不是第 6 步。
7. 输入空格，然后输入 `-exec ls -l {} \;`。
   按回车，完成你的 `find` 命令。这是完成 `find` 命令的第 6 步替代方案。这将向你显示与 `ls -l` 相同的每个文件的详细信息。如果需要，你也可以输入 `-exec` 后接不同的命令，对每个选定的文件执行其他操作。参见附录中关于 `find` 的条目获取更多关于 `-exec` 的信息。

这是一个之前的 `find` 命令示例。它将搜索目录 `/usr/fred` 及其所有子目录。它将显示任何最后访问在 90 天以前的文件路径名；即在过去的 90 天内未被访问的文件。

```bash
find /usr/fred -atime +90 -print
```

这是另一个 `find` 命令。它将在整个系统中搜索任何在 7 天内修改过且由用户 `fred` 拥有的文件。它将显示任何匹配文件的详细输出。

```bash
find / -mtime -7 -user fred -exec ls -l {} \;
```

为了比较所有文件并找到哪些是最近被访问（或修改）的，在你的 `find` 命令的 `-atime`、`-mtime` 或 `-ctime` 选项中选择一个合适的数字数值是非常重要的。某些值可能会找到太多文件，因此无法准确定你正在寻找的极端文件。其他值可能过于极端，导致找不到匹配的文件。继续调整你的天数值，直到得到你想要的结果。

另另参见：有关 `find` 命令的更多信息，请参见第 770 页

按大小比较文件

就如同按日期比较文件一样，当我们按大小比较文件时，我们通常想挑选出最大的文件。我们可以使用 `ls` 命令挑选出一个目录中最大的文件。我们也可以使用 `find` 命令搜索整个目录树或整个系统，以定位最大或最小的文件。

### 确定文件大小

要确定当前目录下文件的字符数大小，请使用以下命令：`ls` 的 `-l` 选项会产生类似下面的详细输出：

```
total 3
-rw-r--r-- 1 users 17157 Feb 1 11:31 report02
-rw-r--r-- 1 users 19728 Feb 1 11:31 report04
-rw-r--r-- 1 users 196484 Feb 1 11:33 report07
```

在前面的示例中，`report07` 是最大的文件，有 196,484 个字符。

### 按大小列出文件

按大小比较一组文件的最佳方法之一是使用 `ls` 并将其输出通过到 `sort` 命令。在文件按大小排序列出后，比较它们并快速确定最大或最小的文件要容易得多。

```bash
ls -l | sort -bn +4
```

`|` 符号使用管道（见术语表）获取 `ls -l` 的输出并使用 `sort` 命令（见附录）对其处理。这里使用的 `sort` 选项有：
- `+4`: 忽略前四个字段，因此按大小进行排序。
- `-b`: 批量排序（Batch sort）。
- `-n`: 数值排序。





-   按数字排序，而非字母排序
-   `-b`
-   忽略大小前面的领先空格

我们将看到类似如下的输出：
```
total 3 -rw-r--r--  1 mori      users           1972 Feb  1 11:31 report04
-rw-r--r--  1 mori      users           17157 Feb  1 11:31 report02
-rw-r--r--  1 mori      users         196484 Feb  1 11:33 report07
```

要按从大到小的顺序列出文件，请使用此命令：
```bash
ls -l | sort -bnr +4
```
为 `sort` 添加 `-r` 选项会反转顺序，因此文件将按从大到小列出。

**另参**
*有关管道的更多信息，请参阅第 26 页*
*有关 `sort` 命令的更多信息，请参阅第 202 页*

### 按大小查找文件

你也可以使用 `find` 命令来列出所有大于或小于给定块大小的文件。`find` 会在一个命令中搜索系统上的许多或所有目录。以下是帮助你编写所需的 `find` 命令的步骤。

#### 列出大于或小于给定大小的文件

1. 输入 `find`。
2. 在接到指示前不要按回车键。
3. 输入一个空格，然后输入你想要开始的目录。`find` 也会搜索该目录的子目录。要搜索整个系统，请输入 `/`。
4. 输入 `-size`。
5. 输入 `+number` 或 `-number`。`+600` 表示文件大于 600 块。`-200` 表示文件小于 200 块。大多数系统假设每个块为 512 字节（即字符），但某些系统每个块使用 1024 字节。检查你系统上 `find` 的帮助页，查看 `-size` 选项每个块使用多少字节。

为了帮助你将 MB（兆字节）转换为块，这里有两个粗略的经验法则：
- 2000 个 512 字节的块 = 1MB（约）
- 1000 个 1024 字节的块 = 1MB（约）

例如，要查找约 10MB 或更大的文件，我会指定 `+20000` 个 512 字节块或 `+10000` 个 1024 字节块。

5. 如果需要，你现在可以输入任何其他搜索标准，以便只查看特定大小、所有者、权限等的文件。查看附录中关于 `find` 的条目获取此类选项列表。
6. 输入 `-print`。
按回车键，完成你的 `find` 命令。你也可以采取更具冒险性的第 7 步代替第 6 步：
7. 输入 `-exec ls -l {} \;`。这是第 6 步的替代。你也可以使用 `-exec` 后接不同的命令对每个文件执行某些操作。这将显示 `ls -l` 显示的输出。（第 26 页）查看 `find` 条目以获取有关 `-exec` 的更多信息。这里是另一个示例：
```bash
find /usr/bin -size +600 -print
```
这将在 `/usr/bin` 中搜索大于 600 块的文件并显示其路径。
```bash
find / -size -200 -group acct -exec ls -l {} \;
```
这将在系统中搜索小于 200 块且同样属于 `acct` 组的文件，并产生与 `ls -l` 显示相同的输出。





# 显示两个文件的差异 (*diff*)

要显示两个文本文件之间的差异，请使用此命令：

```bash
diff file1 file2
```

你应该看到类似下面的输出：

```
287c287
<          Now is the time for all good men to come to the ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)aid of
>          Now is the time for all good men to go to the aid
```

由于在这个示例中 `diff` 的输出很少，这意味着这两个文件非常相似。`diff` 输出大量内容则说明文件之间差异很大。如果在下一个 shell 提示符出现之前没有任何输出，则说明两个文件是完全相同的。

在 `diff` 找到两个文件之间的任何差异后，它会向前查看两个文件，尝试寻找一个文件中的后续行是否匹配另一个文件的后续行。通过这种方式，它可以识别新增的行、删除的行和修改的行。以 `<` 符号开头的行来自第一个文件。`>` 符号表示第二个文件中不同的行。系统只显示不同的行。上面的示例显示，两个文件之间的唯一区别是第一个文件中的单词 *come* 在第二个文件中被改为 *go*。

在前面的输出中，`287c287` 表示将第一个文件转换为第二个文件的指令。在这种情况下，`c` 表示第一个文件的第 287 行必须更改以匹配第二个文件的第 287 行。其他可能的指令是 `a`（添加行）和 `d`（删除行）。在实践中，大多数 UNIX 用户会查看显示的行差异，并忽略除行号信息以外的指令。

使用 `diff` 的 `-b` 选项可以使其忽略行末尾的空格和制表符。它会将任何连续的空格和制表符视为一个空格。如果你想比较两个文件，但想忽略其中一个文件的左侧（即空格更多）比另一个文件大的事实，这就会非常有用。

# 并排显示差异 (*sdiff*)

要并排显示两个文件之间的差异，请使用此命令：

```bash
sdiff file1 file2
```

你应该看到类似下面的输出：

```
report02          report07          report05
report09          <
report04          report03          report03 >report01
```

左列显示第一个文件的行。右侧列显示第二个文件的行。`<` 符号显示出现在第一个文件但不在第二个文件中的行。`>` 符号显示出现在第二个文件但不在第一个文件的行。`|` 符号显示两个文件之间不同的行。`sdiff` 适用于比较短单词列表或文件名列表，但对于较长的行，可能非常难以阅读。

# 显示三个文件之间的差异 (*diff3*)

要显示三个文件之间的差异，请使用此命令：

```bash
diff3 file1 file2 file3
```

这里显示了三个文件的内容：

表 10.1 三个文件的内容

| file1 | file2 | file3 |
| :--- | :--- | :--- |
| green | green | yellow |
| blue | blue | blue |
| red | red | green |
| yellow | yellow | brown |
| blue | blue | tan |
| green | green | red |
| brown | brown | orange |
| pink | azure | black |
| red | red | gray |
| orange | orange | |
| black | black | |
| gray | gray | |

该命令将产生如下输出：

```
====3 1:1,3c
2:1,3c
  green
  blue
  red
3:0a
====
1:8c
  pink
2:8c
  azure
3:5c
  tan
```

`====` 分隔在三个文件中找到的每个差异部分。`====n` 表示文件 *n* 与其他两个文件不同。`====` 表示三个文件在这一部分都不同。以下是对上述 `diff3` 输出的注释：

====3 表示文件 3 与另外两个文件不同，如下 ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)：

1:1,3c 表示文件 1 的第 1 至 3 行的内容与以下文件相同：

2:1,3c 表示文件 2 的第 1 至 3 行包含这 3 行




如下所示的行：
green
blue
red

`3:0a` 意味着文件 `3` 必须在第 `0` 行之后添加上述 3 行，才能与另外两个文件相同。

`====` 意味着三个文件在接下来的区域均不同：

`1:8c` 意味着文件 `1` 的第 `8` 行包含：pink
`2:8c` 而文件 `2` 的第 `8` 行包含：azure
`3:5c` 而文件 `3` 的第 `5` 行包含：tan

# 在排序后的文本文件中查找共同和唯一的行 (*comm*)

如果两个文本文件按排序（即按字母顺序）排列，`comm` 命令可以轻松地显示两个文件中共同的以及唯一的行。要执行此操作，请输入以下命令：

```bash
comm file1 file2
```

你应该看到类似下面的输出：

```
report21 report23
report29 report33 report34
report35 report91
```

最左侧列显示第一个文件特有的行；因此，`report23`、`report34` 和 `report91` 只存在于第一个文件。中间列显示第二个文件特有的行；所以 `report29` 和 `report37` 只存在于第二个文件。第三列显示两个文件共同的行。在这种情况下，`report21`、`report33` 和 `report35` 存在于两个文件中。

我们可以为 `comm` 添加选项来抑制一或多列，如下：

```bash
comm -1 file1 file2 # 抑制第 1 列，因此显示第 2 和 3 列
comm -23 file1 file2 # 仅显示文件 1 特有的行
comm -13 file1 file2 # 仅显示文件 2 特有的行
comm -2 file1 file2 # 仅显示共同行
```

记住，文件必须处于排序状态 `comm` 才能工作。如果你有两个未排序的文件需要比较，可以使用 `sort` 命令（见附录）创建这些文件的排序版本，然后在排序后的版本上使用 `comm` 命令。

如果开头有制表符，请不要使用 `comm`。`comm` 使用一个制表符来开始中间列的行，使用两个制表符来开始右列的行。如果你的文件以一个或多个制表符开头，`comm` 的输出将是不正确的。

# 通过内容比较任意类型 (*cmp*)

要比较任何类型的文件（即使它们不是文本文件），请使用此命令：

```bash
cmp file1 file2
```

你应该看到类似下面的输出：

```
file1 file2 differ: char 26, line 3
```

如果 `cmp` 在没有显示任何消息的情况下返回到 shell 提示符，则文件是完全相同的。`cmp` 在找到第一个差异后停止，因此它不会告诉你是两个文件有多相似。使用 `cmp` 的 `-l` 选项列出两个文件之间所有的差异。

# cmp 对比 diff

如果你只想知道两个文件是否相同，`cmp` 比 `diff` 更快，因为它在发现第一个差异时就会停止。`cmp` 适用于所有类型的文件；`diff` 仅处理文本文件。然而，`diff` 会显示实际差异。`cmp` 不尝试输出差异。在二进制文件上使用 `diff` 可能会让屏幕处于未知状态。

# 比较不同系统上的文件

如果你将文件传输到另一个系统，你可能想验证文件是否完整到达。`diff`、`sdiff` 和 `cmp` 只能比较相同系统上的文件。要比较存在于不同系统的两个文件，请在系统上运行此命令：

```bash
sum -r filename
```

你应该看到类似下面的输出：

```
35424 14 filename
```




`sum` 命令会对文件的完整内容计算校验和（参见术语表）。在前面的输出中，35424 是该文件的校验和。14 是以块（blocks）为单位的大小。如果两个文件的校验和不匹配，则这两个文件不相同。如果校验和相同，则这两个文件相同的概率极高。校验和算法（即计算方法）在几乎所有类型的 UNIX 系统上都是相同的，允许即使 UNIX 系统类型不同，也可以比较远程文件。

### 概率有多大？

`sum` 产生的校验和范围最高可达约 65,000。通常情况下，如果两个文件的校验和相同，那么它们内容仍然不同的概率只有 65,000 分之一。

请注意，`sum` 报告的块大小在两种不同类型的 UNIX 系统之间可能存在两倍差异。这是因为某些 UNIX 系统使用每块 512 字节来计算文件大小，而另一些系统则使用每块 1024 字节。例如，SunOS Version 4（基于 BSD）使用每块 1024 字节，而使用 SunOS Version 5（基于 System V）的 Solaris 2.x 则使用每块 512 字节。请注意，`sum` 命令使用的字节块大小可能与在向文件添加额外块时使用的内部逻辑块大小不同。

`sum` 的 `-r` 选项使其使用更好的（循环的）校验和计算方法，该方法能够更好地检测文件顺序及内容上的差异。如果你想额外确认两个文件是否相同，可以利用这两种不同的计算方法，如下：

### 采取额外步骤以确保文件相同

1. 在第一个系统上，执行以下操作：
```
sum filename sum -r filename
```
2. 在第二个系统上，执行相同的操作：
```
sum -r filename sum -r filename
```
3. 检查两个 `sum` 计算的结果是否相同。检查 `sum-r` 计算的结果是否相同。注意，`sum` 的结果不应与 `sum -r` 的结果匹配。
4. 如果两种类型的校验和都匹配，则文件是相同的（概率极高）。虽然存在极小的概率两个文件不同但仍产生相同的校验和，但两个不同的文件同时符合这两种方法的可能性极低。

### 寻找不同名称下的相同文件

要快速确定目录中哪些文件是相同的，请使用此命令：
```
sum -r *
```
你应该看到类似下面的输出：
```
22792 192 acme.980201
6948 21 report02
14252 15 report04
22792 192 report05
```
如果输出超出了屏幕，请重新运行命令并将输出通过到 `less`。在前面的示例中，`acme.980201` 和 `report05` 具有相同的校验和块大小。因此，它们极可能是相同的。如果我们需要 100% 确定，可以在这两个文件上使用 `diff` 或 `cmp`。`report02` 和 `report04` 的校验和与其他文件不同，因此无法与它们或相互匹配。你可以使用 `*` 以外的通配符来生成需要校验和的文件列表。

**另请参**
*有关如何使用通配符创建文件列表的更多信息，请参第 232 页*




# 关注危险的 SUID、SGID 权限

## 登录安全 - 第 274 页

当你想要登录 UNIX 系统时，系统会提示你输入登录名和密码。登录名是你在该 UNIX 系统上的唯一标识。密码是你账户的密钥，如果经过仔细选择，它就能保证除 `root` 之外的任何人都无法访问你的个人文件。。

### 更改你的登录名

系统管理员可以更改你的登录名，但正如前文所述，这并不被建议。

你可以自己更改密码，但你的登录名将永远不变。如果你更改了登录名，你的电子邮件地址也会随之改变，人们将不知道如何在计算机上联系你。你可以将登录名看作你的个人姓名，而将密码看作你家里的钥匙。

### 无效登录后的延迟

如果你输错了密码，会收到一条信息显示登录无效。在几秒钟延迟之后，计算机会再次要求你输入登录名和密码。

设置这种延迟是为了防止有人反复尝试使用不同的密码登录你的账户。有了延迟，一个程序每小时只能尝试大约 500 种不同的密码。如果没有这种延迟，这样的程序每小时可能会尝试超过一千次密码。

### 次级密码 - 第 275 页

在某些系统中，当你想要使用调制解调器、传真机或其他设备时可能会遇到密码。当你想要启动受许可并因此限制的程序时，也可能遇到密码。

对设备设置密码的原因可能是为了将设备限制给特定的人群。例如，可以将调制解调器的使用限制仅限于大学员工，而不是学生用户。

这种限制可以通过在设备所在的组中设置组来实现。这样，只有该组的成员才对设备具有读写写/执行权限。与组方案相比，设备上的密码限制有一个主要优势：即，即使有人猜中了你的登录密码，他在使用该设备之前，仍然必须猜中该设备的密码。此条的教训是：不要将你的登录密码作为次级密码的相同密码。如果你这样做，安全性将会受到破坏。

### 密码老化 - 第 276 页

在某些系统中，你的密码有效期有一个最长时间，到期后系统会要求你更改。这种设计旨在提高系统的安全级别，主要通过两种方式实现：

当你定期更改密码时，别人可能（从你肩后）获知你密码的机会就会减少。某人可能需要多次尝试才能窃取完整的密码，因此定期更改减少了密码被完全窃取的概率。

如果有人获取了你密码的加密版本（加密密码的描述将在本章稍后的部分出现），他可能会通过对单词进行加密并将加密结果与你密码的加密版本进行比较，从而系统地尝试破解你的密码。每个密码的使用时间越短，别人通过这种方式破解你密码的机会就越小。

除了限制密码的最长有效期外，某些系统还限制了密码的最短有效时间。这是为了确保你不会有一个一直坚持要使用的偏好密码。这可以防止你在系统提示更改密码时使用一个虚假密码，然后迅速切换回你喜爱的密码。

只要按照下一节描述的方法妥善使用密码，在系统每次要求你更改密码时，选择一个新密码应该并不困难。妥善使用密码可以增加安全性，确保其他人无法访问你的个人文件、电子邮件账户等。

### 更改你的密码

你想要更改密码的原因有以下几个：

* 因为你怀疑有人猜中了你的密码，或者目睹了你输入密码
* 因为系统要求你定期更改密码
* 因为提供给你的初始密码难以记忆，或者系统要求在首次登录时必须更改密码




# 密码安全

从技术上讲，三到七个字母的密码也是合法的，但黑客可能会优先尝试这些密码。如果他们拥有你密码的加密版本，只需要几个小时到几天就能猜出这些密码。

- 选择一个至少八个字符的密码（只有前八个字符有效，但如果你觉得更多字符更容易记忆，欢迎使用八个以上的字符）。
- 使用小写字母和大写字母。
- 使用键盘上非字母的字符。例如，数字或某些特殊字符（如美元符号、引号或小于号）都是密码的良好补充。
- 选择一个不在字典、书籍或任何可能通过电子方式获取的文本中的密码。
- 选择易记密码有几条良好的规则：取一首诗、格言或歌曲中每个单词的首字母，并将其中一些字母大写（可能在中间某包含一个非字母）。例如，使用“There is more to love than meets girl”这个短语，它可以为你生成密码 `TimTbmg`（注意这个密码长度为九位，所以最后的 `g` 可以省略，但包含它可能会更容易记忆）。
- 选择两个相互相关的单词并用非字母将它们结合。例如，`dog` 和 `capital`，可能会生成密码 `cApI`、`dOg=capi` 或 `dogcapital`。如果你选择两个对你来说有某种联系（但其他人不知道）的单词，可能会更容易。使用上一个例子，你可能在访问完首府的某人后的周末买了一只狗！

选择好好密码后，是时候真正更改你的登录密码了。根据你的系统，你应该使用 `ypasswd`、`nispasswd` 或 `passwd`。如果你不知道应该用哪一个，请先尝试 `ypasswd` 和 `nispasswd`；如果这两个命令的结果都未找到，请尝试 `passwd`。

当你调用适当的命令后，系统会要求你输入旧密码。（通过先要求旧密码，即使别人发现了你忘记注销的终端，也无法更改你的密码。）接下来，系统会要求你输入新密码。最后，系统会要求你重新输入新密码，以确保你没有输入错误。

## 谁能看到你的密码？

为了完全理解你的密码有多秘密（或多不秘密），你需要了解密码机制的工作原理。当你选择一个新密码时，它会被加密为一个文本字符串并保存在系统上。无法进行逆运算——也就是说，给定一个加密的密码，你无法找到未加密的版本（技术上讲，这是可能的，但概率极低。这种过程即使在最快的计算机上也可能需要数千年）。当你想要登录系统时，未加密的密码（即你登录时输入的密码）将与计算出的加密版本进行匹配。

在旧的 UNIX 系统中，加密后的密码位于 `/etc/passwd` 文件，而每个人都可以读取该文件。这产生了一个潜在的安全漏洞；访问系统的用户可以使用前面描述的方法破解其他用户的密码。后来开发了一种许多系统今天仍在使用的新方法，被称为“影子密码”（shadow passwords）。其核心思想是将加密密码从 `/etc/passwd` 文件中移除，并将其隐藏在一个仅供 root 和登录程序（即 SUID root 程序）可读取的文件中。要检查你的系统是否使用影子密码，可以查看 `/etc/passwd` 文件。如果第二个字段包含 13 个字母（看起来是随机的），那么它就不是（这 13 个字母实际上是你的加密密码）。

## 允许用户成为另一个用户或 root (su)

有时，你想访问另一个用户的文件或以另一个用户的身份运行程序。一种方法是……





实现这一点的方法是注销并让用户在你的终端上登录。然而，有一种更简单的方法！使用 `su`（切换用户）命令，你可以将 shell 所有者更改另一个用户。

输入 `suusername` 会将 shell 的所有者更改为用户 `username`。如果你不提供用户名，将切换到 root。在输入 `su` 命令后，你自然需要提供指定用户的密码。

当你使用 `su` 更改 shell 的所有权时，shell 仍然知道原始用户是谁（由于环境变量的原因）。这有时可能是一个理想的效果，有时则不是。如果你希望在在使用 `su` 时重置所有环境变量，你应该提供一个连字符作为参数，即 `su -username`。

# 系统组规划

UNIX 系统上的每个文件恰恰属于一个用户和一个组。这种所有权决定了谁可以读取和编辑该文件，如果该文件是执行文件，则谁可以执行它。目录具有类似的权限，你稍后会看到。

通过使用带有适当选项的 `ls` 命令可以看到所有权信息：

```
ls -ldg security.html -rw-r--r--  1 blackie users      12383 Mar 15 10:27
```
![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)security.html

在第一列中，你可以看到文件的权限；在第三列中，你可以看到文件的所有者（blackie 就是我）；在第四列中，你可以看到文件所属的组。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 查找文件名

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

第二列是给定文件的数字。如果这是一个普通文件，则它是该文件的硬链接数。对于目录，这个数字是二 加上子目录的数量；每个子目录都通过 `..` 链接到该目录，而它所在的目录则以目录名对其进行引用。

如果几个人需要处理一组文件，他们并不需要以同一个用户的身份登录。相反，应该创建一个组，并将文件集放在该组中并赋予适当的权限。例如，你需要为用户和组设置读取和写操作权限。组不能由普通用户维护，但必须由超级用户（`root`）管理。作为普通用户，你可能同时处于多个组中。要查看你所在的组，请输入 `groups`。

### 理解文件和目录权限

在以下章节中，我们将使用 `file` 一词泛指文件和目录，使用 `plain file` 指代文件（不是目录）。在上节中，你看到 `ls` 可以告诉你关于文件的权限信息：

```
ls -ldg security.html -rw-rr  1 blackie users      12383 Mar 15 10:27
```
![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)security.html

这些权限信息分为四组。![![227-0280a.gif](img/910f4379734630b0f5124fbc70f719a.gif) 图 1。第一个字符表示文件类型：

- `d` 表示目录
- `-` 表示普通文件
- `s` 表示符号链接
- `b` 表示块特殊设备
- `c` 表示字符特殊设备

最后两种类型通常在 `/dev` 目录中看到。接下来是三个三个字母组成的块。第一个块控制文件所有者的权限，第二个块控制与文件同组的人员的权限，第三个块控制其他人（即既不是文件所有者也不是文件所在组的人）的权限。

在这三个块中，用连字符代替字母表示该位置本可能出现的字母缺失。这确保了 `ls` 的输出始终具有相同的宽度，并且第四位置的字母始终保持不变。三个块中每个块的第一个字母可能是字母 `r`，它表示文件的读取权限。普通文件（即不是目录）的读取权限意味着该块描述的人员可以读取该文件。





目录的读取权限表示目录的内容可以被列出——也就是说，有人可以看到目录中包含哪些文件。这并不意味着文件的内容可以被读取，或者文件的属性可以被列出。

三个块中的每个块的第二个字母可以是字母 `w`，表示写权限。对于普通文件，这表示该文件可以被编辑。对于目录，这意味着可以在目录中创建新文件。

每个组的第三个字母表示执行权限。如果它是字母 `x`，则具有以下含义：对于普通文件，该文件是一个程序，可以通过在命令行输入其名称来执行。对于目录，你可以访问其内容——也就是说，当开启 `x` 权限时，你可以执行以下操作：

- 你可以读取文件内容（如果文件允许读取）。
- 你可以进入子目录（使用 `cd`），前提是该子目录允许这样做。
- 你可以获取关于目录内容的信息（例如文件权限、创建日期和大小）。

第三个字母也可能指代其他内容，见下表。

### 表 11. 执行位的附加选项

| 类型 | 用户 | 组 | 其他 |
| :--- | :--- | :--- | :--- |
| **文件** | `s`: 1) 文件对用户有 `x` 权限。2) 该文件是一个 SUID 程序。 | `S`: 1) 文件对用户没有 `x` 权限。2) 该文件是一个 SUID 程序。 | `s`: 1) 文件对组有 `x` 权限。2) 该文件是一个 SGID 程序。 | `S`: 1) 文件对组没有 `x` 权限。2) 该文件是一个 SGID 程序。 |
| **目录** | `s`: 1) 目录对组有 `x` 权限。2) 在此目录中创建的新文件，其组所有权将设置为目录（而不是用户的默认组）。 | `S`: 1) 目录对组没有 `x` 权限。2) 在此目录中创建的新文件，其组所有权将设置为目录（即不是用户的默认组）。 | `t`: 1) 目录对其他人有 `x` 权限。2) 其他人可以在目录中创建新文件，但不能删除他人的文件。 | `T`: 1) 目录对其他人没有 `x` 权限。2) 其他人可以在目录中创建新文件，但不能删除他人的文件。 |

### SUID/SGID 程序

正如你之前通过 `su` 命令所看到的，你可以将 shell 的身份更改为另一个用户。然而，这要求你知道另一个用户的密码，除非你已经是 root 用户。在某些特定情况下，这种限制是不可接受的，如下例所示。

名为 `/etc/passwd` 的密码文件仅允许 root 写（也就是说只有 root 可以编辑此文件）。当你想要更改密码时，必须更改此文件的内容。这是通过 `passwd` 程序实现的，它是一个 SUID 程序（设置用户 ID）。当该程序被执行时，进程的身份会从你变为 root。这种身份转变发生时不会你询问密码。`passwd` 程序是通过 `chmod` 程序被设置为 SUID 程序的。同样，一个程序也可以在执行时切换用户组。这样的程序被称为 SGID 程序。

### 粘滞位保护你的文件

对目录具有写权限的用户对该目录拥有有效的管理控制权。除了创建文件外，这些用户还可以删除和重命名其他用户的文件，即使他们没有修改这些文件。

这可能会产生一个问题，例如如果你是大学的一位老师，想创建一个让学生存放作业的目录。问题在于，如果你给了学生了该目录的写权限，他们也将获得该目录的管理控制权，从而拥有删除其他学生作业的能力！

解决这个问题的办法是在目录上设置粘滞位（sticky bit）。这赋予了学生对目录的写权限，但没有赋予他们管理控制权。在这种情况下，你按照如下方式设置权限：

```
chmod u=rwx,og=wxt directory
```

这提供了 `drwx-wx-wt` 权限。我特意去除了组和其他人的读取权限。这样一来，学生就无法看到目录中的文件，从而无法知道是谁提交了作业。





当你为特定作业设置好小组后，为该作业的文件应以该小组的组身份创建。这可以通过三种方式实现：

1. 你可以创建文件并在稍后使用 `chgrp` 命令更改它们的组身份。
2. 你可以更改新创建的文件所所属的默认组。这可以通过 `newgrp` 命令完成，但它只在你调用 `newgrp` 命令的 shell 中生效。要通过这种方式更改用户组，只需调用命令 `newgrp group` 即可。
3. 你可以在目录上设置 SGID 位。通过这种方法，在该目录中创建的新文件将具有与目录相同的组身份；因此，它们不会共享创建者的组身份。若要为目录设置 SGID 位，请输入 `chmod g+s directory`。

### 目录的读取和执行权限

许多人对目录的读取权限和执行权限的使用感到困惑。让我们仔细观察以下四种情况。

### 没有读取权限且没有执行权限
在这种情况下，该目录是关闭的。

### 具有读取权限和执行权限
在这种情况下，该目录允许列出文件内容、列出目录内容以及访问子目录（如果子目录允许此类）。

### 具有读取权限但没有执行权限
这是一个很少发生的奇特情况。用户可以看到文件名，但无法访问它们、获取其属性信息，也无法进入子目录。

### 没有读取权限但具有执行权限
在这种情况下，用户可能无法列出目录内容，但如果他们知道文件名，则可以访问文件。这在你的主目录上设置这种权限非常方便。例如，通过这种权限，人们最终可能会进入目录并看到你的 .emacs 文件（如果该文件具有权限），但他们可能看不到你拥有的其他文件。换句话之，用户只能看到你告诉他们你拥有且他们有权限查看的文件。

# 修改权限/所有者/用户组

可以使用 `chmod` 命令更改文件和目录的权限。该命令既可以使用数字参数（精确说明权限应该是什么），也可以使用符号参数（可以只更改部分权限，例如仅更改用户的权限）。

只有拥有给定文件所有者的用户才能更改该文件的权限。（当然了，该规则的例外是超级用户，他可以做任何事情！）

`chmod` 程序通过使用 `-R` 选项（R 代表递归）更改层级结构中所有文件的权限。

### 使用数字模式设置权限 (chmod)

`chmod` 命令使用数字来更改文件和目录的权限。这是设置权限的一种非常方便（且快速）的方法。其思想是用四个数字来描述权限，其中每个数字描述一个组：

1. SUID、SGID 和粘滞位 (sticky bit)
2. 文件所有者的权限
3. 组的权限
4. 其他人的权限

在每个组中，每个选项都关联着一个数字。组的值是权限和。第一组中的可用选项包括：
1. 目录粘滞位
2. SGID 位
3. SUID 位

因此，如果你想让文件具有 SUID 和 SGID，你应该使用数字 6（即 2+4）。如果你不想选择这三个选项中的任何一个，则应该使用 0。

三个权限块中的每个块的可用选项包括：
1. 执行权限
2. 写入权限
3. 读取权限

因此，如果你想为名为 `myfile` 的文件赋予用户读写权限，而仅赋予组和其他人读取权限，你应该执行以下命令：





```bash
chmod 0644 myfile.
```

前导零可以省略，因此以下命令与之前的命令相等：

```bash
chmod 644 myfile.
```

表 11.2 和 11.3 显示了给定选项的数值表示。

### 表 11.2 SUID、SGID 和粘滞位（Sticky bits）。

| 数值 | 描述 |
| :--- | :--- |
| 0 | -SUID -SGID -Sticky bit |
| 1 | -SUID -SGID +Sticky bit |
| 2 | -SUID +SGID -Sticky bit |
| 3 | -SUID +SGID +Sticky bit |
| 4 | +SUID -SGID -Sticky bit |
| 5 | +SUID -SGID +Sticky bit |
| 6 | +SUID +SGID -Sticky bit |
| 7 | +SUID +SGID +Sticky bit |

### 表 11.3 `chmod` 命令的权限数值表示。

| 数值 | 描述 |
| :--- | :--- |
| 0 | -r -w -x |
| 1 | -r -w +x |
| 2 | -r +w -x |
| 3 | -r +w +x |
| 4 | +r -w -x |
| 5 | +r -w +x |
| 6 | +r +w -x |
| 7 | +r +w +x |

## 使用符号模式 (`chmod`) 设置权限

在上一节中，你已经了解了如何使用数值模式设置文件权限。这种方式的主要缺点是，无法在不改变当前模式的情况下，一次性为所有文件和目录添加写权限。

使用符号模式，你可以仅修改文件和目录的部分权限。

符号模式的语法如下：`<who><operator><permission>`

- `<who>` 是字符 `u`、`g`、`o` 中的零或多个：
  - `u`: 用户
  - `g`: 组
  - `o`: 其他
  - `a`: 所有权限（用户、组和其他人）
  如果省略了 `<who>`，则默认为 `a`，但会考虑文件创建掩码的值（参见下一节关于文件创建掩码 `umask`）。
- `<operator>` 为 `+`、`-` 或 `=`。该选择表示：
  - `+`: 添加权限
  - `-`: 移除权限
  - `=`: 为 `<who>` 指定组设置绝对权限
- `<permission>` 是 `r`、`w`、`x`、`s`、`t`、`u`、`g` 和 `o` 之一：
  - `r`: 读取权限
  - `w`: 写权限
  - `x`: 执行权限
  - `X`: 如果文件是目录或该文件具有执行权限，则赋予执行权限
  - `s`: 当 `<who>` 为 `u` 时为 SUID，当 `<who>` 为 `g` 时为 SGID
  - `t`: 当 `<who>` 为 `o` 时为粘滞位

`u`、`g`、`o` 分别表示权限来自用户、组或其他。可以通过逗号重复 `<who>`、`<operator>` 或 `<permission>` 来同时更改多个权限。

### 示例

- 为名为 `myfile` 的文件为组和其他人添加读取权限：
```bash
chmod go+r myfile
```
- 为给定目录下的所有文件为组和其他人添加读取权限：
```bash
chmod go+r *
```
- 为给定目录及其子目录下的所有文件和目录为组和其他人添加读取权限：
```bash
chmod -R go+r *
```
- 让用户仅在知道他们想要访问的文件名时，才能访问你家主目录中的文件：
```bash
chmod go=r /home/user/
```




为了稍微放宽限制，让用户组能够看到你拥有的文件，但对其他人隐藏此选项，请输入此行：

```bash
chmod g=rx,o=r /home/user/
```

要让给定目录下的所有文件和目录对用户组开放权限，请输入此行：

```bash
chmod g+rX *
```

这将产生以下效果：
- 对所有文件和目录将添加读取权限。
- 对所有目录将添加执行权限。
- 对已经具有用户、用户组或其他用户执行权限的文件将添加执行权限。

# 修改文件的所属组 (chgrp)

使用 `chgrp` 命令，你可以更改文件、目录或整个目录层次结构的所属组。语法如下：

```bash
chgrp <group> <file> - 更改单个文件或目录的组
chgrp -R <group> <file> - 更改目录及其所有子目录的组
```

你必须是你想要更改的文件的所属组的成员。要查看你所属的组，请使用 `groups` 命令。

# 修改文件的所有者 (chown)

在上一节中，我们学习了如何更改文件的权限和组，但文件可以更改所有者吗？这个问题的答案是既肯定又否定！是的，你可以使用 `chown` 命令更改文件的所有者；但不，普通用户（即不是 root 用户）不能这么做！

如果你真的想把一个文件交给别人，你有两种可能：
- 将其作为附件通过邮件发送给他。
- 赋予文件读取权限（仅持续几秒钟），让对方复制文件，然后删除你的副本。

# 设置新文件的默认权限 (umask)

通过 `umask` 命令，你可以为新文件的权限设置一个模式。`umask` 是一个类似于数值型 `chmod` 使用的数字，由三位 0 到 7 之间的数字组成。设置该数字的原因是技术性的，因此在此不再描述。唯一需要理解的是，当创建新文件时，它们将具有由 `umask` 描述的权限。在表 11.4 中，你可以看到特定数字描述的权限。

表 11.4 umask 命令的数字示图。

| 值 | 描述 |
| :--- | :--- |
| 7 | -r -w -x |
| 6 | -r -w +x |
| 5 | -r +w -x |
| 4 | -r +w +x |
| 3 | -r -w -x |
| 2 | +r -w +x |
| 1 | +r -w -x |
| 0 | -r +w +x |

因此，为了赋予用户对新文件的完全访问权限 (rwx)，并赋予用户组和其他仅读取权限，你应该使用命令 `umask 044`。如果你使用 `umask 033`，创建的普通文件将赋予用户读写权限，并赋予其他人读取权限。

# 监控危险的 SUID、SGID 权限

SUID 和 SGID 文件是危险的，因为它们可能会赋予未经授权的用户 root 权限，至少是以另一个用户的身份运行程序的权限。SUID 程序对黑客来说非常方便，因为它们为 root 账户创建一个后门，即使 root 将密码更改为黑客不知道的密码，该后门仍然可用。

然而，存在一种简单的方法可以验证自上次检查以来系统上没有出现新的 SUID 程序，即使用命令 `crontab`、`find` 和 `diff`。要使用这种策略，你必须拥有支持 `-perm` 选项 `find` 程序。如果你的版本不支持，你可以从 gnu 存档中下载（URL: `http://www.gnu.org/order/ftp.html`）。



通过 `find / -perm ++s` 命令，你可以递归遍历整个文件系统，并搜索具有 SUID 或 SGID 权限的文件。列表 11.1 中的脚本就执行了此操作，并将输出保存到名为 `suid.info` 的文件中。使用 `diff` 将此文件与上一次运行的文件进行比较，从而只输出新的 SUID/SGID 程序（或已消失的 SUID/SGID 程序）。

### 列表 11.1 用于搜索新 SUID/SGID 程序的程序

```sh
#!/bin/sh
test -e suid.info && mv suid.info suid.info.old
test ! -e suid.info.old && touch suid.info.old
find / -perm ++s suid.info
diff suid.info suid.info.old
```

你对该程序需要的一个更改是为它提供一个你想要保存 `suid.info` 文件的完整路径。如果你将这个小程序设置为每天执行一次的 `cron` 任务，你就设置了一个用于检查新 SUID/SGID 文件的系统。只有当出现新的 SUID/SGID 程序时，你才会收到 `cron` 任务产生的邮件，否则它不会输出任何内容。

## SUID/SGID 文件，挂载文件系统时

在某些 UNIX 变体中，`mount` 命令支持 `nosuid` 选项。这意味着使用此选项挂载的文件系统不会赋予 SUID/SGID 程序特殊含义（即它们将不会成为 SUID/SGID 文件）。如果没有此选项，挂载的文件系统可能会带来问题，如下例所示。

假设你是大学校园内某研究所 UNIX 系统的系统管理员。某一天，另一个研究所的系统管理员问你，你是否方便帮忙挂载他 UNIX 系统上的一个文件系统，以便你们的共同学生可以在你的系统中访问他们的文件（位于他的硬盘上）。你应该如何回答？这会影响你系统的安全性吗？

如果你没有在 `mount` 时使用 `nosuid` 选项关闭 SUID/SGID，这绝对会影响你系统的安全性。如果另一个系统是敌意的，他可能会在你挂载的文件系统上创建一个 SUID-root 壳，并获得对你文件系统的 root 权限。即使他不是敌意的，你也应该考虑，如果他系统的 root 密码没有你的那么安全会发生什么。答案可能是黑客破解了 root 密码，从而获得了访问你系统的权限。

## 第 12 章 启动、关闭和作业管理

### 启动系统

完全启动 UNIX 并允许用户登录进行工作所需的步骤在不同系统之间差异很大。这是因为 UNIX 被不同的计算机公司移植到了许多不同计算机和处理器上。在最简单的情况下，你只需打开电源，UNIX 系统就会自动启动。系统将在几分钟后准备就绪，但取决于固件、网络连接、设备初始化等，也可能需要更长时间。其他系统不会自动启动，你必须输入特定命令来启动它们。在大多数系统中，普通用户永远不需要担心这个问题，因为系统位于由计算机操作员和管理员维护的限制区域。然而，在桌面系统和家庭系统中，所有者是唯一的操作员/管理员。我无法告诉你启动每个系统所需的特定步骤，但我可以告诉你一般的阶段。

#### 移除启动介质

`Booting`（启动）是将软件加载到内存中的过程，这使得程序或操作系统能够运行。大多数系统可以从几种类型的设备启动。例如，大多数 i86 系统配置为先从 A 驱（软磁盘）启动，如果软驱中没有磁盘，则从 C 驱（硬盘）启动。其他机器可能从 CD-ROM 或磁带启动。在启动系统之前请移除此类介质，因为 UNIX 通常从硬盘启动。

#### 在主计算机启动前开启辅助子系统

某些系统具有外部磁盘驱动器、磁带驱动器或端口连接盒，它们通过电缆连接到主系统。通常，这些设备应该在主计算机启动之前通电并准备就绪。如果你不这样做，系统可能无法启动，或者在系统以这些设备在线的状态重新重启之前，它将无法使用那些设备。




# 开机诊断

大多数计算机在首次启动时都会运行某种诊断程序。这可能只是快速的内存测试。某些计算机会运行一系列测试，这些测试可能持续几分钟或几小时，除非你知道如何结束诊断，否则它们可能会一直运行下去。在首次启动 UNIX 系统时，你应该观察屏幕输出，以便熟悉典型的信息。这样，如果检测到硬件问题，你至少能识别出某些异常之处。通常，启动过程会扫描系统上的所有设备。如果某个设备响应过慢或完全没有响应，你可能遇到了硬件问题。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

**警告：** 使用不当可能会严重损坏系统

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

我可以为你提供通用的指南，但总会有例外。因此，在没有针对特定计算机的操作指导之前，请不要启动系统。

# 将 UNIX 内核加载到内存

启动的下一步是将 UNIX 内核文件加载到内存中。内核包含了访问系统磁盘、显示器、键盘和其他硬件所需的驱动代码。在某些系统中，你会收到一个启动提示符，从中你可以指定启动选项要加载的特殊内核。有时启动需要你输入一个复杂的命令字符串，其中包含了包含内核文件的主磁盘设备地址。

## 另另参考

![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *更多关于 UNIX 内核的信息，请参见第 27 页*

# 挂载根磁盘并检查 (*fsck*)

启动过程包含一个阶段，以检查操作系统上次是否正常关机。如果不是，根文件系统可能会损坏，你可能会看到如下消息：

```
fsstat: mount failed. Possibly damaged filesystem. okay to check the root filesystem (y/n)?
```

此检查是由名为 `fsck` 的程序执行的。有时 `fsck` 在不等待响应的情况下启动。如果你足够好，`fsck` 将报告一系列紧密的阶段消息：
Phase 1: Check Blocks and Sizes
Phase 2: Check Names
Phase 3: Check Connectivity
以此此类推。

如果你运气不好，阶段消息将充斥着听起来难听的错误，例如：
```
EXCIVE BAD BLOCKS I=1432 FILE SIZE ERROR=257 DUP I=13827 DUP/BAD I=374 OWNER=17 MODE=700 SIZE=14328 FILE=/data/main (REMOVE?)
```
![arrow.gif](img/4505ed21b6bad.gif)

这些错误中的每一个都指示可能的数据损坏或文件丢失。有时会有成千上万这样的错误，系统必须从备份恢复或重新加载。某些现代 UNIX 系统提供了日志文件系统，使它们更有效地抵抗不当关机或系统崩溃等问题。使用 UPS（不间断电源）也是明智之举，它包含一个电池，可以在断电时防止系统崩溃。

# 单用户模式

当 UNIX 启动时，许多系统允许操作员停在单用户模式，在该模式下，系统仅经过部分初始化，可以执行维护功能。在某些系统中，必须使用特殊的命令序列才能进入单用户模式。出于安全考虑，大多数系统要求用户输入 root 登录才能进入单用户模式。在单用户模式下，你以 root（超级用户）权限运行。如果你在单用户模式下输入 `exit`，你不会获得另一个登录提示符。相反，系统将退出单用户模式并通常启动多用户模式。

# 多用户模式

如果系统没有停在单用户模式，它将继续初始化系统和设备进入其主运行模式，称为多用户模式。UNIX 在启动时通常非常详细，在每个子系统激活时会给你提供如下启动消息：

```
Mounting filesystems cron started, pid=274
Network daemons started: portmap inetd routed
printing subsystem started
```

再次，尝试学习你系统的启动消息，即使你不知道它们的含义，这样当启动过程中发生异常时你就能识别出来。一旦初始化完成，你应该通过任何系统端口登录系统。

# System V 运行级别

| 运行级别 | 描述 |
| --- | --- |





# 运行级别 (Run Levels)

| 运行级别 | 说明 |
| :--- | :--- |
| 0 | 完全关闭状态；准备断电 |
| 1 | 维护模式/单用户模式 |
| 2 | 多用户模式 |
| 3 | 导出了文件系统的多用户模式 (Solaris) |
| 3, 4, 5 | 可自定义运行级别（因站点而异） |
| 5 | 关机并断电 (Solaris) |
| 6 | 标准关机并重启 |

AIX 和 SCO UNIX 通常运行在运行级别 2。Solaris 通常运行在运行级别 3。有时存在 `s` 或 `S` 状态表示单用户模式，它与运行级别 1 仅有细微区别。你可以通过 root 输入以下命令显示当前的运行级别：

```bash
# who -r run-level 2 Feb 18 08:13 2 0 S
```

上面的示例显示你当前处于运行级别 2，这是你于 2 月 18 日 08:13 进入的。上一个运行级别是 `S`（单用户模式），这是你每次启动系统时经过的状态。

## 关闭系统

正如我们在上一节中看到的，在切断之前正确关闭 UNIX 对于防止文件损坏或丢失至关重要。UNIX 提供了许多关闭系统的命令，例如 `powerdown`、`reboot`、`haltsys` 或 `init 0`。请小心使用此类命令。手册页会告诉你，在安全运行某些命令之前，所有用户必须已经注销、卸载文件系统并关闭网络。通常情况下，你应该使用 `shutdown` 命令，它设计用于安全地关闭系统。

### 关闭系统的具体步骤

1. 以 root 身份登录。
2. 使用 `who` 和 `ps` 命令确保用户或程序没有在更新系统中的文件。
3. 关闭所有在系统关闭之前需要特殊关机处理的数据库。按照相应的步骤进行操作。
4. 输入 `cd /` 以验证你在关闭系统时处于根目录。如果你在某个挂载目录中，稍后卸载该目录可能会遇到问题。
5. 你会遇到两个版本的 `shutdown` 命令：System V 版本（用于 SCO）和 BSD 版本（用于 AIX）。Solaris 提供了这两个版本，取决于你的 `PATH` 变量。现在继续执行 System V 或 BSD 关机程序。如果你不确定使用哪个版本的 shutdown，请先尝试 System V 方法并输入所有可能的选项：`-g`、`-i` 和 `-y`。如果你应该使用 BSD 版本的 shutdown，你会收到错误，但不会造成任何伤害。

#### 运行 System V 关机

1. 确保你以 root 身份登录。
2. 输入 `shutdown`，但在接到指令前不要按回车键。
3. 输入空格，然后输入 `-g MIN`。此选项指定宽限期。将 `MIN` 替换为分钟，向所有用户广播系统即将关机的消息。（如果省略了 `-g`，默认等待一分钟）。输入 `-g 0` 立即关闭系统而无需等待。只有在你非常确定没有应用程序文件正在更新时才执行关机（参见附录中 UNIX 命令对*应用程序文件*的定义）。
4. 输入空格，然后输入 `-i RLEVEL`，其中 `RLEVEL` 是以下数字之一：
    - `0` 完全关闭系统（准备断电）
    - `1` 进入维护模式/单用户模式
    - `5` 关闭并断电（仅限 Solaris 系统）
    - `6` 关闭并自动重启
    如果未指定 `-i` 选项，大多数系统将默认进入运行级别 0；但某些系统（如 Solaris）将进入运行级别 1（单用户模式）。
5. 如果你确定要关闭系统，输入空格，然后输入 `-y`。
6. 按回车键执行命令。如果你在 shutdown 时没有包含 `-y` 选项，当宽限期结束，系统会询问你（是否）仍想关闭系统。输入 `y` 继续关机命令；输入 `n` 终止关机命令。

#### 运行 BSD 关机

1. 确保你以 root 身份登录。
2. 输入 `shutdown`，但在接到指令前不要按回车键。
3. 输入空格。
4. 如果你想关闭系统电源，输入 `-h` 选项。





如果你想重启系统，请输入 `-r` 选项。

5. 输入一个空格。
6. 你现在有三个选项：
    - 如果你确定可以立即关闭系统，请输入 `now`。
    - 输入 `+MIN`，其中 `MIN` 是系统在定期广播关机消息期间等待的分钟数。
    - 输入 `HH:MM`，其中 `HH` 和 `MM` 是系统关机前的小时数和分钟数。
7. 按 Enter 键执行你的命令。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 防止 UPS 损坏数据库
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
某些 UPS 在长时间停电时会关闭系统。如果你有一个必须在系统关闭之前关闭的数据库，你必须配置你的 UPS 软件以先正确关闭数据库。

### 在启动或关机时自动化作业
UNIX 在允许作业根据系统事件或时间日期自动运行方面体现了极大的灵活性。其中某些机制仅供 root 用户（系统管理员）使用，但许多机制所有用户均可以使用。以下章节描述了 root 用户可以执行的最常见功能。

#### System V UNIX 启动时的自动化作业 (rc.d)
仅 root 用户可以自定义并添加在系统启动时自动运行的作业。某些系统使用 System V 方法；其他系统（甚至是 S4 系统）使用 BSD 方法。查看名为 `/etc` 的目录。如果你的系统拥有 `rc`、`rc0` 和 `rc2` 文件，并且拥有 `rc.d`、`rc0.d` 和 `rc2.d` 目录，则它在使用 System V 类型的启动程序或脚本。这些被称为 `rc scripts`（rc 代表 run control，运行控制），因为这些脚本控制你如何进入或离开运行级别。`rc2` 是当系统切换到运行级别 2（多用户模式）时运行的脚本程序。`rc2` 脚本使用 `rc2.d` 中的文件，如下面的 SCO UNIX 示例所示：在第一个字母之后，每个脚本都有一个数字控制脚本运行的顺序。表 12.2 显示了每个脚本第一个字母的含义：

##### 表 12.2 System V 脚本前缀。
| 前缀 | 含义 |
| :--- | :--- |
| **K** | 通过运行此脚本杀死进程 |
| **S** | 通过运行此脚本启动进程 |
| **P** | 如果该范围内没有 S 脚本，则并行运行 P 数字脚本（仅限 SCO UNIX） |

例如，在之前的列表中，你可以看到 `lp` 打印系统首先启动，然后是 `tcp`，最后是 `nfs`。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)
**警告**：初学者不应修改此目录。错误会导致系统无法启动。

### 修改 System V 启动脚本
1. 在此目录中，创建一个名称以 `S99` 开头的自定义脚本。这将导致脚本在其他初始化脚本之后执行。设置所有者、组和权限以与该目录中的其他文件匹配。可以有多个以 `S99` 开头的脚本。
2. 在你的 `S99` 脚本中，输入你想在系统进入多用户模式时运行的系统命令。对每个命令、目录和文件使用完整路径名；例如，你应该使用 `/etc/shutdown` 而不是 `shutdown`。如果不确定，请使用 `type` 命令确保你拥有命令的正确完整路径，如下例所示：

```
type shutdown shutdown is /sbin/shutdown
```





### 3. 不要在此 `rc2.d` 目录中创建脚本的备份副本。如果你这样做了，例如 `S99yourscript.bak`，它将在每次启动时与 `S99yourscript` 一起执行，因为它们都在 `/etc/rc2.d` 中。

### 4. 使用 `&` 在后台运行子任务，以防止出现系统挂起和无法重启的情况；例如，可以使用 `stty` 命令设置端口的波特率，但如果设备未就绪（例如，调制解调器正在等待呼入），`stty` 可能会一直挂起直到设备就绪。如果这个 `stty` 命令在你的 rc 脚本中，系统也会挂起，你将不得不重置并进入单用户模式来修复问题。为了防止此类问题，请创建一个访问所需端口的脚本，并在 rc 脚本中后台调用该脚本，如下所示：

```
/usr/startup/portsetup &
```

### 5. 如果你的函数需要在系统启动期间执行某些特定代码，并在系统关闭时执行其他代码，你应该执行此额外步骤。将你的脚本副本放入 `/etc/init.d`，并使用不以 `S99.` 开头的名称。Solaris 使用硬链接来实现此操作；SCO。OpenServer 5 使用复杂的符号链接。要了解如何在你的系统上进行操作，请查看 `rc2.d` 和 `init.d` 中的其他脚本并遵循它们的示例。其思想是让一个脚本同时处理该函数的启动和关闭任务。该脚本应将 `$1` 保存为模式，然后如果该模式是启动状态，脚本应执行启动代码；当该模式停止时，脚本应执行关闭代码。完成后，将此脚本链接到多用户启动目录（`/etc/rc2.d`）或关闭目录（`/etc/rc0.d`），并为启动任务添加 `S99`，或为关闭任务添加 `K##`。

#### 在 System V UNIX 上实现系统关闭时的任务自动化 (rc0.d)。

在 System V 类型的系统中，有一个名为 `/etc/rc0.d` 的目录，其中包含与 `/etc/rc2.d` 类似的脚本。你可以将脚本添加到 `rc0.d` 中，以便在系统切换到运行级别 0（完全关闭状态）时运行。

通常一个更好的主意（在 BSD 系统中同样有效）是按照下面的步骤创建你自己的脚本。

##### 用于调用关闭操作的自定义脚本

1. 输入命令 `shutdown` 并按回车。你会看到如下的输出：
```
$ shutdown
shutdown is /sbin/shutdown
```
这是 `shutdown` 的完整路径。
2. 使用 `cd` 命令切换到 `shutdown` 所在的目录。
3. 创建一个文本文件并命名为 `shut`（这不是一个标准名称，你可以为 `shutdown` 命令的替代方案选择不同的名称）。
4. 插入你想在关闭系统期间运行的命令。然后用以下几行结束你的脚本：
```
cd shutdown OPTS
```
将 `OPTS` 替换为你的系统上 `shutdown` 需要的选项。
5. 使用 `chmod`、`chown` 和 `chgrp` 命令赋予 `shut` 与 `shutdown` 相同的权限、所有者和用户组。
6. 现在，每当你想关闭系统时，都使用 `shut` 命令代替 `shutdown`。

**注意**：存在某些管理员或系统进程使用 `shutdown` 命令而非你的 `shut` 脚本的风险。这是一个关键问题，请向 `/etc/rc0.d` 添加关闭脚本，而不是创建这个 `shut` 脚本。

**警告**：有关编写 shell 脚本的更多信息，请参见第 637 页。

#### 在 BSD 上实现系统启动时的任务自动化 (rc scripts)

如果你的系统使用 BSD 启动脚本，你会发现许多以 `rc` 后跟点开头的脚本，例如 `rc.net`。所有这些 rc 脚本都在 `/etc` 目录下。然而，并不是所有的 rc 脚本都会系统启动期间运行。

如果你在 AIX UNIX 系统上运行以下命令：
```
ls -lu /etc/rc*
```





| 你将看到类似以下的输出： |

```text
-r-xr-xr--  1  bin      bin           1786 Aug 21 16:03 /etc/rc
-rw-r--r--  1  root     system        48 Feb  4  1996 /etc/rc.bak
-r-xr-xr--  1  bin      bin           2502 Feb  4  1996 /etc/rc.bsdnet
-r-x------  1  root     system        21187 Feb  4  1996 /etc/rc.motpowerfail
-rw-r--r--  1  root     system        571 Feb  4  1996 /etc/rc.ncs
-r-xr-xr--  1  bin      bin           7352 Aug 21 16:03 /etc/rc.net
-r-xr-xr--  1  bin      bin           4554 Aug 21 16:03 /etc/rc.net.serial
-rw-r--r--  1  root     system        982 Feb  4  1996 /etc/rc.netls
-rwxr-xr-x  1  root     system        4201 Aug 21 16:04 /etc/rc.nfs
-rwx------  1  root     system        29511 Feb  4  1996 /etc/rc.powerfail
-rwxrwxr--  1  root     system        4180 Aug 21 16:04 /etc/rc.tcpip
```

`ls` 的 `-lu` 显示了 `rc` 脚本最后被访问的时间。你可以看到，在 8 月 21 日 16:04 的上次重启中，只有五个脚本被使用了。其他 `rc` 脚本自 1996 年以来未被访问过。以下是来自 `/etc/inittab` 文件的内容，该文件在启动时执行其中一些 `rc` 脚本：

```text
c::init:/sbin/rc.boot 3>/dev/console 2>&1 # Phase 3 of system boot
powerfail::powerfail:/etc/rc.motpowerfail -t 5 2>&1 # Power Failure Detection
rc:2:wait:/etc/rc 2>&1 -tboot>/dev/console # User checks
tcpip:2:wait:/etc/rc.tcpip >dev/console 2>&1 # Start TCP/IP daemons
nfs:2:wait:/etc/rc.nfs >dev/console 2>&1 # Start NFS Daemons
```

要在系统启动时运行任务，你必须将该任务插入到启动时运行的 `rc` 脚本中。这是一项经验丰富的程序员的工作，初学者不应尝试。错误可能会导致你的系统以后无法正常启动。

### 由任何用户自动化任务 (`profile`, `cron`, `at`, `batch`)

普通用户可以自动化特定的任务，使其在登录时、特定时间或特定某天运行。系统管理员使用类似的机制来定期运行系统进程。

#### 在用户登录时自动化任务

每个 Bourne 或 Korn shell 在登录期间都会执行两个文件：`/etc/profile` 或 `.profile`（位于用户家目录中）。

只有 `root` 用户可以修改 `/etc/profile`，因为该文件的更改会影响所有用户的登录。出于安全考虑，你不应给其他人该文件的写入权限。

**安全提示**：在修改 `/etc/profile` 或 `.profile` 时请使用两个屏幕。如果你在更改这些文件时出错，可能会导致即使是 `root` 用户也无法重新登录。在更改 `/etc/profile` 或 `.profile` 后，确保你仍然能从另一个屏幕成功登录。如果失败了，你仍然登录在第一个屏幕，可以纠正或撤销你的更改。

用户通常可以修改他们自己的 `.profile` 文件，以便在登录时设置环境偏好。（在某些系统中，管理员可能允许用户对 `.profile` 读取权限但不写入权限，以防止用户对其 `.profile` 文件进行错误或不理想的更改。）执行 `/etc/profile` 和 `.profile` 中的行，其效果等同于用户在登录后立即在键盘上输入了这些相同的行。例如，来自 `/etc/profile` 或 `.profile` 的 `exit` 命令会将用户带回登录提示符并强制重新登录。

`/etc/profile` 和 `.profile` 是设置 shell 变量（如 `PATH`、`CDPATH`、`TERM` 和 `umask`）的好地方。也可以自动设置端口的首选 `stty` 选项。对 `/etc/profile` 的更改会影响所有用户，但这些更改可以通过用户家目录下 `.profile` 中的代码进行修改。在 `root/.profile` 中添加 `df` 允许 `root` 在每次 root 登录时查看可用磁盘空间。





`/etc/profile` 也可以用于为系统添加额外的安全性。例如，使用标准的 Bourne shell 编程，`/etc/profile` 可以检查用户是否通过调制解调器端口登录，如果是，则只允许在受限制的时间登录，或要求输入额外的密码。如果 `/etc/profile` 代码执行了 `exit` 命令，用户的登录将终止，该用户将返回初始登录提示符。

# 定期重新运行任务调度 (*cron*)

UNIX 维护了一组名为 `crontabs`（时间表）的表，其中包含了调度为定期运行的任务。对于每个提交了 cron 任务的用户，通常有一个表或文件（通常位于 `/usr/spool/cron/crontabs`）。系统将使用该用户的账户运行该任务。

要检查是否提交了任何 `cron` 任务并查看它们，你需要使用 `crontab` 命令的 `-l` 选项（列出）。如果你以 `root` 身份登录，可能会看到如下输出：

```
# crontab -l 17 5 * * 0 /etc/cleanup > /dev/null
0 2 * * * 0,4 /usr/lib/cron/logchecker 3 3 * * * /usr/lib/cleantmp > /dev/null
1 3 * * * /etc/setclk -rd1800 > /dev/null 2>&1
5 18 * * 1-5 /usr/lib/sa/sa2 -s 8:00 -e 18:01 -i 1200 -A
30 1 * * 2,3,4,5,6 /etc/edge.nightly -MB -n root -d
/dev/null 1>/dev/null 2>&1
5 4 * * 0 /etc/shutdown -g5 -i6 -y
```

`crontabs` 中的每一行都有六个字段，用一个或多个空格或制表符分隔。表 12.3 描述了这六个字段及其内容。

### 表 12.3 crontabs 中的字段。

| 字段 | 功能 | 可能的值值范围 |
| :--- | :--- | :--- |
| 1 | 小时内的分钟 | 0-59 |
| 2 | 一天中的小时 | 0-23 |
| 3 | 每月的几几 | 1-31 |
| 4 | 一年中的月份 | 1-12 |
| 5 | 星期几 | 0-6 (0 代表星期日) |
| 6 | 要运行的命令 | |

你可以使用连字符 (-) 表示连续范围。一个字段中的多个值可以以任何顺序指定，并应用逗号（且没有空格）分隔，例如 `1,3,7,2,25`。在表 12.3 中，要运行的命令（第 6 字段）可以是 UNIX 命令或 shell 脚本。使用完整路径名来引用所有文件以及不在 `/bin` 或 `/usr/bin` 中的任何命令。如果你是第一次使用 `cron`，请尝试只使用 `date` 命令，该命令将通过 `cron` 邮件发送给你。另一个良好的第一个 cron 脚本是在你的主目录或 `/tmp` 中创建一个小型结果文件，其结果显示在此：

```bash
echo cron test `date` > /tmp/fred.cron.tst
```

## 添加/删除/修改 Cron 任务

1. 以想要修改的 cron 任务的用户身份登录。（除非绝对必要，否则不要以 `root`  cron 任务。）如果你以前从未添加过 cron 任务，请使用 `root`、`sys`、`adm` 或 `uucp` 以外的账户，以便先练习添加和删除测试 cron 任务。
2. 输入 `cd` 进入你的主目录。
3. 除非通过 `cron` 运行的命令极其简单，否则使用 `vi` 或编辑器创建一个 shell 脚本（在此过程中称为 cron 脚本）。在该 cron 脚本中，插入你想从 `cron` 运行的命令。每当你想要从 `cron` 运行一系列多个命令时，都应该使用 cron 脚本。直接从终端运行你的 cron 脚本进行测试。在 cron 脚本中，对任何要访问的文件使用完整路径名。对于任何不在 `/bin` 或 `/usr/bin` 中的系统命令，使用完整路径名。如果你是第一次使用 `cron`，请尝试只使用 `date` 命令，该命令将通过 `cron` 邮件发送给你。
4. 在 shell 提示符处，如下所示测试你的 cron 脚本。（注意：逻辑）如果系统在计划运行任务的时间点处于关闭状态，则该任务将被跳过。如果系统开机，它将在下一个计划的时间点再次运行。
5. 接下来，缓慢且仔细地输入此命令：
`crontab -l > cronfile`
如果你收到提示“No such file”或“Can't open file”的错误，说明你没有 cron 任务。只需忽略此错误并继续下一步。
6. 在第 5 步中，如果不小心漏掉了 `-l` 选项，你可能会删除所有的 cron 任务。如果你丢失了 `root` cron 任务，重要的系统功能将被禁用。此步骤其余部分讨论了如果不小心漏掉 `-l` 选项，如何尝试保存你的 cron 任务。缺少 `-l` 选项会导致你当前的 crontabs 处于危险。你将看到 PS2 提示符（通常是大于号），这意味着 shell 正在等待键盘输入以替换你当前的 crontabs。按下你的 `INTR` 键（通常是 `Ctrl+C` 或 `DEL`）来取消此命令。如果 `INTR` 键无效，请到另一个端口并正确执行第 5 步。然后返回此端口并输入你的 `EOT` 键（通常是 `Ctrl+D`）来清空你当前的 crontabs。
为了完全避免讨厌的 PS2 提示符，某些用户使用此命令代替第 5 步中描述的命令：
`cp /usr/spool/cron/crontabs/MYID cronfile`





将此行中的 `MYID` 替换为你的登录 ID。

某些用户使用 `crontab -e`（这会自动调用默认的 `EDITOR`）。然而，如果你忘记了 `-e` 选项，你仍然面临此步骤中描述相同的问题。

### 7. 输入 vi cronfile。（你可以使用任何文本编辑器编辑此文件。）现在，你应该能看到之前讨论的六字段格式的所有当前正在运行 cron 任务。例如，你可能会看到如下行：

```
17 5 * * 0 /etc/cleanup > /dev/null
```

如果你的登录账户从未提交过 cron 任务，则此 cronfile 将是空的。如果该 cronfile 是空的但本不应该是空的（例如，root 的 cronfile 不应为空），请返回第 1 步并重新开始。如果你丢失了之前的 cron 条目，你将不得不将它们重新输入。

### 8. 使用文本编辑器修改任何现有的 cron 任务，并以六字段格式向此文件添加新任务。如果你在此过程的第 3 步中创建了 cron 脚本，请向该文件添加一个新的六字段行，并在最后一个字段中填写你 cron 脚本的完整路径。编辑完成后，保存工作并退出编辑器。此 cronfile 只是临时文件，所以如果你不喜欢保存的结果，请返回第 5 步并重新开始。

### 9. 输入 cat cronfile。

确保此文件包含所有先前的 cron 任务的正确六字段条目以便保留，加上你添加的任何修改过的或新的 cron 任务。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

注意：此文件必须包含该登录账户运行的所有 cron 任务。如果你从此文件中删除一个条目，你将从 cron 中删除它，且它将来将不再运行。

### 10. 输入 crontab cronfile。

这将提交你的更改，替换你之前所有的 cron 任务。如果你收到错误提示说不允许提交 cron 任务，请参见后文章节“按用户启用和禁用 cron/at/batch”。

### 11. 输入 crontab -l 以显示你当前提交的 crontab 条目。然后查看在此过程中较早出现的关于此命令的警告。

另另
- 关于使用 `vi` 编辑的信息，请参第 449 页和第 471 页。
- 关于显示文件的信息，请参第 147 页。
- `![sarrow.gif](img/ad91af06ad9c57f0a338bded4c42f0e.gif)`
- 在 Crontabs 中使用星号 (*) 通配符。

#### 在 Crontabs 中使用星号 (*) 通配符。

crontab 允许如表 12.4 所示使用星号 (`*`) 通配符。注意，这是 crontab 通配符，而不是文件名通配符或正则表达式通配符。

关于 crontab 字段 1 的提示：小时内的分钟。如果你在字段 1 中发现星号（为了让你的任务每小时内运行 60 次），这通常是一个错误。避免在每个 cron 任务的分钟字段中放置 0，因为这可能会影响每小时开始时的性能。对于那些不需要正好在整点开始的任务，请错开它们的分钟值。

表 12.4 在 crontabs 中使用星号 (*)。

| 字段 | 星号在该字段中的含义 |
| :--- | :--- |
| 1. 小时内的分钟 | 每分钟执行一次任务，每小时执行 60 次 |
| 2. 一天中的小时 | 每小时执行一次任务，每天执行 24 次 |
| 3. 每月的几几 | 忽略此字段并使用字段 5 |
| 4. 每年的月份 | 每月执行一次任务，每年 12 个月 |
| 5. 星期几几 | 忽略此字段并使用字段 3 |

在字段 3 和 5 中都使用星号意味着该任务每天运行。

#### 运行清晨的工作日任务

这里有一个典型的 crontab 错误：

```
30 1 * * 1-5 /u/backup
```

这家公司从周一到周五上班，并希望在每个工作日的凌晨 1:30 执行备份。然而，使用此命令，周五的工作将等到下周一早上 1:30 才会被备份。由于周末沉重的建筑维护工作和电力问题更频繁，这种做法并不好。以下是修正后的条目，它也会在周六早上运行备份：

```
30 1 * * 2-6 /u/backup
```





出于同样的原因，这对该公司来说并不是一个好的条目：30 1 * * * /u/backup

因为周六和周日办公室没有人，所以磁带不会被更换，而周五晚上的备份（实际上在周六凌晨运行）将在周六晚上和周日晚上被重写。周末的电源问题可能会导致文件损坏，然后这些损坏的文件将替换掉周五晚上良好的备份。

### 另此
有关更多关于备份的信息，请参阅第 327 页。

### 在特定日期/时间调度一次性任务
UNIX 的 `at` 命令允许你安排任务在稍后的预定时间运行一次。如果你想多次运行该任务（例如定期运行），请参阅上一节中关于 `crontab` 命令的介绍。

#### 使用 at 命令调度任务
1. 以将要用于运行任务的账户的用户的身份登录。仅在绝对必要时才使用 root 用户。
2. 输入 `at`，但在没有收到指示前不要按回车键。
3. 输入一个空格，然后使用以下三种方法之一指定运行命令的时间：
    - **方法 1**：仅输入时间，例如：`03` 表示凌晨 3 点，`17` 表示下午 5 点，`0704` 表示早上 7:04，`7:04pm` 表示晚上 7:04。任务将在接下来的 24 小时内于请求的时间运行。
    - **方法 2**：输入时间和日期，例如：`Sat pm`、`Aug 24 7:04pm`。任务将在未来一年内的请求日期的请求时间运行。
    - **方法 3**：提供偏移量，例如：`now + 5 min`、`now + 2 days`。
4. 按回车键执行此行。光标将移动到没有提示符的下一行，并在那里等待更多输入。如果你在此处遇到错误，请参阅后文的章节“按用户启用和禁用 crontab/at/batch”。
5. 输入你想稍后运行的命令。按照你正常运行该命令的方式精确输入。然后按回车键提交命令。你可以继续输入更多命令，每条命令后都按回车键。
6. 完成命令后，光标应位于空白行的开头。输入你的 EOT 键（通常是 Ctrl+D），你的正常提示符就会出现。

#### 使用示例
你可以使用 `at` 的 `-l` 选项来列出你当前的任务。你可以使用 `-r` 选项删除已计划的任务。下面的示例说明了这些选项用法。它展示了一个你可能想要测试 `at` 的快速命令。如果你删除该任务，它将在五分钟后在当前目录下创建一个垃圾文件。

```bash
$ at now + 5 min date > junk
warning: commands will be executed using /bin/sh
job 88071220.a-9910:0 at Sat Feb 21 06:27:00 1998

$ at -l
88071220.a-9910:0    Sat Feb 21 06:27:00 1998

$ at -r 88071220.a
at: 88071220.a does not exist: No such file or directory
```




在上面的示例中，注意 `at` 命令的 `-l` 选项显示任务何时运行，但不会显示将运行哪个命令。注意 `-r` 选项需要输入完整的任务 ID。

如果系统在 `at` 任务预定运行期间关机状态，则 `at` 任务将在系统重新启动后立即运行（与 `cron` 不同）。你甚至可以编写一个 `at` 任务使其定期重新进入队列运行。你可以在 `at` 脚本的末尾添加如下的一行：

```
echo "sh jobname" | at 2330 sat next week
```

# 调度在负载低运行时执行单次任务 (batch)

`batch` 命令可用于系统认为负载足够低时运行任务，这意味着你无法预测它何时运行。如果你的系统始终处于高负载状态，那么 `batch` 对你来说不是一个实用的命令，因为它永远无法启动你的任务。

## 使用 batch 命令

1. 输入 `batch` 并按回车键。光标将移动到下一行，且没有提示符，它将在那里等待更多输入。如果你在此处遇到错误，请参见后文章节 `按用户启用和禁用 crontab/at/batch`。
2. 输入你想稍后运行的命令。按照你正常运行该命令的方式完全输入。按回车键提交命令。你可以继续输入更多要按顺序执行的命令。每个命令后都按回车键。
3. 当你完成命令输入后，光标应位于空行的开头。输入你的 EOT 键（通常是 `Ctrl+D`），你的正常 shell 提示符就会出现。

## 按用户启用和禁用 crontab/at/batch

root 用户（系统管理员）可以修改这两个文件来允许或拒绝用户使用 crontabs：

`/usr/lib/cron/cron.allow`
`/usr/lib/cron/cron.deny`

root 用户还可以修改以下两个文件来允许/拒绝用户使用 `at` 或 `batch` 命令：

`/usr/lib/cron/at.allow`
`/usr/lib/cron/at.deny`

如果存在 `allow` 文件，则只有文件中列出的用户可以使用该命令。如果不存在 `allow` 文件，则使用 `deny` 文件。在这种情况下，除 `deny` 文件中列出的用户外，所有用户都可以使用该命令。

## 任务优先级

以下章节涵盖了查看和更改运行进程优先级的必要命令。

### 查看任务及其优先级 (ps)

你可以使用 `ps` 的 `-lf` 选项来显示每个运行中的进程（任务）及其当前的优先级。例如，请看这里：

```
$ ps -lf F S UID PID PPID C PRI NI ADDR SZ STIME TIME CMD
20 S mori 9998 9374 6 73 20 fb11e798 132 fb11e798 06:54:41 ttyR030 00:00:00 -ksh
20 O mori 10020 9998 7 48 20 fb11e8f0 160 06:55:23 ttyR030 00:00:00 ps -lf
30 S mori 10021 9998 2 78 20 fb11ecf8 72 fb11ecf9 06:55:23 ttyR030 00:00:00 pg
```

标记为 `NI` 的列显示进程的 nice 值（在此情况下为 20）。nice 值越高，获取系统资源和时间的优先级就越低（对系统中的其他用户越“友好”）。表 12.5 概述了典型的 nice 值。

表 12.5 nice（优先级）值

| 类型 | 范围 | 默认值 |
| :--- | :--- | :--- |
| BSD | 1 到 19 | 0 |
| System | -20 到 20 | 0 |

### 以低优先级启动任务 (nice)

1. 输入 `nice`，但在接到指示之前不要按回车键。
2. 输入一个空格，然后输入 `VAL`，将 `VAL` 替换为 1 到 19 之间的数字。值越大，对其他用户越友好。仅 root 用户可以输入 `--VAL` 来降低 nice 值，从而将其任务优先级提高高于其他用户。然而，root 用户必须小心，不要将优先级调得太高，以至于任务接管并禁用所有系统功能。
3. 输入一个空格，然后输入想要运行的命令。如果你输入的是管道，请为管道的每个阶段都输入一个 `nice` 命令。（参见下一个示例。）按回车键执行你的命令。

你的 `nice` 或 `renice` 可能会有所不同。




查看你的 `man` 页面了解 `nice` 和 `renice`。在某些系统中，nice 值的范围以及以正数还是负数形式输入可能与此处描述的有所。

此示例展示了在管道中的每个命令都必须显式地调用 `nice` 命令。该命令将 `ps` 的输出传递给 `pg`。请注意，`ps` 的 nice 增量为 5，`pg` 的 nice 增量为 7。选择不同的值仅是为了说明一点；通常你会对两者使用相同的值。

```bash
$ nice -5 ps -lf | nice -7 pg   F S      UID    PID  PPID  C  PRI NI      ADDR    SZ WCHAN     STIME      TTY         TIME CMD
20 S      mori 10042  9996  5  73  20  fb11e798  132  fb11e798 07:12:35  ttyR029     00:00:00  -ksh
20 O      mori 10066 10042  9  44  25  fb11e8f0  160 -07:13:24  ttyR029     00:00:00  ps -lf
20 S      mori 10067 10042  5  76  27  fb11ecf8   72  f093d7c0 07:13:24  ttyR029     00:00:00  pg
```

注意 `pg` 命令的 nice 值为 27。这是因为 `nice -7` 意味着在默认值 20 的基础上增加 7 个点。

## 更改现有作业的优先级 (*renice*)

现代 UNIX 系统支持 `renice` 命令，允许你更改已启动进程的 nice 值。但是，你必须首先使用 `ps` 命令查找目标进程的 `PID` 值（参见之前的 `ps` 示例）。

**注意**：请参术表以获取 `PID` 值的定义。

### 更改现有作业的优先级 (*renice*)

1. 输入 `renice` 命令，但在接到指示之前不要按回车键。
2. 输入一个空格，然后输入选项 `-n`。
3. 输入一个空格，然后输入 `VAL`，其中 `VAL` 是 1 到 19 之间的数字。这代表增加 nice 值的幅度，从而降低作业的优先级。
4. 输入一个空格，随后输入你要更改的进程（作业）的 `PID`。
5. 你的命令看起来应该这样：
```bash
renice -n 5 10042
```
按回车键执行你的命令。

### 何时使用 `nice`、`at` 和 `batch`

- 当你需要作业完成但想尽量减少对其他用户的影响时，使用 `nice` 或 `renice`。
- 使用 `at` 确保作业在指定时间之前不运行。
- 使用 `batch` 利用系统空闲时间，但不要在繁忙系统上使用 `batch`。

## 后台作业 (&)

UNIX 是一个多任务操作系统。这意味着通常情况下，你可以启动多个作业，且所有作业将并发运行。你的工作站不会因等待它们完成而被占用。你甚至可以指定作业序列，使得在上一个作业完成之前下一个作业不会开始。

### 启动后台作业 (&)

要在后台启动作业，只需在 UNIX 命令末尾加一个空格和一个 ampersand (`&`)，如例所示：

```bash
$ make acmesys > acme.log 2>&1 &
```
以下是该命令各部分的详细说明：

- `make` 是一个可能需要很长时间完成的命令；因此，你可以在后台运行它，使其不会占用你的工作站。
- `> acme.log` 将 `make` 的输出重定向到名为 `acme.log` 的文件中。在启动后台运行时这是一个好主意，因为输出会被保存以便日后查看。如果不这样做重定向输出，它仍然会显示在屏幕上，可能会与其他输出混合。
- `2>&1` 将 `make` 命令的任何错误消息重定向到与标准输出相同的文件文件中（因此你将 make 的输出和错误保存在同一个文件中）。
- `27903` 是作业号，也称为进程 ID 或 `PID`。如果你保存了这个数字，稍后可以使用它检查该作业。

### 防止注销杀死后台作业 (*nohup*)





退出系统通常会终止所有后台作业。某些 shell 会警告你已停止了作业。如果你此时再次输入 `exit`，将终止这些作业并退出系统。`nohup` 命令允许你启动后台作业，这些作业在你注销系统时不会被杀死。

## 使用 `nohup` 启动后台作业

1. 在 shell 提示符下，输入 `nohup`。在接到指令之前，不要按回车键。
2. 输入一个空格，然后输入你想运行的 UNIX 命令。如果需要，请记住重定向标准输出和标准错误消息。
3. 输入一个空格，然后输入和符号 (`&`)。
4. 按回车键在后台执行你的命令。现在，你的注销将不会终止该后台作业。

如果你没有重定向标准输出和标准错误，`nohup` 命令将自动创建一个名为 `nohup.out` 的文件来保存它们。

## 杀死后台作业 (`kill`)

如果你记录了启动后台作业时显示的 `PID`，那么可以使用两个 `kill` 命令中的任意一个轻松终止该作业。以下步骤展示了如何使用这两个命令。

### 如何通过 PID 终止作业

1. 从 shell 提示符下，输入 `kill PID`，其中 `PID` 是你想终止的进程的 PID 数字。双检输入的数字是否正确。然后按回车键。此 `kill` 命令将赋予作业一个优雅终止的机会，关闭应用程序并移除锁文件和临时文件。不会显示任何消息。
2. 现在输入命令 `kill -9 PID`，其中 `PID` 是你在步骤 1 中使用的相同数字。双检输入的数字是否正确。然后按回车。此 `kill` 将结束即使无响应的命令。虽然你可以在步骤 1 之后立即执行步骤 2，但你可能想等待两秒让步骤 1 完成。
3. 如果步骤 2 给出 `No such PID` 错误，请忽略该错误。这意味着步骤 1 已经足够结束任务，步骤 2 是多余但无害的。如果你不记得你的 `PID` 数字，可以使用 `ps` 命令查询。

### 使用 `ps` 查找 PID 数字

1. 从 shell 提示符下，输入以下两个命令：
   ```
   ps -ef
   ps aux
   ```
   某些系统支持这两个命令，但有时只有一个能产生结果。
2. 使用在你系统上有效的命令，查看初始标题以找到 `PID` 列、用户 (`UID`) 列和命令 (`CMD`) 列。
3. 如必要，重新运行命令并将其通过到 `pg`、`more` 或 `less`，以便逐页查看。或者，你可以将 `ps` 命令的输出通过到 `grep` 以过滤出你感兴趣的行。请注意，这也会移除标题。
4. 找到你想终止的命令。检查用户列以确保该命令是你启动的。
5. 找到该命令的 `PID`。然后你就可以按照通过 PID 终止作业的步骤操作了。

这是一个用于查找后台作业的命令示例。然而，输出在处理过程中被截断。由于 `ps` 可以显示许多进程，该命令已使用 `^C`（在 Solaris 上）终止。

```
ps -ef UID PID PPID C STIME TTY TIME CMD
root 0 0 0 Feb 20 ? 0:02 sched
root 1 0 0 Feb 20 ? 0:15 /etc/init-
root 2 0 0 Feb 20 ? 0:00 pageout
root 3 0 0 Feb 20 ? 1:02 fsflush
root 289 1 0 Feb 20 ? 0:00 /usr/lib/saf/sac -t 300
```

假设你正在运行之前的命令来查找早些启动的 `find` 命令。你可以使用 `grep` 来过滤出你需要的行，如下所示：

```
ps -ef | grep find | grep -v grep
root 27961 27955 5 13:53:33 pts/1 0:03 find / -name acme -print
# ps -ef | grep find
```
root 27967 27955 0 13:54:19 pts/1 0:00 grep find
```

从 `CMD` 字段（最后一个字段），你可以看到两个提到 find 的进程。查看第 2 列，你看到 PID 27961 是你想终止的 find 进程。注意 PID 27967 是正在查找 find 的 grep 进程；换句话说，grep 在查找 find 时看到了自己。





acme -print

当你知道想要终止的进程 PID 时，可以输入以下行来杀死进程：

```
kill 27961
kill -9 27961
```

### 另另
有关 grep 的更多信息，请参阅第 380 页。

### Korn Shell 下的额外作业控制
在上一节中，我们涵盖了适用于所有 shell（包括 Bourne shell）的后台作业用法。新的 shell 通过引入名为 *job control*（作业控制）的功能，使得处理后台作业变得简单得多。例如，某些系统已为 Bourne shell 添加了作业控制，可以通过 `jsh` 调用。本节描述了其他作业控制命令，它们与 `jsh` 类似：分别是用于 C shell 的 `csh` 和用于 Korn shell 的 `ksh`。

#### 列出后台作业 (*jobs*)
要列出任何支持作业控制的 shell 中的所有后台作业，进入 shell 提示符并输入 `jobs`。你会看到如下输出：

```
$ jobs [4] + Running find/-name acme-print > /tmp/acme.find &
[3] - Stopped (SIGTSTP) find
[2] - Stopped (SIGTSTP) bc
[1] - Stopped (SIGTSTP) vi acme
```

作业编号位于每行开头的括号中。最近一次在前台的作业（最近在你的屏幕上活跃的作业）用加号 (`+`) 表示。次近的作业用减号 (`-`) 表示。注意，你再也不需要担心 PID 了。

#### 挂起和恢复作业 (Ctrl+Z, bg, fg)
作业控制最强大的应用之一是将前台作业（占用你键盘和屏幕的作业）挂起到后台，以便输入其他命令，稍后恢复该挂起作业。在某些 SCO UNIX 操作系统中，极少数工具支持 `Ctrl+Z` 这种方法；在这些系统中，只有 `vi` 命令可以生效。但在 Solaris 和 AIX 下，`Ctrl+Z` 似乎对每个工具都有效。你可以用它在前台和后台之间移动作业。这在 Korn shell 中是事实，但在 `jsh` 中不是。

#### 将作业移动到后台并返回前台
1. 确保你处于支持作业控制的 shell 中，例如 Korn shell（而不是 Bourne shell）。如果你不确定，使用命令 `exec ksh` 调用 Korn shell。
2. 输入任何需要一些时间完成的 UNIX 命令。不要在命令末尾输入最后的符号 (`&`)，该作业将在前台运行并占用你的键盘和屏幕。
3. 要将该作业移动到后台，按下 `Ctrl+Z`。你应该看到如下确认信息，其中了你正在运行的命令：
```
^Z[1] + Stopped (SIGTSTP) find/-name acme-print > /tmp/acme.find
```
如果没有看到此类消息，说明你的 shell 不支持作业控制，或者你的 UNIX 版本不支持使用 `Ctrl+Z` 挂起作业。你现在将获得一个系统提示符，可以在那里输入其他命令。你之前的作业已被挂起（它不再运行）。
4. 输入 `jobs`，你会看到如下输出：
```
[2] + Stopped (SIGTSTP) find/-name acme-print > /tmp/acme.find &
[1] - Stopped (SIGTSTP) find
```
5. 要让作业在后台继续运行，在 shell 提示符处输入 `bg %JOBID`，其中 `JOBID` 是 `jobs` 命令显示的作业编号。如果该作业是加号 (`+`) 表示的最近的作业，你可以完全省略 `%JOBID`。
6. 再次输入 `jobs`。现在你应该看到如下输出，表示你的作业正在运行：
```
[2] + Running find/-name acme-print > /tmp/acme.find &
[1] - Stopped (SIGTSTP) find
```
7. 要将你的作业带回前台，在 shell 提示符处输入 `fg %JOBID`，其中 `JOBID` 是你想带回前台的作业编号。正在运行的命令将出现在屏幕上，指定的作业将再次获得你的键盘和屏幕的控制权。

#### 在 Korn Shell 下杀死后台作业 (kill)
通过作业控制，终止后台作业变得很容易。





# 使用作业控制终止后台作业

1. 在 shell 提示符下，输入 `jobs` 来确定你想终止的作业的作业号。这应该是一个小的数字，不大于显示的作业总数。这**不是** PID 进程标识号。
2. 输入命令 `kill %JOBID`，其中 `JOBID` 是要终止的作业号。
   - 或者，要终止最近的一个作业，你可以输入 `kill %%`。
   - 或者，要终止倒数第二个作业，你可以输入 `kill %2`。

# 在输出前暂停后台作业 (stty)

某些后台作业会运行很长时间，然后显示结果。你可能希望作业在后台继续运行，但在你准备好之前停止输出。

## 在输出前挂起作业

1. 在 shell 提示符下，输入 `stty stop`。这将导致新的后台作业在启动前暂停。这种模式将持续到你注销。
2. 输入你需要的 UNIX 命令并以 `&` 结尾，使其在后台运行。按回车键。
3. 在 shell 提示符下，输入 `jobs`。根据 `jobs` 命令的输出判断后台作业是否正在运行。如果后台作业的状态为 `running`，则它尚未准备好输出。
4. 当 `jobs` 命令显示你的后台作业为 `stopped` 时，它已准备好提供输出。
   - 注意：可以将 `stty stop` 命令放在你的 `.profile` 文件中，这样每次登录时都会设置它。
   - 输入 `fg %JOBID`，其中 `JOBID` 是挂起作业的编号。这将作业带回前台并启动输出，以便你在需要的时间在屏幕上查看输出。

# 第 13 章使用 `tar` 和 `cpio` 保存和恢复文件

## 通 UNIX 设备、磁带和磁盘设备

### 使用 `tar` 备份
- 列出 `tar` 备份文件
- 从 `tar` 备份恢复文件

### 使用 `cpio` 备份
- 列出 `cpio` 备份文件
- 从 `cpio` 备份恢复文件

## 备份用户文件

`备份`文件意味着制作这些文件的副本，以便在需要时能够恢复这些文件。文件可以复制到硬盘上，但通常情况下是备份到磁带或磁盘上，这样在硬盘损坏时可以保护你的数据。备份可以通过网络在另一个系统的磁带驱动器上进行。`归档`是备份的另一种说法。备份到磁带或磁盘的文件称为数据的`归档副本`。这些磁带或磁盘归档也可用于将数据传输到另一个系统。本节讨论了用户如何备份自己的文件，无论是为了保护数据还是为了传输数据。root 用户可以备份整个系统。本章还讨论了系统备份，它与用户备份相似，但有额外的考虑因素。如果你的 UNIX 系统位于计算机运行区域的限制区域，你可能不允许靠近实际计算机。在这种情况下，你无法为了备份目的插入磁带或磁盘。你可能需要提交此类备份请求，并与系统管理员或计算机运行部门安排时间。管理员可能会告诉你，系统上的所有文件都会定期备份，因此你不需要自己进行特殊的备份。如果是这样，当你需要恢复某些文件时，请向他们了解流程。




网络用户可能会对磁带和软盘设备感到困惑。我曾见过 Windows 用户通过 `telnet` 连接到 UNIX，这允许用户登录并运行 UNIX 命令。相反，用户会将软磁盘插入 Windows 软盘驱动器，并尝试通过输入 UNIX 命令来访问 UNIX！这是行不通的，因为 UNIX 命令访问的是 UNIX 系统上的软盘驱动器。网络和 `telnet` 的魔力允许你在远端的 UNIX 系统上运行命令，但任何 UNIX 软盘命令访问的都是那个远程 UNIX 系统上的软盘，而不是你自己的 Windows PC。在这种情况下，你可以使用如 Windows `ftp` 等工具将 UNIX 文件带到本地系统，然后将其备份到本地软盘驱动器。

本章不是为从远程系统访问 UNIX 的网络用户准备的。本章针对那些物理接触 UNIX 计算机本身的用户。要备份文件，请将你自己的软磁盘或磁带插入 UNIX 机器。然后，运行在本章中讨论的 UNIX 命令将文件备份到该软盘或磁带。最后，取出软盘或磁带并存在安全的地方，直到你需要恢复这些文件的备份副本（如果需要的话）。

在插入带有你想要恢复的重要文件的软盘或磁带时要小心。系统上的其他用户，即使是另一个城市的远程用户，也可能启动软盘或磁带操作，从而覆盖你的磁带。软盘和磁带通常有一个小滑块，可以移动以写保护你的介质并防止写入。

### 另需参考
- 有关 `ftp` 文件传输的更多信息，请参见第 583 页
- *UNIX 设备文件*

### UNIX 设备文件
在 UNIX 中，有特殊文件允许你访问物理设备。这些文件被称为*设备文件*（device files）或*设备节点*（device nodes）。如果你将输出重定向到特殊设备文件，输出将发送到物理设备。如果你从特殊设备文件重定向输入，输入（如果有）将来自该设备。某些设备更为复杂，其设备节点只能通过特定方式或特殊程序访问。

按照惯例，所有的特殊设备文件都存储在 `/dev` 目录下。这导致设备文件的完整路径以 `/dev/` 开头，表示这不是一个普通的 UNIX 文件。每个设备文件都是指向该设备驱动程序的指针。*驱动程序*（driver）是一个包含子程序的软件程序，可以根据所需的设备函数进行调用（例如，读、写、回退、寻道等）。

让我们查看 Solaris 2.6 上的一些设备文件。访问软盘的文件恰好包含 diskette 一词（其他 UNIX 系统并非如此）。这些文件实际上是许多设备名称的符号链接，因此我为 `ls` 添加了 `-L` 选项以跟踪符号链接并查看实际设备文件，如下：

```
ls -L /dev/diskette
brw-rw- 1 root sys 36, 2 Apr 10:57 /dev/diskette
brw-rw- 1 root sys 36, 2 Apr 10:57 /dev/diskette0
crw-rw- 1 root sys 36, 2 Apr 27 11:24 /dev/rdiskette
crw-rw- 1 root sys 36, 2 Apr 27 11:24 /dev/rdiskette0
```

在前面的示例中，注意行首的字符（代表文件类型）是字母 `b` 或 `c`。`b` 代表*块*（block）设备文件；`c` 代表*字符*（character）设备文件。字符设备也称为*原始*（raw）设备。它是一个简单一个接一个传递字符的驱动程序。这被称为*顺序访问*（sequential access）。块驱动程序用于更复杂的情况，允许对软磁盘的特定块进行随机访问。某些设备只有字符设备而块设备（例如，磁带机仅允许顺序访问）。

在同一个示例中，注意缺少文件大小。文件大小通常列在组之后、最后访问日期之前。设备文件没有大小，而是有两个用逗号分隔的数字：主号（major number）和设备号（minor number）。在本示例中，列出的所有文件主号均为 36，设备号均为 2。这些设备文件不包含关于设备的代码或数据。事实上，设备文件是完全空的，这就是为什么没有列出大小。访问系统中所有设备的驱动代码链接在一起形成一个巨大的 UNIX 内核。设备文件的主号表示应使用内核中的哪个驱动程序来访问该设备。设备号为驱动程序提供关于该设备的额外信息。

有些人会错误地将 `/dev` 文件从一个 UNIX 系统复制到另一个 UNIX 系统，认为他们正在将驱动代码传输到新系统。由于 `/dev` 文件仅是内核的指针，你可以理解为什么他们的尝试失败了。

### 确定使用什么设备名称
在本章中，我解释了如何使用 `tar` 和 `cpio` 来备份和恢复文件。你可以在所有 UNIX 系统上使用这些命令。然而，你必须确定使用什么设备名称。这因系统而异。最佳做法是联系系统管理员，询问哪些设备名称可用于备份，以及是否有必须遵守的特殊规则。遗憾的是，系统文档通常不涵盖设备名称。但有一些 man 页有助于查找设备名称：

- Solaris：针对软盘设备：`man -s 7D fd`
针对 SCSI 磁带设备：`man st`





# 设备文档

## 手册页引用

- **SCO UNIX OpenServer**: 软磁盘设备：`man fd`。SCSI 磁带设备：`man Stp`。
- **SCO UNIX UnixWare 7**: 软磁盘设备：`man 7 fd`。SCSI 磁带设备：`man 7 tape`。
- **AIX 4.x**: 软磁盘设备：`man fd`。SCSI 磁带设备：`man rmt`。
- **Linux**: 软磁盘设备：`man fd`。SCSI 磁带设备：`man st`。

## 通过关键字查找设备

在其他 UNIX 系统上，如果支持使用 `man -k` 通过关键字查找手册主题，请尝试以下命令来查找可能设备的帮助页：

```bash
man -k flop
man -k disket
man -k tape
man -k scsi
```

在 Solaris 上，使用以下命令：
```bash
man -k tape
```

该命令产生的输出包含以下行：

```
rmt (1m) - remote magtape protocol module | Page 332
st (7d) - driver for SCSI tape devices
stli (8) - Silo Tape Library Interface
```

## 设备名称

在 AIX 4.x 上，有一个非常有用的命令：`lsdev -C`。该命令显示系统上每个设备的信息。以下是该命令的部分输出：

```
hdisk0 Available 04-B0-00-0,0 4.0 GB SCSI Drive
hdisk1 Available 04-B0-00-1,0 4.0 GB SCSI Drive
rmt0 Available 04-B0-00-4,0 4GB Tape Drive
cd0 Available 04-B0-00-5,0 CD-ROM Drive
```

在陌系统中，没有简单的方法可以确定要使用的确切设备名称。我们查看了一些可以使用的命令来获取这些设备名称的线索。再次，最好的建议是询问你的系统管理员或系统中任何使用你想要使用的设备员。

## 磁带驱动

UNIX 系统上常见的磁带机类型是 SCSI 磁带机。这些设备需要计算机中安装 SCSI 控制器卡。然后可以将 SCSI 磁盘驱动器、SCSI 磁带机和 SCSI CD-ROM 驱动连接到 SCSI 控制器。系统管理员必须设置每个新的 SCSI 设备，尽管某些 UNIX 系统在启动时会自动检测新的 SCSI 设备。任何管理设置过程因系统而异。

以下是一些常见的 SCSI 磁带机类型：

- **四分之一英寸盒式 (QIC) 流光磁带**：四分之一是指磁带的宽度。这些磁带机有不同的型号。有些容量仅为 250 MB；有些容量高达 26 GB。许多大型磁带机可以读取在较小 QIC 磁带机上写入的磁带。
- **4-mm DAT**：这种驱动器的常见型号存储 4 GB 原始数据，压缩后高达 8 GB。磁带长度有 90 米或 120 米。更长的磁带可以存储更多数据。磁带有多种样式，如 `DDS` 或 `DDS-II`，因此为你的驱动器获取正确的磁带类型非常重要。
- **8-mm Exabyte 螺旋扫描**：这种驱动机的常用类型容量为 2.3 GB 或 5 GB。9 迹半英寸磁带机通常具有低（800 bpi）、中（1600 bpi）或高（3200 bpi）密度设置。它们也被称为*卷式 (reel to reel)* 驱动器。由于成本原因，除了在政府机构交换或提交数据外，它们很少使用。新磁带机的出现和列表的更新频繁。例如，现在有了 Trevan、`AIT` 和 `DLT` 磁带机。如果你打算购买磁带盒来备份文件，请确保为你的驱动器购买正确的磁带类型和长度。最好的方法记录下当前使用的磁带品牌和型号。

## UNIX 磁带设备名称

SCSI 磁带的 UNIX 驱动名称简单根据其添加到系统的顺序对每个磁带机进行编号。此磁带编号是一个逻辑数字，与任何物理值（如 SCSI 目标 ID 号）都没有关系。以下是某些特定 UNIX 系统的 SCSI 设备名称：

- **Solaris**: `/dev/rmt/0`, `/dev/rmt/1`, `/dev/rmt/2` 等。
- **SCO UNIX OpenServer**: `/dev/rStp0`, `/dev/rStp1`, `/dev/rStp2` 等。
- **SCO UNIX UnixWare 7**: `/dev/rmt/ctape1`, `/dev/rmt/ctape2` 等。
- **AIX 4.x**: `/dev/rmt0`, `/dev/rmt1`, `/dev/rmt2` 等。
- **Linux**: `/dev/st0`, `/dev/st1` 等。





上述列表显示，要在 Solaris 系统上使用第一个磁带驱动器，您可以使用 `/dev/rmt/0`。要使用添加到 SCO UNIX OpenServer 系统中的第二个磁带驱动器，您可以使用 `/dev/rStp1`。

大多数系统允许为特定的磁带驱动器提供多个设备名称。每个名称具有相同的设备号（因为使用相同的内核驱动程序），但具有不同的设备号，以修改磁带驱动器的功能。常见的备用设备名称是不回带磁带设备名称。使用标准磁带设备名称时，访问磁带的 UNIX 命令在磁带操作完成且磁带完全回带之前不会结束。如果您改用不回带磁带设备，则不会执行最后的这个回带操作。这将磁带定位在最后一次访问的文件之后，以便在该点可以读取或写入新文件，磁带驱动器硬件支持此操作。

以下是 SCSI 磁带设备 0 的一些备用名称：

| Solaris | |
| :--- | :--- |
| `/dev/rmt/0` | 标准设备名称 |
| `/dev/rmt/0n` | 不回带设备 |
| `/dev/rmt/0l` | 选择低密度 |
| `/dev/rmt/0m` | 中等密度 |
| `/dev/rmt/0h` | 高密度 |
| `/dev/rmt/0u` | 超高密度 |
| `/dev/rmt/0c` | 压缩 |
| `/dev/rmt/0b` | BSD 行为 |

这些选项可以组合使用。

以下是 `/dev/rmt` 目录下的可用设备文件：

| | |
| :--- |
| `0` |
| `0bn` |
| `0cb` |
| `0cn` |
| `0hb` |
| `0hn` |
| `0lb` |
| `0ln` |
| `0b` |
| `0c` |
| `0cbn` |
| `0h` |
| `0hbn` |
| `0l` |
| `0lbn` |
| `0m` |
| `0mn` |
| `0u` |
| `0un` |
| `0ub` |
| `0un` |
| `0mb` |
| `0mbn` |

| SCO UNIX OpenServer | |
| :--- | :--- |
| `/dev/rStp0` | 标准设备名称 |
| `/dev/nrStp0` | 不回带设备 |
| `/dev/xStp0` | |





# SCO UNIX UnixWare 7 - 第 335 页

发布特殊命令：

| 设备名称 | 描述 | AIX 4.x |
| :--- | :--- | :--- |
| `/dev/rmt/ctape1` | 标准设备名称 | |
| `/dev/rmt/ntape1` | 非回带设备 | |
| `/dev/rmt/nrtape1` | 留存而非回带设备 | |
| `/dev/rmt/utape1` | 关闭时卸载 | |
| `/dev/rmt0` | 低容量，打开时留存，关闭时回带 | Y |
| `/dev/rmt0.1` | | N |
| `/dev/rmt0.2` | | Y |
| `/dev/rmt0.3` | | Y |
| `/dev/rmt0.4` | | Y |
| `/dev/rmt0.5` | | N, N |
| `/dev/rmt0.6` | | N, N |
| `/dev/rmt0.7` | | Y, Y, N |
| `/dev/rmt0` | Linux | N |
| `/dev/st0` | 标准设备名称 | |
| `/dev/nst0` | 非回带设备 | |

磁带在使用前不需要进行格式化。然而，某些应用程序在第一次为此程序使用磁带时必须对其进行初始化，但应用程序应根据需要提示您。应定期对四分之一英寸（QIC）盒磁带进行重新张紧，以确保在读写过程中磁带流转顺畅，从而实现最大的数据可靠性。在使用完非回带设备节点后，您应该在移除磁带之前执行 `rewind` 命令。以下列表提供了在几种类型的 UNIX 系统上对第一个磁带驱动器进行留存或回带的 shell 命令：

```bash
mt -f /dev/rmt/0 retention
mt -f /dev/rmt/0 rewind
```





# 磁带设备管理

| 操作系统 | 命令 |
| :--- | :--- |
| SCO UNIX OpenServer | `tape reten /dev/rStp0`, `tape rewind /dev/rStp0` |
| SCO UNIX UnixWare 7 | `tape reten /dev/rmt/ctape1`, `tape rewind /dev/rmt/ctape1` |
| AIX 4.x | (无保留命令) `mt -f /dev/rmt0 rewind` |
| Linux | `mt -f /dev/st0 retention`, `mt -f /dev/st0 rewind` |

## 磁盘驱动器

### 软磁盘
软磁盘为备份或传输文件及程序提供了方便的方法，但它们存储的数据量远少于磁带备份。常见的软磁盘驱动器是 3.5 英寸软驱器。每张双面高密度软磁盘的容量为 1.44 MB。在过去，你还能找到盒装容量较低的单面或低密度软磁盘，但这些现在已经很罕见。有些系统使用较旧的 5.25 英寸软驱器。双面高密度 5.25 英寸软磁盘只能容 1.2 MB。5.25 英寸软磁盘也曾有容量较低的单面或低密度品种。你可能会遇到较新的 2.88 MB 软磁盘，它们需要特殊的驱动器才能容纳 2.88 MB 的容量。有些 UNIX 系统完全没有软驱。

### UNIX 软磁盘设备名称
`/dev` 目录下通常有若干软磁盘设备文件，用于处理这些单面和低密度磁盘。例如，在 SCO UNIX OpenServer 上，软磁盘设备名称包含 `48`、`96` 或 `135`，表示磁盘每英寸的道数；`ss` 或 `ds` 表示单面或双面；以及 `15`、`18`、`21` 或 `36` 表示每道的扇区数。

以下显示了 SCO UNIX OpenServer 上软磁盘驱动器 `fd0` 的各种设备：

```bash
cd /dev
ls -CF fd0
```

我们可以忽略大多数此类设备名称，因为小于 1.44 MB 的软磁盘已经很少使用了。在以下列表中，我提供了最常见的 1.44 MB 3.5 英寸软磁盘设备文件。我也提供了 2.88 MB 3.5 英寸软磁盘的设备名称，以防你遇到这种扩展容量驱动器。大多数 UNIX 系统现在还提供自动感应软磁盘设备文件，它可以根据软磁盘的格式化容量自动调整。你可以使用这些自动感应设备进行大多数操作，但某些 UNIX 系统不允许在格式化时使用自动感应设备。我在软磁盘文件列表中也包含了格式化软磁盘的完整命令：

| 操作系统 | 设备文件 | 格式化命令 (1.44 MB) |
| :--- | :--- | :--- |
| SCO UNIX OpenServer | `/dev/fd0` (自动感应块设备文件) | `format /dev/diskette` |
| SCO UNIX OpenServer | `/dev/rdiskette` (自动感应字符设备或原始设备文件) | `format /dev/rdiskette` |
| SCO UNIX OpenServer | `/dev/fd013536` (2.88 MB 块设备文件) | `format /dev/fd013536` |
| SCO UNIX OpenServer | `/dev/rfd013536` (2.88 MB 字符设备或原始设备文件) | `format /dev/rfd013536` |

**注意：** 在 Solaris 下，有一个卷管理守护进程 (`vold`) 想要完全控制所有软磁盘和 CD-ROM 驱动器。在 `vold` 运行时，你无法从命令行访问这些设备。





| 设备路径 | 描述 | 命令 |
| :--- | :--- | :--- |
| `/dev/rfd0135ds18` | 1.44 MB 字符设备或原始设备文件 | 使用 `format /dev/rfd0135ds18` 格式化 1.44 MB 磁盘 |
| SCO UNIX UnixWare 7 | | |
| `/dev/dsk/f0t` | 自动感应块设备文件 | |
| `/dev/rdsk/f0t` | 自动感应字符设备或原始设备文件 | |
| `/dev/dsk/f03et` | 2.88 MB 块设备文件 | |
| `/dev/rdsk/f03et` | 2.88 MB 字符设备或原始设备文件 | |
| `/dev/dsk/f03ht` | 1.44 MB 块设备文件 | |
| `/dev/rdsk/f03ht` | 1.44 MB 字符设备或原始设备文件 | 使用 `format /dev/rdsk/f03ht` 格式化 1.44 MB 磁盘 |
| AIX 4.x | | |
| `/dev/fd0` | 自动感应块设备文件 | |
| `/dev/rfd0` | 自动感应字符设备或原始设备文件 | |
| `/dev/fd0.36` | 2.88 MB 块设备文件 | |
| `/dev/rfd0.36` | 2.88 MB 字符设备或原始设备文件 | |
| `/dev/fd0.18` | 1.44 MB 块设备文件 | |
| `/dev/rfd0.18` | 1.44 MB 字符设备或原始设备文件 | 使用 `format -d /dev/rfd0` 格式化 1.44 MB 磁盘 |
| 第 339 页 | Linux | |
| `/dev/fd0` | 自动感应块设备文件（无） | |
| `/dev/rfd0` | 自动感应字符设备或原始设备文件（无） | |
| `/dev/fd0E2880` | 2.88 MB 块设备文件（无） | |
| `/dev/rfd0E2880` | 2.88 MB 字符设备或原始设备文件（无） | |
| `/dev/fd0H1440` | 1.44 MB 块设备文件（无） | |
| `/dev/rfd0H1440` | 1.44 MB 字符设备或原始设备文件（无） | 使用 `format /dev/fd0H1440` 格式化 1.44 MB 磁盘 |
| 选择 *tar* 或 *cpio* 或其他备份程序 | | |





`tar` 和 `cpio` 是所有类型 UNIX 系统中常见的两种传统工具，它们允许你保存和恢复文件。UNIX 系统上还有许多其他备份工具，它们比 `tar` 或 `cpio` 更好用且更容易上手。它们的名称包括 `dump`、`ufsdump`、`Lone Tar`、`BackupEdge`、`bru`、`mksysb`、`Solaris Data Backup`、`ARCserve`、`Legato Networker` 等。其中某些是特定类型 UNIX 的标准工具，某些是从第三方提供的付费软件。对于自己的 UNIX 系统，你应该调查适用于你类型 UNIX 的可用备份程序，并选择提供最全功能的一个。

### 警告：恢复完整备份并非易事

你可能认为由于你有了完整备份，你的系统就是安全的。然而，在许多类型的 UNIX 上，在恢复备份之前，你必须重新安装并重新配置操作系统（这可能听起来很困难，甚至更难）。在评估备份程序时，应为能够在紧急情况下自动恢复整个系统的工具打出高分。

### 既然有更好的程序，为什么还要考虑 tar 或 cpio？

答案是，`tar` 和 `cpio` 很有价值，因为你几乎在所有的 UNIX 系统上都能找到它们。假设你正在奔波，将访问十个不同的 UNIX 系统，并希望每个站点加载一个演示程序。你会带什么种类型的演示程序备份？如果这些是未知系统，最稳妥的方法是带上演示程序的 `tar` 或 `cpio` 备份。由于同样的原因，如果你需要将软件发送到许多不同的 UNIX 系统上，`tar` 或 `cpio` 是一个明智的选择。

如果你从支持多种类型 UNIX 系统的供应商那里接收软件，收到的软件很可能是 `tar` 或 `cpio` 格式。

学习 `tar` 和 `cpio` 对你来说很有价值，因为你可能会收到任何形式的数据。然而，`tar` 是一个更容易使用的工具，许多供应商选择这种格式来发送他们的软件产品。`tar` 对于备份特定文件或目录非常方便。它可以递归地备份任何目录，这意味着会备份该目录下的所有文件和子目录，以及这些子目录的所有文件和子目录，以此类推。

在互联网上，你有时会看到扩展名为 `.tar` 的文件，这表示一个 tar 归档。这意味着使用 `tar` 将一组文件保存了一个单一磁盘文件，这样只需要下载一个文件而不是多个文件。你可能还会看到扩展名 `.tgz`，它是一个经过 `gzip` 压缩的 tar 归档，这样下载速度会更快。

`tar` 在历史上具有一些局限性，这使得它不适用于备份整个系统（参见后文章节）。然而，`cpio` 在备份内容方面提供了更好的灵活性和控制，但这使得 `cpio` 使用起来更复杂。使用 `cpio`，你可以选择只备份目录的一部分或选择排除目录的一部分，而 `tar` 无法做到。在从备份中恢复文件时，`cpio` 提供的灵活性比 `tar` 大得多。`cpio` 允许你进行增量备份，这意味着你备份自上次备份以来更改的文件；而 `tar` 不。尽管 `cpio` 增加了复杂度，但它是执行完整备份的更好选择，特别是在旧的 UNIX 系统上。

后续章节将讨论如何在系统备份和恢复中使用 `tar` 和 `cpio`。

### 使用 tar 备份和恢复文件

你会发现，关于 `tar` 的这一节使用的措辞与后续关于 `cpio` 的章节大部分相同。这两个命令具有相似的功能，仅有某些特定细节有所不同。备份目录子树

`tar` 是 tape archive（磁带归档）实用工具，因为典型的 UNIX 备份是在磁带驱动上进行的。`tar` 也可以备份到软磁盘或磁盘文件。这是一个备份一个完整目录的 basic `tar` 命令示例：

```bash
$ cd /usr/fred/projects $ tar cvf /dev/XXX? .
```

首先使用 `cd` 切换到要备份的目录。`tar` 会递归地备份该目录，自动包含所有文件、子目录及其内容。以下是该 `tar` 命令中其他元素的描述：





# Tar 命令

## 选项

- `c`: 创建备份。在此 tar 选项列表中，第一个字母必须是 `c`、`x` 或 `t`。
- `v`: 详细模式（显示正在备份的文件名）。
- `f`: 允许指定要备份到的设备或文件。
- `/dev/XXX?`: 非常重要，必须将此替换为你想要备份的磁带或软磁盘设备名称。（我们在 ... 章节中介绍过这些设备名称。）你也可以指定一个磁盘文件名来存放 tar 归档。
- `.`: 点是一个相对路径，表示当前目录为要备份的目录。某些用户会错误地在此处使用星号 `*` 而不是点，但星号不会备份该目录下的隐藏文件（以点开头的文件）。

## 使用示例

给 tar 一个有效的 `/dev` 名称。不要假设在某一个系统上有效的设备在另一个系统上也能工作。当你输入 tar 命令时，请双倍检查用于备份路径的 `/dev` 拼写。如果你使用了错误的设备名称或拼写错误，tar 将把你的文件备份到磁盘文件中，这可能会耗尽可用的磁盘块并导致系统崩溃。

当你运行此 tar 命令时，你可能会看到类似下面的输出：

```bash
$ cd /usr/fred/projects $ tar cvf /dev/XXX? .
a ./0K
a ./acme/ 0K
a ./acme/report6 1K
a ./pegasus/ 0K
a ./pegasus/1997/ 0K
a ./pegasus/1997/expenses 1K
a ./pegasus/1997/sales 4K
a ./pegasus/1998/ 0K
a ./pegasus/1998/expenses 8K
a ./pegasus/1998/sales 10K
```

由于我们使用了 tar 的 `v` 选项，我们可以看到每个正在备份的目录和文件名，以及文件的大小。每行开头的字母 `a` 告诉我们文件正在被归档（保存到备份软磁盘或磁带上）。如果数据量很大，备份可能需要数小时才能完成。一旦 tar 备份完成，我们可以包含备份的介质称为 tar 归档（tar archive）。根据介质类型，我们也可以将备份称为 tar 软磁盘（tar diskette）或 tar 磁带（tar tape）。

如果你省略了 `v` 选项，在 tar 备份期间不会显示文件名：

```bash
$ cd /usr/fred/projects $ tar cf /dev/XXX? .
```

## 备份指定的目录或文件

你可以使用以下命令为 tar 指定特定的文件或目录列表进行备份：

```bash
$ cd /usr/fred/projects $ tar cvf /dev/XXX? ./acme* ./reports/1997 ./reports/1998
```

`./acme*` 说明 shell 通配符可以用来生成文件列表，在这种情况下，这些是所有以 acme 开头的文件和目录。`./reports/1997` 说明可以指定目录。这些目录会被递归地备份。上一个示例指定了要备份的路径，这是推荐的做法。

### 另参
有关星号 (**) 通配符的更多信息，请参第 232 页。

## 列出 tar 归档的目录

输入以下命令向标准输出显示 tar 归档的内容（保存在该 tar 软磁盘或磁带上的文件名）：

```bash
$ tar tvf /dev/XXX?
drwxr-xr-x 1001/10 0 Apr 28 21:23 1998 ./
dr-xr-x 1001/10 0 Apr 28 21:24 1998 ./acme/
-r--r--r-- 1002/10 29 Apr 28 21:24 1998 ./acme/report6
drwxr-xr-x 1001/10 0 Apr 28 21:25 1998 ./pegasus/
drwxr-xr-x 1001/10 0 Apr 28 21:26 1998 ./pegasus/1997/
-rw-r--r-- 1001/10 135 Apr 28 21:26 1998 ./pegasus/1997/expenses
-rw-r--r-- 1001/10 3281 Apr 28 21:27 1998 ./pegasus/1997/sales
```

`t` 显示备份的目录列表。在此 tar 选项列表中，第一个字母必须是 `c`、`x` 或 `t`。此操作不会保存或恢复任何文件。`/dev/XXX?` 应该替换为 tar 设备或备份文件名。当你运行此 tar 命令时，你可能会看到如下所示输出：





# 销售 / 支出

```
drwxr-xr-x 1001/10         0 Apr 28 21:27 1998 ./pegasus/1998/
-rw-r--r-- 1001/10      7995 Apr 28 21:26 1998 ./pegasus/1998/
-rw-r--r-- 1001/10      9463 Apr 28 21:27 1998 ./pegasus/1998/
```

## 销售

`$ 让我选取此输出的第三行并解释每个字段。这一行以 `report6` 结尾。

```
-r--r--r--  这是文件类型和权限，就像 `ls -l` 显示的一样。
1002/10 1002 表示该文件的所有者（UID 号）。10 表示文件的所属组（GID 号）。
29  这是文件以字节为单位的大小。
Apr 28 21:24 1998 这是文件的最后修改日期和时间。
./acme/report6 这是备份中的文件名。
```

如果你省略了 `v` 选项，则只显示文件名：

```
$ tar tf /dev/XXX? ./acme
./acme/report6
./pegasus/
./pegasus/1997/
./pegasus/1997/expenses
./pegasus/1997/sales
./pegasus/1998/
```

请注意，列出目录所需的时间与最初写入 `tar` 归档的时间相同。

## 使用 tar 恢复归档

为了使用 `tar` 备份中的任何文件，我们必须首先将所需的文件或多个文件从 `tar` 磁带或软磁盘恢复到硬盘上。然而，在使用 `tar` 恢复一个大型 `tar` 归档之前，有几个重要的细节需要检查。以下章节将介绍此类问题，例如检查磁盘空闲块、绝对和相对路径、规划文件恢复的位置、绕过绝对文件名的限制以及切换到正确的目录。

### 检查磁盘空闲块

检查各种文件系统中的磁盘空闲块是非常重要的，因为任何 UNIX 文件系统如果用尽了可用块，应用程序可能会报错，这可能导致数据库处于损坏状态。如果根文件系统用尽了块，整个 UNIX 系统可能会崩溃。同样，任何文件系统中的可以创建的文件数量都是有限的。`df` 显示每个文件系统还可以创建多少个文件。在恢复归档之前，请先检查文件系统是否即将用尽文件。

以下是 `df` 命令的示例：

```
$ df /dev/dsk/c0t0d0s0  154776 blocks 46382 files
usr             /dev/dsk/c0t0d0s6  240348 blocks 254137 files
/proc               0 blocks 940 files
/dev/fd             0 blocks 0 files
/export/home    /dev/dsk/c0t0d0s3  3456112 blocks 427351 files
/opt            /dev/dsk/c0t0d0s5  382996 blocks 268002 files
/tmp             swap  198216 blocks 9636 files
/export/home/data /dev/dsk/c0t0d1s0  8231524 blocks 933162 files
```

你将在 `df` 中为你的 UNIX 系统中存在的每个文件系统看到一行。在上面的示例中，有八个文件系统。每个文件系统通过行开头的目录来识别。你可以通过查找 `df` 中最长的起始目录来确定目录位于哪个文件系统。例如，`/export/home/data/acme` 位于 `/export/home/data` 文件系统，而不是 `/export/home` 文件系统，因为你使用了最长的 `df` 目录。

## 另阅

有关 `df` 和文件系统的更多信息，请参阅第 74 页。





# 检查绝对路径与相对路径

在从 tar 备份中恢复任何文件之前，请列出 tar 目录并检查文件名是否以斜杠（`/`）开头。绝对路径或全路径以斜杠开头。相对路径则不以斜杠开头。

查看以下示例：

```bash
$ tar tvf /dev/XXX? drwxr-xr-x 1001/10      0 Apr 28 21:23 1998 /mori/
dr-xr-x--- 1002/10      0 Apr 28 21:24 1998 /mori/acme/
-r--r--r-- 1002/10      29 Apr 28 21:24 1998 /mori/acme/report6
$ tar tvf /dev/XXX? 1001/10      0 Apr 28 21:25 1998 /mori/pegasus/
drwxr-xr-x 1001/10      0 Apr 28 21:26 1998 /mori/pegasus/1997/
-rw-r--r-- 1001/10      135 Apr 28 21:26 1998 /mori/pegasus/1997/expenses
-rw-r--r-- 1001/10      3281 Apr 28 21:27 1998 /mori/pegasus/1997/sales
drwxr-xr-x 1001/10      0 Apr 28 21:27 1998 /mori/pegasus/1998/
-rw-r--r-- 1001/10      7995 Apr 28 21:26 1998 /mori/pegasus/1998/expenses
-rw-r--r-- 1001/10      9463 Apr 28 21:27 1998 /mori/pegasus/1998/sales
```

在这个示例中，所有文件名都以斜杠开头（例如，`/mori/acme/report6`）。因此，上面的 tar 包含了绝对路径。

现在考虑这个示例：

```bash
$ tar tvf /dev/XXX dr-xr-x--- 1002/10      0 Apr 28 21:24 1998 ./acme/
-r--r--r-- 1002/10      29 Apr 28 21:24 1998 ./acme/report6
drwxr-xr-x 1001/10      0 Apr 28 21:25 1998 ./pegasus/
drwxr-xr-x 1001/10      0 Apr 28 21:26 1998 ./pegasus/1997/
-rw-r--r-- 1001/10      135 Apr 28 21:26 1998 ./pegasus/1997/expenses
-rw-r--r-- 1001/10      3281 Apr 28 21:27 1998 ./pegasus/1997/sales
drwxr-xr-x 1001/10      0 Apr 28 21:27 1998 ./pegasus/1998/
-rw-r--r-- 1001/10      7995 Apr 28 21:26 1998 ./pegasus/1998/expenses
-rw-r--r-- 1001/10      9463 Apr 28 21:27 1998 ./pegasus/1998/sales
```

在前面的示例中，所有文件名都以点斜杠（`./`）开头。因为它们不是斜斜开头，所以它们是相对路径而不是绝对路径。

最后，来看这个示例：

### 文件将恢复到何处

如果路径以斜杠开头，tar 通常会将该文件仅恢复到该绝对路径。这可能是危险的，因为我们得到的是每个文件的旧版本，会丢失自备份以来所做的任何更新。在恢复此文件之前，最好的做法是将该文件的当前版本复制一份，以确保保留所有更新。

例如，假设我们显示目录表，并在输出中看到这一行：
`-rw-r--r-- 1001/10 135 Apr 28 21:26 1998 /mori/pegasus/1997/expenses`

然而，如果 tar 归档文件使用相对路径，我们可以将文件恢复到许多不同的目录。这非常有用，例如当我们想从 tar 备份的旧文件中查找信息，而不覆盖该文件的当前版本时。在这种情况下，我们将备份文件恢复到临时工作目录，查找所需信息，完成后删除旧文件。

另参
关于相对路径和绝对路径的更多信息，请参阅第 49 页。





```
-rw-r--r-- 1001/10      135 Apr 28 21:26 1998 ./mori/pegasus/1997/expenses
-rw-r--r-- 1001/10      135 Apr 28 21:26 1998 mori/pegasus/
```

无论哪种情况，我们的备份文件使用的都是相对路径。你可以通过在要恢复的相对路径开头插入当前目录，来预测 `tar` 将恢复这些文件的位置。

例如，如果我的当前目录是 `/tmp`，那么 `tar` 将把上节中的 `expenses` 文件恢复到这个绝对路径：

```
/tmp/mori/pegasus/1997/expenses
```

另一个例子是，如果我的当前目录是 `/mori/pegasus`，那么 `tar` 将把上节中的 `expenses` 文件恢复到这个绝对路径：

```
/mori/pegasus/mori/pegasus/1997/expenses
```

最后，如果我的当前目录是 `/`（根目录），那么 `tar` 将把上节中的 `expenses` 文件恢复到这个绝对路径：

```
/mori/pegasus/1997/expenses
```

总结来说，如果 `tar` 归包包含绝对路径，`tar` 将这些文件（从磁带或软磁盘）恢复到它们的原始位置。如果归包包含相对路径，`tar` 将通过将当前目录添加到 `tar` 路径中来决定恢复文件的路径。

## 考虑绝对文件名的变解决方案

如果你使用绝对文件名创建 `tar` 归包，你（通常）只能将这些文件恢复到它们的原始位置。这是 `tar` 一个既伟大又令人沮丧的限制。因此，`tar` 的文档通常建议你在执行 `tar` 备份时使用相对路径。在本书之前使用 `tar` 备份目录的章节中，我只了如何使用相对路径进行备份。

在 Linux/GNU 系统下，`tar` 在创建 `tar` 备份时会自动剥离开头的斜杠，因此 `tar` 归包始终使用相对路径。然而，你仍可能通过两种方式在 Linux/GNU `tar` 下遇到绝对路径带来的烦恼：你可以使用特殊的 Linux/GNU `tar -P` 选项来保留开头的斜杠，或者你可能会收到来自另一个系统的写入绝对路径的磁带。

SCO UNIX 下 `tar` 有一个非常好的 `-A` 选项，可以在恢复时抑制开头的斜杠。这样你就可以像处理 `tar` 归包中的相对路径一样恢复绝对路径。你可以将 `-A` 选项添加到 `tar` 选项列表的任何位置，只要它在初始 `x` 选项之后即可。我在 AIX、Solaris 或 Linux/GNU 上没有找到这个 `-A` 选项。

如果 `tar` 中的绝对路径对你来说大问题，请查看你的系统是否支持 `pax` 命令，它能够读取 `tar` 归包并支持通过 `-s` 选项修改文件名。

### 切换到正确的目录

如果 `tar` 归包中的文件使用绝对路径，那么在执行 `tar restore` 命令之前切换到哪个目录都没有区别。

如果 `tar` 归包中的文件是相对的，那么在使用 `tar` 恢复相对文件时，最关键且最危险的决定之一就是在开始 `tar restore` 之前切换到哪个目录。因为你正在恢复一个或多个旧归包文件，存在无意覆盖这些文件当前版本的危险。要确定切换到哪个目录，请比较磁带上的路径与你想恢复文件位置的绝对路径：

**示例 1**
- `tar` 归包中的路径：`./mori/pegasus/1997/expenses`
- 恢复后的目标绝对路径：`/tmp/restoredata/mori/pegasus/1997/expenses`
- 执行 tar restore 之前切换的目录：`/tmp/restoredata`

**示例 2**
- `tar` 归包中的路径：`mori/pegasus/1997/expenses`
- 恢复后的目标绝对路径：`/mori/pegasus/1997/expenses`（即我们想将文件恢复到原始位置）
- 执行 tar restore 之前切换的目录：`/`

**示例 3**
- `tar` 归包中的路径：`mori/pegasus/1997/expenses`
- 恢复后的目标绝对路径：`/pegasus/1997/expenses`
- 执行 tar restore 之前切换的目录：我们无法仅通过设置当前目录来完成此示例。可以通过更复杂的步骤完成，例如创建一个指向根目录 (`/`) 的符号链接目录 `mori`，或者将文件恢复到某个临时目录然后移动到目标位置。

### 将所有文件恢复到原始目录




你可能不想使用最简单的恢复方法，即将所有文件放回它们所在的地方。如果你这样做，就会毁掉那些包含最新信息的文件，并用备份中带有旧信息的文件来替换它们。现在你明白为什么我之前说你可能不想这样做了。这种操作很少执行。例如，如果某次重大更新操作出现问题，导致所有当前文件都损坏了，你可能希望从备份中从较旧但未损坏的版本恢复所有文件。

要将 `tar` 备份中的所有文件恢复到原始目录，请切换到你最初创建备份的目录。然后执行此处所示的 `tar restore` 命令：

```bash
cd /usr/fred/projects 
tar xvf /dev/XXX?
```

`/usr/fred/projects` 只是一个示例目录名。请替换为你创建备份的目录。如果 `tar` 归包包含绝对路径，那么你切换到哪个目录都无关。

`x` 意味着从备份中提取文件。此 `tar` 选项列表中的第一个字母必须是 `c`、`x` 或 `t`。提取（恢复）文件始终是一个危险的操作，因为你必须确保不会覆盖错误的文件。

`/dev/XXX?` 应该替换为你的 `tar` 归包的文件或设备名称。

这是一个示例显示了运行此命令时屏幕的状况：

```bash
cd /usr/fred/projects
tar xvf /dev/XXX?
x ., 0 bytes, 0 tape blocks
x ./acme, 0 bytes, 0 tape blocks
x ./acme/report6, 29 bytes, 1 tape blocks
x ./pegasus, 0 bytes, 0 tape blocks
x ./pegasus/1997, 0 bytes, 0 tape blocks
x ./pegasus/1997/expenses, 135 bytes, 1 tape blocks
x ./pegasus/1997/sales, 3281 bytes, 7 tape blocks
x ./pegasus/1998, 0 bytes, 0 tape blocks
x ./pegasus/1998/expenses, 7995 bytes, 16 tape blocks
x ./pegasus/1998/sales, 9463 bytes, 19 tape blocks
```

注意每一行都以 `x` 开头，表示该行显示的文件是从 `tar` 归包提取到磁盘的。

### 将所有文件恢复到不同的目录

请注意，从 `tar` 归包将所有文件恢复到不同目录的过程仅在 `tar` 归包中包含相对路径时才可用。请前面的章节以检查绝对与相对路径，检查磁盘空块，并选择一个有大量可用块的文件系统。然后切换到正确的目录。这是一个示例：

```bash
cd /tmp
tar xvf /dev/XXX?
x ., 0 bytes, 0 tape blocks
x ./acme, 0 bytes, 0 tape blocks
x ./acme/report6, 29 bytes, 1 tape blocks
x ./pegasus, 0 bytes, 0 tape blocks ./pegasus/1997, 0 bytes, 0 tape blocks
x ./pegasus/1997/expenses, 135 bytes, 1 tape blocks
x ./pegasus/1997/sales, 3281 bytes, 7 tape blocks
x ./pegasus/1998, 0 bytes, 0 tape blocks
x ./pegasus/1998/expenses, 7995 bytes, 16 tape blocks
x ./pegasus/1998/sales, 9463 bytes, 19 tape blocks
```

在这个示例中，`tar` 备份中的 `acme` 和 `pegasus` 目录被恢复到 `/tmp` 目录。如果另一个文件系统有足够的可用磁盘块，你可以选择 `/tmp` 以外的目录。再次警告：如果 `tar` 归包包含绝对路径，你的当前目录将被忽略，文件将恢复到它们的原始位置，这可能是灾难性的！

### 仅恢复选定的目录或文件

如示例所示，可以只恢复选定的目录或文件。重要的是要按照 `tar` 目录列表中出现的精确格式指定目录或文件，包括任何前导斜杠 (`/`) 或点斜杠 (`./`）。任何目录都会被递归恢复。考虑以下命令：

```bash
cd desired-dir
tar xvf /dev/XXX? ./acme/report6 ./pegasus/1997
```

`desired-dir` 应该替换为你想要执行 `tar` 命令的目录。`/dev/XXX?` 应该替换为 `tar` 文件或设备。`./acme/report6` Illust 了如何恢复一个文件。`./pegasus/1997` Illust 了如何恢复一个目录及其所有的文件和子目录。注意，恢复选定文件花费的时间与最初写入 `tar` 归包的时间一样。

### 设置和使用 tar 备份设备表

许多 Solaris 和 SCO UNIX 等 UNIX 系统允许将常用的 `tar` 设备放在名为 `/etc/default/tar` 的文件中。这是来自 Solaris 2.6 的该文件示例：

```
# device block size archive0=/dev/rmt/0 20
archive1=/dev/rmt/0n 20
archive2=/dev/rmt/1 20
archive3=/dev/rmt/1n 20
archive4=/dev/rmt/0 126
archive5=/dev/rmt/0n 126
archive6=/dev/rmt/1 126
archive7=/dev/rmt/1n 126
```



系统管理员可以使用常用的 tar 设备名称来替换此文件中显示的设备名称。这允许在 `tar` 命令中使用单个数字来指定目标设备：

```bash
tar cv2 .
```

在上述示例中，`2` 指的是 `/etc/default/tar` 中的 `archive2` 条目。根据上方的 `/etc/default/tar` 文件，上述 tar 命令等同于以下命令：

```bash
tar cvf /dev/rmt/1 .
```

如果没有指定数字，Solaris 默认使用 `archive0` 设备。SCO UNIX 则查找以 `archive=` 开头的行。对于最常用的 tar 设备，请使用此默认情况：

```bash
tar cv .
```

### 设置 tar 块大小（Blocking Size）

`tar` 允许使用 `b` 选项设置块大小，范围为每条磁带记录 1 到 20 块（每块 512 字节）。如果未指定 `b` 选项，默认值为 20。`tar` 在 UNIX 命令中的独特之处在于，所有的选项字母都先指定，然后按照选项字母的顺序列出这些选项的任何参数：

```bash
tar cvfb /dev/XXX? 10 .
```

注意在上述命令中，`f` 选项指定在 `b` 选项之前，因此 `/dev/XXX?`（`f` 选项的参数）必须在 `10`（`b` 选项的参数）之前指定。

指定 `b` 选项的唯一情况是尝试读取一条以非标准默认值 20 写入的磁带。

### 局限性

`tar` 在历史上存在许多局限性。新版本的 `tar` 移除了其中许多限制，但你仍应该意识到这些问题并进行测试。

-   注意多卷备份（即超过一盘磁带容量的 tar 备份）。旧版本的 `tar` 不允许延续到第二盘磁带，或者无法可靠地处理这种情况。在使用它或将每组文件备份到单盘磁带之前，请进行彻底测试。
-   `tar` 不备份目录。它会在恢复时根据需要创建目录，但所有者、组和权限与原先不同。
-   `tar` 不备份空目录。只有当有文件需要恢复到该目录时，它才会创建目录。
-   `tar` 不备份 `/dev` 设备文件。这使得 `tar` 成为完整系统备份的糟糕选择。
-   `tar` 无法从磁带坏点之后恢复文件。

### 使用 cpio 备份和恢复文件

你会发现这一节关于 `cpio` 的内容使用了与之前 `tar` 章节大部分相同的表述。这两个命令的功能相似，只有某些特定细节和示例在两个章节之间有所。`tar` 和 `cpio` 章节本身是完整的，彼此之间复杂的引用。

#### 备份目录子树

`cpio` 代表 *copy in/out*（输入/输出），它允许你将文件备份到磁带、软磁盘或磁盘文件。以下是一个备份一个完整目录的 Basic `cpio` 命令示例：

```bash
cd /usr/projects
find . -print | cpio -ocvaB > /dev/XXX
```

首先使用 `cd` 切换到备份的目录。然后使用 `find` 命令将所有路径名传递给 `cpio` 进行备份。以下是 `cpio` 命令其他元素的描述：

-   `$` 代表 shell 提示符。你的 shell 可能有所不同。
-   `find . -print`: 此 `find` 命令列出当前目录下所有文件和子目录的相对路径。
-   `cpio`: 一个通过执行输入或输出来备份文件的 UNIX 命令。此 `cpio` 归档通常保存在磁带或软磁盘上，也可以保存在磁盘文件中
-   `-ocvaB`: `cpio` 命令的选项。逐个查看每个字母：
-   `o`: 将文件输出到归档中。`cpio` 的第一个选项字母应该是 `i`（输入）或 `o`（输出）。




-   写入 ASCII 头部以提高移植性，以便在另一个系统上读取此磁带。
-   `v`: 详细模式（显示正在备份的文件名）。
-   `a`: 将每个备份文件的最后访问日期重置为运行 `cpio` 之前的状态。
-   `B`: 设置磁带块大小为 5120 字节。某些磁带（如 `DAT` 磁带或 `Exabyte` 磁带）需要大于 1 的块大小。
-   `/dev/XXX`: 非常重要的是将其替换为你想要备份的磁带或磁盘设备名称（我们在本章开头介绍过这些设备名称）。你也可以指定一个磁盘文件名来存储 `cpio` 归包。

当你运行此 `cpio` 命令时，你可能会看到如下输出：

```bash
$ cd /usr/fred/projects $ find . -print | cpio -ocvaB > /dev/XXX?
acme
acme/report6
pegasus
pegasus/1997
pegasus/1997/expenses
pegasus/1997/sales
pegasus/1998
pegasus/1998/expenses
pegasus/1998/sales
50 blocks
```

由于我们使用了 `v` 选项，可以看到每个正在备份的目录和文件。如果数据量很大，备份可能需要几小时才能完成。`cpio` 备份完成后，我们可以包含备份的介质称为 `cpio` 归包。根据介质类型，我们也可以将其称为 `cpio` 磁盘或 `cpio` 磁带。注意在备份结束时，`cpio` 会告诉你备份占用了多少块（在本例中为 50 blocks）。在磁带标签上记录这个数字是一个好主意。如果你想恢复这块磁带，你就知道硬盘上需要多少空闲块了。

如果你省略了 `v` 选项，则在 `cpio` 备份期间不会显示文件名，只在最后显示备份大小：

```bash
$ cd /usr/fred/projects $ find . -print | cpio -ocaB > /dev/XXX?
50 blocks
```

`cpio` 还允许使用 `V` 选项，它会在每备份一个文件时仅打印一个点（.）。这允许你观察备份进度，并确保备份正在进行，而不会因为输出过多拖慢备份速度：

```bash
$ cd /usr/fred/projects $ find . -print | cpio -ocaB > /dev/XXX?
..........
50 blocks
```

### 备份指定的目录或文件

`cpio` 只备份你通过管道传递给它的文件名。如果你给它一个目录名，它只会备份该目录而不包含其内容。要备份整个目录，你必须使用像 `find` 的工具来提供该目录内的所有文件路径。我们可以这样备份选定的单个文件：

```bash
$ cd /usr/fred/projects $ ls ./acme* ./pegasus/report7 cpio -ocaB > /dev/XXX?
```

`ls` 列出了由 `cpio` 备份的文件。这在 Linux/GNU 系统上可能不起作用，因为 `ls` 可能会在文件名结尾添加特殊指示。`./acme*` 说明了 Shell 通配符可以用于生成文件列表（在这种情况下是所有以 acme 开头的文件）。`./pegasus/report7` 说明了另一个要备份的文件。上一个示例指定了要备份的相对路径，这是推荐的操作。

我们可以通过如下方式将多个目录备份到 `cpio`：

```bash
$ cd /usr/fred/projects $ ( find ./expenses -print | find ./pegasus -print ) cpio -ocaB > /dev/XXX?
```

括号 `()` 用于组合多个 `find` 命令并将合并后的输出发送给 `cpio`。行开头的大于符号 `>` 是 PS2 提示符。Shell 会打印此符号（而不是用户），以表示它正在等待上一行开始的命令。

我们可以通过如下方式备份单个文件和完整目录：

```bash
$ cd /usr/fred/projects $ ( echo ./acme* ./pegasus/report7; find ./expenses -print; find ./pegasus -print ) cpio -ocaB > /dev/XXX?
```

然后我们可以如下方式使用 `grep -v` 排除选定的文件：

```bash
$ cd /usr/fred/projects $ ( echo ./acme* ./pegasus/report7; find ./expenses -print; find ./pegasus -print ) | grep -v /tmp/; grep -v junk cpio -ocaB > /dev/XXX?
```





前面的示例备份了以下文件：

- 当前目录下所有以 `acme` 开头的文件
- `pegasus` 子目录下的 `report7`
- `expenses` 目录下的所有文件和目录
- `pegasus` 目录下的所有文件和目录

然而，从上述文件中，从备份中排除以下内容：

- 路径名中包含 `/tmp/` 的任何文件或目录
- 路径名中包含 `junk` 的任何文件或目录

# 列出 cpio 存档的目录列表

输入以下命令来向标准输出显示 `cpio` 存档的内容（已保存在此 `cpio` 磁磁盘或磁带上的文件名）。

```bash
cpio -itcvB < /dev/XXX
```

在此命令中，`i` 表示从已创建的 `cpio` 存档中输入。`cpio` 选项列表中的第一个字母必须是 `i` 或 `o`。`t` 显示备份的目录列表。此操作不会保存或恢复任何文件。

在某些 UNIX 系统上，`cpio` 会自动检测磁带是否在使用 `c` 选项写入的，因此从磁带读取时不需要 `c` 选项。在其他 UNIX 系统上，如果你在 `cpio` 上使用 `c` 选项，会报错。

当你运行此 `cpio` 命令时，可能会看到类似这样的输出：

```bash
cpio -itcvB < /dev/XXX
dr-xr-x 4 mori staff 0 Apr 28 22:23 1998 .
dr-xr-x 2 jane 0 Apr 28 22:24 1998 acme
-r--r-- 1 jane staff 29 Apr 28 22:24 1998 acme/report6
dr-xr-x 4 mori staff 0 Apr 28 22:25 1998 pegasus
-rw--r-- 1 mori staff 135 Apr 28 22:26 1998 pegasus/expenses
-rw--r-- 1 mori staff 3281 Apr 28 22:27 1998 pegasus/sales
dr-xr-x 2 mori staff 0 Apr 28 22:27 1998 pegasus
-rw--r-- 1 mori staff 7995 Apr 28 22:26 1998 pegasus/expenses
-rw--r-- 1 mori staff 9463 Apr 28 22:27 1998 pegasus/sales 50 blocks
```

此输出包含与 `ls -l` 显示相同的字段。

如果省略了 `v` 选项，则只显示文件名：

```bash
cpio -itcB < /dev/XXX
acme/report6
pegasus/1997
pegasus/1997/expenses
pegasus/1997/sales
pegasus/1998/expenses
pegasus/1998/sales 50 blocks
```

注意，列出目录列表所需的时间与最初创建 `cpio` 存档的时间一样长。

# 使用 cpio 恢复存档

为了使用 `cpio` 备份中的任何文件，我们必须先将所需的文件或文件从 `cpio` 磁带或磁磁盘恢复到硬盘。在使用 `cpio` 恢复大型 `cpio` 存档之前，有几个细节需要检查。以下章节将解决这些问题，如检查磁盘空块、绝对路径和相对路径、规划文件恢复的位置、解决绝对限制以及切换到正确的目录。

## 检查磁盘空块

检查各种文件系统中的磁盘空块是非常重要的，因为如果任何 UNIX 系统用尽了可用磁盘块，应用程序可能会报错并终止，这可能导致数据库损坏。如果根文件系统用尽了块，整个 UNIX 系统可能会崩溃。

请回顾上一节“检查磁盘空块”。关于 `df` 命令的注释适用于 `cpio`。在这方面，`cpio` 相比 `tar` 的一个优势是它会告诉你完整备份中的块数，因此你知道大约恢复完整备份需要多少可用块。

## 检查绝对路径与相对路径

在从 `cpio` 备份中恢复任何文件之前，列出 `cpio` 目录列表并检查文件名是否以斜杠 (`/`) 开头。绝对路径或全路径以斜杠开头。相对路径不以斜杠开头。

考虑以下示例：

`/mori/acme/report6` — 此文件名是绝对路径。
`acme/report6` — 此文件名是相对路径。





`cpio` 会移除文件名中任何开头的点斜杠 (`./`)，因此 `./acme/report6` 被保存为 `acme/report6`，这是一种等效形式。

## 规划文件还原的位置

在前面的章节中，我们看到 `cpio` 备份可能包含绝对路径或相对路径。如果路径以斜杠开头，则该路径是绝对路径。这意味着 `cpio` 只能将文件从备份中还原到它们来源的原始目录，而不论当前目录位于何处。这可能是危险的，因为我们将恢复每个文件的旧版本，从而覆盖新版本，并丢失自制作 `cpio` 备份以来所做的任何更新。

例如，假设我们显示 `cpio` 目录列表，并在输出行中看到这一行：

```
-rw-r--r--  1 mori  staff 135 Apr 28 21:26 1998, /mori/pegasus/1997/expenses
```

`/mori/pegasus/1997/expenses` 是一个绝对路径。`cpio` 通常只能将此文件还原到磁盘上的该绝对路径。在还原此文件之前，拷贝该文件的当前版本将是一个好主意，这样就能保留所有更新。

如果 `cpio` 存档中的文件使用相对路径，我们可以将文件还原到许多不同的目录。这非常有用，例如当我们想要从 `cpio` 备份的旧文件中查找信息，而不覆盖该文件的当前版本时。在这种情况下，我们将备份文件还原到一个临时工作目录，查找所需信息，然后在完成后删除旧文件。

假设我们显示 `cpio` 目录列表，并看到文件名既不以点也不以斜杠开头：

```
-rw-r--r--  1 mori  staff 135 Apr 28 21:26 1998, mori/pegasus/1997/expenses
```

在这种情况下，我们的备份文件是相对路径。你可以通过在相对路径开头插入当前目录来预测 `cpio` 将这些文件还原到何处。

例如，如果我的当前目录是 `/tmp`，那么 `cpio` 将上段落中的 `expenses` 文件还原到此绝对路径：

```
/tmp/mori/pegasus/1997/expenses
```

另一个例子是，如果我的当前目录是 `/mori/pegasus`，那么 `cpio` 将上段落中的 `expenses` 文件还原到此绝对路径：

```
/mori/pegasus/mori/pegasus/1997/expenses
```

再另一个例子，如果我的当前目录是 `/`（根目录），那么 `cpio` 将上段落中的 `expenses` 文件还原到此绝对路径：

```
/mori/pegasus/1997/expenses
```

总结来说，如果 `cpio` 存档包含绝对路径，`cpio` 将这些文件（从磁带或磁盘）还原到它们的原始位置。如果存档包含相对路径，`cpio` 将文件还原到通过将当前目录添加到 `cpio` 路径确定义的路径。

## 考虑绝对文件名的变通方案

如果你使用绝对文件名创建 `cpio` 存档，你只能将这些文件还原到它们的原始位置（通常情况下）。这是 `cpio` 一个非常大且令人沮丧的限制。出于这个原因，`cpio` 的文档通常建议在执行 `cpio` 备份时使用相对路径。在本书之前关于使用 `cpio` 备份目录树的章节中，我只记录了如何使用相对路径进行备份。

UNIX 下的 `cpio` 有一个很好的 `-A` 选项，可以在还原时抑制领先斜杠。你可以在选项列表的任何地方添加 `-A` 选项。我在 AIX、Solaris 或 Linux 上没有找到它。如果 `cpio` 中的绝对路径对你是一个大问题，请查看 `pax` 命令，它应该能够读取 `cpio` 存档并支持通过 `-s` 选项修改任何文件名。

## 切换到正确的目录

如果 `cpio` 存档中的文件使用绝对路径，执行 `restore` 命令之前切换到哪个目录都没有。

如果 `cpio` 存档中的文件是相对的，在使用 `cpio` 还原相对文件时最关键且危险的决定之一是在开始 `restore` 之前切换到哪个目录。由于你正在还原一个或多个旧文件，存在无意覆盖这些文件当前版本的危险。要确定切换到哪个目录，请将磁带上的路径与你想还原文件的绝对路径进行比较，如下例所示：

### 示例 1
cpio 存档上的路径：
```
mori/pegasus/1997/expenses
```





### 恢复后的期望绝对路径
`/tmp/restoredata/mori/pegasus/1997/expenses`

### 执行 cpio restore 之前需要切换的目录
`/tmp/restoredata`

#### 示例 2
| cpio 归包中的路径 | 恢复后的期望绝对路径（将文件恢复到原始位置） | 执行 cpio restore 之前需要切换的目录 |
| :--- | :--- | :--- |
| `mori/pegasus/1997/expenses` | `/mori/pegasus/1997/expense` | `/` |

#### 示例 3
| cpio 归包中的路径 | 恢复后的期望路径 | 执行 cpio restore 之前需要切换的目录 |
| :--- | :--- | :--- |
| `mori/pegasus/1997/expenses` | `/pegasus/1997/expenses` | `/usr/fred/projects` |

### 将所有文件恢复到原始目录
恢复文件可能是复杂且危险的：你可能会覆盖掉错误的文件。我将向你展示几种恢复方法，并讨论它们的优缺点。

你可能不想使用最简单的恢复方法，即将所有文件放回它们来源的地方。如果你这样做，就会破坏掉包含最新信息的文件，并用备份中带有旧信息的文件来替换它们。现在你明白为什么我说你可能不想这样做了。这种操作很少执行；例如，当重大更新操作出现问题且所有当前文件都损坏时，你可能希望从备份中较旧但未损坏的版本中恢复所有文件。

要将 cpio 备份中的所有文件恢复到原始目录，请切换到你最初制作备份的目录。然后执行此处所示 `cpio restore` 命令：

```bash
cd /usr/fred/projects
pio -icvdum < /dev/XXX
```

`/usr/fred/projects` 只是一个示例名称。请输入你制作备份的实际目录。如果 cpio 归包包含绝对路径，那么切换到哪个目录都无关。

输入备份中的文件。此 `cpio` 选项的第一个字母必须是 `i` 或 `o`。输入（恢复）文件始终是一个危险的操作，因为你必须确保不会覆盖错误的文件。我们已经查看了 `c`（ASCII 头文件）和 `v`（详细模式）。

`d` 根据需要创建目录。否则，不允许备份中的较旧文件覆盖磁盘上的较新文件。`m` 保留文件最后修改的日期和时间，使其与备份时保持一致。否则，此恢复操作将被视为文件修改。`/dev/XXX` 应该替换为你的 cpio 归包的文件或设备名称。以下是一个显示运行此命令时屏幕内容的示例：

```bash
cd /usr/fred/projects
cpio -icvdum < /dev/XXX
.
acme
acme/report6
pegasus
pegasus/1997
pegasus/1997/expenses
```

### 将所有文件恢复到不同的目录
我们无法仅通过设置当前目录来完成这个示例。这可以通过更复杂的步骤完成，例如创建一个 `mori` 子目录作为指向根目录 (``) 的符号链接，或者将文件恢复到某些临时目录，然后将它们移动到目标位置。

```bash
cd /tmp
cpio -icvdum < /dev/XXX
.
acme
acme/report6
pegasus
pegasus/1997
pegasus/1997/expenses
```





# pegasus/1997/expenses
# pegasus/1997/sales
# pegasus/1998
# pegasus/1998/expenses
# pegasus/1998/sales

50 块

在本示例中，`cpio` 备份中的 `acme` 和 `pegasus` 目录被恢复到 `/tmp` 目录。如果该文件系统有足够的可用磁盘块，你可以选择 `/tmp` 以外的目录。

再次警告：如果 `cpio` 归档包含绝对路径，将忽略你的当前目录并将文件恢复到它们的原始位置，这可能是灾难性的！

## 仅恢复选定的目录或文件

如下例所示，可以只恢复选定的目录或文件。非常重要的一点是按照 `cpio` 目录中的出现精确指定目录或文件，包括任何前导斜杠 (`/`)。目录不会被递归恢复（`cpio` 不恢复目录的内容）。如果你想恢复整个目录，必须使用通配符。

```bash
cd desired-dir
cpio -icvdum < /dev/XXX? acme/report6 'pegasus/1997/*'
```

将 `desired-dir` 替换为你想要执行 `cpio` 命令的目录。将 `/dev/XXX?` 替换为 `cpio` 文件或设备名称。

`acme/report6` 演示了如何恢复文件。`'pegasus/1997/*'` 演示了如何恢复目录及其所有的文件和子目录。（注意单引号：我们必须防止 shell 将星号 (`*`) 作为文件名生成通配符进行处理。）

请注意，恢复选定文件的时间与最初写入 `cpio` 归档的时间相同。

### 设置块大小

`cpio` 允许使用 `-B` 选项将块大小设置为 512 字节。可以使用 `-C` 选项代替 `-B` 设置更大的块大小。较大的块可能有助于备份到高性能驱动器的性能：

```bash
cd desired-dir
find .print | cpio -ocC4096 > /dev/XXX?
```

注意在上一个命令中，使用 `-C` 来设置 4096 字节的磁带块大小。读取此磁带时必须使用相同的 `-C` 值：

```bash
cpio -icvdumC4096 < /dev/XXX?
```

另参：有关如何使用 `cpio` 将目录树从磁盘的一个部分复制到另一部分的更多信息，请参第 189 页

# 第 14 章 管理系统资源：磁盘空间

UNIX 系统连接了许多资源。这些资源包括 I/O 子系统（管理磁盘）、终端、CPU、内存等。在这里，我们将关注如何管理 UNIX 系统上的磁盘空间。各种系统资源由系统管理员管理，管理员可以通过 `root` 超用户身份登录并添加、修改或删除资源。尝试管理资源本质上是危险的，因为修改任何或所有资源可能会影响一个或多个用户。

磁盘空间是以文件系统为单位管理的。一个 `filesystem` 由其下的一个或多个目录子目录组成。你可以有多个磁盘卷，它们构成一个 `filesystem`，目录或文件可以位于 `filesystem` 的任何地方。文件或目录不能跨越 `filesystems`。

磁盘系统的层级结构如下：
- 物理磁盘
- 分区
- 文件系统
- 目录和文件
- 子目录和文件
- 文件

如果你必须增加目录空间，必须向该目录所在的分区或 `filesystem` 添加更多空间。

### 挂载文件系统

在访问 UNIX 系统中设置的目录之前，系统管理员必须将物理磁盘上的 `filesystem` 挂载。在系统启动时，系统会挂载 `/etc/filesystem` 文件中定义的所有真实挂载点。在其他时候，你可以手动挂载文件系统。

你可以使用以下命令获取已挂载文件系统的列表：

```bash
mount
```





系统将返回类似的内容：

```
node    mounted     vfs    date             options  over ----  -------  -------    ---    ------    ---------
/dev/hd0  /           jfs    Dec 17 08:04   rw, log  =/dev/hd8
/dev/hd3  /tmp       jfs    Dec 17 08:04   rw, log  =/dev/hd8
/dev/hd1  /home      jfs    Dec 17 08:06   rw, log  =/dev/hd8
/dev/hd2  /usr       jfs    Dec 17 08:06   rw, log  =/dev/hd8
```

对于每个文件系统，`mount` 命令列出了节点名称、设备名称、挂载点、虚拟文件系统类型、挂载日期时间以及其选项。你可以使用以下选项：

```

- `rw`: 读写。
- `ro`: 只读。
- `bg`: 允许你在后台处理挂载操作。如果挂载失败，系统将继续尝试挂载指定的로系统。 ```

如果你想以读写选项挂载名为 `xyz` 的文件系统，可以使用以下命令：
```
mount -o rw /dev/hd4/xyz
```
另一方面，如果你想挂载定义在 `/etc/files` 中的所有文件系统，可以使用 `/etc/files`。然后你可以使用以下命令：
```
mount -a
```

### 卸载文件系统

如果你想对文件系统进行任何维护，必须使该文件系统处于离线状态。你可以使用 `umount` 命令来卸载文件系统。例如，如果你想卸载名为 `xyz` 的文件系统，可以使用以下命令：
```
umount xyz
```
但是，如果该文件系统的任何一个文件正在被使用，你就无法卸载它。`umount` 不会提供关于哪些文件正在被使用或是谁在使用的详细信息。你可以使用该命令的 `-f` 选项强制卸载：
```
umount -f xyz
```
但是，如果你这样做，使用文件的程序将无法正常终止，你可能会丢失某些信息。

### 空间信息

要评估文件系统的可用空间，可以使用 `df` 命令。如果你想查看所有系统的详情，可以使用以下命令：
```
df .
```
系统将返回以下内容：
```
Device    512-blocks  free  %used  iused  %iused  Mounted on
/dev/hd0  19368      9976  48%   4714  5%     /
/dev/hd1  24212      4808  80%   5031  19%    /usr
/dev/hd2  9744       9352  4%    1900  4%     /site
/dev/hd3  3868       3856  0%    986   0%     /usr/venus
```
在某些系统中，空间以 512 字节块的形式显示，你可以使用 `df` 命令配合 `-k` 标志以 1024 字节块显示空间。在其他系统上，空间默认以 1024 字节块显示。

如果你想显示特定目录空间使用情况，可以使用以下命令：
```
df .
```
现在你已经知道哪个文件系统可能空间不足（使用 `df`），你可以使用 `du` 命令找到哪些文件占用了空间。要获取当前目录的磁盘占用情况，可以使用以下命令：
```
du -k
```
你将从系统获得以下响应：
```
240  ./test
120  ./test/file2
20   ./test/file3
8    ./info
16   ./info/lost
264  .
```
每行显示子目录所占用的 1024 字节数，并在最后显示总计。如果你想找到目录及其子目录中每个文件的大小，可以使用以下命令：
```
du -k -a
```





你也可以使用 `find` 命令来查找文件的大小。此外，`find` 命令还允许你列出大小等于、小于或大于特定大小的文件。

如果你想查找当前目录中大小恰好为 100000000 字节的文件列表，可以使用以下命令：

```bash
find . -size 100000000c -print
```

如果你想查找当前目录中大小大于 100000000 字节的文件列表，可以使用以下命令：

```bash
find . -size +100000000c -print
```

如果你想查找当前目录中大小小于 100000000 字节的文件列表，可以使用以下命令：

```bash
find . -size -100000000c -print
```

# 为用户限制磁盘空间

作为磁盘管理工作的一部分，你可以限制用户可以使用磁盘空间限额，或者限制用户可以创建的文件的大小。

你可以使用 `quota` 命令来限制用户使用的空间量。你可以通过此命令查看用户的当前配额：

```bash
quota -u user1
```

系统将返回如下：

```
Quotas for user1 (uid 502): Filesystem blocks limit grace Files limit grace
/u      20     55   60      20     60  65
```

你可以获取文件系统以及用户 keith (uid 502) 的配额：

```
Filesystem blocks limit grace Files limit grace
/u      20     55   60      20     60  65
```

你可以通过此处所示的 `repquota` 命令获取文件系统 `/u` 上所有用户的配额列表：

```bash
repquota -u /u
```

系统将返回如下：

```
Block limits File limits User used soft hard grace used soft hard grace
root    - 3920     0     0           734     0    0
davec  +-  28     8    30 3 days     3     0    0
keith  -   48     0     0               7     0    0
```

在第一列 `davec` 旁打印的 `+` 表示该用户已超过限制。

你可以使用 `edquota` 命令修改用户的磁盘配额。如果你想让 `user2` 的磁盘配额与 `user1` 相同，可以使用以下命令：

```bash
edquota -p user1 user2
```

你可以设置进程可以创建的最大文件大小。这通过限制进程一次可创建的文件的大小，来帮助管理磁盘空间。你可以使用以下命令来显示进程的文件限制：

```bash
ulimit -f
```

系统将返回：

```
4194303
```

这意味着最大文件大小为 4194303 块（每块 512 字节）。系统管理员可以使用以下命令修改文件大小限制：

```bash
ulimit -f 5000000
```

# lost+found 目录

`fsck` 工具会对任何未被目录项引用的文件在 `lost+found` 目录中创建一个条目。如果系统在删除过程中宕机，文件可能无法被正确删除；在这种情况下，`fsck` 可能会 `lost+found` 中创建一个条目。系统管理员应该检查 `lost+found` 中创建的文件和目录，并决定是删除它们还是通知相关用户采取纠正措施。

# 其他磁盘管理命令

完成此之后，你仍然需要一些空间，因为原始文件在完全压缩之前不会删除。你可以使用以下命令对名为 `xyz` 的文件进行原地压缩：

```bash
compress xyz
```

压缩后的文件将被命名为 `xyz.Z`。压缩释放出的空间可能从原始占用空间的 90% 开始不等。实际压缩效果取决于文件内部的数据以及所使用的压缩算法。



在某些情况下，你可以将违规文件归档到存档文件中然后删除这些文件以获取所需的磁盘空间。可以使用 `tar` 命令来实现此操作。如果你想将当前目录下所有以 `test` 开头的文件归档，可以使用以下命令：

```bash
tar cf test.tar test*
```

该命令会创建一个名为 `test.tar` 的归档，稍后可用于提取文件。要从归档中提取文件，你可以使用以下命令：

```bash
tar xf test.tar
```

# 第四部分 UNIX 文本处理

## 15 在文件或管道中搜索行
## 16 在文件或管道中替换或删除文本
## 17 使用 *vi* 编辑文本文件
## 18 让 *vi* 编辑器为你工作
## 19 Korn Shell 中的命令行编辑
## 20 介绍 emacs 编辑器

---

# 第 15 章：在文件或管道中搜索行

### 查找包含模式的行 (*grep*)
要查找并显示文件中包含某个名称或模式的行，你可以使用 `grep` 命令（稍后我会告诉你它的名字是从哪里来的）。例如，假设你有一个员工文件，每行包含一个员工的名称和信息。要只显示该文件中包含名称 `Smith` 的行，你需要输入：

```bash
grep Smith employee-file
Smith, Carl - 555-6379, hired 3-7-92, dept 6
Smith, Dennis - 555-3291, hired 8-27-96, dept 2
Smithers, Jane - 619/555-1720, hired 4-4-89, dept 2
```

在上面的输出中，注意到只显示了包含单词 Smith 的行。其他员工的行并没有显示。注意最后一行，Smith 是作为 Smithers 名字的一部分被找到的。

### 显示文件中包含模式的行
1. 在 shell 提示符下，输入：`grep`。在接到指示之前，不要按回车键。
2. 输入一个空格，然后输入你想在文件内容查找的模式。该模式可以是一个名称或任何字符序列。这种模式被称为*正则表达式*（regular expression），可以包含特殊的通配符（我将在本章稍后部分介绍）。如果模式包含任何标点符号或空格，你需要将模式括在单引号或双引号中。（我将在本章进一步讨论这一点。）通常情况下，一个实用的经验是始终将模式括在单引号中。
3. 输入一个空格，然后输入一个或多个用空格分隔的文件名。如果文件在当前目录下，只需输入每个文件的 `basename`（请参术语表获取 `basename` 的定义）。如果文件不在当前目录下，请为每个文件输入绝对路径或相对路径。你可以使用文件名生成通配符模式（Filename Generation Wildcard patterns）来替换列表中所有文件的某一部分。
4. 按回车键执行你的命令。
5. `grep` 会显示任何包含模式的行的标准输出，即使该模式包含在一个较大的单词中。如果你在步骤 3 中指定了多个文件，`grep` 会显示文件名以及包含模式的行，如下所示：

```bash
grep Acme report* report3:   Acme Enterprises   1,373,383,234 world-wide
report.acme.13:of the four Acme divisions, it is the least
```




如果你在命令行中为 `grep` 提供文件列表，它会在这些文件中搜索给定的模式，并仅显示包含该模式的行。如果你不提供文件列表，`grep` 将从标准输入读取输入，因此 `grep` 可以用于管道中，如下例所示：

```bash
$ who | grep smith
smith      tty3     Mar  6 19:48
smith      ttya03   Mar  6 17:23
```

在上面的命令行中，`who` 询问哪些用户正在登录。`who` 命令的输出被传递给 `grep`，后者查找包含 `smith` 名称的行，无论它是完整单词还是较大单词的一部分。请注意，在管道中使用 `grep` 时，不能在搜索模式之后指定任何文件名。

`grep` 是典型的 UNIX 过滤器。可以想一下咖啡机中的纸过滤器。过滤器盛着咖啡渣和热水。过滤器允许液体咖啡通过，但留下了咖啡渣。过滤器的工作是有选择性地允许你想要的东西通过，并阻塞你不想要的东西以便它们无法通过。这就是 `grep` 所所的，特别是当你在管道中使用它时。在上面的示例中，你从 `who` 命令开始。但因为你只想看到引用 `smith` 的行，`grep` 传递了这些行。`grep` 阻塞了所有不包含 smith 的行——你可以说它过滤掉了这些行，因为你不想看到它们。由于某些输出可能包含数万行甚至更多，`grep` 是 UNIX 下一个极其重要且经常使用的实用程序，它可以过滤掉你不需要的行，让你专注于你感兴趣的行。

**另参**

- 有关文件列表的更多信息，请参阅第 231 页。
- 关于过滤器和管道的更多信息，请参阅第 31 页。

### 在选择行时忽略大小写 (`grep -i`)

要在使用 `grep` 搜索模式时忽略大小写，你需要为 `grep` 添加 `-i` 选项，如下例所示：

```bash
$ grep -i acme report7
The Acme account is currently handled by Linda. It is once they merged with ACME INDUSTRIES, their stock value Pauley, Mr. Robert Kacmeth, Ms. Jean Bensen, and other
```

当你在 `grep` 中使用 `-i` 选项时，无论你指定大写、小写还是混合大小写的模式都可以。在上面的示例中，`-i` 选项指示 `grep` 找到所有包含模式的行，无论它是以大写、小写还是混合情况出现。如果没有 `-i` 选项，只有当行的大小写与模式的大写完全匹配时，`grep` 才会显示该行。在旧版本的 UNIX 中，使用 `-y` 代替 `-i` 来忽略大小写。某些较版本的 UNIX 允许使用 `-y` 向兼容，但建议使用 `-i`。

### 将选行保存到文件中 (`grep`)

你可以使用重定向（>` 或 `>>`）将 `grep` 的输出保存到文件中，如下：

```bash
grep 'Acme Shoes' /usr/fred/report > acme/file
```

在这个示例中，你正在查找模式 `Acme Shoes`。由于它包含空格，你必须用单引号或双引号将模式括起来。要查找的文件列表由文件名模式指定，该模式指定了 `/usr/fred` 目录下所有以 `report` 开头的文件。命令告诉 `grep` 将所有匹配的行保存到当前目录下 `acme` 子目录中的 `file` 文件中。`grep` 不会在屏幕上显示行，因为输出被重定向了。

这是另一个类似的示例：

```bash
who | grep fredp >> file
```

在这里，你检查用户 `fredp` 是否正在登录。如果是，你想让 `grep` 将 `who` 报告的登录信息追加到 `file` 文件。

### 将选行管道到其他命令 (`grep`)

`grep` 经常用于管道以过滤掉不需要的行，以便其他命令处理所需的行。要查看这是如何工作的，请考虑以下示例：

```bash
$ who | grep fredp | wc -l
3
```

在这个示例中，`who` 生成了每个当前登录用户的列表。`grep` 将该列表缩减为仅提到 `fredp` 的行。`wc -l` 统计它接收到的行数。从输出中，你可以看到用户 `fredp` 目前同时登录在三个端口。但这个结果可能是误导性的，因为即使找到的模式是较大单词的一部分，`grep` 也会认为该行匹配匹配。在示例中，假设有一个名为 `fredpenn` 的用户。注意字符串 `fredp` 位于 `fredpenn` 内部。如果 `fredpenn` 登录了三个端口，而 `fredp` 完全没有登录呢？你会得到相同的结果。





# 选择你的模式 (`grep`)

使用 `grep` 的技巧很大程度上取决于明智地选择要搜索的模式，特别是模式的开头和结尾。例如，使用以下 `grep` 命令可能不是一个好主意：

```
$ grep ' acme' report*
```

此命令要求在模式的 `acme` 之前有一个空格，以避免匹配如 `Dacmer` 这样的单词。然而，要求开头有空格并不是好主意，因为如果 `acme` 位于行首或在引号内，`grep` 将无法找到它（因为 `acme` 开头不是空格）。

假设你有一个巨大的 `phone-list` 文件，其中包含如下行：

```
Bower, Linda 714/555-8182
Decker, Tom 818/714-6192
Mellinger, Fred 714/639-1215
Smith, Will 714/909-3818
Smithson, Charlie 818/603-2194
```

要快速查找姓氏为 `Smith` 的人，你可以输入：

```
$ grep Smith, phone-list Smith, Will 714/909-3818
```

注意，你之所以可以在 `grep` 模式末尾添加逗号，是因为文件中名字后面确实有一个逗号。逗号允许你显示 `Smith` 同时避开 `Smithson`。这个逗号并不是 `grep` 的功能；它仅仅是文件设置方式的结果。

要统计区号为 `714` 的人数，你可以输入此命令：

```
$ grep 714/phone-list | wc -l
```

你之所以可以指定 `/`，是因为你的文件在区号和电话号码之间确实有一个 `/`。在模式中使用 `/` 允许你忽略它是否是电话号码的一部分（只要不是区号即可）。再次，`/` 并不是 `grep` 命令的功能。它展示了你如何观察数据并明智地选择模式，以返回你想要看到的行。

## 显示不包含模式的行 (`grep -v`)

`grep` 也可以用作反向过滤器：可以使用它来移除包含特定模式的不需要的行，以便查看剩余内容。要显示不包含模式的行，请配合 `grep` 使用 `-v` 选项使其作为反向过滤器工作，例如所示：

```
$ who | grep -v guest | wc -l
```

在这里，`who` 会为每个登录系统的每个用户显示一行。`grep` 命令随后使用反向过滤器排除包含单词 `guest` 的行，这样所有其他登录都将通过，但 guest 登录将被忽略。`grep` 的输出随后通过管道传给 `wc -l`，用于统计排除 guest 登录后的登录人数。

## 为找到的行添加行号 (`grep -n`)

要让 `grep` 显示包含模式的行的行号，请为 `grep` 添加 `-n` 选项：

```
$ grep -n Acme report
13:Acme Industries
246:Pacific Acme Ltd
1202:Paul Acmeersch
```

如你所见，`grep -n` 先显示行号，然后是匹配模式的行。如果在多个文件上显示行号的 `-n` 选项，`grep` 的输出将以文件名开头，然后是行号，如下例所示：

```
$ grep -n Acme report*
report2:25:Acme Enterprises
... (继续)
```

## 显示包含模式的文件名 (`grep -l -c`)

有时你只是想知道哪些文件引用了特定模式。如果每个文件中几万行都提到该模式，普通的 `grep` 输出将太长，无法轻易分析。要仅显示包含模式的文件名，请配合 `grep` 使用 `-l` 选项列出文件名，而不是包含模式的行：

```
$ grep -l Acme report*
report2
report.acme
```

要显示每个文件名以及该文件中包含模式的行数，你可以使用 `grep` 的 `-c` 选项，如下：

```
$ grep -c Acme report*
report2:1
report4:0
report8:3
report12:0
report.acme:1
report.pegasus:0
```

## 查找包含两个模式的行 (`grep | grep`)




你可以使用两次 `grep` 来实现双重过滤。行必须同时包含两个模式才能通过，如下所示：

```bash
$ grep -i acme report* | grep merge report7:246:once they merged with ACME INDUSTRIES, their stock value
report.acme:45:whose former name was Acme Inc. until they merged
```

```bash
$ grep -i acme report* | grep merge report*
```

`grep -c` 统计的是行数，而不是出现次数。

在查看 `grep -c` 的输出时，人们经常犯一个常见的错误，认为文件名旁边的数字是模式在文件中出现的次数。但请注意，`grep -c` 统计的是行数，而不是出现次数。如果模式出现了 10 次，但都在同一行中，`grep -c` 将显示结果为 1，而不是 10。

在这个示例中，你将 `grep` 管道传输给另一个 `grep` 以实现双重过滤。要通过第一个过滤器，行必须包含大写或小写的 `acme` 单词。要通过第二个过滤器，行还必须包含 `merge` 单词。输出显示了行中同时包含这两个模式的行。第二个模式出现在行中第一个模式之前或之后都没有关系。将 `grep` 管道到 `grep` 设置了一个逻辑与（AND）条件，这意味着行必须同时满足两个条件才能通过。

注意，第二个 `grep` 命令不能指定任何文件，这样它才会从标准输入读取并处理第一个 `grep` 命令的输出。以下示例显示了人们有时会犯的错误：

```bash
$ grep -i acme report* | grep merge report*
```

不要犯这个错误。这个示例不会产生错误，但它无法实现你的预期目标。因为第二个 `grep` 命令被赋予了一个文件列表，它忽略了来自第一个 `grep` 的输出。你在这里得到的是通信失败。第二个 `grep` 命令是一个独立的单一过滤器，它只查找包含 `merge` 的行并显示它们，即使它们不包含 `acme`。第一个 `grep` 命令做了一无用功，因为它的输出被忽略了。

你还可以将普通过滤器与反向过滤器结合，如示例所示：

```bash
$ grep -i acme report* | grep -v Dacmer
```

在这里，你首先使用普通过滤器来查找包含大写或小写 `acme` 的行。但请注意，第一个过滤器找到了包含 `Dacmer` 的行，因为 `Dacmer` 包含了 `acme`。第二个 `grep` 是一个反向过滤器，会从第一个过滤器中移除行。结果是包含 `Acme` 但不包含 `Dacmer` 的行。然而，这里仍然存在一个问题：任何包含 `Acme` 和 `Dacmer` 的行都会被反向过滤器删除。稍后你会看到 `perl` 如何通过忽略其他单词中的模式来过滤掉整个单词。

哪个过滤器应该放在第一个？如果你有一个双重过滤器，无论你以什么顺序应用过滤器，得到的结果都是相同的。但为了提高效率，第一个过滤器应该是过滤掉最多行的那个。这样第二个过滤器的工作就会少很多。

### 行中的通配符匹配（正则表达式）

让 UNIX 变得非常强大的特性之一是模式可以指定你在文件中查找的内容。你已经在文件名通配符中看到了这一点，它允许你根据模式形成文件列表。在本节中，你将遇到正则表达式。

正则表达式是你想要搜索的字符字符串。正则表达式可以组合成一个更大的表达式。正则表达式可以包含特殊字符或元字符。我将这些特殊字符称为正则表达式通配符，以区分区别于文件名通配符。

尽管正则表达式很复杂，但了解它们很重要，因为它们是 UNIX 的基本工具，赋予了它许多力量和优雅。在本章中，你将看到如何使用正则表达式在文件中查找所需的行。在接下来的章节中，你将学习如何修改文件。有关文件名通配符的更多信息，请参阅第 232 页。

### 选择包含模式的行 (grep)

这是一个典型的 grep 命令：




```bash
grep acme report7
```

如果你输入此命令，`grep` 将搜索文件 `report7` 的内容，并显示所有包含字符串 `acme` 的行，即使 `acme` 是某个较大单词的一部分。请注意，模式 `acme` 可以位于行中的任何位置，`grep` 都会显示该行。

## 选择以模式开头的行 (`^*`)

如果你只想查看以 `acme` 开头的行怎么办？你可以通过添加一个正则表达式通配符来实现。如下所示，你可以在模式的开头添加脱字符符号（`^`），它也称为“帽号”或“caret”：

```bash
grep '^acme' report7
```

注意搜索模式周围的单引号。通常情况下，给模式加上单引号是一个好主意（但有一种情况下你应该使用双引号；你稍后会学到这一点）。正如你可能记得的，如果模式包含任何标点符号或空格，你通常会在模式周围加上单引号。但即使没有标点符号或空格，使用单引号也没有坏处。

在上面的示例中，脱字符符号（`^`）是一个表示行首的正则表达式通配符。因此，只有以 `acme` 开头的行才会匹配模式。在输出中，`grep` 将显示这些行，包括行中 `acme` 之后的任何文本。

脱字符符号（`^`）只有在出现在模式开头时才是一个通配符字符。例如，考虑以下命令：

```bash
grep '2⁴' mathproblems
```

在这里，`grep` 将显示行中任何位置包含 `2⁴` 的行。脱字符符号（`^`）只是另一个要搜索的字符，因为它没有出现在模式的开头。

要搜索以脱字符符号（`^`）开头的行，你需要输入这样的命令：

```bash
grep '^^' filename
```

在上面的示例中，第一个脱字符符号（`^`）是表示行首的正则表达式通配符。第二个脱字符符号（`^`）不是通配符；它表示字面上的脱字符（`^`）。要指定开头的脱字符（`^`）是字面的 `^` 而不是表示行首，你可以在它前面加一个反斜杠（`\`）：

```bash
grep '\^acme' report7
```

在这个示例中，`grep` 搜索并显示行中任何位置包含 `^acme` 的行。请注意，每一行都有开头。因此，以下命令将匹配文件中的每一行：

```bash
grep '^' report7
```

## 选择以模式结尾的行 (`$`)

如果你只想查看以 `acme` 结尾的行怎么办？你可以通过在模式末尾添加另一个正则表达式通配符——美元符号（`$`）来实现：

```bash
grep 'acme$' report7
```

在这里，美元符号（`$`）是一个表示行尾的正则表达式通配符。因此，只有以 `acme` 结尾的行才会匹配模式。`grep` 随后显示这些行，包括行中 `acme` 之前的任何文本。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

美元符号（`$`）只有在出现在模式末尾时才是通配符；否则它表示字面上的美元符号。要指定搜索作为行最后一个字符的字面美元符号，请在美元符号（`$`）前面加一个反斜杠（`\`）。





```
acme
the end of the line
```

例如，此行并不匹配之前指定的模式：
```
acme acme
```
尽管该行以 `acme` 开头并以 `acme` 结尾，但它并不匹配。如果你从左到右将正则表达式 `^acme$` 与行 `acme acme` 进行比较，很容易看出该正则表达式允许行中仅存在 `acme`。

这里是另一个结合使用脱字符（`^`）和美元符号（`$`）的示例：
```
grep '^$' report7
```执行此命令，`grep` 会搜索并显示所有空行，即行尾紧跟在行首之后。

现在考虑另一个示例：
```bash
grep '$^' report7
```
在这里，脱字符（`^`）不是通配符，因为它没有出现在模式的开头。同样，美元符号（`$`）也不是通配符。因此，此 `grep` 命令会搜索并显示文件 `report7` 中在行任意位置包含美元符号（`$`）后跟脱字符符号（`^`）的行。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

`grep` 的名字是从哪里来的？
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) `ed` 是一种在 `vi` 出现之前常用的文本编辑器。在 `ed` 编辑器中，`g/re/p` 是一个用于全局搜索由斜杠（`/`）括起来的正则表达式并打印每一行的命令。当开发出一个独立的实用程序来执行相同的功能时，它保留了 `ed` 的名称但去掉了斜杠。

### 在正则表达式中包含 Shell 变量

你可以在正则表达式中使用 Shell 变量，如下：
```
who | grep $LOGNAME
```
在此示例中，`$LOGNAME` 通常包含用户名。`who` 显示所有登录情况，`grep` 过滤掉不需要的行，只显示用户已登录的行。

如果 Shell 变量与其他模式元素相邻，请使用以下大括号 `{}` 将其括起来：
```bash
grep "${prefix}acme${SUFFIX} Inc" report7
```
对于此示例，假设 `$prefix` 包含 `g4` 且 `$SUFFIX` 包含 `UK`。该示例将执行以下命令：
```bash
grep "g4acme-UK Inc" report7
```
由于模式包含空格，你必须将其用双引号括起来。更多信息请参阅后文关于正则表达式引号的章节。

另参阅 ![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 获取更多关于 Shell 变量的信息

### 在正则表达式中包含命令替换

正则表达式还可以包含你使用命令替换指定的元素，命令替换通过反引号（`` `` ``）或 `$()` 表示。例如，查看以下命令：
```bash
grep "report`date '+%Y'" report
```
在此示例中，正则表达式由两个元素组成：
1. 单词 `report`
2. 这个反引号内的命令：`date '+%Y'`

在第二个元素中，`+%Y` 是 `date` 命令的一个选项，告诉它以四位数字显示当前年份。反引号（`` ` `` 和 `` ` ``）获取所包含命令的输出，将其替换到当前命令行中，并移除反引号内的命令。

因此，如果当前年份是 1998 年，之前的 `grep` 命令等同于：
```bash
grep "report1998" report
```
当你使用命令替换时，正则表达式可以包含由任何其他 UNIX 命令或管道生成的元素。





# 使用正则表达式以防止问题

如果你的正则表达式不包含标点符号或空格，则无需将其放在任何类型的引号中。不过，你也可以在模式周围使用双引号或单引号。

如果你的正则表达式确实包含标点符号或空格，但没有使用任何 Shell 变量或命令替换（如前所述），你应该将整个正则表达式封装在单引号中。这可以确保 Shell 不会尝试将某些标点符号解释为 Shell 指令、文件名通配符等。如果你的正则表达式包含任何反斜杠（`\`），请在每个反斜杠之前额外添加一个反斜杠（`\` ）。

然而，这些规则有一个例外。如果你的正则表达式包含一个或多个单引号（`'` ），请在正则表达式中的每个标点符号和空格前面加上反斜杠（`\` ），并且*不要*将其封装在任何引号中。例如，假设你想搜索包含包含单引号的以下精确字符串：

`item '73' corneil`

要实现这一点，你会使用以下 `grep` 命令：

```
grep item\ \'73\' corneil filename
```

但是，如果你的正则表达式使用了 Shell 变量或命令替换，你应该将整个正则表达式封装在双引号中。然后，在你的正则表达式中出现的任何以下字符前面加上反斜杠：

- 美元符号（`$` ），如果它不是 Shell 变量的开头
- 反引号（`` ` `` ），如果它没有包裹命令替换
- 你的正则表达式内部的双引号（`"` ）
- 你还必须将任何单独的反斜杠（`\` ）改为四个反斜杠（`\\\\` ），因为 Shell 会移除其中的两个，并且为了让 grep 正常工作，实际的反斜杠前面必须先跟一个反斜杠。

例如，假设 `$cost` 是一个包含金额的 Shell 变量，你想找到 report 中包含以下内容：`"honest"s$cost` 的所有行

你会使用此 `grep` 命令：

```
grep "\"honest\"s\$cost" report
```

或者，你也可以像这里所示，在正则表达式的区域周围结合使用单引号和双引号：

```
grep '"honest\'s\\'$cost"' report
```

但注意，如果 `$cost` 包含标点符号，情况可能会变得复杂。

## 允许正则表达式的 UNIX 命令

只有以下命令允许使用正则表达式：
- `grep`, `egrep`, `fgrep`, `sed`
- `awk`
- `perl`
- `vi`（在搜索和替换时）

## 文件名通配符与正则表达式的比较

有时人们会困于何时使用正则表达式，何时使用文件名模式。以下指南可以缓解一些困惑：

- 当你想搜索文件或管道的内容时，使用正则表达式。只有少数命令支持使用正则表达式；请参见前一节。
- 当你想根据模式创建文件名列表时，使用文件名模式。许多 UNIX 命令接受命令行上的文件列表。

### 在特定位置允许任意字符 (*.*)

点（`.` ）是一个正则表达式通配符。它代表任何字符，允许你精确地指定在其他模式元素之前、之后或之间允许多少个字符位置。以下命令显示点字符使用的示例：

```
grep 'dog.bone' report
```

给定该命令，`grep` 将显示所有包含 dog、紧跟任意单个字符、然后是 bone 的行。例如，它可能会返回包含以下字符串的行：

- dog-bone
- dog bone
- dog/bone
- dogEbone



第 396 页

然而，`grep 'dogbone'` 不会显示包含 dogbone 的行，因为在那种情况下 `dog` 和 `bone` 之间没有字符分隔。若想在正则表达式中匹配实际的点号 `.`，需要在点号前加一个反斜杠 `\`，如下所示：

```
grep '5\.25' report
```
该命令将显示任何包含 5.25 的行。在点号之前需要反斜杠 `\` 是为了防止 `grep` 将该点号误认为匹配任意字符的正则表达式通配符。

方括号 `[]` 允许你为正则表达式中该位置的字符指定一组备选字符，如下例：

```
grep 'dog[-EZ1-3]bone' report
```
根据该命令，`grep` 将显示包含以下任何字符串的行：
- dog-bone
- dogEbone
- dogZbone
- dog1bone
- dog2bone
- dog3bone

但注意，除非行中包含了允许的 bone 引用，否则 `grep` 将不会显示包含以下字符串的行：
- dog4bone（因为 4 不是允许的备选字符）
- dogEZbone（因为方括号仅表示模式中的单个字符）

在方括号 `[]` 内部，两个字母或数字之间的连字符 `-` 表示一个范围。若要将连字符 `-` 视为普通字符，必须将其放在列表的开头或结尾。若要将右括号 `]` 视为字符，应将其放在 `[]` 中的第一个列表元素。方括号内的点号 `.`、星号 `*`、左括号 `(` 或反斜杠 `\` 都被视为字面量，没有特殊含义。现在考虑以下命令：

```
grep '[0-9][0-9][0-9]' report
```
在这里，`grep` 显示任何包含三个（或更多）连续数字的行。即使你只搜索三个数字，`grep` 也可能会找到三个以上的数字，因为该模式并没有限制在三个数字前后出现更多数字。这是另一个例子：

```
grep '^[A-Z]' report
```
根据该命令，`grep` 将显示所有以大写字母开头的行。

在模式位置指定禁止的字符 `[^...]`

如果方括号中的列表以脱字符符号 `^` 开头，它将匹配列表之外的任何单个字符。例如，给定以下命令：

```
grep 'acme[⁰-9]' report
```
`grep` 将显示所有包含 acme 且后跟一个字符的行，只要该字符不是数字。它不会显示以 acme 结尾的行，因为在这一模式中 acme 后面必须有一个字符。这里是另一个例子：

```
grep '[^a-z]' report
```

第 397 页

文件名生成通配符（Filename Generation Wildcards）中的方括号与正则表达式通配符非常相似。然而，为了排除方括号中的字符，文件名生成通配符使用感叹号 `!` 作为第一个字符，而正则表达式通配符则使用脱字符符号 `^` 作为第一个字符。

指定正则表达式元素出现的次数 `{n}`

在指定正则表达式时，你可以使用简写方法来指定上一个正则表达式元素出现的次数。这种简写方法使用转义的大括号 `\{` 和 `\}`。以下是一个带有转义括号的命令示例：

```
grep '2[0-9]{10}000' report
```



在此命令中，正则表达式告诉 `grep` 查找一个 2，后面紧跟正好 10 个数字，最后是 000。`grep` *并没有*将其读取为一个 2，后面跟任意一个数字，再跟 10 个数字。它将其读取为一个 2，后面跟 10 次数字（而不是 11 次），最后是 000。

## 指定元素出现的次数

1. 在 shell 提示符下，输入包含包含正则表达式的所需命令。输入你想要重复的模式元素。该模式元素可以是一个简单的字母、数字，也可以是正则表达式通配符，如点 `.` 或中括号 `[]`。在没有接到指示之前，请勿按回车键。
2. 输入 `{`。（除非接到指令要求，否则请勿输入任何空格。）
3. 输入上一个模式元素所需的出现次数。
4. 如果该数字是最小次数，且你希望允许模式重复更多次数，请输入逗号 `,`。
5. 如果有一个想要允许模式元素重复的最大次数，请现在输入该数字。
6. 输入 `}`。
7. 现在完成正则表达式的其余部分及命令。完成后，按回车键执行你的命令。

考虑以下示例：

```
grep '$[0-9]{3,5}\.' report7
```

给定此命令，`grep` 将显示所有包含美元符号 (`$`)、后面紧跟至少三个数字且不超过五个数字、最后是一个点号 (`.`) 的行。注意，点号被转义了，它不是通配符。

这是另一个示例：

```
grep '[a-zA-Z]{2,}' report7
```

此命令将显示所有包含 2 个或更多大写或小写字母单词的行。注意这里的逗号是多余的；你将在关于无界或更多通配符的章节中学习到这一点。

## 指定正则表达式元素的零次或多次出现 (*)

星号 `*` 是一个正则表达式通配符，你可以用它作为表达式 `{0,}` 的简写。星号 (`*`) 告诉 `grep` 允许上一个正则表达式元素出现零次或多次。不要将其与文件名通配符 `*` 混淆，后者的含义完全不同，且用于完全不同的语境。

以下命令展示了如何使用星号正则表达式通配符：

```
grep 'ab*c' report7
```

在此命令中，`b*` 表示 `grep` 允许出现零次或多次 `b`。给定此命令，`grep` 将显示包含以下任何字符串的行：

- ac (0 次 b)
- abc (1 次 b)
- abbc (2 次 b)
- abbbc (3 次 b)
- abbbbc (4 次 b)
- 以此类推，包括 abbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbc

为什么 UNIX 脚本中包含 `[ ]`？因为由于左边距存在空格或制表符，某些 `grep` 命令可能包含类似 `^[]*acme` 的模式。中括号内的字符是一个空格和一个制表符。该模式用于在在零个或多个空格或制表符的左边距之后，立即查找 `acme`。

要表示任意字符的零次或多次，你可以将点和星号结合使用 (`.*`)，例如所示：

```
grep 'dog.*bone' report7
```

此命令将显示包含以下字符串的行：

- dogbone
- dog-bone
- doggy bone
- My dog has a bone.
- My dog is named Rover. Please add a soup bone to the grocery list.

上述命令不会显示 dog 在某行而 bone 在下一行的情况。整个正则表达式必须在同一行内。



另一个例子，这个命令：

```bash
grep '[0-9]*' report7
```

它将显示所有包含零或多个数字的行。文件的每一行都会被显示，因为文件的每一行都包含零或多个数字。（数一数每行中的数字，你会发现我是对的。）

```bash
grep '[0-9][0-9]*' report7
```

此命令显示任何包含一个数字、后跟零或多个数字的行。本质上，它会找到并显示所有包含一个或多个数字的行。

```bash
grep '$[0-9][0-9]*.' report7
```

给定此命令，`grep` 显示任何包含美元符号（`$`）、其后跟一个或多个数字、最后是一个点（`.））的行。上一个命令与这个命令也是等价的：

```bash
grep '$[0-9]\{1,\}' report7
```

每当你看到正则表达式元素连续出现两次并跟一个星号（`*`）时，记住你可以使用如下命令来查找一个或多个该元素：

```bash
grep 'abb*c' report7
```

此命令告诉 `grep` 显示任何包含 a、其后跟一个或多个 b、其后跟一个 c 的行。

### 丢弃无边界的“或更多”正则表达式通配符

UNIX 提供了几种方法来表示某个元素的使用次数为次数或更多。例如，你可以使用以下任何一种：

- `a{6,}`（6 个或多个字母 a）
- `b*`（0 个或多个字母 b）
- `cc*`（1 个或多个字母 c）
- `ddd*`（2 个或多个字母 d）

比较这两个命令：

```bash
grep '[0-9]\{3,\}' report7
grep '[0-9]\{3\}' report7
```

这两个命令中的第一个将显示包含三个或多个数字的行。第二个命令没有对这三个数字之后可能出现的内容进行限制。因此，第二个命令允许在三个数字之后出现更多数字。换句话说，它也会显示包含三个或多个数字的行。换句话说，尽管你在第一个命令中指定了“或更多”，而在第二个命令中没有指定，这两个命令的输出是完全相同的。

这两个命令的情况也是一样的：

```bash
grep 'abb*' report7
grep 'ab' report7
```

第一个命令将显示包含 a、其后跟一个或多个 b 的行。第二个命令将显示包含 ab 的行。然而，这两个命令是等价的，因为任何包含 a、其后跟一个或多个 b 的行也包含 a、其后跟一个 b（反之亦然）。尽管如此，不带“或更多”的命令更好，因为它效率更高且更容易理解，而且你可以预测结果。

我将这些情况称为“无边界的‘或更多’情况”，因为你没有在“或更多”元素的前后指定模式元素。如果该“或更多”元素（在元素之前或之后）是无边界的，请从你的 `grep` 命令中省略“或更多”部分。这将使 `grep` 命令更高效，你也能更好地理解 `grep` 命令将输出什么内容。

这里是一些有边界的“或更多”情况：

```bash
grep "abb*c" report7
grep '^[0-9]*$' report7
grep '$[0-9]\{5,\}' report7
```

在这些命令中，在“或更多”通配符的前后都指定了模式元素。然而，这里的“或更多”是有意义的；如果省略，将会改变命令的输出。

### egrep 中可用的正则表达式通配符

`egrep` 命令是 `grep` 的扩展版本，它允许一些 `grep` 不支持的正则表达式通配符。然而，`egrep` 不支持使用大括号 `{}` 来指定出现次数。有时 `egrep` 的正则表达式通配符集被称为*扩展正则表达式*或*全正则表达式*。`egrep` 的语法与 `grep` 相同。

### 使用 egrep 指定元素出现一次或多次

要指定上一个模式元素被使用一次或多次，你可以在 `egrep` 中使用加号（`+`）通配符，如下所示：

```bash
egrep 'ab+c' report7
```

此命令将显示包含 a、其后跟一个或多个 b、其后跟 c 的行。`grep` 不支持加号（`+`）通配符。

### 使用 egrep 指定元素出现零次或一次

要指定元素出现零次或一次，你可以在 `egrep` 中使用问号（`?`）：




```bash
egrep 'Mrs?. Smith' report7
```

上述命令将显示包含此类字符串的行：

```
Mr. Smith
Mrs. Smith
```

然而，它不会显示包含 Mrss. Smith 的行。问号（`?`）前面必须有一个反斜杠（`\`），或者包含在双引号或单引号内（如所示）。`grep` 不支持问号（`?`）通配符。

### 搜索多个模式中的一种

使用 `egrep`，你可以搜索并显示包含多个模式之一的行。你使用竖线（`|`）分隔这些模式，该符号也用作管道符号（`|`）。这是一个示例：

```bash
egrep 'acme|pegasus|apollo' report7
```

此命令将显示包含 acme 或 pegasus 或 apollo 的行。竖线（`|`）前面必须有一个反斜杠（`\`），或者包含在双引号或单引号内（如所示）。

括号 `()` 可用于竖线（`|`）选择进行分组，如下所示：

```bash
egrep 'project (acme|pegasus|apollo)' report7
```

此命令将显示包含 project acme 或 project pegasus 或 apollo 的行。

### 仅在 perl 中可额外正则表达式通配符

`perl` 是一种运行在 UNIX 和 Windows 下的完整语言。虽然它没有包含在任何商业 UNIX 发行版中，但大多数 UNIX 系统都可以通过互联网轻松获取。如果你的系统中可用 `perl`，你可以将其作为一个类似 grep 的命令行工具，提供 `grep` 或 `egrep` 不具备的搜索和显示功能。

### 使用 Perl 查找包含模式的行

1. 如果你要在管道中使用 `perl`，请输入生成供 `perl` 处理输出的 UNIX 命令。以管道符号（`|`）结束此序列。在收到指示之前不要按回车。
2. 输入 `perl -ne 'print if /'`。`perl` 的 `-e` 选项允许你在命令行输入一行 perl 代码。`-n` 选项允许 perl 处理标准输入的每一行或命令行上指定的任何文件。在收到指示之前不要按回车。
3. 输入要搜索的模式。你可以包含 `grep` 和 `egrep` 的任何正则表达式。表示重复次数的大括号 `{}` 前面不应该有反斜杠（`\`），不像在 `grep` 中那样的。
4. 输入 `/`。
5. 如果你想忽略模式中的大小写，输入 `i`。
6. 如果你想忽略模式中的空格，输入 `x`。
7. 输入单引号 `'`。
8. 如果你不是通过管道传递给 `perl`，请输入空格，然后输入一个或多个要搜索的文件名。
9. 按回车键执行你的命令。这是一个完整的示例：

```bash
perl -ne 'print if /[acme0-9]/ix' report7
```

在此示例中，正则表达式放置在斜杠（`/`）之间。同样，你在最后一个斜杠（`/`）之后使用 `x` 选项，以便在正则表达式中插入空格以提高可读性。另一个 `perl` 特性是在大括号 `{}` 前面不使用反斜杠。

### 查找不是更大单词一部分的单词

使用 `perl`，你可以搜索不是更大单词一部分的单词。这使用 `grep` 或 `egrep` 是困难或无法做到的。要指定单词边界，请在 `perl` 的正则表达式中输入 `\b`。在 `perl` 中，单词可以包含大写或小写字母、数字或下划线字符（`_`）。

```bash
perl -ne 'print if /\bin\b/ix' report7
```

此命令将显示 `report7` 中任何包含单词 `in` 的行。通过在单词 `in` 前后 `\b`，你可以指定单词 `in` 不能是更大单词的一部分。




因此，输出将不会包含 `tin`、`bin`、`dinner` 或 `into` 单词的行。然而，如果 `in` 位于行首、行尾或周围有标点符号，则它会被显示出来。

在以下命令中：
```bash
perl -ne 'print if /\b in /ix' report7
```
`\b` 只出现在单词 `in` 之前。该命令将显示所有包含以 `in` 开头的单词的行，包括 `into` 或 `intend` 等较大的单词。

要指定某个位置不在单词边界上，您可以使用 `\B`，例所示：
```bash
perl -ne 'print if / in \B /ix' report7
```
此命令将显示所有包含 `in` 字符串作为较长单词部分的行，例如 `inn`、`into` 或 `dinner`。然而，单词 `tin` 和 `bin` 将不会匹配模式，因为它们在单词 `in` 之后有一个单词边界。

**另另**
有关 `perl` 的更多信息，请参阅第 717 页。

## 关闭正则表达式通配符

要关闭正则表达式通配符的特殊性质，请如示例所示在它前面加上反斜杠（`\`）：
```bash
grep '2\*3' mathreport
```
在这里，您正在查找字符串 `2*3`，因此您必须关闭星号（`*`）的含义。如果有大量的通配符需要关闭，可以使用 `fgrep` 命令，它不允许正则表达式通配符。对于 `fgrep` 来说，所有字符都是普通字符。因此，通过此命令：
```bash
fgrep '*****' report
```
您可以查找所有包含五个或更多星号的行。不过，您不需要在每个星号前面加反斜杠，因为您使用的是 `fgrep` 命令而不是 `grep`。

`fgrep` 也用于忽略 变量内容中的通配符，例所示：
```bash
fgrep "$USERINPUT" report
```

### 避免使用 fgrep 的两个原因
`fgrep` supposed supposed 是快速 grep，因为它不需要处理正则表达式。然而，它通常是所有 `grep` 命令中最慢的。X/Open (Ver 2) 规范认为 `fgrep` 已过时，并倾向于使用等效命令 `grep -F`。

## 检查特定字段以选择行 (awk)
`awk` 是一种在所有商业系统中可用的扩展编程语言。您可以使用它的子集作为类似于 grep 的行工具，提供 `grep` 或 `egrep` 不具备的搜索和显示功能。

**另**
有关 `awk` 的更多信息，请参阅第 671 页。

### 如果单字段精确匹配则显示行 (awk)
`grep` 检查整行是否匹配。如果您只想检查行的某个特定字段，可以使用 `awk` 实现。

### 根据单字段的精确匹配显示行
1. 如果您准备在管道中使用 `awk`，请输入将生成供 `awk` 处理输出的 UNIX 命令。以管道符号（`|`）结束此序列。在收到指示前不要按回车键。
2. 输入 `awk '$FNUM ==`。
3. 将 `FNUM` 替换为您想要检查的字段编号。对于 `awk`，您用一个或多个空格或制表符分隔字段。第一个字段是 `1`。最后一个字段可以通过将 `FNUM` 替换为 `NF` 来指定（如 `awk '$NF ==`）。在收到指示前不要按回车键。
4. 输入一个空格，然后输入由双引号括起来的搜索模式。不允许使用通配符。（如果您想使用通配符，请查看下一节。）
5. 输入单引号（`'`）。
6. 如果您没有通过管道到 `awk`，请输入一个空格，然后输入一个或多个要搜索的文件名。
7. 按回车执行您的命令。这里是一个示例：





```bash
awk '$3 == "acme"' report7
```
该命令将显示 `report7` 中第 3 字段仅包含 `acme` 单词的行。

### 根据单个字段的数值显示行 (*awk*)

你可以使用相同的格式，当某个特定字段包含数值时显示该行。数值周围不需要加双引号。你可以进行以下测试：

- `==` 等于
- `!=` 不等于
- `>` 大于
- `>=` 大于等于
- `<` 小于
- `<=` 小于等于

```bash
awk '$1 > 3.6' yearend.rpt
```
上一个命令将显示 `yearend.rpt` 中所有第 1 字段包含大于 3.6 的数字的行。如果该字段（第 1 字段）以字母开头（即它不是数值），awk 会将其视为一个大到无法实现的数值。

### 当单个字段存在正则表达式匹配项时显示行 (*awk*)。

在检查匹配字符串时要使用正则表达式，请将测试操作从 `==` 改为波浪号 (`~`)，并在正则表达式周围加上斜杠 (`/` )如下所示：

```bash
awk '$3 ~ /^acme[0-9]/' report7
```
该命令将显示 `report7` 中所有第 3 字段以 `acme` 开头并跟一个数字的行。

`awk` 允许使用 `egrep` 相同的表达式通配符，包括：
- `+` 匹配前一个元素出现一次或多次
- `?` 匹配前一个元素出现零次或
- `|` 允许的模式
- `()` 用于模式分组

`awk` 和 `egrep` 一样，不允许使用 `{}` 来指定出现次数。

### 根据多个条件显示行 (*&&,|*)

若要在显示行之前检查两个条件，请使用 `&&` 表示逻辑与（AND）。例如，在该命令中：

```bash
ls -l | awk '$3 == "fred" && $5 > 2300'
```
`awk` 正在检查 `ls` 输出的第 3 字段，即每个文件的所有者。它同时检查第 5 字段，即文件的大小（字节）。该命令将仅显示所有者为 fred 且大于 2300 字节的文件。

若要检查一个条件或另一个条件是否真，请使用 `||` 表示逻辑或（OR），例如：

```bash
ls -l | awk '$3 == "fred" || $5 > 2300'
```
该命令将显示所有所有者为 fred 或大小大于 2300 字节的文件。若要对条件进行分组，如下所示使用括号 `()`：

```bash
ls -l | awk '($3 == "fred" || $3 == "jane") && $5 > 2300'
```
该命令将显示所有者为 fred 或 jane 的文件，前提是大小大于 2300 字节。

# 第 16 章 从文件或管道中替换或删除文本
作者 Steve Moritsugu

## 将一个字符串替换为另一个

### 使用正则表达式模式查找替换项
### 在替换中使用找到的文本
### 删除字符串
### 使用 Shell 变量进行替换
### Perl 中的特殊替换功能
### 替换不是较大单词部分的单词 (*perl*)





上一章展示了如何使用正则表达式通配符在文件或管道中查找包含模式的行。该章还展示了正则表达式通配符看起来与文件名生成通配符（Filename Generation Wildcards）相似，但尽管它们使用了一些相同的通配符字符，它们是两组用于完全不同目的通配符。本节将教你如何替换行中的子字符串，以及如何使用正则表达式模式来定义要替换的字符串。

### 另参
有关关于正则表达式通配符的更多信息，请参阅第 388 页。

## 用另一个字符串替换字符串 (*sed*, 正则表达式)

在显示文件输出时将一个字符串替换另一个字符串，请如下使用 `sed` 命令：

```bash
sed 's/Mr. Smith/Ms. Wilson/g' report7
```

`sed` 是流编辑器。它在逐行处理数据流时，执行我们指定的任何编辑更改。

`'s/Mr. Smith/Ms. Wilson/g'` 是我们提供给 `sed` 的编辑命令。该命令通常包含在单引号中，以防止内部的标点符号被 shell 解释。如果你想将任何 shell 变量作为编辑命令的一部分，请使用双引号而不是单引号。

`'s/Pattern/Repl/g'` 是 `sed` 命令的一般格式。`Pattern` 是要搜索的字符串，`Repl` 是用于替换的字符串。`Pattern` 可以包含正则表达式通配符，但 `Repl` 不可以我们的示例搜索字符串 `Mr. Smith` 并将其所有出现的地方替换为字符串 `Ms. Wilson`。即使 `Pattern` 是一个较大单词的一部分，情况也是如此；例如，`Smithson` 将变成 `Wilsonson`。我们将在本章稍后的部分中看到 Perl 如何防止这种情况。

`report7` 是 `sed` 处理的文件。你也可以指定一个文件列表，`sed` 将显示每个文件的内容并进行指示的替换。可以使用文件名生成通配符来生成文件列表。请注意，`sed` 将更改后的输出显示到标准输出；它不会修改文件本身。该命令的输出随后可以管道到另一个命令，或者重定向到文件中。

以下是在管道情况下的使用的相同 `sed` 命令：

```bash
cat report* | sed 's/Mr. Smith/Ms. Wilson/g'
```

`report*` 不是正则表达式通配符。它是一个文件名生成通配符，生成所有以单词 *report* 开头的文件列表。`cat` 命令将这些文件输出到标准输出，并管道到我们刚刚分析的相同 `sed` 命令。`sed` 的输出将逐页显示在屏幕上。

## 在 sed 搜索字符串中使用正则表达式通配符

上一章讨论了正则表达式（R.E.）通配符。请查看附录中的通配符部分以快速参考所有特殊符号。这是一个在搜索字符串中使用 R.E. 通配符的 `sed` 命令示例：

```bash
sed 's/JPC[^A-Za-z]*SPR/JPC-SPR/g'
```

在这个示例中，`[^A-Za-z]` 是正则表达式通配符，表示任何非大写或小写字母的字符。`[^A-Za-z]*` 是正则表达式通配符，表示零或多个任何非字母字符。`JPC[^A-Za-z]*SPR` 是上述 `sed` 命令中搜索的模式。它正在寻找 `JPC` 后面跟着 `SPR`，中间有零或多个非字母字符。该模式可以在以下每一行中找到，最后一行除外：

JPCSPR company long history of JPC-SPR relations
many JPC/SPR employees
JPC*SPR company president negotiate contracts
two companies, JPC and SPR, merged

在这些行中，作者在引用公司名称时并不一致，但我们可以使用 R.E. 通配符模式来匹配所有不同的引用，并将它们替换为一个一致的引用。以下显示了在运行我们的示例 `sed` 命令后，之前的行的显示情况（该命令在此重复）：





```bash
sed 's/JPC[^A-Za-z]*SPR/JPC-SPR/g' report7
```
JPC-SPR 公司悠久的 JPC-SPR 关系、许多 JPC-SPR 员工、JPC-SPR 公司总裁、四次 JPC-SPR 投票、谈判 JPC-SPR 合同、两家公司 JPC 和 SPR 合并。注意最后一行没有匹配正则表达式 (R.E.)，因此该行未进行替换。

### 将替换后的输出保存到原始文件中 (sed)

`sed` 将替换后的行显示到标准输出。如果你想替换文件的内容，必须使用两个 UNIX 命令和一个临时文件。例如：

```bash
sed 's/pattern/repl/g' report7 > /tmp/sed$$
mv /tmp/sed$$ report7
```

这种技术在第 4 章中介绍过。

### 另另参考
有关将输出保存到原始文件的更多信息，请参阅第 114 页。

### 每行仅进行一次替换 (sed)

从替换命令中移除 `g` 标志，使每行最多只替换一次。如果没有 `g` 标志，我们仍然会在模式出现的每行中进行一次替换，但在任何给定行上的替换次数都不会超过一次。例如：

```bash
sed 's/IBW/MCC/' partslist
```

假设前述命令提到的文件 `partslist` 如下行：
```
402 IBW-10 IBW(4),IBW(5) 403-6 IBW-11-6 IBW(3),NT(16)
527 GRV-6 GRV(13),NT(14)
```

前面的 `sed` 命令将把这些行替换为：
```
402 MCC-10 MCC(4),MCC(5) 403-6 MCC-11-6 MCC(3),NT(16)
527 GRV-6 GRV(13),NT(14)
```

注意，每行中只有第一个 `IBW` 被替换了。当你使用脱符号 (`^`) R.E. 通配符或美元符号 (`$`) R.E. 通配符时，应该省略 `g` 标志（参见附录中的通配符部分）。例如：

```bash
sed 's/^[ \t]*Chapter/Section/' book3
```

在这个示例中，`[ \t]` 是一个 R.E. 通配符，表示空格或制表符。方括号内有一个空格和一个制表字符。`^[ \t]*` 表示行开头零或多个空格或制表符。`^[ \t]*Chapter` 表示左侧边缘的 `Chapter` 单词，该单词可以缩进但仍匹配模式。前面的 `sed` 命令仅在 `Chapter` 是行的第一个单词（忽略任何前导空格）时，才会将 `Chapter` 替换为 `Section`。如果 `Chapter` 有缩进，替换后的单词 `Section` 将不会缩进。我们将在下一节介绍如何保留通配符，这将允许替换具有相同的缩进。如果你在配合脱符号 (`^`) 或美元符号 (`$`) R.E. 通配符时包含 `g` 标志，你的命令仍然有效。`g` 标志只是多余的且效率略低，因为当你使用这两种 R.E. 通配符时，每行不可能会多于一个匹配项。

### 更改分隔符 (sed)

紧随 `s` 的字符是标记搜索模式和替换字符串开始与结束的分隔符。斜杠 (`/`)、冒号 (`:`) 和百分号 (`%`) 是常用的分隔符。这三个命令的作用完全相同：

```bash
sed 's/xxx/yyy/g' report7 # 分隔符是斜杠 (/)
sed 's:xxx:yyy:g' report7 # 分隔符是冒号 (:)
sed 's%xxx%yyy%g' report7 # 分隔符是百分号 (%)
```

选择一个不在搜索模式或替换字符串中的字符作为分隔符。例如，将所有的 `/usr/fred` 替换为 `/usr/jane`，我会选择斜杠 (`/`)以外的分隔符。例如：

```bash
sed 's:/usr/fred:/usr/jane:g' report7
```

某些 UNIX 系统允许上述三种常用符号外的任何字符作为分隔符。或者，如果你不想更改分隔符，可以在分隔符字符前加上反斜杠 (`\`)，以便在源字符串或目标字符串中使用它。以下行与前面的示例等效，但更难阅读：





```bash
sed 's/\/usr\/fred/\/usr\/jane/g' report7
```

## 从行中移除（删除）字符串 (`sed, R.E.*`)

要移除或删除一个字符串，请使用 `sed` 替换命令并指定一个空替换字符串。例如：

```bash
sed 's/ (LPX)//g' report
```

此示例会搜索空格后跟着括号 `(LPX)` 的内容，并在任何找到它的地方删除这六个字符。

## 选择性替换或删除

我们可以限制 `sed` 作用的行范围以执行替换或删除。做到这一点的一种方法是指定起始行号和结束行号。例如：

```bash
sed '14,253 s/Mr. Smith/Ms. Wilson/g' report7
```

- `14` 指定了 `sed` 开始替换的起始行号。行 `1` 是文件或管道的第一行。
- `253` 指定了 `sed` 替换的最后一行号。

使用美元符号（`$`）来指定文件的最后一行，如下：

```bash
sed '14,$ s/Mr. Smith/Ms. Wilson/g' report7
```

此命令在你想要处理文件的大部分，但包含一个不想处理的头部部分时非常有用。

选择性替换或删除模式的另一种方法是指定一个必须出现在待处理行中的匹配模式。例如：

```bash
sed '/Acme/s/Mr. Smith/Ms. Wilson/g' report7
```

在前面的示例中，替换将只会在包含匹配字符串 `Acme` 的行上发生。除了 `Acme`，我们还可以使用一个包含 R.E. 通配符的匹配模式。如果匹配模式包含斜杠（`/`），请在它前面加一个反斜杠（`\`），如下：

```bash
sed '\usr\/fred/s/Mr. Smith/Ms. Wilson/g' report7
```

在例例中，替换只会在包含匹配字符串 `/usr/fred` 的行上发生。你也可以使用初始的 `\x` 来选择任何字符 `x` 作为匹配模式的分隔符。例如：

```bash
sed '\:/usr/fred:s/Mr. Smith/Ms. Wilson/g' report7
```

在前面的示例中，替换只会在包含匹配字符串 `/usr/fred` 的行上发生。

如果你想处理一段连续的行，但不知道起始和结束行号，可以使用模式来指定开始和结束，如下：

```bash
sed '/^Chapter 2/,/^Chapter 3/s/Mr. Smith/Ms. Wilson/g' report
```

在此示例中，替换将发生在该区域的所有输出行上，该区域的第一行包含 `Chapter 2,` 单词（其前面可能有一些领先空格）。替换区域结束于包含 `Chapter 3` 的行（允许有前导空格）。注意两个模式都在斜杠（`/`）中并用逗号分隔。

## 使用特殊字符

要在搜索模式中搜索字面星号（`*`）或点（`.`），请在该字符前加一个反斜杠（`\`），这样 `sed` 就不会将其视为通配符。例如：

```bash
sed 's/321\.43/421.43/g' report7
```

在前面的示例中，反斜杠（`\`）表示点不是通配符，因此 `sed` 将搜索 `321.43` 并将该精确字符串的所有出现处替换为 `421.43`。

没有办法可以搜索从一行开始并在另一行结束的模式。你不能在搜索模式或替换字符串中使用 `\n`。你可以使用经过转义的换行符在替换字符串中开始换行，如下：

```bash
$ date
sed 's/ /\/g'
Sun
Mar
22
11:38:09
PST
1998
$
```

在此示例中，你正在将输出中的每个空格更改为换行符。注意在 `sed` 替换字符串中按下回车键换行之前，我们在前面放了一个反斜杠。随后，我们得到了 `PS2` 提示符（`>`），它告诉我们我们仍在输入上一个命令的一部分。然后我们输入剩余的 `sed` 命令。

若要在搜索或替换字符串中包含字面单引号（`'`），你不能像之前的示例中那样使用单引号来包裹字符串。同样，使用前面的反斜杠来转义内部的单引号（`'`）也没有帮助。你必须将 `sed` 命令周围引号改为双引号，如下：

```bash
sed "s/it's/it is/g" report7
```





请参阅后续章节了解在使用 `sed` 时使用双引号而非单引号时可能遇到的其他问题。

# 在搜索或替换字符串中使用 Shell 变量

如果你在搜索或替换字符串中经常使用某个短语，可以将其保存在 Shell 变量中以便重复使用，如下所示：

```bash
CO="Acme"
```

要在 `sed` 命令中使用 Shell 变量，请使用双引号而非单引号，如下所示：

```bash
sed "s/president of $CO/chairman of $CO/g" report7
```

该命令搜索 `president of Acme` 并这些单词更改为 `chairman of Acme`。

如果 Shell 变量与其他字母、数字或下划线相邻，请用花括号 `{}` 将变量括起来，如下所示：

```bash
sed "s/president of ${CO}Ltd/chairman of ${CO}Ltd/g" report7
```

上一个命令搜索 `president of AcmeLtd` 并将这些单词更改为 `chairman of AcmeLtd`。

在使用双引号而非单引号时，你还必须在以下内容之前加上反斜杠 (`\`)：
- 美元符号 (`$`)，如果它不是 Shell 变量的开头
- 反引号 (`` ` ``)，且未包含替换内容
- 字符串内部的双引号 (`"`)
- 你还必须将搜索或替换字符串中的任何字面反斜杠 (`\`) 更改为四个反斜杠 (`\\\\`)。（因为 Shell 会移除其中两个，而反斜杠前面必须有一个反斜杠来表示字面上的反斜杠。）

另请参：关于 Shell 变量的信息，请参阅第 30 页

# 不要替换 0 次或多次出现的内容 (*sed*)

假设 `report7` 包含以下行：
```
five trucks XXX three XX cars
```

假设我们想将任何组 `Xs` 替换为问号 (`?`)。以下是错误的做法：

```bash
sed 's/X*/?/g' report7 # 错误方法
```

以下是上一个命令的输出：
```
? trucks ? ? cars
```

我们之所以多次看到替换字符串的原因是，在任何两个字符之间总是存在任何字符的零次出现。如果我有字母 `ab,`，那么这两个字符之间字母 `X` 的出现次数为零。要修正上一个 `sed` 命令，我们应该指定一个或多个 `Xs`，而不是零或多个 `Xs`。

以下是使用的正确 `sed` 命令：

```bash
sed 's/XX*/?/g' report7 # 正确方法
```

`XX*` 指定一个 `X` 后跟零或多个 `Xs`，这等同于一个或多个 `Xs`。该命令的输出如下：
```
five trucks ? cars
```

# 在替换字符串中使用、通配符匹配的内容 (*sed*)

如果你用转义的括号将正则表达式（R.E.）模式的部分或全部括起来，`sed` 将记住匹配该模式部分的精确字符。然后你可以在替换模式中使用 `\1` 使用该被记住的字符串。使用 `\2` 用于第二个被记住的模式，依此类推。以下是在本章之前分析过的一个示例：

```bash
sed 's/^[ ]*/Chapter/Section/'
```

它将 *Chapter* 更改为 *Section*，但正如我们看到的，替换字符串丢失了它先前的左侧边距。我们可以如下进行修正：

```bash
sed 's/^\([ ]*\)Chapter/\1Section/'
```

`\([ ]*\)` 使用转义的括号来记住在 *Chapter* 单词之前左侧边距发现了多少空格或制表符。`\1` 插入该被记住的字符串。




目标字符串中的 `\1` 会恢复被记住的字符串。

这里有一个不同的示例。假设 `report7` 包含最多六位数字的行。例如：

```
12345 cartons and 534723 sets 73293 boxes of 24 items
1837 containers of 144 packages
```

我们可以使用 `sed` 在数字中插入逗号以使其更具可读性，如下：

```
sed 's/\([0-9]\{1,3\}\)\([0-9]\{3\}\)/\1,\2/g' report7
```

`([0-9] \{ 1,3 \})` 是要查找的模式的第一部分。它匹配一个、两个或三个连续的数字。这些是在上一章中讨论过的通配符。另请附录中的“通配符”部分。我添加了空格以便你看到模式中的元素，但在实际命令中是不允许空格的。匹配到的实际数字被记录为第一个记住的字符串（`\1`）。

`([0-9] \{ 3 \})` 是要查找的模式的第二部分。它匹配三个连续的数字。这些数字必须紧跟模式的第一部分。将这两个模式结合起来，我们的命令就会查找（并替换）任何四个到六个连续数字。此正则表达式（R.E.）匹配到的实际数字被记录为第二个记住的字符串。

`\1,\2` 是替换字符串。它由第一个记住的字符串、逗号以及第二个记住的字符串组成。因此，我们在原始数字之间加上逗号并放回去。`sed` 可以使用许多标点符号。当我开始使用 UNIX 时，我会自动忽略任何带有大量标点符号的 `sed` 命令。这是 UNIX 可能晦涩难的典型例子。我希望曾有人告诉我如何将此类模式分解为简单的元素。命令行上的模式匹配是赋予 UNIX 优雅和力量的特性之一。这是该命令的输出：

```
12,345 cartons and 534,723 sets 73,293 boxes of 24 items
1,837 containers of 144 packages
```

### 消除除搜索模式以外的内容 (*sed*)

假设 `report7` 包含如下行：

```
Income in Jan 52384 as reported in accounting report.
Income in Feb 63283 as reported in accounting report.
Income in Mar 61966 as reported in accounting report.
```

假设我们只想显示月份和金额，并想删除行中剩余的文本。与其为要删除的剩余文本构建模式，我们还有另一种选择：为要保留的文本构建模式，这样更容易。我们可以通过将找到的文本作为搜索模式并记住，来消除除搜索模式以外的内容，如下：

```
sed 's/.*\([A-Z][a-z][a-z][0-9]\{5\}\).\1/' report7
```

`.*` 结束了我们的搜索模式。它指定了模式前后任意零或多个字符，因此整行都将被替换。`(...)` 将记住匹配我们模式的字符，以便我们可以在替换中使用它们。

`[A-Z][a-z][a-z]` 匹配以大写字母开头的三个字母月份。

`[0-9]\{5\}` 匹配五个连续的数字。

替换字符串中的 `\1` 只将匹配到的月份和金额放回，替换掉整行。这是该 `sed` 命令的输出：

```
Jan 52384
Feb 63283
Mar 61966
```

这种技术在设置来自某些 UNIX 命令的值的 shell 变量时也非常有用。我们可以使用 `sed` 提取我们需要的模式并将其保存到变量中，正如下一节所讨论的那样。




# 规则：正则表达式通配符匹配最长跨度

以下是 UNIX `id` 命令的输出：

```bash
$ id uid=501(mori) gid=100(users) groups=100(users),11(floppy)
```

我们可以使用 `sed` 从 `id` 的输出中提取当前登录用户名，该名称位于第一组括号内。以下是实现的一种错误方法：

```bash
$ id sed 's/.*(\(.*\)).*/\1/'      # 错误方法 floppy
```

`.*` 是我们模式的开始和结束，使得我们可以像前一节讨论的那样替换整行内容。

`( ... )` 告诉 `sed` 我们正在寻找括号内的文本。

`\(.*\)` 告诉 `sed` 记住括号内找到的所有实际字符。

替换字符串中的 `\1` 告诉 `sed` 替换内容仅包含括号内找到的内容。

### 第 425 页

由于正则表达式通配符总是匹配最长跨度的这一规则，上述命令找到了最后一个括号内的单词。在待搜索模式的开头，我们有 `.*`，它表示括号之前的零个或多个字符。这可以匹配行中直到第一个括号、第二个括号……或最后一个括号的所有内容。我们可以通过将第一个 `.*` 替换为 `[^]*` 来接近正确结果，`[^]*` 表示左括号以外的零个或多个字符。例如：

```bash
$ id sed 's/[^(]*\(.*\*/\1/' # 仍然错误 mori)gid=100(users),11(floppy)
```

现在问题是，中间的 `.*` 因为最长跨度规则匹配了从第一个左括号到最后一个右括号的所有字符。我们可以通过将中间的 `.*` 替换为 `[^)]*` 来修正这个问题，`[^)]*` 表示右括号以外的零个或多个字符，如下：

```bash
$ id sed 's/[^(]*([^)]*\)).*/\1/' # 正确 mori
```

现在我们提取了第一个括号的内容。我们可以使用相同的结构将结果放入 shell 变量中，如下：

```bash
MYLOGIN=`id sed 's/[^(]*([^)]*\)).*/\1/'` # 提取第一个括号
```

### 正则表达式通配符是贪婪的

我们可以使用术语“贪婪”（greedy）来描述匹配行中最长可能字符字符串的通配符。

### 使用 Perl 替换或删除字符串

perl 是一门完整的编程语言，可以在 UNIX 和 Windows 下运行。尽管它通常没有随任何 UNIX 发行版一起发布，但大多数 UNIX 系统都可以通过互联网获取。如果你的系统上有 Perl，你也可以将其作为简单的命令行工具使用，提供 sed 无法提供的替换功能。

对于简单的替换，如果你对 perl 使用 `-pe` 选项，perl 就像 `sed` 一样。以下两个命令是等价：

```bash
sed 's/Mr.Smith/Ms.Wilson/g'
perl -pe 's/Mr.Smith/Ms.Wilson/g'
```

本章之前讨论了 `sed` 的 `g` 标志。它对 perl 意味着同样的意思：处理行上的所有模式，而不仅仅是行中的第一次出现。像 `sed` 一样，你可以对 perl 省略 `g` 标志，如下：

```bash
perl -pe 's/Mr.Smith/Ms.Wilson/'
```

上述命令只会替换行中第一次出现的 Mr. Smith。同一行中 Mr. Smith 的其他出现不会被替换。

perl 不像 `sed`、`grep` 和 `awk` 那样在用于重复次数的大括号 `{}` 之前或用于记忆字符串的括号 `()` 之前使用反斜杠 (`\`)。如果你想在模式中将括号作为字面字符表示，必须在 perl 中使用前面的反斜杠。只有当字面括号的形式为 `{n}`、`{n,}` 或 `{n,m}` 时，才需要前加反斜杠，因为这些可能会与正则表达式通配符混淆。

虽然 perl 可以完成很多事情，但在这一节中，我将查看 perl 中 sed 无法实现的命令行替换能力。

### 另参阅





有关 R.E. 通配符和 Perl 的更多信息，请参阅第 30 页。

有关 Perl 编程的更多信息，请参阅第 717 页。

### 如何匹配最短跨度 (*perl*)

`perl` 支持但 `sed` 不支持的通配符之一是问号（`?`）。在另一个通配符（例如 `*` 或 `+`）之后使用它，可以将该通配符的匹配范围限制在最短的跨度上。现在我们可以更轻松地解决前一节中的 ID 提取问题了。例如：

```bash
$ id perl -pe 's/.*?\((.*?)\*/\1/' mori
```

`.*?(` 表示左括号之前的任意零或多个字符。`?` 表示匹配最短跨度，因此该模式会匹配行中直到并包括第一个左括号的所有内容。

`(...)` 记录匹配到的实际字符。`perl` 在此处不使用反斜杠（`\`）。

`\(.*?\)` 表示左右括号之间的最短跨度。这限制我们只匹配一组括号内的内容。

### 增强模式的可读性 (*perl*)

`x` 标记（仅在 `perl` 中可用）允许在搜索模式中加入空格，以便分离元素以提高可读性。模式中的所有空格除非在前面有反斜杠（`\`）跟进，否则都会被忽略。我们可以将此应用于 `id` 提取命令：

```bash
$ id perl -pe 's/.*?\(.*)\*/\1/'
```

以下是带有 `x` 标记并为了可读性添加空格相同的命令：

```bash
$ id perl -pe 's/.*? \(.*?\).*/\1/x'
```

### 替换不作为更大单词部分的单词 (*perl*)

在本章较早之前，我们看过了这条命令：

```bash
sed 's/Mr. Smith/Ms. Wilson/g'
```

我们看到它也会将 `Mr. Smithson` 改为 `Ms. Wilsonson`。如果你的 UNIX 系统上安装了 `perl`，可以通过使用 `\b` 通配符（它在 `perl` 中匹配单词边界）来避免这种情况，如下所示：

```bash
perl -pe 's/Mr. Smith\b/Ms. Wilson/g'
```

`Mr. Smith` 匹配模式并会被替换。`Mr. Smithson` 不匹配模式，不会被替换。如果 `Mr. Smith` 后面跟着标点符号或行尾，它仍然满足 `\b`（单词边界）条件并会被替换。多个 `\b` 通配符可以使用搜索模式的开头、结尾和内部。关于 `\b` 通配符的更多信息，请参阅第 40 页。

### 替换字符串或另一种 (*perl*)

使用竖线（`|`）在搜索模式中分隔不同的备选项，如下：

```bash
perl -pe 's/cars|trains|planes/vehicles/g'
```

上述命令将搜索单词 `cars`、`trains` 或 `planes`，并将每一个替换为单词 `vehicles`。

我们可以使用括号对备选方案进行分组，如下所示：

```bash
perl -pe 's/in (two|four)(cars|trains)/by freight/g'
```

上述命令将查找以下短语：
- in two cars
- in four cars
- in two trains
- in four trains

它会将这四个短语的所有出现处替换为单词 `by freight`。

这些括号还会记录匹配的实际文本，可以作为 `\1` 或 `\2` 被引用。如果你不想记录模式，请使用 `(?:...)`，如下所示：

```bash
perl -pe 's/in (?:two|four)(cars|trains)/in three \1/g'
```




`||` 在此处允许匹配单词 `two` 或 `four`。它不会记录匹配到的内容。

`|(cars|trains)` 在此处允许匹配单词 `cars` 或 `trains`，并且会记录匹配到的内容。

`\1` 允许我们在替换部分中使用被记录的字符串（`cars` 或 `trains`）。

## 在匹配 R.E. 模式时忽略大小写

在使用 `sed` 进行替换时，忽略大/小写会非常繁琐。例如：

```bash
sed 's/[aA][cC][mM][eE] [cC][oO][rR][pP]\./Acme Inc./g' report7
```

`/i` 标志会让 `perl` 忽略大小写，允许我们编写如下等效命令：

```bash
perl -pe 's/acme corp\./Acme Inc./gi' report7
```

## 选择性替换或删除

我们可以使用 `if /Q.R.E./` 格式添加限定正则表达式（R.E.），在 `perl` 中进行选择性的替换或删除，其中 `Q.R.E.` 是限定正则表达式的缩写。

```bash
perl -pe 's/Mr.Smith/Ms.Wilson/g if /acme/' report7
```

在在上述示例中，`if /acme/` 设置了 `Q.R.E.`，使得将 `Mr. Smith` 替换为 `Ms. Wilson` 的操作只会在包含 `acme` 的行上发生。

## 使用 awk 替换或删除字符串

`awk` 是一种所有 UNIX 系统都提供的强大的编程语言。正如在前章提到的，当我们需要根据特定字段的内容选择性地处理行时，可以使用简单的命令行形式运行 `awk`。

另需参考
关于使用 `awk` 显示行的信息，请参阅第 407 页
关于 `awk` 编程的信息，请参阅第 671 页

## 基于字段的替换或删除

在之前的章节中，我们学习了当特定字段等于指定值时如何显示文件中的行。例如：

```bash
awk '$3=="acme"' report7
```

在此示例中，只有当 `report7` 中的行第 3 字段完全匹配单词 `acme` 时，该行才会被显示。

可以修改该命令，在第 3 字段匹配单词 `acme` 的行上搜索并替换正则表达式（R.E.）模式，如下：

```bash
awk '$3=="acme" {gsub("R.E.",repl)}{print}' report7
```

`$3` 是要检查的字段编号。`$1` 是第一个字段。`$NF` 表示行的最后一个字段。每个字段由一个或多个空格或制表符分隔。`acme` 是要检查的示例字符串。由于使用了 `==`，它可能不包含任何 R.E. 通配符。`R.E.` 是可能包含通配符的搜索模式。`repl` 用于替换行中所有匹配搜索模式的字符串。`repl` 字符串中的 `&` 将替换为匹配整个 R.E. 的字符。`report7` 是要处理的示例文件也可以指定包含文件名通配符的文件列表。如果没有提供文件，`awk` 将从标准输入读取，因此你可以从其他命令通过管道向其传递。

单引号内部不需要空格。我添加空格是为了可读性，因为它们是被允许的。如果你只想删除所选行上的 R.E. 模式，将 `repl` 字符串更改为空字符串，如下：

```bash
awk '$3=="acme" {gsub("R.E.","")}{print}' report7
```





若只想替换行中第一次出现的内容，而不替换该行中其他出现的内容，请使用 `sub` 而不是 `gsub`，如下：

```bash
awk '$3 == "acme" { sub ("R.E.","") } {print}' report7
```

正如我们在上一章通过 `grep` 看到的那样，我们可以使用 `==`、`!=`、`>`、`>=`、`<` 或 `<=` 等运算符来测试字段中的数值。

```bash
awk '$3 > 6.7 { gsub ("repl") } {print}' report7
```

在上一个命令中，只有当字段 3 包含大于 6.7 的数值时才会发生替换。我们也可以将替换限制在特定字段包含正则表达式模式的行，如下：

```bash
awk '$3 ~ /Q.R.E./ { gsub ("R.E.","repl") } {print}' report7
```

`Q.R.E.` 是对“合格正则表达式”（qualifying R.E.）的缩写，即该正则表达式必须出现在行的某处，替换才会发生。我们可以使用 `||` 表示“或”（OR），使用 `&&` 表示“与”（AND）来组合多个条件，如下：

```bash
awk '$2 <= 3.14 && $3 ~ /acme/ { gsub ("R.E.","repl") } {print}' report7
```

在前面的示例中，除非两个条件都成立，否则不会发生替换：字段 2 小于等于 3.14 且字段 3 等于或包含 `acme`（即指定的 Q.R.E. 模式）。

### 仅显示指定字段

当我只想显示行中的某些特定字段时，我经常使用 `awk`。使用 `{ print $n }` 来仅输出输出中的字段 `$n`，如下：

```bash
ls -l report7 | awk '{print $5}'
```

在前面的示例中，我们使用 `awk` 仅打印 `ls -l` 的字段 `$5`，这给了我们 `report7` 文件的字节大小。我们可以使用相同的命令将大小保存到变量中，如下：

```bash
SIZE=`ls -l report7 | awk '{print $5}'`
```

在上一个命令中，我们使用反引号将 `report7` 的大小保存到变量 `SIZE`。我们可以像这个示例一样同时显示字段 9 的名称和字段 5 的大小：

```bash
ls -l | awk '{print $9, $5}'
acme 17263
report7 2966
report8 34238
```

我们可以在输出中使用双引号指定字面量。我们还可以使用制表符让列对齐得更好。在下面的示例中，我在 `$9` 和 `$5` 之间的双引号内指定了一个制表符作为唯一字符：

```bash
ls -l | awk '{print "file: " $9 " " $5}'
file:acme 17263
file:report7 2966
file:report8 34238
```

另一个例子。在 `ls -l` 的输出中，字段 3 是所有者。我们已经见过如何让 `awk` 根据特定字段的内容处理字段。例如：

```bash
ls -l | awk '$3 == "root" {print "file: " $9 " " $5}'
```

在这个示例中，只有当文件所有者为 root 时，我们才会显示文件名和大小。在下一个示例中，我们检查字段 2 以查看文件的链接数是否大于 4，如下：

```bash
ls -l | awk '$2 > 4 {print "file: " $9 " " $5}'
```

在下一个示例中，只有当字段 4（组名）包含正则表达式模式时，我们才会显示文件信息。例如：

```bash
ls -l | awk '$4 ~ /^work/ {print "file: " $9 " " $5}'
```

在前面的示例中，只有当字段 4（文件所在组）以单词 work 开头，我们才会显示文件名和大小。正如我们之前通过 `awk` 看到的，我们可以分别使用 `||` 作为“或”条件，使用 `&&` 作为“与”条件，如下：

```bash
ls -l | awk '$2 > 4 && $4 ~ /^work/ {print "file: " $9 " " ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)" $5}'
```

### 条件替换特定值 (*awk*)

我们可以通过添加符合此格式的 `awk` 动作来有条件地替换输出字段的值：

```awk
awk {if(condition) $n=value}{print action}
```

这通常用于在当字段低于或高于某个阈值时对其进行修改。

```bash
ls -l | awk '{if ($5 > 20000) $5=20000} {print "file: " $9 ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)" $5}'
file:acme 17263
file:report7 2966
file:report8 20000
```





在在上的示例中，`report8` 的值大于 20000，但我们使用 `awk` 命令将最大的报告值设置为 20000。我们也可以将值设置为双引号中的某个单词，如下：

```bash
ls -l | awk '{if ($5 > 20000) $5="overflow"} {print "file: " $9 "    " $5}'
```
```text
file: acme      17263
file: report7  2966
file: report8  overflow
```

### 将字段格式化为直列 (awk)

`awk` 具有许多 C 语言特性，包括 `printf` 函数。例如：

```bash
ls -l | tail +2 | awk '{ printf("Name: %16s, Size: %5d, Blocks: %6.2f\n", $9, $5, $5/512)}'
```
```text
Name:             acme, Size: 17263, Blocks:   33.72
Name:            report7, Size:  2966, Blocks:    5.79
Name:            report8, Size: 34238, Blocks:   66.87
```

`ls -l` 是我们示例的第一行。注意，shell 管道可以在管道符号 (`|`) 之后拆分，延续到下一行。

`tail +2` 允许我们忽略 `ls -l` 输出的第一行，该行包含了文件开始之前的总块数。

`printf("格式化字符串", v1, v2, ...)` 是 `printf` 函数的通用形式。格式字符串可以包含诸如 `Name:` 这样的字面量。它应该以 `\n` 结尾，表示换行。

我们示例中的 `%16s` 表示格式字符串之后的第一个变量应该使用至少 16 个字符位置来显示。16 之后的 `s` 表示以字符串的格式显示该值。在我们的示例中，该规格被用于显示文件名。

`%5d` 表示格式字符串之后的下一个变量或值应该使用至少 5 个字符位置来显示。5 之后的 `d` 表示以十进制整数的格式显示该值，即一个没有小数部分的整数。在我们的示例中，该规格被用于显示以字节为单位的大小。

`%6.2f` 表示格式字符串之后的下一个值应该使用至少 6 个字符位置来显示。6.2 之后的 `f` 表示以浮点数的格式显示值，即带有小数部分的数字。`.2` 表示在小数点右侧显示两位小数。在我们的示例中，该规格被用于显示以块为单位的计算大小。

`$5/512` 是我们为块大小所做的计算。`$5` 是字节大小，因此 `$5/512` 是块大小。

我们可以在百分号 (`%`) 之后输入负号 (`-`)，使 `printf` 在字段中左对齐输出，如下：

```bash
ls -l | tail +2 | awk '{ printf("Name: %-16s, Size: %-5d, Blocks: %-6.2f\n", $9, $5, $5/512)}'
```
```text
Name: acme         , Size: 17263, Blocks:   33.72
Name: report7      , Size:  2966, Blocks:    5.79
Name: report8      , Size: 34238, Blocks:   66.87
```

当在字段中左对齐输出时，字段后紧跟逗号就不太好看了，因此我们可以从格式字符串中删除逗号，如下：

```bash
ls -l | tail +2 | awk '{ printf("Name: %-16s  Size: %-5d  Blocks: %-6.2f\n", $9, $5, $5/512)}'
```
```text
Name: acme          Size: 17263  Blocks: 33.72
Name: report7       Size:  2966  Blocks: 5.79
Name: report8       Size: 34238  Blocks: 66.87
```

现在注意，数字列在右对齐时更容易比较。让我们回到对两个数值字段进行右对齐，并在第二个字段后重新加上逗号，如下：

```bash
ls -l | tail +2 | awk '{ printf("Name: %-16s  Size: %5d, Blocks: %6.2f\n", $9, $5, $5/512)}'
```
```text
Name: acme          Size: 17263, Blocks:   33.72
Name: report7       Size:  2966, Blocks:    5.79
Name: report8       Size: 34238, Blocks:   66.87
```

是的，现在注意数字列更容易比较了。如果任何一个值都超过了我们指定的长度，完整的值将会被显示，并且其他列将发生偏移，如下：

```bash
ls -l | tail +2 | awk '{ printf("Name: %-16s  Size: %5d  Blocks: %-6.2f\n", $9, $5, $5/512)}'
```





| Name: acme Size: 17263, Blocks: 33.72 |
| Name: long-long-long-filename Size: 1993126, Blocks: 3892.82 |
| Name: report7 Size: 2966, Blocks: 5.79 |
| Name: report8 Size: 34238, Blocks: 66.87 |

## 按列位置删除字符 (cut)

我们可以使用 UNIX `cut` 命令从文件列表或管道中删除指定的列位置并显示结果。`cut` 的 `-c` 选项允许我们指定一个列位置范围。该命令的思考方式是：我们将从输出中剪出这个范围并将其保留，而丢弃其余部分，如下：

```bash
$ date Sun Mar 22 17:58:40 PST 1998
$ date | cut -c5-10
Mar 22
```

在前面的例中，`-c5-10` 指定我们想要保留第 5 到第 10 列，并丢弃其余部分。我们可以指定多个范围，并用逗号分隔，如下：

```bash
$ date | cut -c5-10,24-28
Mar 22 1998
```

在范围中省略结束数字，可以允许该范围延伸到行的末尾，如下：

```bash
$ date | cut -c5-10,24-
Mar 22 1998
```

`cut` 的 `-f` 选项可用于制表符分隔字段时指定字段号，如下：

```bash
$ cat data2 acme	1978	24.6
saturn	1953	8.3
wondra	1981	16.7
cut -f1,3 data2
acme	24.6
saturn	8.3
wondra	16.7
```

在这个例中，`-f1,3`  `cut` 剪出并保留第 1 和第 3 字段。

如果使用制表符以外的字符作为字段分隔符，可以使用 `-d` 选项指定该字段字符，如下：

```bash
$ cat data3 acme:1978:24.6
saturn:1953:8.3
wondra:1981:16.7
cut -d: -f1,3 data3
acme:24.6
saturn:8.3
wondra:16.7
```

虽然可以将 `-d` 字段分隔符设置为空格，但在大多数情况下这并不可用，因为 `cut` 不允许将多个空格视为单个字段分隔符。例如：

```bash
$ cat data4 xxx  yyy   zzz
$ cut -d' ' -f1,3 data4
xxx yyy
```

在前面的例中，数据文件中 `xxx` 和 `yyy` 之间有两个空格。`yyy` 和 `zzz` 之间有三个空格。因此 `cut` 认为文件 `data4` 具有以下内容：

`field1:xxx field2:empty field3:yyy field4:empty field5:empty field6:zzz`

如果你难以理解这一点，可以将空格想象成冒号（`:`），如下：`xxx::yyy:::zzz`。每当两个冒号（实际上是两个空格）连在一起时，它们之间有一个空字段，如下：`xxx::yyy:::zzz`。

我们通常认为一组空格是一个字段。因此，对于显示空白分隔的字段，`awk` 比 `cut` 更有用。例如：

```bash
$ cat data4 xxx  yyy   zzz
$ awk '{print $1,$3}' data4
xxx zzz
```

## 从 UNIX 命令中提取字段

如果你想从 UNIX 命令的输出中提取字段，你应该使用 `awk` 按字段号提取，还是使用 `cut` 按列位置提取？许多命令允许通过这两种方法提取字段。以 `ls -l` 为例：

```bash
$ ls -l -rw-r--r--  1 mori     users      2966 Mar 22 15:08 report7
```

文件名是输出中大小变化最大的字段，所以幸运的是它是最后一个字段。如果它是第一个字段，长文件名会将所有其他字段移出并改变它们的位置。在 `/dev` 目录中，`ls -l` 的字段数量发生了变化，如下：

```bash
$ ls -l /dev | head -5
total 13
crw-------  1 root  root      134 Jan 20 1997 apm_bios
crw-------  1 root  root       16 Feb 18 1994 arp
crw-rw-rw-  1 root  sys        10 Jul 17 1994 atibm
crw-rw-rw-  1 root  sys        14 Jul 18 1994 audio
```




在此目录下，文件的第 5 字段没有大小。相反，它们有两个由逗号和空格分隔的值。这使得文件名位于第 10 字段，而不是其他目录中的第 9 字段。因此，要编写一个程序从包含 `/dev` 目录的 `ls -l` 输出中提取文件名，使用 `cut` 比使用 `awk` 更好。尽管在某些系统上，你可能会遇到非常长的组名或巨大的文件大小，这迫使你调整所使用的列位置。

```
-rwxr-xr-x   1  root      bin             2688  Oct 15  1995 arch
-rwxr-xr-x   1  root      bin             61201  Aug  6  1995 ash
-rw-rw----    1  mori      group           1828  Mar 19  14:56 Main.dt
-rw-rw----    1  mori      group             231  Feb 19  19:04 Personal.dt
```

在前面的示例中，你看到了来自两个不同系统的 `ls -l` 输出。前两行来自 Linux 系统。后两行来自 SCO UNIX。注意，这两个版本的 UNIX 之间 `ls -l` 的列位置是不同的。如果我想写一个程序来从 `ls -l` 中提取文件名，并想让它在 Linux 和 SCO UNIX 上都能运行，我将使用 `awk` 来提取第 9 字段（只要程序不需要处理来自 `/dev` 目录的 `ls -l`）。

从 UNIX 命令输出的字段中提取信息的程序非常常见。有些会使用 `awk`，有些会使用 `cut`。当字段中的值变得很大或者你想在不同的系统上运行相同的程序时，可能会出现问题。只要你意识到这些问题点，通常可以快速发现问题并通过修改提取代码来解决。例如，你可能需要更改 `cut` 命令中使用的列位置，或者更改 `awk` 命令中使用的字段。

## 在文件或管道中替换/删除字符 (`tr`)

`tr` 命令允许我们将一个特定字符的所有出现处转换为另一个字符。它还允许我们删除特定字符的所有出现。`tr` 不允许在命令行上直接处理文件，因此你必须通过管道将任何数据传递给 `tr` 进行翻译。

### 确定你的 UNIX 系统是哪种类型的 `tr`

遗憾的是，有两个版本的 `tr`。它们的区别在于是否要求在字符范围周围使用方括号 `[]`。某些 UNIX 版本有一种类型的 `tr`；其他版本则是另一种类型的 `tr`。

以下是不带括号版本的 `tr` 的工作方式：
```
echo abcdef | tr 'a-c' '1-3'
123def123
```
在该命令中，`echo` 将字母 `abcdef` 发送给 `tr` 命令。`tr` 查找每个字母。如果找到，它将其转换为第二个列表中对应的字符。如果在第一个列表中没有找到该字符，则将其原样传递到输出。

带括号版本的 `tr` 工作方式相同，但它要求对范围使用方括号，如下：
```
echo abcdef | tr '[a-c]' '[1-3]'
123def123
```
以下 UNIX 版本要求 `tr` 使用括号：
- HP-UX
- SCO UNIX 3.2
- Solaris 2.x (SunOS 5.x)

以下 UNIX 版本不需要括号：
- SCO UNIX 3.5 (OpenServer 5)
- Linux (Slackware 3.0.0)
- IBM AIX 4.x

这是一个你可以在系统上运行的简单测试，以查看你有哪种类型的 `tr` 命令：
```
echo abc[] | tr '[a-c]' '12345'
```
如果 `tr` 需要括号，你将看到此输出：
```
123def123
```
如果 `tr` 不需要括号，列表中的括号将被视为任何其他字符；因此它将给出此输出：
```
12345
```

### 将大写转换为小写或反之亦然 (`tr`)

`tr` 最常见的用途之一是将所有大写字母映射（即翻译）为小写字母，如下所示：
```
echo ABCdef | tr "[A-Z]" "[a-z]"
abcdef
```





# 不要使用 `tr` 来替换字符串

`tr 'wilson' 'smith'` 会将所有的 `ws` 翻译为 `ss`，所有的 `is` 翻译为 `ms`以此此类推。当你想要替换字符串时，请使用 `sed`，如下：`sed 's/wilson/smith/g'`

即使你的 `tr` 版本不需要括号，也请使用上述示例中的方括号。如果你的版本需要括号，第一个列表中的 26 个字符将映射到第二个列表中对应的 26 个元素。如果你的版本不需要括号，第一个列表中的 28 个字符将映射到第二个列表的 28 个字符。在这两种情况下，左括号（`[`）都会作为左括号（`[`）传递，右括号（`]`）也是如此。

我们可以如下所示将小写转换为大写：

```bash
echo ABCdef[] | tr "[a-z]" "[A-Z]" ABCDEF[]
```

## 将每个字符的第八位置零 (`tr`)

文本文件通常每个字符的第八位设置为零。这也被最高位。如果设置为 1，它会将字符的含义变为某些扩展字符集，这可能会导致奇怪符号的出现甚至导致你的终端崩溃。下载文件时，你可能会得到一个无法显示的文件，因为它包含某些第八位开启（即设置为 1）的字符。我们可以使用 `tr` 来关闭第八位，如下：

```bash
tr "[\201-\376]\377" "[\001-\176]\177" < file1 > file2
```

`file1` 是某些字符第八位开启的文件。`file2` 将由 `tr` 命令创建，它是 `file1` 的拷贝，但所有字符的第八位都已关闭。即使你的 `tr` 版本不需要括号，也请使用括号，因为相同的命令在所有 UNIX 系统上都能运行。大多数系统允许我们在范围中包含 `\377`，但 SCO UNIX 3.2v 不行。因此，我在上一个命令中在方括号范围之外单独指定了 `\377`，以便该命令适用于所有类型的 UNIX 系统，包括 SCO UNIX 3.2v。

如果你需要开启所有字符的第八位，可以使用类似的命令：

```bash
tr "[\001-\176]\177" "[\201-\376]\377" < file1 > file2
```

## 删除选定的字符 (`tr`)

你可以使用 `-d` 选项配合单个列表从管道中删除选定的字符，如下：

```bash
tr -d '!@#$%^&*()' < file1 > file2
```

该命令从 `file1` 中删除选定的标点符号字符，并将结果保存到 `file2` 中。

如果控制字符出现在数据或文本文件中，可能会导致问题。终端用户在不支持箭头键的应用程序中使用箭头键时，可能会无意输入控制字符。下一个 `tr` 示例显示了如何删除除制表符和换行符以外的所有控制字符：

```bash
tr -d '[\001-\010][\013-\037]\177' < file1 > file2
```

上述命令应用于 `tr` 需要括号的系统。如果在另一种类型的系统上使用，它还会删除输出中我们需要的括号。对于不需要括号的系统，这里是删除除制表符和换行符以外的所有控制字符的相同命令：

```bash
tr -d '\001-\010\013-\037\177' < file1 > file2
```

## 将大多数控制字符翻译为一个错误字符 (`tr`)

与其删除所有控制字符，你可能想将它们翻译为某些字符，作为内容已修改修改的错误指示。使用 `[X]` 作为第二个字符串，将第一个列表中的所有字符翻译为字符 `X`，如下：

```bash
tr '[\001-\010][\013-\037]\177' '[^*]' < file1 > file2
```

上述命令将除制表符和换行符以外的所有控制字符翻译为脱号（`^`）。如果你的系统不需要括号，请使用这种形式的 `tr` 命令：

```bash
tr '\001-\010\013-\037\177' '[^*]' < file1 > file2
```

注意，即使在范围不使用括号的第二种情况下，`[^*]` 周围也是需要括号的。

## 替换/删除整行

有几种方法可以替换或删除整行。





# 替换整行 (sed)

要完全替换包含特定模式的任意行，你可以如下使用 `sed` 命令：

```bash
sed 's/.*acme.*/  ***canceled***  /'
```

`acme` 代表要查找的模式。你可以将其替换为任何所需的正则表达式（R.E.）。

`.*acme.*` 匹配包含 `acme` 的整行，因此整行都将被替换。

# 删除包含 R.E. 模式的行 (grep)

要完全删除任何包含模式的行，对 `grep` 使用 `-v` 选项，如下：

```bash
grep -v 'R.E.'
```

`grep` 的 `-v` 选项会反转 `grep` 的含义。`grep` 不再显示包含模式的行，而是只显示不包含模式的行，从而从输出中移除任何包含模式的行。

另另：有关 `grep` 命令的更多信息，请参阅第 30 页。

# 删除行 (uniq)

使用 `uniq` 命令从输出中删除任何与前一行完全匹配的行。假设我们有一个名为 `cars` 的文件，其中包含不同品牌的汽车，如下所示：

```bash
$ cat cars
ford
pontiac
BMW
ford
pontiac
```

这是对该文件执行 `uniq` 命令的输出：

```bash
$ uniq cars
ford
pontiac
BMW
```

在前面的文件中，只有第 2 行与前一行匹配，因此它被删除了。你可以看到该文件中还有其他匹配的行，但 `uniq` 没有删除它们，因为它们并不相邻。注意，`sort` 命令会将相同的行并置相邻，如下所示：

```bash
$ sort cars
BMW
ford
ford
pontiac
pontiac
$ sort cars | uniq
BMW
ford
pontiac
```

在这个示例中，我们通过先对行进行排序让 `uniq` 运行得更高效。我们可以通过将上一个命令的输出通过到 `wc -l` 来统计行数，从而计算文件中不同汽车的数量，如下所示：

```bash
$ sort cars | uniq | wc -l 3
```

`uniq` 的 `-u` 选项仅显示唯一的行——即没有相邻匹配行的行。例如：

```bash
$ sort cars | uniq -u
BMW
```

`-d` 选项仅显示重复的行，如下：

```bash
$ sort cars | uniq -d
ford
pontiac
```

`-c` 选项统计每行重复的次数，如下：

```bash
$ sort cars | uniq -c
1 BMW
3 ford
2 pontiac
```

另另：有关 `sort` 命令的更多信息，请参阅第 202 页。

# 第 17 章 使用 vi 编辑文本文件

Steve Moritsugu

## 开始使用 vi 文本编辑器

## 学会 10 个命令，你就可以编辑一切

### 接下来需要学习的八条命令
### 插入文本的所有方法
### 在文档中移动的所有方法
### 删除文本的所有方法
### 修改文本的所有方法

## 介绍 vi 文本编辑器





文本编辑器允许你创建和修改文本文档，这些文档仅包含你可以在键盘上输入的字母和字符。相比之下，文字处理器不仅允许编辑文本，还允许通过选择字体大小和样式来更改文本的呈现。在 UNIX 下，简单的文本文件极其重要。除少数例外外，所有的 UNIX 系统管理工作最终都是通过编辑自定义系统并控制其运行的文本文件完成的 Shell 脚本和 C 程序是由程序员以文本文件的形式输入的。即使是 Internet Web 页面也是简单的文本文件，其字体、颜色和图形都是作为文本指令指示 Web 浏览器的。

`vi` 是所有 UNIX 系统上都可用的文本编辑器。不要在 `vi` 中寻找字体选择，因为它不是文字处理器。有些 UNIX 用户不喜欢 `vi`，因为你必须记住所有的命令。它没有下拉菜单来帮助你剪切、粘贴或替换文本。`vi` 内部没有帮助功能（但我将教你如何解决这个问题）。

某些类型的 UNIX 系统提供了 `vi` 的替代方案，例如 `emacs`、`pico` 或适用于 UNIX 的 `WordPerfect`。有些用户在 Windows 下编辑文本，然后将其下载到 UNIX。如果你只在一个 UNIX 系统上工作，并且能保证永远不需要在不同的系统上工作，请选择系统上可用的任何文本编辑器。然而，如果你处理多种类型的商业 UNIX 系统，你可能会发现将你喜欢的编辑器移植到每个系统中是一场徒劳的战斗。在这种情况下，请跟随我学习这一关于 `vi` 的章节，我将让你轻松学会基础知识。`vi` 就像 UNIX：入门很难，但一旦你开始，就可以做一些强大的事情，这一切都是值得的。

## 如何开始 vi

## 如何启动和结束 vi

1. 在 shell 提示符处，输入 `vi`。（不要按回车。）
2. 输入一个空格，然后输入你要编辑的文件名。（不要按回车。）如果文件尚不存在，`vi` 将为你创建它。如果文件在另一个目录中，请输入其 `pathname`。如果你只想练习 `vi`，请看以下内容。高级用户可以在此阶段省略文件名；这允许你进入 `vi`，但你必须记住在退出 `vi` 之前保存你的工作。
3. 按回车键。`vi` 将启动并显示你的文件内容。由于 `vi` 是全屏编辑器，它会在超出文件末尾的行开头放置波浪号 (`~`)）。如果你正在编辑一个新文件，屏幕上的所有行都会以波浪号开头，直到向这些行中插入文本。
4. 注意，你所有的更改都在工作区中进行，而不是在文件本身。如果你在退出 `vi` 之前没有保存工作，所有的编辑将丢失。
5. 完成编辑后，按 `Esc` 然后输入以下内容：
```
:wq (保存工作并退出 vi)，或者输入：
:q! (放弃[即，丢弃]你的更改并退出 vi)
```
按回车键完成此步骤。

## 创建用于 vi 练习的文件

如果你是 UNIX 的初学者，你可能还没有任何可以安全编辑的文件；因此，请按照此程序创建一个临时文件，可以用它来练习 `vi`。

### 如何使用 vi vi

1. 登录 UNIX。
2. 在 shell 提示符处，输入 `> cal-junk`。按回车键执行此行。在任何仅用于练习且以后可以删除的文件名中使用 `junk` 单词。此步骤将创建一个你可以编辑的文本文件。
3. 当你想练习 `vi` 时，在 shell 提示符处，输入 `vi-junk`。按回车键执行此行。
4. 完成 `vi` 练习后，按 `Esc` 然后输入以下内容：
```
:wq (保存工作并退出 vi) 或 :q! (放弃[即，丢弃]你的更改并退出 vi)
```
按回键完成此步骤。要删除此练习文件，输入以下内容：
```
rm cal-junk
```
按回车键执行此行。完成工作后清理现场是良好的习惯，但在练习 `vi` 期间，你可以延迟几天几周删除此文件。

## 仅需 10 条 vi 命令即可编辑任何内容





vi 中有超过 75 个独立的字母和标点命令需要学习。你应该从哪里开始呢？这里有需要学习的前 10 个 vi 命令，它们将让你能够编辑任何内容。如果你是 vi 初手，请按照前面的步骤创建一个 `cal-junk` 练习文件，以免意外修改重要文件。

## 使用 h, j, k, l 移动

在 vi 中，你可以通过输入表 17.1 所示的命令来移动光标。

永远不要在 `/etc/passwd` 上练习。这是一个关键的系统文件，你不应该动它，特别是当你以 root 登录时。实际上，不要对 `/etc` 中的任何文件进行练习。不要以 root 身份进行练习。

### 表 17.1 使用 h, j, k, l 移动

| vi 命令 | 说明 | 助记 | 备用键 |
|---|---|---|---|
| h | 向左移动 | 最左侧字符 | 左箭头键 |
| j | 向下移动 | j 到行下方 | 下箭头键 |
| k | 向上移动 | k 循环向上 | 上箭头键 |
| l | 向右移动 | 最右侧字符 | 右箭头键 |

这四个键 `h`, `j`, `k`, `l` 在键盘上彼此相邻。表中的助记方法将帮助你记住每个键的作用。例如，小写的 `j` 位于行下方，提醒你它是“向下”（down）。

不要过度依赖箭头键作为备用。有时你会发现 vi 中除了箭头键外，所有功能都能正常工作，因为箭头键需要终端设置、键盘以及某些系统文件（如 `termcap` 或 `termin`）之间的良好协调。即使箭头键在大多数情况下都能用，在连接缓慢或负载过重的系统或网络上，它们也可能变得不可靠。学习使用 `h`、`j`、`k` 和 `l` 而不是箭头键，也将有助于你以后进行键映射以及在 Korn shell 中进行命令行编辑（这是一个非常有用的功能）。

当你在 vi 中输入 `h`、`j`、`k` 或 `l` 时，屏幕不应该回显这些字符。相反，光标应该向所需的方向移动。你不需要按 `Enter` 来执行命令。如果 `h`、`j`、`k` 或 `l` 出现在屏幕上，说明你某种方式进入了插入模式并将这些字符插入了工作区。按 `Esc` 退出插入模式；`h`、`j`、`k`、`l` 就能正常工作了。

注意大写锁定下的 `J` 键。如果你不小心开启了大写锁定，使用 `h`、`k` 或 `l` 移动是无害的。但 `j` 是向下，而 `J` 是合并行。多个 `J` 会合并许多行，在你还没反应过来之前就已经成了一团糟。在下一章关于映射的内容，我将展示一种防止这种情况的方法。

除非工作区的该位置有文本，否则 vi 不允许你移动到那里。你不能越过行尾。你不能从最后一行向下。如果你编辑一个空文件，在输入某些文本之前，你将无法移动。

另另：有关命令行编辑的更多信息，请参阅第 497 页

错误蜂鸣声

如果你尝试在 vi 中执行非法命令（例如从最后一行向下移动），vi 会发出蜂鸣以指示错误。可以关闭此功能（`:set noerrorbells`），但 vi 初学者应该留意错误蜂鸣声并从这些错误中学习。

使用重复计数

你可以直接在大多数 vi 命令之前加上一个重复计数。`50h` 将向左移动 50 个字符。`999j` 将向下移动 999 行。有了重复计数，很容易向上或向下移动很距离，这在巨大的文件中是必要的。如果给定的光标移动重复计数太大，结果将取决于你所使用的哪种 UNIX。如果 vi 发出蜂鸣，光标将不会移动。如果没有蜂鸣，vi 已将你移动尽可能远并停止在工作区的最后一个字符或行。

使用 i 插入

这是要学习的第五个 vi 命令。输入 `i` 进入插入模式。在插入模式下，你输入的所有文本都会在当前光标位置输入到工作区。按 `Esc` 关闭插入模式；这会让你回到 vi 命令模式。你可以在每行后按 `Enter` 在一次插入中输入多行。

使用 x 和 dd 删除




## vi 命令概述

这是要学习的第六个 vi 命令。输入 `x` 可以删除光标所在位置的一个字符。`25x` 将删除 25 个字符。vi 会减小任何大于行剩余部分的重复计数，以便只删除当前行的剩余部分，而不会影响后续行。

**提示：** 注意插入模式（Insert mode）下的箭头键。如果你在插入模式下尝试使用箭头键，在某些系统上可能无法产生你预期的更改。在移动光标之前，请按 `Esc` 退出插入模式。然后将光标移动到下一个区域并输入 `i` 重新进入插入模式。

这是要学习的第七个 vi 命令。输入 `dd` 删除当前行。在输入 `dd` 时，你可以处于行的任何位置。`25dd` 将删除 25 行，包括当前行在内的所有行。

### `dd` 的名字是怎么来的？

vi 有有一种约定，双字母命令作用于整行。`cc` 更改整行；`yy` 复制（yank）整行；而 `dd` 删除整行。

### 使用 `J` 合并行

与某些编辑器不同，vi 没有可以通过删除来合并两行的行尾字符。合并两行的唯一方法是使用 `J` 命令。`5J` 将合并 5 行。`J` 和 `2J` 的作用相同：它们都会合并行。第二行开头的任何空格都会缩减为单个空格。

### 使用 `:wq` 保存并退出

到目前为止，你所有的更改都修改了 vi 工作区，这是一个临时文件。要保存工作并退出，请输入以下内容：`:wq`。冒号会让光标移动到最后一行，`w` 和 `q` 会显示在屏幕上。按回车完成此命令以及任何其他以冒号（:）开头的 vi 命令。

### 使用 `:q!` 放弃更改

这是要学习的第十 vi 命令。如果你不喜欢你的更改，可以通过输入 `:q!` 在不保存回原始文件的情况下退出 vi。这将让你回到 shell 提示符并丢弃你所做的所有编辑。请注意，通过 `:q!` 丢弃编辑更改后，你以后无法改变主意并找回它们。

**提示：** 使用退格键（backspaces）取消冒号（:）命令。如果你输入了类似 `:q!` 的命令，然后改变了主意，**不要**按 `Esc`，因为这将执行 `:q!` 命令并丢弃所有更改。要取消冒号命令，请反复按退格键或 `Ctrl+H` 直到光标离开最后一行。左箭头键无法实现此功能。这就完成了使用 vi 需要的 10 个命令。你现在可以编辑任何内容了。练习这 10 个命令一段时间。然后阅读本章的后续章节，查看你应该掌握的下一组 vi 命令。

## 为 vi 添加帮助功能

vi 内部没有帮助功能，这使得如果你偶尔使用它，它会变得很难用。这里是在你在 vi 中添加一个帮助功能的方法。

1. 使用 vi 创建一个文本文件 `/tmp/vihelp`，内容如下：

```echo "(You may put repeat count BEFORE most commands.)"
:q!--abort vi without saving
cW--change word(s) until ESC
x dd--delete char(s) or line(s)
G--go to end of file
1G--go to line of file
i--insert text until ESC
A--insert at end of line until ESC
J--join lines
h,j,k,l--move left,down,up,right
Ctrl+L Ctrl+R--repaint the screen
r--replace one char
:wq--save and exit
:f--show filename, current line, size
u--undo
```

2. 确保你在第一行和最后行包含了引号（''）。
3. 以 root 身份登录或要求你的系统管理员执行后续操作。




4. 输入 `ls -l /usr/bin/vihelp`。

我们希望看到 `No such file.` 消息。

如果此文件已经存在，请**不要**继续此操作。

5. 输入以下命令：

```bash
cd /usr/bin mv /tmp/vihelp vihelp
chmod 755 vihelp
```

6. 现在退出并以非 root 用户身份重新登录。

7. 输入 `vi` 编辑任意测试文件，并通过输入以下内容来检查新的帮助功能：

```vi
!:vihelp
```

8. 当你阅读完帮助信息并准备恢复 `vi` 编辑时，按下 Enter 键。

9. 你可以根据需要使用 `vi` 来扩展文件 `/usr/bin/vihelp` 中的帮助信息。请确保最后的引号出现在最后行的末尾。

# 接下来学习这八个 `vi` 命令

## 按 `Ctrl+L` `Ctrl+R` 重绘屏幕
有时在通过调制解调器线路或慢网络时，屏幕上可能会出现乱码，或者光标最终停留在与 `vi` 认为的位置不同的行。如果光标在错误的行上，当你向右移动空格时，你会看到来自其他行的字符出现。为了解决这个问题，按下这两个字符 `Ctrl+L` `Ctrl+R` 来重绘屏幕以匹配工作区状态。某些终端只需要 `Ctrl+R` 或只需要 `Ctrl+L` 即可重绘屏幕。如果你同时使用两者（无论顺序如何），它适用于所有情况！

## 使用 `u` 撤销更改
`vi` 会记住最后一次的插入、删除或修改。如果你想撤销它，请在 vi 命令模式下输入 `u` 命令。执行 `u` 命令时，你不需要位于更改所在的行附近。移动光标的命令会被 `u` 命令忽略且无法被撤销（实际上，光标移动命令可以通过输入 `` ` `` 来撤销）。第二次 `u` 命令将撤销撤销操作，再次恢复上一次更改。第三次 `u` 命令将切换撤销状态并移除上一次更改。第四次 `u` 命令将再次恢复上一次更改，以此此类推。如果你使用 `5J` 命令合并了五行，执行 `u` 命令会将它们拆分成原始的行。第二次 `u` 将再次将它们合并。你可以观察行在每次输入 `u` 命令时神奇地合并然后又分离。这是学习更多 `vi` 命令的极佳方法。

## 出错时使用 `u` 命令
1. 有时，意外的控制字符或行噪声会导致 vi 屏幕上出现乱码。按下 `Ctrl+L` `Ctrl+R` 重绘当前屏幕并清除乱码。
2. 输入 `u` 命令撤销上一次更改。光标将移动到该更改的位置。
3. 多次输入 `u` 以观察更改的切换。如果该更改是意外导致的不良副作用，请再输入一或两次 `u` 来撤销该错误的更改。

## 在行尾追加文本
`A` 命令将光标移动到行末尾。然后它允许你从该字符之后开始插入。按下 `Esc` 退出模式。

## 定期保存你的工作
如果你在会话中进行了大量更改，定期保存工作是明智的。输入 `:w`。这样，如果你不小心按错了按键或系统崩溃，你可以重新登录，磁盘文件将包含已保存的内容。

## 保存到不同的文件
你可以通过输入以下内容将工作保存到与正在编辑的不同的文件中：

```vi
:w newfile
```
例如，如果我正在编辑关键文档，我可能会输入：

```vi
:w doc1
```
在更多编辑之后，我可能会输入：

```vi
:w doc2
```




# 处理写入权限失败

当尝试保存工作时，`vi` 可能会返回类似 `Permission Denied`（拒绝访问）或 `Read Only`（只读）的错误。

## 在 `vi` 中处理保存文件的错误

1. 尝试使用此命令保存文件：
```bash
:w!
``````
2. 如果失败，按如下方式临时保存工作：
```bash
:w /tmp/cantwrite :q
``````
3. 现在，你可以将 `/tmp/cantwrite` 中的更改移动到目标的文件名或目录。

## 使用 `r` 替换单个字符

输入 `r` 替换一个字符。输入的下一个字符将显示在屏幕上，替换光标位置的字符。然后你将回到命令模式，准备好输入新的 `vi` 命令。

## 使用 `cW` 修改单词

使用 `cW` 修改单词

1. 将光标移动到要更改的单词或多个单词的开头。
2. 如果你想更改多个单词，输入要更改的单词数量。不要按回车键。
3. 输入 `cW`。美元符号 (`$`) 将出现在最后一个更改单词的末尾。不要按回车键。
4. 开始输入替换文本。它可以比被更改的单词短，也可以长。它的单词可以更少或更多。你可以使用回车键输入多行。如果新文本较长，随着你的输入，行的剩余部分将向右移动。
5. 输入所有替换文本后按 `Esc`。如果新文本比被替换的单词短，行的剩余部分将自动向左移动以填充空格。
6. 这是一个示例命令：
```bash
3cWacmeESC
```
上述命令将更改（替换）三个单词（包括光标所在的单词）。它会将这三个单词替换为单个单词 `acme`。

## 使用 `1G/G` 跳转到文件开头/结尾

输入数字然后按大写 `G` 跳到该行，例如 `1475G` 将将光标移动到工作区的第 1475 行。如果文件没有那么多行，它会发出错误提示。对于 C 语言程序员来说，快速跳转到文件中的特定行非常有用，因为编译器通常会报告发生错误的源代码行号。`G` 命令的两个常用用途是 `1G` 跳到文件开头和 `G` 跳到文件结尾。

## 使用 `:f` 查看文件名、大小和当前位置

输入 `:f` 查看你正在编辑的文件名、当前所在的行以及文件的总行数。例如：`"Modified line 43 of 35"`

## 帮助你使用 `vi` 的技巧

这里是需要学习的第三组 `vi` 命令。

### 使用 `U` 恢复整行

在 `vi` 命令模式下，大写 `U` 将撤销自你移动到该行以来的所有更改。离开该行后，你将失去将其恢复到原始状态的能力。

## 使用 spell 查找拼写错误的单词

标准 UNIX 仅具有基本的拼写检查功能。以下步骤演示了如何使用它。

### 如何查找拼写错误的单词

1. 从 shell 提示符输入：
```bash
spell < filename
```
（filename 是要拼写检查的文件。）将 `pg` 替换为你喜的工具，以便逐页查看结果。
2. 所有未知单词将显示在屏幕上，每行一个。不会显示拼写错误单词所在的上下文（即完整行）。
3. 在脑中标记任何拼写错误的单词，然后手动使用 `vi` 在文件中一个一个查找并纠正它们。





# 段落格式化

如果你正在使用标准的英文段落，vi 的令人沮丧的限制之一就是当你需要延长或缩短段落内部某一行时。长度不正常的行在段落中间看起来非常不协调。你可以通过将文本移动到下一行或从下一行拉取文本来修复该异常行；但现在下一行又变成了长度不正常。你随后必须手动调整每一行直到段落末尾。

这里是处理这种情况的两种更简单的方法。

## 如何使用 Fmt 格式化段落

1. 在 shell 提示符下，输入以下内容：
```
fmt
```
如果 get 错误 `Not found`，说明你的 UNIX 版本不支持 `fmt`。如果未找到 `fmt`，请跳过此步骤并使用以下步骤进行格式化。SCO UNIX OpenServer 5 不提供 `fmt`，但在 Solaris 2.x、AIX 4.x 和 Linux 上可用。

2. 在 vi 中格式化段落，将光标移动到段落开头。输入以下内容：
```
!fmt
```
这应该调整段落中其余行，使得没有行太长或太短。如果这不起作用，输入 `u` 撤销该更改，并改用下一个步骤。

3. `fmt` 命令假设段落的左边距是正确的。如果左边距也需要调整，输入：
```
!fmt-c
```

如果你的系统上没有 `fmt` 且行中没有制表符，以下是一个效果良好的段落格式化步骤。如何格式化段落：

1. 输入 `cd` 进入主目录。
2. 输入 `cp .exrc .exrcbak` 备份你当前的 `.exrc` 文件。如果 `.exrc` 不存在，请忽略任何 `cp` 错误（在这种情况下，不需要备份）。
3. 输入 `vi .exrc`。
4. 查看此文件的完整内容，并确保没有哪行以 `map` 开头。如果有这样的行，请**不要**继续此操作。
5. 确保有一行以 `set wrapmargin=` 或 `set wm=` 开头。如果你没有找到这样的行，请在文件末尾输入此行：
```
set wm=10
```
6. 按 `Esc` 然后按 `Q`。光标将跳到最后一行并出现冒号。
7. 输入 `map g072lBi`。不要按回车。
8. 按 `Ctrl+M`。按 `Esc`。按 `Ctrl+V`。按 `Esc`。现在按回车。
9. 输入 `vi`。屏幕底部应该应回显 `vi` 单词。按回车。
10. 输入 `:wq` 将你的更改保存到 `.exrc` 并退出 `vi`。
11. 输入 `cat -v .exrc` 检查一切是否顺利。在文件末尾，你应该看到这一行：
`map g072lBi^M^[`
如果出现错误，请使用 `vi` own 正该行。如有必要，从备份恢复 `.exrc` 并重新开始。
12. 上述步骤准备了 `.exrc` 文件，每个登录用户仅需执行一次。现在使用 `vi` 编辑一个包含需要格式化段落的测试文件。确保文件已备份，以防出现问题。将光标移动到需要格式化的段落开头。
13. 数一下段落中的行数。输入该数字后跟 `J`，将段落中的所有行合并为一条长行。
14. 重复输入 `g` 直到段落的所有行都已格式化。

## 恢复丢失的编辑





在 shell 提示符中输入 `vi -r`。

1. 你将看到一个文件列表，这些文件是 `vi` 在编辑它们时异常终止而保留的。这些实际上是 `vi` 工作区文件，它们可能包含某些尚未保存到磁盘文件的编辑。

2. 如果你看到了想要查看的文件，输入以下内容：
```
vi -r filename
```
文件名必须与列表中显示的完全一致，即按照显示的内容精确输入任何前置的目录名称。

3. 使用 `vi` 查看文本后，如果你决定保留这些信息，请输入：
```
:w absfile
```
`absfile` 代表你想要保存为该文件的文件的完整路径。

4. 按照以下方式退出 `vi`：
```
:q
```

5. 在你通过这种方式恢复文件并退出 `vi` 后，该文件将从保留列表中移除，你将无法再次尝试恢复它。定期检查你的保留文件并进行恢复、保存或丢弃是一个好习惯，以防止 `vi` 保存文件在保留区域堆积。

# 以只读模式启动 vi

若要在只读模式下编辑文件，请在命令行中将 `vi` 替换为 `view`。`view` 以只读模式启动。如果你尝试写入文件，`view` 将报错提示该文件是只读的。对于那些只想查看内容而不打算进行更改的情况，这是一种很好的预防措施。我特别建议 root（即系统管理员）用户在仅查看配置文件时使用 `view`。你可以如下所示覆盖只读模式并保存更改：
```
:w!
```

# vi 插入命令表

| 命令 | 描述 |
| :--- | :--- |
| `i` | 在光标前插入文本，直到按下 `Esc` |
| `I` | 在行首插入文本，直到按下 `Esc` |
| `a` | 在光标后插入文本，直到按下 `Esc` |
| `A` | 在行尾插入文本，直到按下 `Esc` |
| `o` | 在当前上方打开新行并插入，直到按下 `Esc` |
| `O` | 在当前下方打开新行并插入，直到按下 `Esc` |

# 在 vi 中移动

`vi` 中的许多光标命令允许我们移动到屏幕的不同部分或我们正在编辑的文件。首先，我们需要介绍如何计算单词，这对于移动、删除和替换非常有用。

## 使用分离单词、包含单词与非单词的区别

分离单词（或定界单词）是指任何由一个或多个空格、制表符或行尾分隔的字符组。包含单词是指任何由标点符号、空格或行尾分隔的字母或数字组。`Hudson-on-the-Bay` 是一个分离单词，但四个包含单词。每个双连字符（--）都是一个非单词。因此，`Hudson-on-the-Bay` 包含了包含单词和非单词。下表显示 `w` 命令允许我们按包含单词和非单词向前移动。下一章将展示分离单词与包含单词的有用之处。

# vi 移动命令表

| 命令 | 描述 |
| :--- | :--- |
| `hjkl` | 向左/下/上/右移动 |
| `0` | 移动到当前行首 |
| `^` | 移动到当前行第一个单词的开头 |
| `$` | 移动到当前行的最后一个字符 |
| `wb` | 向前/后移动一个包含单词或非单词 |
| `WB` | 向前/后移动一个分离单词 |
| `eE` | 移动到当前包含/分离单词的末尾 |
| `LMH` | 移动到屏幕上最低/中间/最高的行 |
| `{}` | 移动到上一个/下一个段落的开头 |
| `Ctrl+FC+B` | 向前/后移动一整屏 |
| `Ctrl+DC+U` | 向下向上移动半屏 |
| `nG` | 跳到第 `n` 行 |
| `1GG` | 跳到第一/最后一行 |

# 通过搜索字符串移动

将光标移动到特定模式

1. 在 `vi` 命令模式下，输入 `/` 在工作区内向前搜索。输入 `?` 在工作区内向后搜索。光标将移动到屏幕的最后一行并显示 `/` 或 `?`。在接到指示前不要按回车键。




2. 输入要搜索的模式。按回车键执行。光标将移动到该模式的下一次出现处。你的模式可能包含第 15 章中描述的正则表达式通配符模式。
3. 如果在文件的剩余部分没有找到该模式，`vi` 将绕回并从文件的另一端开始搜索。如果 `vi` 必须绕回，通常会显示此消息：`Wrapped`。如果模式在整个文件中任何处都不，光标将留在原处，并显示此消息：`Not found`。
4. 要重复上一次搜索，输入 `n`。这将找到相同模式的下一次出现处。
5. 要反反方向重复上一次搜索，输入 `N`。如果你之前是在文件中正向搜索，`N` 将在文件中反向查找下一个出现处。

## 在行内移动到特定字符

如果你通过互联网登录到 UNIX 系统，可能会发现对 `vi` 按键的响应有几乎让人无法忍受的延迟。与其计算移动多少个字符或单词，当我需要通过一个命令向右移动到目标字符时，我经常使用 `vif` 命令。

### 在行内移动到特定字符

1. 确定我想移动到的字母或数字。我通常避开元音，因为它们在行中太常见。
2. 输入 `f` 后跟所需的字母或数字。
3. 光标将移动到该字符的下一次出现处。
4. 输入 `;` 移动到该字符的下一次出现处。

### 寻找匹配的括号符号

如果你是程序员，可能需要使用嵌套的括号符号（如 `( { ] )` 输入复杂的公式。例如：
```
printf("%d", ...)
```
`vi` 理解这种嵌套，可以自动找到匹配的闭合或开启括号、中括号和大，即使它们在不同的行。将光标放在所需的括号符号上并按下 `%`，即可移动到该嵌套层级的匹配括号符号上。

## 设置标记以便返回那里

`vi` 为处理巨大的文本文件提供了极大的便利。`vi` 可以标记并返回到文件中多达 26 个不同的位置。

### 设置标记并返回标记处

1. 将光标移动到文件中的目标位置并输入 `ma`。`m` 是标记此处的 `vi` 命令，`a` 是我们稍后引用此处的名称或标签。我们可以使用字母表中的任何字母；因此我们可以设置最多 26 个标记。
2. 要稍后返回该处，输入：`'a` 或 `` `a``。
3. 单引号 (`'`) `a` (`'a'`) 表示跳转到包含标记 `a` 的行开头。
4. 反引号（`` ` ``）表示跳转到设置标记时所在的精确字符。

## 删除文本的 vi 命令

在下表中，请注意 `vi` 删除命令是如何基于光标移动的。你可以在大多数这些命令前加上重复计数。

| vi 命令 | 描述 |
| :--- | :--- |
| `dd` | 删除字符(s)/整行 |
| `D` | 从光标删除到行尾 |
| `dwW` | 向前删除到下一个包含的/分隔的单词 |
| `dB` | 向后删除到下一个包含的/分隔的单词 |
| `dE` | 删除到包含的/分隔的单词末尾 |
| `d0$` | 删除到当前行的开头/结尾 |
| `dh` | 删除左侧/右侧字符 |
| `d{}` | 删除到上一个/下一个段落的开头 |
| `d'a` | 删除到包含标记 `a` 的行开头 |
| `d``` | 删除到包含标记 `a` 的精确字符 |

## 恢复被删除的文本

`vi` 会将之前的删除操作自动存在编号缓冲区中。如果你删错了，只要意识到得快，就可以将其找回。注意，许多 UNIX 系统只保存通过 `d` 命令删除的文本，而不是 `x` 命令。

### 从编号缓冲区恢复被删除的文本

1. 将光标移动到某些空行，你可以很容易看到任何可能恢复的文本。
2. 输入 `1p`。最近删除的文本将插入到光标处。




3. 如果这不是你想要的内容，输入 `u` 撤销插入并移除不需要的文本。
4. 输入一个点（`.`）。这将插入上一次最近删除的文本。
5. 如果这不是你想要的内容，输入 `u` 撤销插入并移除不需要的文本。
6. 继续输入这两个字符：点（`.`）和 `u`。

这允许你查看所有九个编号的删除缓冲区（delete buffers），以检查所需的文本是否可以恢复。

# 用于更改文本的 `vi` 命令表

下表显示了 `c` 命令将更改多少文本。待更改区域的末尾会显示一个美元符号（`$`）。输入新的替换文本，完成后按 `Esc` 键。行中剩余文本将根据需要向左或向右移动。

如果显示待更改区域末尾的美元符号不在你的预期位置，请按 `Esc`，整个区域将消失。然后立即按 `u`，该行将恢复到原始文本。

在下表中，请注意 `vi` 更改命令是基于光标移动命令的。

你可以在大多数这些命令之前加上一个重复次数。

### 表 17.5 用于更改文本的 `vi` 命令表

| `vi` 命令 |  |
| :--- | :--- |
| `cc` | 更改整行 |
| `C` | 从光标处更改到行尾 |
| `cwcW` |向前更改到下一个包含/分离的单词 |
| `cbcB` | 向后更改到上一个包含/分离的单词 |
| `ceE` | 更改到包含/分离单词的结尾 |
| `c0$` | 更改到当前行的开头/结尾 |
| `chl` | 向左/右更改字符 |
| `c{}` | 更改到上/下一个段落的开头 |
| `c'a` | 更改到包含标记 `a` 的行的开头 |
| `c`a` | 更改到包含标记 `a` 的精确字符 |

### 替换文本
输入 `r` 替换一个字符。输入新字符。`vi` 将准备接受新命令。不要按 `Esc`。输入 `R` 进入替换模式（Replacement mode）。现在你输入的任何内容都将替换当前文本。按 `Esc` 结束此模式。

# 第 18 章让 vi 编辑器为你工作
Steve Moritsu 

### 如何快速完成编辑
### 如何将一系列 `vi` 命令映射到按键
### 映射 `J` 以防止意外
### 在整个文档中全局替换文本
### 在文档章节中进行文本替换
### 更改左边缩进
### 全局和部分文本替换
### 剪切、复制与粘贴

第 472 页

### 使用 . 重复编辑
`.` 命令重复上一次的插入、删除或修改，但将其应用于当前位置。问题在于，它只重复最后一次更改。例如，假设你正在写一封信，想要反复更改一个三个单词的公司名称（如 Acme Products）。如果你先删除了旧的三个单词名称，然后插入新名称，最后替换你写错的一个字符；那么你做的最后一次更改就是替换一个字符。点命令现在可以反复这个最后一次更改，但重复替换一个字符并不是一个有用的操作。

`.` 命令是 `vi` 的强大工具之一。要使用它，你必须首先能够通过单个 `vi` 命令完成你的更改。你可以在该命令之前加上重复次数。然后点命令就可以根据需要重复那个有用的命令。在前面的示例中，我们想要替换三个单词，所以我们应该使用以下：

```3cw
```

`3` 是重复次数，因为我们想要更改三个单词。`c` 命令允许我们输入任何长度的新内容来替换指定的文本，直到按 `Esc` 为止。`w` 表示包含单词（contained words），这意味着第三个单词后的任何标点符号都不会被更改。我们在上一章中讨论了分离单词与包含单词的区别。`3cW` 将更改三个分离或由空格分隔的单词，这也会更改随后的任何标点符号。



在成功执行过一次 `3cw` 后，我们现在可以找到想要更改的三个单词的下一次出现处，并将光标移动到那里。按下点键 (`.`)，当前包含的三个单词将被替换为之前输入的相同文本。将光标移动到下一次出现处并按下点键，按需要替换整个文档中所有的三单词序列。这是选择性替换，因为你可以查看每次出现的情况，并根据需要决定在何时按下点号。在移动过程中要避免进行其他编辑的诱惑，因为会导致点号命令忘记你的三单词更改并记住新的更改。下一节将向你展示如何进一步地自动化这种选择性的查找和替换。在此之前，还有几点。

注意，`3cw` 是一个语法命令，它没有指定原始内容——这意味着点号 (`.`) 命令可以用于任何所需的三个单词。如果有几个三个单词组成的公司名称，点号命令可以将任何一个更改为我们的新文本。只需将光标移动到任何三单词模式并按下点键即可。

有时，要更改的文本可能包含不同数量的单词，但它们总是适用于相同数量的字符，例如表格中的条目。假设我们的表格条目长度为 15 个字符，我们想要输入相同的新条目来替换几个不同的条目。成功使用点命令的关键是构建一个单一的 `vi` 命令来重复。在这种情况下，我们的第一个命令可以是以下任意一个：

```
15cl R
```

`15cl` 使用 `l` 命令向移动，因此 `15cl` 更改光标右侧的 15 个字符，包括当前字符。由于这是表格，我们需要精确地输入 15 个字符，以便新文本完全契合表格大小。我们还可以使用 `R` 命令在一个命令中精确地替换 15 个字符。

### 使用 `n` 和 `.` 搜索并选择性重复编辑

我们可以将重复上一次搜索的 `n` 命令与点号命令结合，以此快速完成重复性的编辑工作。注意，当你想要查看每一行以决定是否应该更改它时，此程序有用。如果你不需要查看每次出现的情况，请使用本章后面讨论的全局或部分文本替换步骤。

### 双指编辑

1. 启动 `vi` 以编辑你想选择性替换某些文本的文档。
2. 输入 `1G` 确保你处于文档开头。
3. 输入 `/pattern`，其中 `pattern` 是你想要替换的单词。这会将光标移动到该模式的第一次出现处。
4. 决定是否想要保留紧跟在模式后的任何标点符号，例如句号 `.` 或引号。如果是，使用包含单词（contained words）。如果不是，使用分离单词（separated words）（在前面的关于点命令的节中会有更多讨论。）
5. 计算要替换的单词数。对于分离单词，每个单词由空格或制表符分隔。对于包含单词，计算要替换的非单词数量。输入该数字。不要按回车。
6. 输入字母 `c`。不要按回车。
7. 对于包含单词，输入 `w`。对于分离单词，输入 `W`。美元符号 (`$`) 将显示要更改文本的结束。
8. 如果美元符号 (`$`) 没有出现在正确的位置，按下 `Esc`，然后输入 `u`。这将恢复原始文本。回到第 4 步再次尝试。
9. 输入新的替换文本。它可以比原始文本长或短。完成后按下 `Esc`。
10. 按下字母 `n` 转到模式的下一次出现处进行替换。查看它并决定是否要在那里进行替换。
11. 如果你想进行替换，输入点号 (`.`)。你的新文本将替换该模式。
12. 现在为了实现真正的速度，将一个食指放在点键上，另一个食指放在 `n` 键上。按下 `n` 跳到模式的下一次出现处并查看它。只有在你想替换时才按下点。通过这种双指编辑，你可以在几分钟内替换几百处出现的内容。

另另
*有关关于包含单词与分离单词的更多信息，请参第 465 页*

不要忘记你可以撤销错误



当你进行双指编辑时，可能会在本想按 `n` 键时按到了点号。点号会导致你的上一次更改被再次应用。要纠正这个错误，只需输入 `u` 来撤销上一次更改。

# 将按键映射到常用的命令序列

点号（`.`）命令的局限性在于它只能重复你执行的最后一次插入、删除或修改编辑命令。有时，通过 `n` 命令和点号命令无法完成重复编辑，因为每次重复都需要执行多个编辑命令和/或移动命令。

我们可以通过将一个未使用的命令键映射到一串 vi 编辑命令和/或移动命令序列来处理这种情况。在上一章关于 vi 的介绍中，你已经看到如何将字母 `g` 映射到一个可以格式化段落的命令序列。字母映射后，将光标置于并按下该字母。随后映射到该字母的命令就会被执行。

然而，在映射按键之前，你必须确认你的终端是否支持在可视模式下 `Ctrl+V`。`Ctrl+V` 对于映射至关重要，因为它允许你将控制字符作为映射序列的一部分输入。某些终端需要特殊的序列来使用 `Ctrl+V`，因此你需要首先检查这一点。

## 检查可视模式下是否支持 Ctrl+V

1. 在 shell 提示符下，输入 `vi`。
2. 按回车键执行此命令。注意不要指定文件名。
3. 在 `vi` 中，输入冒号（`:`）。光标应该移动到最后一行，那里会出现一个冒号（`:`）。
4. 按 `Ctrl+V` 输入任意控制字符。
5. 观察你的屏幕。如果底部看起来像这样：
`:^` 且光标直接位于脱号（`^`）下方，则你的终端支持可视模式下的 `Ctrl+V`。如果你的屏幕显示任何其他结果（例如底部是空行），则你的终端不支持支持可视模式下的 `Ctrl+V`。
6. 连续两次 `Esc`。
7. 输入冒号（`:`）。
8. 输入 `q!`，然后按回车。你现在应该已经回到了 shell 提示符。

现在我们准备好映射一个字符了。这里有一个映射示例可以让你感受映射的功能。假设我想映射可用的 `v` 键，使得每次我在命令模式下输入 `v` 时，都会执行以下操作：

- 移动到行：`j`
- 回到行首：`0`
- 向右移动 15 个字符：`15l`
- 将后续 10 个字符替换为 acme：`10clmeESC`（`10cl` 表示将右侧的 10 个字符更改为输入的内容，直到我按下 `ESC`）
- 到行尾并插入连字符（`-`）：`A-` 注意我们使用大写的 `A` 命令在行尾插入。
- 然后插入 `Dept 2` 并结束插入模式：`Dept2ESC`

以下是实现所有操作的 `map` 命令：

```
map vj015l10clme^A-Dept2^
```

在上一条命令中，请注意以下点：多个 vi 命令可以组合在一起形成我们的映射。命令之间不要留留任何空格。`Esc` 字符显示在 `[` 上方。控制字符前面通常带有一个脱号（`^`）。如果你在映射中插入回车键，它将显示为 `^M`。在映射命令的每个控制字符或回车键之前，你必须按下 `Ctrl+V`。按下 `Ctrl+V` 会让 `vi` 显示脱号（`^`），提醒你紧接着输入的字符如果是控制字符，将被视为行中的另一个普通数据字符。现在你准备好实际设置映射了。

## 如何将按键映射到命令序列

1. 从命令模式（即不是插入模式）输入冒号（`:`）。光标应该移动到屏幕的最后一行，那里会出现一个冒号（`:`）提示符。在接到指令前不要按回车。
2. 在前面的步骤中，你确定了终端是否支持可视模式下的 `Ctrl+V`。如果你的终端不支持（或者你不确定），从 vi 命令模式输入 `Q`。注意这是一个大写的 `Q`。不要按回车。光标将到屏幕底部并出现冒号（`:`）提示符。你现在退出了可视模式。这一步不需要，但如果你的终端支持可视模式下的 `Ctrl+V`，执行它也是无害的。
3. 输入 `map`。





| 在接到指示前请勿按回车。 | 

4. 输入一个空格，然后输入想要映射的对应命令字母。你应该避免使用任何作为 `vi` 命令的字母，因为在映射了该字母后，你将无法再次执行该命令。实际上，只有五个大写或小写字母不是 `vi` 命令：`g`、`K`、`q`、`v`、`V`。我通常将 `g` 映射为格式化段落，如前所示。我不建议映射大写的 `K`，因为 `h`、`j`、`k` 和 `l` 被用于移动光标，如果不小心开启了大写锁定（Caps Lock），我们不希望这些光标移动字母干扰到我们的文本。因此，我建议你使用小写的 `v` 或大写的 `V` 作为要映射的命令字母。

5. 输入一个空格，然后输入在每次按下映射字母时要执行的 `vi` 命令序列。正如你之前看到的，在命令序列中的任何控制字符或 `Esc` 或 `Enter` 键之前，先输入 `Ctrl+V`。`Ctrl+V` 会在你的控制字符前出现一个光抑符（`^`）。

6. 现在按回车完成你的映射命令。因为你没有在此之前加 `Ctrl+V`，所以这个 `Enter` 键会终止映射命令。

7. 如果你的终端不支持 `Ctrl+V`，你仍停留在带有冒号（`:`）提示符的最后一行。输入 `vi` 然后按回车。这将让你回到可视模式（Visual mode）。

8. 你的光标现在应该已经离开底行，处于 `vi` 命令模式，准备好输入 `vi` 命令，包括你刚刚映射的新型命令字母。

当你有数百个重复的编辑更改需要进行时，加速这一过程的最佳方法是像之前讨论的那样设置双指编辑：使用 `n` 命令搜索下一个要修改的模式，并使用点（`.`）命令重复上一次更改。如果上一次更改太复杂无法通过单个命令完成，请设置一个映射，使得可以通过单个字母（如 `v` 键）完成整个命令序列。使用斜杠（`/`）命令找到第一个要修改的地方。现在将一个食指放在 `n` 键上，另一个食指放在 `v` 键上。按 `n` 找到下一个要修改的位置。只有在你想要修改它时才按 `v`。

当你退出 `vi` 时，将会丢失你的映射。在上一章关于 `vi` 的章节中的格式化部分，你看到过如何将字母 `g` 的映射写入用户主目录下一个名为 `.exrc` 的文件中。注意，在这个文件中你写了完整的 `map` 命令，但没有在 `map` 单词前加冒号（`:`）。在用户主目录的 `.exrc` 中设置的任何映射在你每次使用 `vi` 时都可用。

### 防止文本混乱

如果你使用 `h`、`j`、`k` 和 `l` 移动光标而不是方向键，你会发现，如果不小心开启了大写锁定，输入 `H`、`K` 和 `L` 是无害的。`H` 将光标移动到屏幕上最高的一行。`K` 不是一个命令（只要你不映射这个字符）。`L` 将光标移动到屏幕上最低一行。

### 为什么 `Ctrl+V` 在某些终端上会有问题？

如果你的 `TERM` 设置为 `vt10`，向下箭头会发送一个 `Ctrl+V`。如果你在 vi 中按下 `Ctrl+V`，vi 会认为按了向下箭头。我们可以通过使用 `Q` 临时退出来消除这个问题。或者，如果你的 `TERM` 设置为 `ansi`，只要你不使用 `Ctrl+V`，就不会有这个问题。

### 防止误触 `J` 导致的问题

1. 将此映射放入你用户主目录下的 `.exrc` 文件中：`map J J:`
2. 完成后，如果你不小心输入了几个大写的 `J`，第一个 `J` 将合并两行，然后在底行进入冒号（`:`）模式。其余的 `J` 将无害地出现在底行上。当你意识到自己的错误后，只需一直按退格键（Backspace）或 `Ctrl+H` 直到你移动到最左侧并离开最后一行。
3. 如果你想撤销执行的单个 `J` 命令的效果，请输入 `u`。你现在已经完全从错误中恢复了。





如果你确实想合并多行，仍然可以在 `J` 前面加上重复次数。这将合并请求的行数，然后进入最后一行行的冒号模式（Colon mode）。只需按 `Backspace` 或 `Esc` 即可退出最后一行并继续你的其他编辑。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

不要映射 `K` 键。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

在四个光标移动命令 `h`、`j`、`k` 和 `l` 中，只有 `j` 在不小心开启 Caps Lock 的情况下会出问题。然而，如果你映射了 `K` 键，你可能会有两个问题的键。

# 全局和局部文本替换

vi 内置了一个冒号命令 `g`，用于全局搜索并替换所有出现特定模式的次数。然而，由于你在前面的章节中刚刚学习了如何使用 `sed` 和 `awk`，我将向你展示如何使用其他 UNIX 命令（如 `sed` 和 `awk`）来修改整个文件或文件的任何部分。学习了这项技术后，你可以做比全局 `g` 命令多得多的操作。

## 在整个文件中替换 R.E. 模式

### 如何在文档中全局替换模式

1. 在 vi 命令模式下，输入冒号（`:`）。这应该会将光标移动到等待冒号提示的最后一行。
2. 输入以下内容：
```
:sed/R.E./newstring/g
```
这告诉 vi 将下面的 UNIX 命令应用到文件的所有行。`sed` 是我们在上一个章节中看过的流编辑器。`s` 是用一个字符串替换另一个字符串的 `sed` 命令。`R.E.` 代表正则表达式（regular expression）。输入要搜索的字符串，其中可以包含 `R.E.` 通配符。`newstring` 代表放置在找到的 R.E. 字符串位置的替换字符串。`g` 告诉 `sed` 只要发现源字符串，就多次执行此替换。你可以省略 `g`，以告诉 `sed` 只替换每行中第一次出现的源字符串，而不替换同一行中的后续出现。![arrow.gif](img/4505ed21b36ef4ebf4df520fc03bad.gif)

3. 按回车键（Enter）执行你的命令。
4. 更改将应用到所有行，你现在应该回到了 vi 命令模式。在某些类型的 UNIX 系统上，你可能会被提示按 Enter 或 Return 键。
5. 检查你文件的每一行，看看你对所所的更改是否满意。如果不满意，可以通过输入 `u` 命令来撤销所有更改。记住 `u` 命令只能撤销上一次更改，因此在执行这些替换后立即检查文件。

另另：![sarrow.gif](img/ad91af06ad9657f0a338bded4c42f0e.gif) *有关关于 R.E. 模式的更多信息，请参阅第 388 页*

## 在文件的部分区域替换 R.E. 模式

使用上一节的技术，你也可以仅在文件的部分进行操作（这在介绍过的全局 `g` 命令中是不可能的）。以下步骤利用了你可以在文件中设置标记（marks）来引用该行的事实，正如你在早之前的章节中看到的那样![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

为什么不用内置的 vi 命令呢？vi 支持两个内置的冒号命令 `g`（全局）和 `s`（替换），我没有在本书中介绍它们，因为调用外部 `sed` 命令可以实现这两个内置命令相同的功能。这让你有更多机会练习 `sed`，它是一个重要的 UNIX 命令，并向你展示了如何调用外部 UNIX 命令来处理你的文本（你以后将不得不这样做）。

### 如何在文件的部分区域替换字符串

1. 在 vi 中，将光标移动到想要进行文本替换区域区域。
2. 输入 `ma`。这将在该行设置标记 `a`。如果标记 `a` 已经用于标记文件的另一行，你可以选择任何其他字母作为你的标记。你最多可以设置 26 个标记。
3. 将光标移动到要修改区域的最后一行。
4. 输入 `!'a`。在接到指示之前不要按回车键。如果你使用了不同的标记，请更改前面示例中的字母 `a`。注意引号是单引号，而不是反引号。这应该将光标带到最后一行，那里应该出现一个感叹号（!）提示。





5. 输入以下内容：
```
sed 's/R.E./newstring/g'
```
这是我们在上一个逐步操作过程中分析过的完全相同的 `sed` 命令。

6. 按回车键执行你的命令。

7. 更改将应用于你文件的该部分，你现在应该返回了 `vi` 命令模式。在某些类型的 UNIX 系统上，你可能会被提示按回车或 Return 键继续。

检查你的文件行，查看你对所做的更改是否满意。如果不满意，你可以输入 `u` 命令来撤销所有更改。记住 `u` 命令只能撤销上一次更改，因此在执行这些替换后请立即检查文件。

总结一下：
- `:%!sed ...` 在整个文件中进行替换
- `!'a sed ...` 替换到标记或向前到标记

### 另请参考
有关在 `vi` 中设置标记的更多信息，请参阅第 467 页。

### 在 vi 中进行条件文本替换*

我们可以将前一节中的 `sed` 命令替换为其他 `sed` 命令或其他完全不同的命令，以便我们能够很好地控制 `vi` 中文本替换的方式。

```
sed '/R.E.1/s/R.E.2/newstring/g' # 通用形式
```
```
sed '/acme$/s/^president/chairperson/g' # 示例
```
第一行显示了我们也可以在 `vi` 中用于条件替换文本的修改后的 `sed` 命令的通用形式。在这种形式的 `sed` 命令中，`sed` 将搜索 `R.E.2` 并将其替换为 `newstring`，但仅限于包含 `R.E.1` 的行。在第二行中，你可以看到使用这种形式的 `sed` 的示例。

在那个示例中，如果 `president` 出现在行首，我们将将其替换为 `chairperson`，但前提是该行以单词 `acme` 结尾。

```
awk '$n == "sstring" {gsub("R.E.2","newstring")};print}' # 通用形式
```
```
awk '$3 == "K6697" {gsub("D...","M46253")};print}' # 示例
```
第一行显示了我们也可以在 `vi` 中用于条件替换文本的 `awk` 命令的通用形式。使用 `awk`，我们可以检查特定字段以决定是否应该对该行进行文本替换。在这种形式的 `awk` 命令中，`awk` 搜索所有次数的 `R.E.2` 并将其替换为 `newstring`，但仅限于字段 `n` 确匹配 `sstring` 的行。在第二行中，你可以看到使用这种形式的 `awk` 的示例。在那个示例中，每当 `D` 后面跟着三个字符时，`D` 和那三个字符将被替换为 `M46253`，但前提是行的第 3 字段包含 `K6697`。

```
awk '$n >= numval {gsub("R.E.2","newstring")};print}' # 通用形式
```
```
awk '$3 >= 16.2 {gsub("D...","M46253")};print}' # 示例
```
这个示例显示了与前面的 `awk` 命令类似的通用形式。当你想要进行替换，但仅当特定字段包含大于或等于 `numval` 的值时，使用这种 `awk` 形式。可以用以下符号替换：
- `>=`
- `<=`
- `==`
- `!=`
- `>`
- `<`

```
awk '$n ~ /R.E.1/ {gsub("R.E.2","newstring")};print}' # 通用形式
```
```
awk '$3 ~ /P[0-9]$/ {gsub("D...","M46253")};print}' # 示例
```
上一个示例再次显示了与之前两个 `awk` 命令类似的通用形式。当你想要进行替换，但仅当特定字段包含 `R.E.` 模式时，使用前述形式。在此特定的特定示例中，每当 `D` 后面跟着三个字符时，`D` 和那三个字符将被替换为 `M46253`，但前提是行的第 3 字段以 `P` 后跟一个数字结尾。

### 修改行的缩进

你可以使用 `sed` 命令通过向左边距添加空格或删除空格来更改缩进。

```
sed 's/^ *//'
```
前面的 `sed` 命令删除了文件中所有行的前导空格。

```
!'a sed 's/^ *//'
```
这个 `sed` 命令删除了到标记 a 的当前行的前导空格。

```
sed 's/^/   /'
```
前面的 `sed` 命令为文件的每行添加了三个前导空格。





```bash
!'a sed 's/^/   /'
```
此 `sed` 命令会在从当前行开始的每行开头添加三个空格，以进行标记。

# 在 vi 中移动/复制文本段

移动和复制文本可以通过多种方式实现。我将向你展示如何使用标记（marks）来完成，因为我认为这能给你提供最好的控制力和最理想的结果。

## 在同一文件中移动/复制文本

1. 在 vi 中，将光标移动到要移动或复制文本的开头。
2. 输入 `ma`。此命令无需按回车键即可执行。它在该行设置标记 `a`。如果标记 `a` 已用于标记该文件的其他行，你可以选择任何其他字母作为标记。你最多可以设置 26 个标记。
3. 将光标移动到要移动或复制段的最后一行。
4. 如需移动文本，输入 `d'a`。此命令无需按回车键即可执行。它会删除从当前行到标记 `a` 的所有文本，并将其保存到所谓的无名缓冲区（unnamed buffer）中。
5. 如需复制文本，输入 `y'a`。此命令无需按回车键即可执行。它会复制从当前行到标记 `a` 的所有文本，并将其保存到无名缓冲区中。
6. 将光标移动到放置移动或复制文本的正上方行。如果你想将文本移动或复制到文件开头，则必须在文件开头插入一个空行，以便你能够处于想要插入位置的上方行。
7. 输入 `p`。此命令无需按回车键即可执行。它将插入之前步骤 4 或 5 保存到无名缓冲区中的所有文本。

## 在文件之间移动/复制文本

1. 使用 vi 编辑源文件，即包含要移动或复制文本的文件。
2. 将光标移动到要移动或复制文本的开头。
3. 输入 `ma`。此命令无需按回车键即可执行。它在该行设置标记 `a`。如果标记 `a` 已用于标记该文件的其他行，你可以选择任何其他字母作为标记。你最多可以设置 26 个标记。
4. 将光标移动到要移动或复制段的最后一行。
5. 如需移动文本，输入 `d'a`。此命令无需按回车键即可执行。它会删除从当前行到标记 `a` 的所有文本，并将其保存到缓冲区 `b` 中。如果缓冲区 `b` 已在使用，你可以选择任何其他字母作为缓冲区。你最多可以拥有 26 个缓冲区，对应字母表中的每个字母。
6. 如需复制文本，输入 `y'a`。此命令无需按回车键即可执行。它会复制从当前行到标记 `a` 的所有文本，并将其保存到缓冲区 `b` 中。如果缓冲区 `b` 已在使用，你可以选择任何其他字母作为缓冲区。你最多可以拥有 26 个缓冲区，对应字母表中的每个字母。
7. 如果在此文件中进行了任何想要保留的文本修改，请现在保存。输入 `:w`。前一个命令将 vi 工作空间写入文件。此时不要退出 vi，因为那会清除所有无名缓冲区和具名缓冲区。
8. 输入 `:e file2`。冒号（`:`）e 会切换你正在编辑的文件，同时保留命名缓冲区中的文本。将前一个命令中的 `file2` 替换为你想要移动或复制保存文本的文件名。




9. 在此新文件中，将光标移动到该文件中目标位置正上方的一行，以便放置移动或复制的文本。如果你想将文本移动或复制到文件的开头，你必须在文件开头插入一个空行，这样你就可以处于想要插入位置的正上方行。

10. 输入 `bp`。此命令无需按回车键即可执行。它会粘贴——即插入之前第 5 或 6 步中保存在缓冲区 `b` 中的所有文本。

### 设置插入文本的选项

在 `vi` 中，`set` 命令允许你开启或关闭 `vi` 中的各种模式。本节将介绍能够增强文本输入的模式。

#### 设置 vi 始终显示输入模式

有时人们在 `vi` 中操作会遇到困难，因为他们忘记了自己处于插入模式（Insert mode）还是命令模式（Command mode）。我见过初学者创建的文件中包含如下这样的行：

```
:wq :w!q
:wq!
wq
q
:q
```

`vi` 有一种模式，可以在屏幕右下角告诉你你正处于插入模式、替换模式（Replace mode）、追加模式（Append mode）等。要开启此模式，请输入：

```
:set showmode
```

```
|
|
第 488 页
||
```

要关闭此模式，请输入：

```
:set noshowmode
```

#### 在行尾处开启自动换行（Autowrap）

`vi` 有一种模式，会在你插入文本时检查你是否接近行尾。如果是，它会将当前单词移动到下一行的开头，就好像你在该单词开始之前刚刚按了回车键一样。开启此模式后，你永远不需要手动按回车键。`vi` 会为你自动换行行。要开启此模式，请输入：

```
:set wrapmargin=10
```

`set wrapmargin=10` 命令会导致任何距离行尾 10 个字符以内的单词自动换行到下一行的起始位置。你可以设置一个比 10 更大或更小的数字，来决定你希望换行结束的位置。要关闭此模式，请输入：

```
:set wrapmargin=0
```

此命令可以缩写为 `wm`，如下所示：

```
:set wm=10
```

#### 在行首处开启自动缩进（Autoindent）

如果你在具有缩进左边的文档中使用 `vi`，那么开启自动缩进对你很有帮助。当你在插入、追加或替换模式下进入下一行时，`vi` 会自动输入与上一行相同数量的空格。要关闭此模式，请输入：

```
:set noautoindent
```

你可以将此命令缩写为 `ai`，如下：

```
:set ai :set noai
```

```
|
第 489 页
9|
```

#### 使用缩写处理长字符串

如果你有一个经常输入的长短语，可以设置一个输入缩写，`vi` 会在你输入缩写后立即将其展开。

##### 设置和使用 vi 缩写

1. 在 `vi` 中，输入 `:` 然后输入 `abbrev`。
2. 输入空格，然后输入你用来表示要插入长短语的缩写。
3. 输入空格，然后输入长短语本身。
4. 按回车设置此缩写。
5. 要使用已设置的缩写，在 `vi` 中进入插入模式并开始输入文本。在你输入的文本中，插入该缩写。你应该看到 `vi` 立即将该缩写展开为长短语。

#### 行号

在 `vi` 中，有一种模式可以在文件的每行之前显示行号。这些行号并不会插入到文件本身，而只是显示在屏幕上。如果你正在编译 C 语言程序且编译器告诉你在第 1453 行有错误，这就会非常有用。要开启 `vi` 行号显示，请输入：

```
:set number
```



要关闭此模式，请输入：

```
:set numberumber
```

该命令可以缩写为 `nu`，如下所示：

```
:set nu
:set nonu
```

# 使用 / 或 ?? 搜索时忽略大小写

为了在使用斜杠 (`/`) 向前搜索字符串或使用问号 (`?`) 反向搜索字符串时忽略大小写，请输入以下内容：

```
:set ignorecase
```

要关闭此模式，请输入：

```bash
:set noignorecase
```

你可以将此命令缩写为 `ic`，如下：

```bash
:set ic
:set noic
```

## 将你的选项保存到 .exrc 中

如果你希望每次进入 vi 时都使用某些 `:set options`，你可以在家目录下创建一个名为 `.exrc` 的文件。它可以包含设置选项、映射命令和缩写，如下所示：

```
set autoindent set ignorecase
set showmode
set wm=10
map g 072lBi^M^[
map J J:
abbrev SVR4 UNIX, System V, Release 4
```

注意，该文件中的每一行*都没有*以冒号 (`:`) 开头。

关于主目录的更多信息，请参见 ![arrow.gif]() 第 44 页

## 利用其他命令在 vi 中工作

你之前已经看到如何将 `sed` 应用于部分或行。你可以利用该技术在 vi 中使用其他 UNIX 命令。

## 在 vi 中检查 UNIX 命令

在 vi 中编辑时，你可能想通过运行 UNIX 命令或管道来查找某些信息。你可以在 vi 模式下通过输入以下来实现：

```
!:cmd
```

将 `cmd` 替换为所需的运行 UNIX 命令或管道。该命令的输出将显示在你的屏幕上。最后，它会提示你按 Enter 键。然后将返回 vi 模式准备好对文件进行编辑。你在上一章关于 vi 编写显示帮助信息的脚本时已经见过这个过程。在那个练习中，我们使用冒号叹 (`!`) 来运行 `vihelp` 脚本，以便查看帮助信息并恢复编辑。

```
!:cal 1998 pg
```

上一个示例显示了 1998 年的日历，一次一页。你现在可以使用 `pg` 在 1998 年的日历中切换，查找特定日期是星期几。在结束此 `cal 1998` 管道后，你会自动恢复到 vi 编辑，当前屏幕将完全刷新。

## 将其他 UNIX 命令的输出插入你的文件

你可以通过将光标移动到空行，将任何 UNIX 命令或管道的输出插入到文件中。然后输入：

```
!!cmd
```

将 `cmd` 替换为所需的运行 UNIX 命令或管道。双叹号 (`!!`) 会将你所在的行作为标准输入提供给该命令。该命令的输出将替换文件中当前的行。

```
!!cal 1998
```

此示例将 1998 年的日历插入到文件中替换当前行。或者，你也可以使用 vi 内置命令 `:r filefile` 将 `filefile` 的内容插入到光标位置。`filefile` 可以指定为文件名、绝对路径或相对路径。

## 排序部分文件

在 vi 中，你可以通过输入以下内容对文件的所有行进行排序：

```
:%sort
```

你可以输入任何所需的排序选项（参见附录 A）。文件的所有行都将传递给 `sort` 命令。sort 命令的输出将替换文件的当前内容。如果你不喜欢结果，可以输入 `u` 来撤销上一次修改。




# 如何排序文件的部分内容

1. 将光标移动到要排序部分的开头。
2. 输入 `ma`。此命令无需按回车键即可执行。它会在该行设置标记 `a`。如果标记 `a` 已被用于标记文件的其他行，你可以选择任何其他字母作为标记。你最多可以设置 26 个标记。
3. 将光标移动到要排序部分的最后一行。
4. 输入 `!'a sort`。在 `sort` 之后输入任何所需的选项（参见附录 A）。按回车键执行此命令。
5. 现在，该部分中的行将将完成排序。

**另请参阅**
关于 `sort` 命令的更多信息，请参阅第 202 页。

## 删除匹配模式的行

在 vi 中，你可以通过输入以下命令删除文件中所有包含正则表达式（R.E.）的行：

```
:%grep -v'R.E.'
```

你可以输入任何所需的 `grep` 选项（参见附录 A）。文件的所有行将传递给 `grep` 命令。`grep` 命令的输出将替换文件的当前内容。如果你不喜欢结果，可以输入 `u` 来撤销该修改。

### 删除部分中包含模式的行

1. 将光标移动到想要删除包含模式行的部分的开头。
2. 输入 `ma`。此命令无需按回车键即可执行。它会在该行设置标记 `a`。如果标记 `a` 已被用于标记文件的其他行，你可以选择任何其他字母作为标记。你最多可以设置 26 个标记。
3. 将光标移动到该部分的最后一行。
4. 输入 `!'a grep -v R.E`。在 `grep` 之后输入任何所需的选项（参见附录 A）。遵循 `grep` 的标准规则，包括在正则表达式模式周围添加任何必要的引号。按回车键执行此命令。
5. 现在，该部分中包含正则表达式的行将被删除。

**另请参阅**
关于 `grep` 命令的更多信息，请参阅第 380 页。

## 加密/解密整个或部分文件

如果你的 UNIX 支持 `crypt` 命令，你可以将上一节中的技术应用于 `crypt`。

```
:%crypt
```

上述的 vi 命令将要求你输入密钥。然后它将使用该密钥对整个文件进行加密或解密。请仔细保管你的密钥，因为没有它无法解密文本。

```
!'ac
```

上述 vi 命令将从当前行到标记 `a` 的文件部分进行加密或解密。

**另请参阅**
关于 `crypt` 命令的更多信息，请参阅第 217 页。

## 在文档中插入横幅

你可以使用 UNIX `banner` 命令更改行，使每个字符高度约为 10 个字符，如下所示：

```
!!banner
```

此 vi 命令将文件的当前行通过给 `banner`，并用 `banner` 的输出替换该行。

**另请参阅**
关于 `banner` 命令的更多信息，请参阅第 167 页。

## 打印文件的部分

1. 在 vi 命令模式下，输入以下内容：

```
:w
```




# 从 vi 中打印文件的某个部分

1. 在 vi 命令模式下，输入以下内容：
```
:w
```
此 `vi` 命令将文件写入磁盘，在执行后续步骤之前执行此操作是至关重要的。
2. 在要打印部分的起始处设置标记 `a`。
3. 移动到要打印部分的末尾并输入：
```
!'a lp
```
你可以使用 `lp` 或 `lpr`，具体取决于你的系统支持哪一个。你可以添加任何所需的选项，例如选择目标打印机或打印份数。
4. 上述命令会从你的文件中删除所有要打印的行。输入 `u` 可以撤销删除操作并将这些行恢复到你的文件中。在执行步骤 3 之后立即运行 `u` 命令是非常重要的。

**另请参阅**：有关关于打印的更多信息，请参阅第 169 页。

# 统计文件中部分的行数/单词数/字符数

1. 在 vi 命令模式下，输入以下内容：
```
:w
```
此 `vi` 命令将文件写入磁盘，在执行后续步骤之前执行此操作是至关重要的。
2. 在要统计部分的起始处按如下方式设置标记 `a`：
```
ma
```
3. 移动到要统计部分的末尾，并输入：
```
!'a wc
```
4. 上述命令会删除所有要统计的行，并将其替换为三个数字：
该部分的行数
该部分的单词数
该部分的字符数
如果你需要这些数字中的任何一个，请将其记录。
5. 输入 `u` 可以撤销删除操作并将这些行恢复到你的文件中。在步骤 3 之后立即运行 `u` 命令是非常重要的。

## 编辑多个文件

你可以给 `vi` 提供一个要编辑的文件列表，如下所示：
```
vi report
```
当你完成一个文件的编辑时，保存它 (`:w`) 并使用 `:n` 开始编辑列表中的下一个文件。

# Korn Shell 中的命令行编辑

在 UNIX 或任何其他操作系统上工作时，你必须使用终端上的可用键来纠正输入错误。然而，并不是所有键盘的布局都是相同的，而且可能没有相同的键。由于由于原因，你可能无法纠正键入错误，并发现自己需要重新输入整个命令字符串。

Korn shell 提供了在命令行中编辑命令的两种方式。你可以使用编辑器 `vi` 的按键，也可以使用编辑器 `emacs`。根据你熟悉的哪种编辑器，你可以调用其中任一选项进行命令行编辑。你必须显式地调用 `vi` 或 `emacs` 命令行编辑选项。如果你没有在 `.profile` 文件中这样做，那么默认将获得 Korn Shell 的行编辑选项，而这些选项是有限的。

## 调用命令行选项

如果你熟悉 `vi`，那么你可以在命令行上使用以下命令，或将其放在 `.profile` 文件（在登录时执行）中，以使用 `vi` 命令进行命令行编辑：
```
set -o vi
```
另一方面，如果你熟悉 `emacs` 编辑器，请使用以下命令：
```
set -o emacs
```
你任何时候只能激活其中一个。最后一次执行的命令将生效。




Korn shell 会保留整个会话期间的命令历史。这意味着，即使你注销，你仍然可以使用 Korn shell 命令 `fc` 获取你在上一个会话中输入的命令。历史记录默认存储在 `$HOME/.sh_history` 文件中，其中 `$HOME` 是用户的家目录。如果你想修改历史文件的文件名，可以修改系统变量 `HISTFILE` 中指定的名称。你可以将以下命令包含在 `.profile` 文件中来修改历史文件名。

```bash
export HISTFILE=$HOME/myhistoryfile
```

如果你想查看最近的命令列表，可以使用以下命令：

```bash
fc -l
```

系统输出如下：

```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10
```

左侧的数字是历史文件中的命令行号。较大的数字表示比较小的数字更接近当前的命令。如果你想查看指定行范围内的命令，可以使用以下命令：

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

系统输出如下：

```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

系统输出如下：

```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

系统输出如下：

```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

系统输出如下：

```

如果你想以倒序顺序查看命令列表，可以使用以下命令：

```bash
fc -l -r
```

系统输出如下：

```

如果你想查看最近的 10 条命令的列表，可以使用以下命令：

```bash
fc -l -10 -5
```

如果你想执行历史文件中的某一个命令，可以使用 `fc` 命令配合 `-s` 参数。如果你只想执行最近的命令，可以使用以下命令：

```bash
fc -s
```

例如，如果你想执行第 18 行的命令，可以使用以下命令：

```bash
fc -s 18
```

## 编辑模式

`vi` 命令行编辑器像源编辑器一样有两个模式：输入模式和命令模式。

在输入模式下，你输入命令并按 `Enter` 键表示执行该命令。你可以在输入模式下随时使用 `Esc` 键切换到命令模式。在命令模式下，你可以导航到已输入命令的任何部分并进行修改，包括在命令中间插入字符串。在命令模式下，可以使用一个或多个字母来激活 `vi` 的不同的编辑命令。在命令模式下，如果你按下没有 `vi` 命令的键，通常会听到终端发出的提示声。在 `vi` 命令模式下，小写字母的含义与大写字母不同。

Korn shell 会保留你之前输入的命令历史。你可以使用命令行编辑命令来调用这些命令，并在执行之前对其进行修改或添加。现在来看在使用 `set -o vi` 将 `vi` 设置为命令行编辑器后的一些命令行编辑命令细节。这些按字母顺序讨论：

- `a`: 插入模式，在当前光标位置后插入文本。
- `A`: 插入模式，在行尾插入文本。
- `b`: 允许光标向后移动字符。你可以在前面加一个数字 *n* 来重复 *n* 次。





# 命令参考

| 命令 | 说明 |
| :--- | :--- |
| `b` | 允许光标移动到上一个单词（由空格或分隔符划分的文本）。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `C` | 删除从当前位置到行尾的所有字符，并允许你输入新字符。 |
| `dd` | 删除整行文本。 |
| `D` | 从当前光标位置删除到行尾。 |
| `e` | 将光标移动到当前单词的末尾。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `E` | 将光标移动到当前由空白符分隔的单词的末尾。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `f` | 后跟一个字符，将光标移动到下一个指定字符出现的位置。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `F` | 后跟一个字符，将光标移动到上一个指定字符出现的位置。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `G` | 取出命令历史中最早的命令。你可以在前面加上数字 `n` 来定位到命令历史中的第 `n` 条命令。 |
| `h` | 将光标向左移动一个字符。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `i` | 将你置于光标位置之前的插入模式以输入文本。 |
| `I` | 将你置于行第一个非空白字符之前的插入模式。 |
| `j` | 取出命令历史中的下一个命令。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `k` | 取出命令历史中的上一个命令。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `l` | 将光标向右移动一个字符。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `n` | 重复命令历史文件的上一次搜索。搜索方向是从最近的命令到最旧的命令。 |
| `N` | 重复命令历史文件的上一次搜索。搜索方向是从最旧的命令到最近的命令。 |
| `p` | 在光标位置后插入来自删除或复制缓冲区的文本。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `P` | 在光标位置前插入来自删除或复制缓冲区的文本。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `r` | 后跟一个字符，用指定的字符替换当前光标位置的字符。你可以在前面加上数字 `n` 来重复执行 `n` 次。 |
| `R` | 将你进入替换模式，在该模式下你可以覆盖从当前光标位置开始的所有字符。你可以越过当前的最后一个字符。按 Esc 键结束替换模式。 |

第 502-503 页





# Vi 命令行参考

- `S`: 删除当前命令行行并进入插入模式以输入文本。
- `t` 后跟一个字符：将光标移动到当前命令行行中下一次出现的指定字符处。
- `T` 后跟一个字符：将光标移动到当前命令行行中上一次出现的指定字符处。
- `u`: 撤销对命令行行进行的最后修改。如果重复执行 `u` 命令，将在修改后的命令行行和未修改的命令行行之间切换。
- `U`: 通过撤销所有修改来恢复命令行行中的原始文本。
- `v`: 以当前命令行行的内容进入 `vi` 编辑器。然后你可以使用标准的 `vi` 命令对其进行编辑。使用 `:wq` 退出时，每行命令将按顺序执行。你可以在其前面加一个数字 `n` 来编辑历史记录中的第 `n` 行。
- `w`: 将光标移动到命令行行中的下一个单词。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `W`: 将光标移动到命令行行中下一个由空格分隔的单词。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `x`: 删除光标位置的字符并将其保留在删除缓冲区。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `X`: 删除光标位置之前的字符并将其保留在删除缓冲区。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `yy`: 复制当前命令行行并将其保留在复制缓冲区中。
- `Y`: 复制从光标位置到行尾的文本并将其保留在复制缓冲区中。
- `0`: 将光标移动到命令行行第一个非空格、非制表符的字符。
- `$`: 将光标移动到命令行行的最后一个字符。
- `-`: 与 `j` 相同。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `+`: 与 `k` 相同。你可以在其前面加一个数字 `n` 来重复 `n` 次。
- `0`: 将光标移动到命令行行的第一个字符。如果你在其前面加一个数字 `n`，光标将移动到命令行行的第 `n` 个字符位置。
- `/` 后跟一个字符串并按回车键：在命令历史文件中搜索指定的字符串，范围为命令中的任意位置，方向从最近的命令到最旧的命令。
- `/^` 后跟一个字符串并按回车键：在命令历史文件中搜索位于命令开头的指定字符串，方向从最近的命令到最旧的命令。
- `?` 后跟一个字符串并按回车键：在命令历史文件中搜索指定的字符串，范围为命令中的任意位置，方向从最旧的命令到最近的命令。





- `?` 后紧跟 `^` 和一个字符串，然后按回车键。
- `^` 在命令历史文件中，按照从最旧命令到最近命令的方向，搜索命令开头匹配指定字符串。
- `~`
- 将小写字母修改为大写字母，或反之亦然。
- `#` 在命令行开头插入井号（`#`）并执行，使其进入命令历史文件。该命令不会被实际执行，因为开头的 `#` 符号意味着 Korn shell 将其视为注释。
- `=` 显示与当前单词匹配的文件名。
- `*` 将当前单词替换为以匹配当前单词开头的文件和目录列表。
- `Space` 与 `l` 相同。
- `Enter` 执行当前命令。
- `Control` 后紧跟字母 `l` 重绘当前行。
- `Alias` 你可以使用 `alias` 命令为命令字符串定义快捷方式。别名有两种类型：普通别名和跟踪式别名（tracked alias）。*跟踪式别名*会向你显示命令的完整路径。你可以单独使用 `alias` 命令来生成当前环境中设置的所有别名列表。如果你像如下所示使用 `-t` 命令，将获得所有跟踪式别名的列表：`alias -t`。
- 你可以使用 `alias` 命令为一个命令或多个命令定义别名。在下面的示例中，为 `ls` 命令设置了别名仍为 `ls`，但带有 `-l` 选项。

```
alias="ls -l"
```

# 第 20 章 介绍 emacs 编辑器
作者 Jesper Pedersen

## 开始 emacs
按键绑定
定义宏
搜索与替换文本
文档拼写检查
主模式与辅助模式
获取 emacs 帮助
继续使用 emacs

文本编辑器允许你创建和修改文本文档，这些文档包含你在键盘上输入的字母和字符。相比之下，使用文字处理器你不仅可以编辑文本，还可以通过选择字体大小和样式来更改文本的呈现方式。

本章将向你介绍最先进的文本编辑器：emacs。关于 emacs 有句常用俗言：*如果一件事在 emacs 中无法完成，那么它根本就不值得做*。以下一些 emacs 基本功能列表让你大致了解它的含义：

- 极其实用的撤销功能。
- 每隔 300 个字符自动保存文件，或大约每 30 秒一次。这保证了在发生程序/电源/人为故障时，你只会丢失极少的工作。
- 通过 Info 系统（一种类似于万维网超文本格式）提供的大量在线帮助。
- 针对不同任务的模式，包括加速工作的功能和键盘绑定（例如编写 HTML 文档、C 程序、LaTeX 文档）。
- 拼写检查设施（例如 `ispell` 程序）。
- 可以大幅提高你工作速度的强大宏。
- 增量搜索。
- 使用正则表达式进行搜索和替换。





# Emacs

将键盘上的按键绑定到你的特定需求上。

emacs 让你能够在计算机上完成几乎任何事情（以及所有事情……）。以下列表仅列出了在 emacs 中值得执行的一些任务：

- 使用 `ediff` 对文件进行差异比较
- 查找文本文件中的差异
- 读取/撰写邮件
- 在其他文件系统上编辑文件

最重要的是，emacs 具有极高的配置配置。你可以根据自己的需求对其进行任何自定义！（本章展示了许多自定义示例供你参考。）

## 技术术语

为了真正向你解释 emacs，有必要介绍一些技术术语。当你理解了这些术语后，这个主题将变得更容易理解和上手。深入理解这些术语也将为你进一步构建关于 emacs 的知识打坚实的基础。掌握了以下基础术语，你就可以在 emacs info 页面中开始建设性地搜索信息：

- **Buffer (缓冲区)**：缓冲区是 emacs 中的基本编辑单元。一个缓冲区对应于正在编辑的一个文本文件。虽然你可以拥有多个缓冲区，但一次只能编辑一个。不过，你可以同时显示多个缓冲区。通常情况下，一个缓冲区包含你正在编辑的文件文本。
- **Point (光标)**：光标指的是如果你向给定缓冲区插入文本，文本将出现的位置。每个缓冲区恰有一个光标。
- **Region (区域)**：区域是指被选中的文本。许多函数可以作用于整个缓冲区，也可以仅作用于区域（例如拼写检查）。
- **Ctrl+X**：这是 `Control+X` 的含义：按下 `Ctrl` 键不放同时按下 `x`；然后释放。
- **M+X**：这是 `Meta+X` 的含义：按下标记为 `Meta` 的键（如果没有标记为 `Meta` 的键则按 `Alt`），并保持住同时按下 `X`；然后释放两个键。如果你的键盘没有 `Meta` 键，或者你通过 `Telnet` 登录（此时 `Meta` 键可能不起），你可以使用替代键：`Esc+X`。按下 `Escape` 键（通常标记为 `Esc`），松开，然后按下 `X`。
- **emacs 菜单栏**：在 `X` 环境和非 `X` 环境下运行 emacs 的区别在于窗口顶部是否存在菜单栏。然而，在较版本的 emacs 中，即使在非 X 模式（也称为文本模式）下运行时也可能发现菜单栏。如果你的 emacs 版本早于 `19.22`，你应该考虑更新你的 emacs 安装。新版本具有许多让升级非常值得的功能。

## 启动 emacs

emacs 可以在有或没有 `X` 的情况下运行。本章假设你拥有 `X` 窗口。如果没有 `X` 窗口也不要担心；以下信息并不代表你拥有它。

要启动 emacs，只需输入 `emacs`。这将弹出一个类似于图 20.1 的窗口。工具栏位于窗口顶部。你可以像使用 Windows 中的工具栏一样使用它。它的内容会根据你正在的操作而变化。

工具栏下方是缓冲区。起初它包含一些启动信息。当你开始输入时，缓冲区的内容会被替换为你的文本。

窗口底部是状态行，采用反色显示。在 emacs 会话开始时，状态栏包含以下信息：

- 文本 `emacs:` 的左侧有五个横线。这表示缓冲区已与磁盘上的文件同步（即缓冲区的内容与磁盘上的文件内容一致）。如果缓冲区内容被更改，五个横线将被替换为文本 `--`。
- 文本 `emacs:` 旁边是缓冲区名称。因为你还没有加载任何文件，该缓冲区只是名为 `scratch` 的虚拟缓冲区。当你打开一个文件时，文件名将显示在这里。
- 接下来是关于你启动了什么模式的信息（文本 `Fundamental`）。例如，如果你加载了 HTML 模式，这里可能是 HTML。





接下来是点所在的行号（文本 `L1`）。

最后，你会看到关于你正在查看缓冲区哪个部分的信息。`All` 表示整个缓冲区可见。其他选项有：`Bot` 文本底部；`Top` 文本顶部；以及缓冲区向下 `8%` 处。

状态行下方是一个空行。当 emacs 需要你提供信息时，此行用于与你进行交互。

# 打开/保存文件以及退出 emacs

## 如何使用鼠标打开文件

1. 从 `Files`（文件）菜单中选择 `Open File`（打开文件）。
2. 输入你想要编辑的文件名。（如果你输入了一个不存在的文件名，将创建一个新文件；然后将打开这个新文件。）
3. 现在文件已加载到缓冲区中，你可以尽情意地编辑它。要在缓冲区内移动，请使用光标方向键。

当你选择菜单栏中的某项时，应该非常关注项目旁边列出的快捷键。如果你学会了这些快捷键，你与 emacs 的交互速度将大幅提高，从而能够完成更多工作。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 输入命令和插入文本

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

与 `vi` 不同，emacs 没有“编辑模式”（Editing mode）和“命令模式”（Command mode）。在 emacs 中，你使用 `Ctrl` 键和 `Meta` 键输入命令；直接输入即可插入文本。

## 如何不用鼠标打开文件

1. 按下 `Ctrl+x, Ctrl+f`。
2. 输入你想要编辑的文件名。
3. 完成编辑后，你可以按 `Ctrl+x, Ctrl+s` 保存文件，或者从菜单栏中选择 `Files, Save Buffer`（文件，保存缓冲区）。
4. 退出 emacs，从 `Files` 菜单中选择 `Exit Emacs`，或使用快捷键 `Ctrl+x, Ctrl+c`。

## 使用撤销功能

emacs 拥有非常强大的撤销机制，当你后悔某次修改时可以提供帮助。要撤销修改，请进入 `Edit`（编辑）菜单并选择 `Undo`。（绑定为 `Ctrl+_`；即按 Control 再按下划线）。如果你连续执行多次撤销操作，将撤销相应数量的修正。请注意，emacs 可能会将多个文本插入命令合并为一个实体。这意味着一个撤销命令可能会删除几个单词。

关于撤销功能一个非常重要的点是：撤销操作也可以被“撤销”！（也就是说，撤销和重做是相同的功能。）通过一个例子可以说明这一点。

### 撤销命令示例

1. 启动 emacs。
2. 在不同行上输入 `1`、`2`、`3`、`4`。
3. 现在不断撤销直到删除了 `3` 和 `4`。
4. 输入 `5`。
5. 现在开始撤销并观察。你会发现 `5` 被删除了，然后 `3` 和 `4` 再次插入。如果你继续撤销，你会看到 `4`、`3`、`2` 以及最后的 `1` 将被删除。

## 剪切和粘贴

计算机优于普通打字机的功能之一是剪切和粘贴，这允许你在文档中移动文本、将文本复制到多处等。要标记一段文本，你可以使用鼠标或键盘。

### 使用鼠标复制/剪切文本

1. 将鼠标悬停在你想要标记的文本的开头。
2. 按住鼠标左键。在按住鼠标键的同时，拖动到选择结束的位置。
3. 放开鼠标键。
4a. 如果你想将文本复制到剪贴板（且不想从缓冲区删除它），选择 `Edit` 菜单并点击 `Copy`。
4b. 如果你想将文本剪切到剪贴板（并从缓冲区删除删除），选择 `Edit` 菜单并点击 `Cut`。

### 使用键盘复制/剪切文本

1. 将光标（记住是插入光标）置于想要选择的文本开头。





# 使用鼠标

你只能在 emacs、Xemacs 或在 X 环境下的较新版本的 emacs 中使用鼠标。

1. 按 `Ctrl+spacebar`（即 Control 键和空格键）。在缓冲区底部，会出现 `Mark`（标记）设置的文本。
2. 移动到你想让选择结束的位置。
3a. 如果你想将文本复制到剪贴板，请按 `M+w`（`M` 是 Meta 键）。
4b. 如果你想将文本剪切到剪贴板，请按 `Ctrl+w`。

虽然记住这些键绑定似乎很困难，但你应该非常努力地去尝试；这将使你与 emacs 的交互变得快得多。例如，当你想要剪切和粘贴时，你就不再需要去拿鼠标了。

## 使用鼠标将最近一次选择的内容粘贴到缓冲区

1. 将鼠标悬停在你想要粘贴文本的位置。
2. 按下鼠标中间键。

## 使用键盘将最近一次选择的内容粘贴到缓冲区

1. 将光标置于你想要粘贴的位置。
2. 按 `Ctrl+y`。
记住，emacs 保存了撤销的多个步骤。对于选择也是如此：你可以粘贴一个不是最近一次选择的内容。

## 使用鼠标将不是最近一次选择的内容粘贴到缓冲区

1. 将光标置于你想粘贴文本的位置（通过光标方向键移动，或者在该位置点击鼠标左键）。
2. 从 `Edit`（编辑）菜单中选择 `Select`（选择）和 `Paste`（粘贴），然后选择你想粘贴的选择项。

## 使用键盘将不是最近一次选择的内容粘贴到缓冲区

1. 将光标置于你想要粘贴的位置。
2. 按 `Ctrl+y` 粘贴最近一次选择。
3. 现在，你可以通过按 `M+y` 遍历旧选择列表，直到到达你想要的选择项。

## 备份

Emacs 会定期将你的缓冲区保存到磁盘，以确保如果你在退出前不小心没有保存缓冲区，该内容也不会丢失。当 emacs 打开一个备份文件更更新的文件时，它会建议你从自动保存的文件恢复数据。自动保存的文件与原始文件同名，区别是自动保存的文件名开头和结尾都有 `#` 字符。如果你收到了备份通知，使用 `diff` 命令查看原始文件和自动保存文件之间的差异可能是个好主意。

## 恢复自动保存的文件

1. 按 `M+x`。
2. 输入 `recover-file` 并按回车。
3. 输入文件名并按回车。
4. Emacs 会询问你是否确定这么做。如果是，输入 `yes` 并按回车。

## 键绑定

你现在脑中可能有三个重要的问题：

1. 为什么这些绑定如此困难且如此不符合直觉？
2. 我有机会学会所有这些的绑定吗？
3. 我可以更改绑定，例如将撤销功能绑定到 `Ctrl+backspace` 吗？

简单的回答是：1) 你没有更重要的事情要担心吗？2) 可以；3) 可以。下面是更详细的回答。对于第一个问题，即你是否会学会所有不同的绑定，我可以给出肯定的回答。只要你强制自己在有替代方案时不使用鼠标，这会随着时间的推移而变得自然。





这些绑定的原因并不十分清晰，但一个合理的猜测是，因为 Emacs 并不是从零开始设计的，而是多年开发的结果。由于向后兼容性问题，键位才变成了现在这样。不过，似乎有一套通用计划：

键盘上所有的字母、数字和符号，如果在不按下 `Control` 或 `Meta` 键的情况下按下，将插入该按键上给出的标签。

在按下 `Control` 或 `Meta` 键时，可以使用非常常用的函数。（例如，`go to end of line` 绑定到 `Ctrl+e`，`undo` 绑定到 `Ctrl+_`（即 Control 和下划线），`paste` 绑定到 `Ctrl+y`。）

如果 `Control` 前缀绑定到一个处理特定按键字符的函数，那么 `Meta` 前缀将作用于单词（如果这对于该函数有任何意义的话）。同样，如果 `Control` 前缀作用于行，那么 `Meta` 前缀将作用于句子。示例包括：`Ctrl+t` 交换两个字符；`M+t` 交换两个单词；`Ctrl+e` 将光标移动到行尾；以及 `M+e` 将光标移动到句尾。

较少使用的函数通过前缀 `Ctrl+x` 绑定。示例包括：`Ctrl+x, Ctrl+c` 退出 Emacs；`Ctrl+x 2` 将窗口分成二，每个窗口一个缓冲区。

特定模式下的函数以 `Ctrl+C` 为前缀。

极少使用的、或认为不适合绑定到键盘上的函数完全没有绑定，但可以通过按下 `M+x` 并输入函数名称来访问。

## 如何查看所有键盘绑定列表

1. 按下 `Ctrl+h`, `Ctrl+B`。这应该分割窗口。在其中一个窗口中将出现所有绑定的描述。
2. 按下 `Ctrl+x, o`。这将选择移动到包含描述的窗口。
3. 使用方向键浏览文本。
4. 完成后，按下 `Ctrl+x, 0`（零）来隐藏缓冲区。
5. 当你找到一个听起来有趣的函数时，可以获取它的更多信息：

### 如何查看函数的描述

1. 按下 `Ctrl+h, f`。
2. 输入你想查询信息的函数名称（例如，`open-line`）。
3. 完成后按下 `Ctrl+x, 1` 隐藏窗口。（这次是 `Ctrl+x, 1`，因为选择器在你想要保留的窗口中。）

现在我们几乎准备好按照你的个人喜好重新绑定键盘了。然而，在此之前，了解特定按键存在哪些绑定是非常用的。这些信息可以通过按下 `Ctrl+h, c` 然后按下你想考虑的按键来获取。此操作将显示绑定在该按键上的函数名称。要获取有关该函数的更多信息，请遵循之前的说明。

### 如何重新绑定按键

1. 按下 `M+x`。
2. 输入 `global-set-key` 在所有缓冲区中绑定按键，或输入 `local-set-key` 只在给定缓冲区中绑定按键。
3. 按下 `Enter`。
4. 按下你想重新绑定的键。
5. 输入你想绑定到该按键的函数名称。

现在你可以按照自己的意愿绑定键盘了。然而，你仍然需要学习如何将绑定从会话保存下来。位于你主目录下的名为 `.emacs` 的文件是 Emacs 的设置文件。该文件中的信息在每次启动 Emacs 时都会被读取。文件使用一种名为 `emacs LISP` 或简称 `elisp` 的语言编写。以下描述仅适用于全局键绑定。绑定本地键要困难得多，因为需要某种对其适用于哪些缓冲区的描述。这超出了本书的范围。

### 如何将按键绑定保存到 *.emacs 文件

1. 按照之前的描述创建键绑定。
2. 按下 `M+x`。
3. 输入 `repeat-complex-command` 并按下 `Enter`。
4. 使用上/下方向键浏览历史列表，或者按下 `M+p` 和 `M+n` 直到找到以 `(global-set-key.` 开头的一行。
5. 将此行复制到剪贴板。
6. 按下 `Ctrl+g`。（这会让你的扬声器发出哔的一声，缓冲区应该消失。）




7. 打开你主目录下的 `.emacs` 文件。
8. 到该文件的合适位置并粘贴。这应该会插入文本（`global-set-key`）。
9. 保存文件。

## 使用 Control+Shift 进行键绑定

不同的模式可能会重新绑定按键，从而无视你已经绑定的键。通过使用 `Control+Shift` 作为你自己的键绑定的前缀，可以避免这种情况。

## 定义宏

计算机比人类更擅长的主要事情之一就是处理琐碎、重复的工作。emacs 拥有宏可以帮助你完成此类任务。`macro`（宏）是一种允许你记录一系列按键序列以供以后播放的功能。

### 如何录制宏

1. 按 `Ctrl+x(`。（这开始录制。）
2. 执行你想记录的按键操作。
3. 按 `Ctrl+x)`。（这结束录制。）

如果你想同时保留多个定义的宏，你需要为它们命名。

### 如何为宏命名

1. 按 `M+x`。
2. 输入 `name-last-kbd-macro` 并按回车。
3. 为新定义的宏输入一个名称。

你可以通过按 `Ctrl+x, e` 调用上一个定义的键盘宏（无论是否命名）。你可以通过按 `M+X` 输入其名称并按回车来调用命名的键盘宏。如果你为宏命了名，就可以将其绑定到按键上（如前一节所述）。

宏的生存周期仅与 emacs 同等。当你关闭 emacs 时，除非将它们保存到 `.emacs` 文件，否则所有定义的宏都会消失。

### 如何将宏保存到 *.emacs* 文件中

1. 如前所述定义宏。
2. 如前所述为定义的宏命名。
3. 如果你想将宏绑定到按键上，请按前一节所述操作。
4. 打开你的 `.emacs` 文件并进入其中的合适位置。
5. 按 `Ctrl+1, M+x`。
6. 输入 `insert-kbd-macro` 并按回车。
7. 输入定义的宏名称并按回车。

### 重复宏

当你定义了一个宏后，你可能经常使用它（甚至可能几百次）。为了实现这一点，你可以使用 emacs 的重复功能。如果你按住 `Control` 并输入一个数字（保持 `Control` 按下状态），则后续命令将执行相应的次数。（这并不是 100%准确的，但在大多数情况下是正确的。）因此，如果你想重复执行 20 次宏，请按 `Ctrl+2 Ctrl+0 Ctrl+x, e`。（这是 `Control 20`，以及执行宏的键盘前缀。）

通常，你可能希望在几行上执行宏。一个例子是在文本区域的每行开头插入 `>`。

### 使用重复宏在区域的每行开头插入

1. 录制一个在行首插入 `>` 的宏。
2. 转到该区域的起始行。
3. 按你为此宏绑定的按键（例如 `Control+spacebar`）。
4. 转到该区域的末尾。
5. 按 `M+x`。
6. 输入 `apply-macro-to-region-lines` 并按回车。

### 使用鼠标选择





你也可以通过鼠标选择区域来完成第 24 步。

如果你需要创建一个涉及插入数字（增加或减少）的宏，请访问 `ftp://archive.cis.ohiostate.edu/gnu/pub/emacs/elisp-archive/functions/counter.el.Z`。这里不再对其进行描述，因为它不是标准 emacs 发行版的一部分。然而，它的安装非常简单，而且证明极其有用。如果前面的站点很忙，请尝试镜像站点 `ftp://src.doc.ic.ac.uk/gnu/emacsBits/elisp-archive/`。

如果你发现自己正处于一种键盘声音发出 *Tik taak tik tik . . . Tik taak tik tik . . . Tik taak tik tik* 的情况下，那么可能值得考虑创建一个宏！

# 搜索和替换文本

当你编写程序或文档时，可能经常想在文档中搜索特定的文本。emacs 有几个用于搜索文本的函数。本节将描述这些函数。

另一个你经常发现自己的任务是将某些文本替换为其他文本。共有三种搜索方式：

## 普通搜索
在此类搜索中，你输入想要搜索的文本；emacs 将跳转到该文本首次出现的地方。然后你可以要求它跳转到第二次、第三次出现的地方，依此类推。

## 增量搜索
在此类搜索中，emacs 在你输入第一个字母时就会开始搜索。随着你输入更多字母，emacs 会在文档中进一步搜索，以反映你对所搜索内容信息水平的增加。

## 正则搜索
在此类搜索中，你可以像在 shell 中那样添加通配符（尽管通配符是通过一种称为正则表达式的特殊方式构造的）。

有两种替换文本的方法：

### 普通搜索和替换
在这种策略中，你输入想要替换的文本以及想要替换进去的文本。然后对于每个匹配项，emacs 会询问你是否想要替换该匹配项。

### 正则搜索和替换
在正则搜索和替换中，你可以使用正则表达式来替换文本。例如，你可以将 `.*` 替换为 `...`。

# 增量搜索

最常用的搜索类型是增量搜索。因此，让我们从这种搜索开始吧。

要使用增量搜索向前搜索，请按下 `Ctrl+s`。要向后搜索，按下 `Ctrl+r`。在你按下 `Ctrl+s` 或 `Ctrl+r` 后，你可以输入你正在搜索的字母。每当你添加一个新字母，emacs 都会测试找到的单词是否匹配（通过使用之前的字母进行搜索）。如果不符合，emacs 将在你的文档中继续搜索。当你添加了足够数量的字母后，可以按下 `Ctrl+s` 或 `Ctrl+r` 使用目前已输入的字母继续搜索。通过这种方式，你就可以在输入字母和按下 `Ctrl+s` 或 `Ctrl+r` 之间切换。

增量搜索比普通搜索快得多，因为你不需要输入整个单词。例如，如果你正在搜索 `miscellaneous` 这个词，只需输入 `misc` 可能就足够。如果 `misc` 在文档中出现多次，在普通搜索中你可能需要重新开始。但在增量搜索中，你只需要输入字母 `e`，这将让你搜索 `ce`（这不会匹配 `calculation` 单词）。

在一种情况下，普通搜索优于增量搜索，即你的剪贴板上有要搜索的单词。

如何使用普通搜索
1. 按下两次 `Ctrl+s` 或 `Ctrl+r` 进行普通向前搜索；相应的进行向后搜索。
2. 输入你想要搜索的字母。或者，如果字母位于剪贴板上，按下 `Ctrl+y`。

## 普通搜索和替换

emacs 有一个将一个字母序列替换为另一个的函数。该函数替换从缓冲区当前位置到缓冲区末尾的文本。

如何搜索和替换
1. 按下 `M+%`。（这是 `query-replace` 函数。）
2. 输入你想要替换的文本，并按回车。
3. 输入你想要插入的文本，并按回车。




emacs 现在将跳转到文本的首次出现处，并询问你想做什么。你有以下几种选择：

- 按 `y` 替换该匹配项并跳转到下一个。
- 按 `n` 跳过该匹配项并跳转到下一个。
- 按 `!` 替换该匹配项以及后续之后的所有匹配项。
- 按 `q` 停止替换。
- 按逗号键（（`）替换当前匹配项，但不会立即移动光标点。（要重新开始替换，请按 `y`。）

# 正则表达式搜索与替换

有两个用于正则表达式增量搜索的函数，分别绑定到 `Ctrl+M+s` 和 `Ctrl+M+s` 用于正向和反向搜索。还有一个名为 `query-replace-regexp` 的函数（未绑定到任何按键），用于使用正则表达式进行搜索和替换。

正则表达式超出了本书的范围。因此，我不会解释所有细节，而是向你展示一个它的强大示例。更多信息，你应该查阅 info 页面。

## 示例：将 `printf(''. . .')` 替换为 `write ...`

假设你想将所有模式 `printf(" . . . ")` 的出现处替换为 `write . . .`。三个点代表的文本在 `write` 之后应与引号之间的文本相同。也就是说，`printf("Hello world")` 应该被替换为 `write Hello world`。普通的替换在这里是不行的，因为你可能期望模式 `")` 出现在几处，但那里并不匹配 `printf(".`。

首先，我们必须创建一个匹配 `printf("...")` 的正则表达式，其中三个点可以是任何内容。这是通过正则表达式 `printf([^*)` 完成的。好的，让我们一步步来：

1. `\b` 匹配单词边界。这样我们的替换就不会替换掉例如 `sprintf(...)`，因为在开头有一个 `s`。
2. 这只是要匹配的普通文本。
3. `(` 开始一个正则分组。如果我们希望在替换中引用括号之间的文本，这是必须的。
4. 方括号 `[]` 表示一个要匹配的字符列表。列表开头的 `^` 字符表示该列表应该是被取反的（也就是说，它是一个不应该包含的字符列表）。总而言之，这个元素表示可以匹配不同于右括号的单个字符。
5. `*` 表示前一个元素可以被匹配任意次数。配合方括号，这表示可以读取任意数量的字符，只要它不是结束括号。
6. `)` 结束第 3 部分开始的分组。
7. 要匹配的普通文本。
8. `\b` 匹配单词边界（见第 1 部分）。

正则表达式尝试匹配尽可能多的内容。因此，如果第 4 部分没有规定结束括号是非合法的，它将从第一个 `printf` 一直读取到最后一个 `printf`（单个点号可以匹配任何字符）。

现在我们准备好进行替换了。将 `printf ...` 替换为 `write ..`

1. 按 `M+x`。
2. 输入 `query-replace-regexp` 并按回车。
3. 输入 `printf([^*)` 并按回车。
4. 输入 `write\1` 并按回车。

现在 emacs 将询问你是否替换 `printf ...` 的首次出现。注意替换字符串中的 `\1`。它将展开为被替换文本中括号内匹配到的文本。

## 编译匹配项列表

有时你想看到匹配给定文本搜索的所有行列表。这可以通过函数 `list-matching-lines` 实现。它没有绑定到任何按键；因此，访问它需要使用 `M+X`。如果给此函数提供一个数字前缀（通过之前描述的重复计数方式，按住 Control 并输入数字），将显示相应数量的行作为上下文。

### 如何获取所有匹配项列表

1. 如果你想看到上下文（即匹配行周围的行），按住 Control 键，输入要作为上下文显示的行数。
2. 按 `M+x`。



3. 输入 `list-matching-lines` 并按回车。
4. 输入你正在查找的文本。（从技术层上说，这实际上是一个正则表达式。只要你不是搜索 `+`、`*`、`(`、`)`、`\|`，你就永远不会察觉这一点。）

emacs 现在会将窗口一分为二，你将在其中一个窗口中看到列表。通过点击其中一个匹配项的鼠标中间键，另一个窗口将更新视图以显示该匹配项。

完成后，你可以通过按下 `Ctrl+x, 1`（如果你位于想要保留的窗口中）或 `Ctrl+x, 0`（如果你位于想要移除的窗口中）来关闭带有匹配列表的窗口。

图 20.2 显示了在上下文 1 中创建的此类列表示例。

### 搜索中的大小写问题

emacs 是高度可配置的。你已经看到如何将键盘绑定到你的个人偏好。内置函数可以使用变量来控制，这些变量会指示它们如何工作。

有一个变量可以告诉 emacs 搜索应该是区分大小写还是不区分大小写。如果其值设置为 `t`（elisp 中的 True），搜索将不区分大小写。然而，如果将其设置为 `nil`（elisp 中的 False），搜索将区分大小写。

![8227-0526a.gif](img/d221025122760f0ffc16580aa2f2e96d.gif)
图 20.2 使用 *list-matching-lines* 显示匹配列表。

### 启用不区分大小写的搜索

1. 按 `M+x`。
2. 输入 `set-variable` 并按回车。
3. 输入 `case-fold-search`。
4. 输入 `t` 以启用不区分大小写的搜索，或输入 `nil` 在搜索中使用大小写。
5. 按回车。

### 拼写检查

emacs 有一个非常实用的接口叫做 `ispell`：拼写检查器。如果你的系统中没有安装 `ispell`，可以通过 FTP 从 `ftp://ftp.gnu.org/pub/gnu/` 下载它。

基本上，emacs 提供了三个函数：`ispell-word`（绑定到 `M+$`）、`ispell-region` 和 `ispell-buffer`。

要启动 `ispell`，按 `M+x` 并输入其中一个函数的名称（你以前见过这个过程，记得吗？）。现在 emacs 将开始拼写检查。如果你只检查单个单词且单词是正确的，它会显示 `miscellaneous is correct`。如果你检查一个区域或整个缓冲区，emacs 在完成缓冲区处理后显示 `Spell-checking done`。

在出现拼写错误的情况下，emacs 会高亮显示在字典中未找到的单词，并提供可能的选项列表。你可以通过按下单词旁边列出的数字从列表中选择正确的单词，如图 20.3 所示。

![8227-0527a.gif](img/57871d5158c65c4bac18e73c9e6f16ad.gif)
图 20.3 使用 emacs 进行拼写检查。

如果 emacs 没有猜到正确的单词，你可以通过按下 `r`（`r` 代表 replace）、输入单词并最后按回车手动输入。如果该单词在整个文档中可能会被多次拼写错误，那么按下大写的 `R` 可能更好的主意，它会要求替换，然后执行 `query-replace`。这样你就不需要为每个拼写错误的出现输入替换内容。

相反，如果该单词是一个拼写正确的新表达式，你可以按下空格键接受本次的单词，按下 `a` 在整个缓冲区生命周期内接受该单词，或按下 `i`（`i` 代表 insert）将单词插入你的个人字典中。

使用 `ispell` 还有额外的选项。要查看这些选项，按 `Ctrl+h, f` 并输入 `ispell-help`。

### 主模式与要模式

当你编写 HTML 文档时，你会发现希望 emacs 以一种方式配置。当你编写 C++ 程序或普通信件（即发给你母亲的生日信）时，你会希望它以完全不同的方式配置。

两种配置之间的差异示例包括：

- 文本缩进的方式。（在 C++ 模式下，缩进级别在左括号处增加，在右括号处减少。）
- 绑定到 `Ctrl+c` 前缀键的函数集。
- 菜单的内容。（C++ 模式添加了一个名为 C++ 的菜单项。）




所有此类配置都保存在名为 `modes` 的包中。大多数编程语言都存在相应的模式；例如 C、C++、Java、Python、TCL、汇编语言、HTML、LISP、TeX、AmsTeX、LaTeX 等等。

针对特定 `language` 的模式被称为 `major modes`（主模式）。另一种类型的模式（称为 `minor modes`，次要模式）是那些对 emacs 行为进行细微更改的模式。你一次只能加载一个主模式，但可以同时加载许多次要模式。你想要加载的次要模式集在不同的主模式下可能是相同的。

次要模式的示例包括：

*   **自动填充模式 (Auto-fill mode)**：开启此次要模式时，emacs 会自动插入换行符。你可以将光标移动到该列并按下 `Ctrl+x, f` 来配置换行符发生的列位置。
*   **鼠标避让模式 (Mouse-avoidance mode)**：当加载此次要模式时，如果光标太近，光标会自动移开。
*   **字体锁定模式 (Font-lock mode)**：当启用 `Font-lock mode` 时，文本会在你输入时进行字体化。
*   **自动压缩模式 (Auto-compress mode)**：当此次要模式激活时，emacs 会自动压缩和解压文件。
*   **列数模式 (Column-number mode)**：启用此次要模式时，状态栏会显示列数。

要查看主模式列表，请参考标题为 Getting Help About emacs" 的章节。

### 加载次要模式

你可以通过按下 `M+X` 并输入其名称来切换次要模式的开启或关闭。

次要模式有两种类型：独立于缓冲区的和依赖缓冲区的。在前面的列表中，`Mouse-avoidance mode`、`Auto-compress mode` 和 `Column-number mode` 是独立缓冲区的；`Auto-fill mode` 和 `Font-lock mode` 是依赖缓冲区的。

你希望默认可用的独立缓冲区次要模式可以在 `.emacs` 文件中通过在括号内输入模式来启动。考虑以下示例：

```lisp
; 分号是 .emacs 文件中的注释
(mouse-avoidance-mode) ; 以其默认设置启动 mouse-avoidance-mode
; 另一种启动方式，这次带有一个参数，描述了它应该如何启动。只需使用这些命令中的一个。
mouse-avoidance-mode 'exile
```

某些次要模式可能有一个可选参数（如所述的 `Mouse-avoidance mode`）。要查看给定模式是否有任何选项，你应该查看带有模式名称的函数描述（使用 `Ctrl+f, f`）。

依赖缓冲区的次要模式默认启动要困难一些。有一种在主模式启动时启动次要模式的通用方法，即使用 `hooks`（钩子）。钩子是在主模式启动时可以调用的额外函数。每个主模式都有一个名为 `mode-name-hook` 的钩子。在使用 Text mode 时，在 `.emacs` 文件中启动 `Auto-fill-mode` 所需的代码如下：

```lisp
(add-hook 'text-mode-hook (function
    (lambda () (auto-fill-mode 1))))
```

### 加载主模式

你仍然可以通过按下 `M+X` 并输入其名称为给定缓冲区选择主模式。然而，你无法通过这种方式关闭它（因为缓冲区始终应该恰好有一个主模式）。因此，要关闭一个主模式，你必须开启另一个。（存在一种几乎没有任何功能的主模式，被称为 Fundamental mode。你可以切换到这种模式来关闭特定的模式。）

你可以通过在文件的第一行放置模式来告诉 emacs 启动主模式，如下所示：

```c++
// mode++
```
注意行开头的两个斜杠，这告诉 C++ 编译器不要尝试编译该指令。

另一种让 emacs 自动启动主模式的方法是根据文件名告诉它启动哪种模式。通过这种方式，你可以告诉 emacs 以 `.c` 结尾的文件应该以 C 启动，以 `.doc` 结尾的文件应该以 Text 模式启动。这是通过设置变量 `auto-mode-list` 实现的。你可以可以使用示例作为模板：

```lisp
(setq auto-mode-list (append (list
  ("\\.html" . html-helper-mode)
  ("Makefile" . makefile-mode))
  auto-mode-list))
```





在你开始以这种方式定义许多模式之前，先检查变量 `auto-mode-alist` 可能值得的，因为许多模式指定符是默认定义的。可以通过按下 `Ctrl+h`、`v`，输入 `auto-mode-alist` 然后按下 `Enter` 来检查。

# 获取关于 emacs 的帮助

emacs 有许多在线帮助，范围从按键绑定的描述到 emacs 的通用介绍不等。它们的共同点是可以通过按键前缀 `Ctrl+h` 获取。在以下列表中，你可以获得可用信息的概览：

- `Ctrl+h`, `Ctrl+h` (描述帮助)。这是你需要记住的最重要的按键绑定。它是所有按键绑定索引的入口。
- `Ctrl+h, f` (描述函数)。给定一个函数名，它将提供有关该函数的文档。（我们已经见过许多此类示例了。）
- `Ctrl+h, v` (描述变量)。给定一个变量名，该函数将描述该变量。变量用于配置 emacs 在不同情况下的工作。
- `Ctrl+h, c` (描述按键)。通过此函数，你可以发现给定按键的功能。
- `Ctrl+h, w` (命令所在)。当你发现一个喜欢的函数时，你可能想知道它是否绑定到了某个键上，如果是，绑定在哪里。此函数可以帮助完成此任务。
- `Ctrl+h, a` (查找)。当你搜索执行特定任务的函数时，此函数非常有用。它允许你输入命令名称的一部分，然后它将列出所有匹配项。
- `Ctrl+h, p` (查找软件包)。此函数允许你根据类别搜索软件包和模式。这是寻找增强 emacs 配置项的极佳方法。
- `Ctrl+h, i` (加载 info)。这会加载 info 页面。见下节。

## Info 页面

如果你按下 `Ctrl+h, i`，你将进入巨大的信息世界，即 info 页面。info 页面类似于 Web 上使用的 HTML 页面，不同文档之间有超链接。如果你通过按下问号 (`?`) 开始这段旅程，将进入一个包含 info 系统中按键绑定的页面。以下是四个重要的操作：

- 如果你在引用上方按下 `Enter`，你将进入它所引用的文档。（引用是**粗体**的。）如果你有这样的鼠标，也可以通过点击引用上方的鼠标中间键跟随超链接。
- 当你跟随超链接后，可以按下 `l` 回到来源文档。（这是字母 `l`。）
- info 页面像书一样组织，具有顺序页面（这与 HTML 文档不同，HTML 文档的给定页面可能有多个“下一页”）。通过这种方式，你可以逐页阅读 info 页面。你可以通过 `n,` 进入下一页，通过 `p` 回到上一页。
- 如果你按下 `i`,`，将会被要求在给定的 info 页面集的索引中查找一个单词。接下来，将加载描述该单词的页面。

图 20.4 显示了一个 info 页面的示例。在第一行，你可以看到指向上一页（按页面顺序）和上方页面的引用。注意，没有 `Next` 页面；这是该章节的最后一个。文本 `Entering emacs` 是一个超文本引用，它被高亮显示是因为在取截图时鼠标悬停在文本上。窗口底部有四个指向子章节的引用。

![8227-0533a.gif](img/e8b99bb3b5ed3fe0e2724cc4e56e59c8.gif)

## 继续使用 emacs

在 Web 上，你可以在 `http://www.imada.dk/Technical/Refcards/` 找到 emacs 的参考卡，这可能帮助你记忆所有的按键绑定。（Jesper K.）

我写了一个程序，我认为它对 emacs 初学者非常有价值。它被称为 Dotfile Generator，是一个帮助你设置许多 emacs 变量的配置工具。Dotfile Generator 可以从它的首页 `http://www.imada.dk/~blackie/dotfile` 下载。

在 `ftp://ftp.gnu.org/pub/gnu/` 你可以找到两个关于 elisp 的手册：一本名为 `elisp-manual` 的参考手册和一本名为 `emacs-lisp-introduction` 的介绍。（该介绍是给编程新手的！）

## 额外的 emacs 软件包

你已经看到了 emacs 的许多功能。然而，它最强大的功能之一仍待探索。也就是说，emacs 具有使用用户代码进行扩展的能力。在早之前的一个章节中，你已经看到如何在 `.emacs` 文件中跨会话保存你的按键绑定和宏。你还可以编写完全新的函数，这些函数可以通过 `M+X` 和另一个绑定的键来访问。





这种能力从字面上讲是用户共享的。许多人已经开发了与 emacs 一起使用的额外功能，其中许多功能已经直接随 emacs 一起发行了。在网络上，你可以找到一千多个供 emacs 使用的包。请查看以下地址：`ftp://archive.cis.ohio-state.edu/pub/gnu/emacs/elisp-archive`。这些包包含了主模式（major modes）、次模式（minor modes）以及大量的用户函数。

### 文中未提到的实用 emacs 函数列表

表 20.1 列出了 emacs 函数（我相信它们非常有用）。

#### 表 20.1 适用的 emacs 命令。

| 函数 | 绑定的按键 | 描述 |
| :--- | :--- | :--- |
| `downcase-word` | `M+l` | 将从起始点到单词末尾的所有字母转换为小写。 |
| `capitalize-word` | `M+c` | 将首字母设为大写，单词其余部分设为小写。 |
| `upcase-word` | `M+u` | 将光标点到单词末尾的所有字母转换为大写。 |
| `beginning-of-line` | `Ctrl+a` | 将光标移动到行首。 |
| `end-of-line` | `Ctrl+e` | 将光标移动到行尾。 |
| `goto-line` | 未绑定 | 询问用户行号并跳转到该行。 |
| `kill-line` | `Ctrl+k` | 如果光标不在行尾，则将文本移动到行尾；否则，删除换行符。 |
| `kill-buffer` | `Ctrl+x, k` | 删除当前缓冲区。 |
| `TX fill-paragraph` | `M+q` | 重新排列给定的段落，使所有行都填满。 |

---

# 第五部分 与用户和其他系统通信

## 21 通过调制解调器访问其他 UNIX 系统（第 539 页）
## 22 在网络或互联网上访问其他 UNIX 系统（第 563 页）
## 23 从 Windows 访问 UNIX（第 589 页）
## 24 UNIX 与互联网（第 611 页）

### 第 21 章通过调制解调器访问其他系统（第 539 页）

本章主要介绍如何通过调制解调器（modem）访问其他 UNIX 系统。我将提供逐步说明，引导你完成与这种系统间通信相关的常见任务。

在此之前，需要涵盖一些基础知识。记住，UNIX 是一个多用户操作系统环境，因此它需要对可用（且共享的）系统资源实施一些基本的控制。在成功利用这些资源之前，你必须对它们是如何配置的有一个基本的了解。

本章从一些概念开始。我们将首先查看一些通用特性和要求。之后，我们将重点介绍你需要如何进行配置。最后我们将以具体细节结束。

#### 调制解调器通信概述
调制解调器就像电话。和任何标准电话一样，它们处理传入和传出的数据。因此，当调制解调器拨打号码时，必须由另一个调制解调器接听才能进行有意义的通信。但毕竟，给一个不通相同语言的人打电话有什么意义呢？

一旦两个调制解调器连接起来，两个主机之间进行有效通信成为可能的。通常，这种通信可以实现文件和资源共享以及远程应用程序的执行。

#### 串口设备
UNIX 系统使用名为 `devices` 的特殊文件来让用户访问系统硬件。这些设备通常存储在 `/dev` 子目录中，一个或多个文件提供对特定硬件的访问。

#### 图 21.1 连接 UNIX 主机
图 21.1 总结了在两个远程主机之间建立连接涉及的事件。这为确定过程每个阶段阶段涉及的设备提供了有用的指南。（第 541 页）





任何特定系统上串口端口的具体数量和名称取决于硬件配置和 UNIX 的版本。幸运的是，有一些常见的标准实现可以作为我们的指南。

通常，大多数硬件平台都有四个串口端口，分别称为 `COM1`、`COM2`、`COM3` 和 `COM4`。这些端口对应的 UNIX 设备文件通常称为 `/dev/ttyS0`、`/dev/ttyS1`、`/dev/ttyS2` 和 `/dev/ttyS3`。这些设备的具体名称可能会根据你运行的 UNIX 类型（flavor）而有所不同。

回想图 21.1，你需要能够配置 UNIX 来同时处理拨入（dial-in）和拨出（dial-out）调制解调器服务。UNIX 根据你想要使用的服务提供不同的设备文件，你应该尽量记住使用正确的设备。提供拨出设备的设备通常被称为 `/dev/cua1`、`/dev/cua2`、`/dev/cua3` 和 `/dev/cua4`。相应的 `/dev/ttyS1` 到 `/dev/ttyS4` 设备通常留作拨入使用。

由于你的调制解调器物理上连接到串口上，因此你访问它的唯一方法是通过相应的设备文件。了解你的 UNIX 系统上配置了哪些端口以及哪些可用是重要的。下一节概述的任务将帮助你检查存在哪些串口设备驱动程序。

### 检查串口设备文件

了解你的 UNIX 系统上有哪些设备是重要的。

#### 查找可用串口设备

1. 输入 `ls -l /dev/ttyS?` 并按回车。
2. 出现类似下面的设备列表：
```
crw--w--w-  1 root  root    4, 64 Mar 14 20:56 /dev/ttyS0
crw--w--w-  1 root  root    4, 65 Mar 14 20:56 /dev/ttyS1
crw--w--w-  1 root  root    4, 66 Mar 14 20:56 /dev/ttyS2
crw--w--w-  1 root  root    4, 67 Mar 14 20:56 /dev/ttyS3
```
3. 输入 `ls -l /dev/cua?` 并按回车。
4. 出现类似下面的设备列表：
```
crw--w--w-  1 root  root    5, 64 Mar 14 20:56 /dev/cua0
crw--w--w-  1 root  root    5, 65 Mar 14 20:56 /dev/cua1
crw--w--w-  1 root  root    5, 66 Mar 14 20:56 /dev/cua2
crw--w--w-  1 root  root    5, 67 Mar 14 20:56 /dev/cua3
```

这些设备文件的具体名称可能有所不同，取决于 UNIX 版本和类型。例如，在大多数 SCO UNIX 和 Linux 实现中，拨出线路的串口设备文件称为 `/dev/ttyna`，拨入线路的串口设备文件称为 `/dev/ttynA`，其中 `n` 代表串口号。

### 串口通信配置

现在我们已经确定了 UNIX 主机可以使用的设备，我们有一些服务配置任务需要完成。这些配置任务取决于我们将启用拨入设备、拨出设备还是两者的结合。一个非常重要的考虑因素是有效控制。我们需要确保一旦某个用户占用了一个设备，在通话完成之前，其他用户无法访问该设备。

#### 串口通信拨入

当用户拨入时，你希望在输入有效的用户名和密码后向他显示登录提示符。UNIX 通过不同程序之间的交互来实现这一点。`init` 进程是你每当启动 UNIX 系统时运行的第一个进程。因此，一个名为 `/etc/inittab` 的特殊文件至关重要，它告诉它该做什么。实际上，`init` 并不聪明，它依赖于 `/etc/inittab`。

示例 `/etc/inittab` 文件的节：
```
# Serial lines
s1:45:respawn:/sbin/getty 19200 ttyS0
s2:45:respawn:/sbin/getty 19200 ttyS1
s3:45:respawn:/sbin/getty 19200 ttyS2
s4:45:respawn:/sbin/getty 19200 ttyS3
```
这可以作为 `init` 如何行使其对可用设备权限的示例。




`/etc/inittab` 文件中任何条目的语法都非常简单。每个条目由四个不同的部分（字段）组成，用冒号（:）分隔。第一个字段称为 `tag`，它是一个任意值，用于在 `/etc/inittab` 文件中提供索引。列表 21.1 列出了标记为 `s1`、`s2`、`s3` 和 `s4` 的独立标签，每个标签对应四个可用的串口设备。

第二个字段告诉 `init` 进程在哪个运行级别（run level）执行该特定条目。列表 21.1 中的所有条目都是针对运行级别 4 和 5 的。第三字段告诉 `init` 在第四个字段指定的程序完成后应该做什么。在列表 21.1 中，该字段包含单词 `respawn`，意味着在程序终止后重新启动它。

第四个字段最有趣，因为它包含了你想让 `init` 运行的程序名称。在我们的示例中，这是一个名为 `/etc/getty` 的程序。该程序带有两个选项运行：第一个是连接的调制解调器的最大比特特率，第二个是串口设备文件 `/dev/ttyS1` 到 `/dev/ttyS4`。

`/etc/getty` 是一个监控程序。它读取名为 `/etc/gettydefs` 文件，该文件用于存储任何连接调制解调器的配置设置，包括调制解调器支持的数据速率、流控制和校验位设置等。`/etc/getty`进程读取 `/etc/gettydefs` 并等待调制解调器接收电话。当拨入电话到达时，`/etc/getty` 会启动一个登录进程，向拨入的用户显示登录提示符，然后终止。

让 `init` 将 `/etc/getty` 分配给你的任何串口设备文件，为处理拨入用户请求提供了一种有效方法。当通话完成后，shell 程序终止，`init` 进程会重新启动另一个 `/etc/getty`进程来监控下一次拨入电话。通过这种方式，你的串口设备的生命循环就会持续下去。

## 拨出的串口配置

为了能够从你的 UNIX 系统拨出，你需要能够从 `/etc/getty` 进程获取对串口设备的控制权。最好的方法是编辑特定串口设备的 `/etc/inittab` 条目，将第三字段中的 `respawn` 设置更改为 `off`：

```
S3:45:off:/etc/getty 19200 ttyS3
```

如果你想同时进行拨出和拨入电话怎么办？使用上述配置，你只能安装两个调制解调器和两条电话线（一个入站，一个出站）。然而，还有另一种替代方案。它利用锁文件（lock files）来记录串口设备何时被使用（无论是拨入还是拨出通话），在通话完成之前防止其他对该设备的访问。这种替代方案使用一个名为 `/etc/uugetty` 的程序及其相关的配置文件 `/etc/conf.uugetty`。

为 配置串口设备同时进行拨入和拨出访问

1. 使用 `vi` 命令编辑 `/etc/inittab` 文件，输入 `vi /etc/inittab` 并按回车。
2. 滚动查看 `/etc/inittab` 以找到控制连接调制解调器的串口设备现有条目。
3. 在行开头放置 `#` 字符以注释掉该条目。生成的行看起来如下：
```
#s2:45:respawn:/etc/getty 19200 ttyS2
```
4. 输入 `o` 使用 `vi` 编辑器开启新行，然后输入以下文本：
```
S2:456:respawn:/etc/uugetty ttyS2 19200
```
5. 保存 `/etc/inittab` 文件并按 `Esc` 键然后按 Shift+ZZ 退出 `vi` 程序。
6. 完成 `/etc/inittab` 文件的编辑后，你需要指示 `init` 进程读取你的新配置。要做到这一点，在 shell 提示符下输入以下命令：
```bash
kill -HUP 1
```

前面的步骤演示了如何通过使用 `/etc/uugetty` 配置你的系统以接受并回答拨入请求。需要注意的是，通过在你的任何串口设备上运行 `/etc/uugetty`，该设备将不再可用于拨出。在示例中，通过在 `/dev/ttyS2` 设备上运行 `/etc/uugetty`，你实际上为拨入请求预留了该设备。如果你只有一个有一个调制解调器和电话线，处理同时拨入和拨出请求可能会棘手。

然而，并非一切无望。UNIX 提供了另一组串口设备文件供你用于拨出目的。在 Linux 和 SCO UNIX 系统，这些文件被称为 `/dev/cua#`，其中 `#` 指端口号。例如，在前面的步骤中，你配置了 `/dev/ttyS2` 设备以接受拨入电话。要使用同一个调制解调器和电话线进行拨出请求，你可以使用相应的拨出设备 `/dev/cua2`。只要没有人在同时拨入系统，你就可以使用 `/dev/cua2` 设备拨出电话，并让 `/etc/uugetty` 空闲监控连接的入站电话。

## 使用 cu 程序登录



既然你已经配置了 `/etc/getty` 来监听传入的电话，让我们尝试拨号接入系统。大多数 UNIX 版本都提供一个名为 `cu` 的标准通信程序，全称是 call UNIX（拨打 UNIX）。`cu` 程序非常基础，不具备许多商业通信软件包中常见的各种华丽功能。不过，`cu` 功能完全完备。本节将探索如何利用该程序完成简单的主机到主机之间的通信。管理员通常将 `cu` 程序用作故障排除工具，因为它提供了一种测试串口设备、控制文件和调制解器配置的简单且有效的方法。

在我们研究 `cu` 的高级功能之前，让我们从检查你的配置开始。

### 使用 cu 登录另一个 UNIX 系统

1. 在 shell 提示符下输入 `cu` 并按回车启动 `cu` 程序。该程序将返回以下语法语句：
```
Usage: cu [options] [system or phone number]
```

2. 我的调制解器连接到 COM3 端口，因此我需要指示 `cu` 使用设备 `/dev/cua2`。在 shell 提示符下，我输入 `cu -l /dev/cua2` 来使用该串口设备启动 `cu`。你应该输入相同的命令，并替换为你正在使用的设备名称。

3. 如果一切配置正确，`cu` 程序将回显单词 `Connected` 并等待进一步指令。如果 `cu` 回显了类似下面的消息，说明你遇到了问题：
``````
cu: open (/dev/ttyS2): Permission denied
cu: /dev/ttyS2: line in use
```
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

#### 保持 init 信息同步

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 你可以使用从 `/dev/ttyS1` 到 `/dev/ttyS4` 的任何设备，但如果你这样做了，你需要告诉 `init` 不要针对该设备运行 `/etc/getty` 或 `/etc/uugetty`。类似这样的消息意味着有其他东西正在使用该特定线路。那个其他东西可能是 `init` 进程，它可能正在运行 `/etc/getty`。

4. 使用 `vi` 程序打开 `/etc/inittab` 文件，并确保该串口条目已被注释。记住，如果你更改了 `/etc/inittab` 文件，你需要告诉 `init` 进程重新读取该文件。这可以通过两种方式实现：输入 `init q` 并按回车，或者输入 `kill -HUP 1` 并按回车。

5. 如果 `cu` 程序最初回显 `Connected`，但随后立即回显显示 `cu: hangup` 的错误消息，说明你正在连接到一个没有调制解器的串口。确定你的调制解器连接到哪个线路，并使用正确的设备重新运行 `cu`。

6. 如果你成功将 `cu` 连接到调制解器，输入 `at`。在输入时你可能看不到字符，但你应该能看到屏幕上回显 `OK`。这条消息来自你的调制解器，它在告诉你它运行正常且在线。

7. 输入 `ate1` 并按回车。调制解器将在屏幕上回显 `OK`。现在你输入的内容都将显示出来。

8. 现在让我们尝试连接到你的远程主机。输入 `atdt` 后加上主机调制解器的电话号码。调制解器会忽略任何空格。如果你通过 PBX 拨号，可能需要先拨打 9 以访问外部线路。你可以输入逗号来表示暂停，为交换机分配线路留出额外。

9. 调制解器将拨号并连接到远程调制解器。在远程主机上，`/etc/getty` 或 `/etc/uugetty` 程序将注意到传入的电话并发布登录提示，该提示将回显在你的屏幕上。使用你的用户名和密码登录。

10. 要断开连接，输入 `exit` 退出远程 shell。系统将通过回显括号中的系统名称来响应。然后输入 `..`

### 配置 cu

可以配置 `cu` 程序拨打远程系统，而无需指定使用哪种设备，也不需要直接连接调制解器来拨打电话号码。通过这种方式，你可以为系统配置一个或多个拨出线路，并要求 `cu` 程序获取第一条可用线路并自动拨打所需的电话号码。

`cu` 程序使用与 `uucp` 程序套件相关的四个配置文件。这些配置文件通常位于 `/usr/lib/uucp/` 子目录下，分别称为 `Devices`、`Dialers`、`Systems` 和 `Permissions`。重要的是，这四个配置文件是相互关联的，必须相互交叉引用才能成功工作。下面的步骤将引导你完成这些文件的示例配置。




## 1. 进入 vi 设备
（注意文件名中的大写字母 D）。在该文件中，你需要定义想要使用的串口端口，并对这些端口设置引用，这些引用可以供 `/usr/lib/uucp/Systems` 和 `/usr/lib/uucp/Dialers` 配置文件使用。以下代码演示了 `Devices` 文件中条目的的语法：

```text
# /usr/lib/uucp/Devices 
#为每个用于拨号输出的串口设备添加定义
modem cua1 - 19200 hayes
modem cua2 - 19200 hayes
modem cua3 - 19200 hayes
modem cua1 - 19200 hayes
```

`Devices` 文件中的每一行都指向 `/dev` 中一个定义的拨出设备。你需要识别调制解调器和最高可用调制解调器速度，以及用于识别连接到此端口的设备类型的关键字。注意所有条目都使用相同的关键字 `modem`。这样一来，拨出请求就能简单地获取第一个可用端口，而无需等待特定设备释放。

## 2. 在 /usr/lib/uucp/Devices 文件中输入新行
输入 `o` 然后输入 `modem device - 19200 hayes`（将单词 *device* 替换为你的拨出设备文件名称）。按 `Esc` 然后按 `Shift+ZZ` 退出并保存 `/usr/lib/uucp/Devices` 文件。

## 3. 编辑 /usr/lib/uucp/Dialers 文件
输入 `vi Dialers`（同样，注意文件名中的大写字母 D）。在该文件中，你需要定义 `cu` 或 `uucp` 程序发送给调制解调器的初始化设置。这是一个示例：

```text
# /usr/lib/uucp/Dialers 
#为 Drivers 文件中定义的每个调制解调器添加定义
hayes =W-, ""ATZ OK ATDT\T CONNECT
```

## 4. 引用 hayes 关键字
你需要引用位于 `/usr/lib/uucp/Devices` 文件中的 `hayes` 关键字。按 `o` 输入新行并输入以下内容：

```text
hayes =W-, ""ATZ OK ATDT\T CONNECT
```

`ATZ` 命令重置调制解调器，并预期调制解调器返回 `OK`。`ATDT` 命令在 `cu` 程序中应该常见。`\T` 指向为系统定义并从 `/usr/lib/uucp/Systems` 文件传递的电话号码。

## 5. 保存并退出
按 `Esc` 然后按 `ZZ` 保存 `/usr/lib/uucp/Dialers` 文件。

## 6. /usr/lib/uucp/Systems 文件
`/usr/lib/uucp/Systems` 文件定义了拨号的系统名称、应使用的端口类型、允许无人连接的调度（专门针对 `uucp` 程序）、拨号电话号码，以及连接后允许自动登录的一些脚本命令。这是一个示例：

```text
# /usr/lib/uucp/Systems 
#为用户想要访问的远程系统添加定义。
Horse MoTuWe0800-1700 modem 19200 123456 "\nlogin:-login:name word:pass
Jupiter Any modem 19200 123456 "\nlogin:-login:username word:password
Remote Any modem 19200 12345678
```

## 7. 为远程连接编辑 Systems 文件
输入 `vi /usr/lib/uucp/Systems` 编辑此文件。按 `o` 进入新行并输入：

```text
remote Any modem 19200 12345678
```

这为 `cu` 程序定义了一个条目，使其可以在全一天中的任何时间，使用 `/usr/lib/uucp/Devices` 文件中所示的任何类型为 `modem` 的设备连接到你的远程系统。此外，你还指定了连接速率和拨号电话号码。按 `Esc` 和 `ZZ` 保存并退出文件。

## 8. 配置 /usr/lib/uucp/Permissions 文件
在远程 UNIX 系统上，你需要配置 `/usr/lib/uucp/Permissions` 文件以允许自己远程登录，并定义你想提供的读写权限。打开或创建 `/usr/lib/uucp/Permissions` 文件，并添加以下行：

```text
LOGNAME=local_machine
MACHINE=local_machine
SENDFILE=yes
```

当你允许无人 `uucp` 访问你的 UNIX 主机时，`/usr/lib/uucp/Permissions` 文件至关重要。在这种情况下，文件中应为所有允许访问的主机定义条目，并应针对以下关键字提供条目：

- `MACHINE`: 系统名称
- `LOGNAME`: 日志文件中系统名称
- `CALLBACK`: 在给定号码建立连接后回拨的号码
- `REQUEST`: 指定远程系统是否可以请求文件
- `SENDFILE`: 明确远程系统是否可以发送文件





- 规定远程系统是否可以发送文件。
- READ：指定远程系统可以读取的目录。
- WRITE：指定远程系统可以写入的目录。
- COMMANDS：指定 uux 可以执行的命令。
9. 按 `Esc` 然后按 `ZZ` 保存权限文件并退出到 shell 提示符。

### 使用 `cu` 程序

你现在可以使用你的新配置文件来改进 `cu` 程序的操作。此外，你还可以探索一些其他的 `cu` 的功能，例如传输文件。

#### 使用 `cu` 传输文件

1. 登录 UNIX 并输入 `cu-z remote`（其中 *remote* 是你在 `/usr/lib/uucp/Systems` 文件中指定的系统名称）。`cu` 程序将自动连接到远程系统，并返回用于用户名和密码的登录提示符。
2. 登录到远程系统。然后输入命令 `~?`。`cu` 程序将显示可用命令列表。
3. 输入 `~put` 将文件传输到远程主机。
4. `cu` 程序将提示你输入要传输到远程系统的本地文件。输入本地文件名。
5. `cu` 程序将提示你文件传输到远程系统后的名称。你可以直接按回车键使用相同的名称。
6. `cu` 程序将指示传输何时完成。
7. 输入 `~.` 断开连接并返回 shell 提示符。

列表 21.2 展示了上述步骤的执行情况，显示了将文件 `/home/report` 传输到远程连接的系统。注意，也可以使用其他转义序列来传输文件。输入 `~?` 命令可以列出你的 `cu` 程序实现中的可用命令。

**警告**：尽管 `cu` 程序可以在系统之间传输文件，但它执行时不进行任何错误检查或恢复。应该使用 `sum` 命令来对潜在的数据损坏进行一致性检查。

#### 使用 *cu* 传输文件

转义序列：
- `~local_host`
- `~.` 挂断
- `~!CMD` 运行 shell
- `~$CMD` 将 stdout 输出到远程
- `~CMD` 从远程接收 stdin
- `~+CMD` 将 stdin 和 stdout 都重定向到远程
- `~#` 发送中断 (break)
- `~cDIR` 切换目录
- `~>` 发送文件
- `~<` 接收文件
- `~p FROM TO` 发送到 Unix
- `~t FROM TO` 从 Unix 接收
- `~s VAR VAL` 设置变量
- `~s VAR` 设置布尔值
- `~s!VAR` 取消布尔值
- `~v` 列出变量
- `~z` 挂起
- `~%` 发送中断
- `~%cd DIR` 切换目录
- `~%put FROM TO` 发送文件
- `~%take FROM TO` 接收文件
- `~%nostop` 无 XON/XOFF
- `~%stop` 使用 XON/XOFF

```
connected
~put
file to send: /home/report
Remote file name [report]:
...
file transfer complete
connected
~.
Disconnected
```

#### 在本地系统上运行命令

1. 登录 UNIX 并使用 `cu -z remote` 连接到远程主机（其中 *remote* 是你在 `/usr/lib/uucp/Systems` 文件中配置的远程系统主机名）。连接到远程主机后，使用有效的用户 ID 和密码登录。
2. 在 shell 中输入 `vi /home/cu_remote_file` 在远程主机上创建一个名为 `/home/cu_remote_file` 的新文件。按 o 并输入 This is a test of the `cu` program.。按 Esc 键然后按 ZZ 保存文件并返回 shell 提示符。
3. 输入命令 `sum cu_remote_file`。`sum` 程序将输出两个数字：文件 `cu_remote_file` 的 16 位校验和，以及该文件大小的估计值。记下这两个值。
4. 输入 `~%take /home/cu_remote_file /home/cu_local_file` 将文件传输到本地 UNIX 主机，并使用相同的文件名保存。
5. 当 `cu` 表明传输完成后，你可以通过对传输后的副本运行 `sum` 命令来检查文件是否已无错误传输。




5. 输入 `~! /bin/sh` 以从 cu 程序内部在本地系统上运行 shell。在 shell 提示符下，输入 `sum cu_local_file` 然后按回车。与之前一样，`sum` 程序将输出两个数字。将这些数字与步骤 3 中生成的数字进行比对。如果传输过程中没有错误，这些数字将是相同的。
6. 输入 `exit` 返回 cu 程序。退出远程连接并按 `~.` 退出 cu 程序。

在配置好用于 cu 操作的文件后，你还可以运行 uucp 命令。

## 通过 uucp 传输文件

UUCP 代表 UNIX-to-UNIX Copy（复制程序）。它不仅仅是一个程序，而是一套实用程序，提供了一种跨越物理分布的 UNIX 平台传输文件和执行应用程序的方法。uucp 套件最常用于无人值文件传输，特别是系统之间的电子邮件传输。然而，用户也可以使用这些程序来满足自己的文件传输需求。

## 创建文件传输程序

1. 登录 UNIX 并创建一个名为 `uucp_data` 的测试文件。
2. 在 shell 提示符下，输入 `uucp uucp_data remote!/home/uucp_data`。
3. 使用 `vi` 编辑 `/usr/lib/uucp/Systems` 文件，并为你主机 `remote` 创建的条目添加以下命令。在电话号码之后，添加以下测试：
```
" \rgin:-gin:<userid> word:<password>
```
将 `<userid>` 和 `<password>` 替换为 `remote` 上有效的用户名和密码。
4. `uucp` 命令将引用 `/usr/lib/uucp/Systems` 文件并定位到 `remote` 的条目。当找到引用时，将与 `remote` 主机建立，`uucp` 将使用用户名密码对自动登录。一旦登录完成，文件 `uucp_data` 将被传输`uucp` 将终止连接。
5. `uucp` 程序期望若干提供额外功能的参数。可以使用 `-m` 切换强制系统在传输完成后返回一封电子邮件。在 shell 提示符下输入以下命令：
```
uucp -m uucp_data remote!/home/uucp_data
```
然后按回车。
6. 同样，如果你将文件复制到远程系统，你可能希望在文件到达时通知该系统的用户。你可以通过 `-n` 切换来实现。使用以下命令在文件传输完成后向远程系统上的用户 `Lauren` 发送电子邮件：
```
uucp -nLauren uucp_data remote!/home/uucp_data
```

### 限制用户放置文件的位置

需要编辑 `/usr/lib/uucp/Permissions` 文件以允许将文件传输到指定位置。在之前的示例中就是如此。但是，限制用户在远程系统上放置文件的位置是一个良好的习惯。通常这应该是 `/usr/spool/uucp` 或 `/usr/spool/ucpp`。

## 运行远程命令

`uux` 程序是 uucp 套件的一部分。它允许拥有权限的用户在远程主机上执行命令。再次，该命令的执行通过 `/usr/lib/uucp/Permissions` 文件控制。

1. 登录 UNIX 并发布 `uuxdate` 命令。
2. 程序将在远程主机上执行 `date` 命令并将结果返回给你的 shell。
通常，`uux` 命令不会由用户直接执行，而是作为电子邮件和网络新闻服务器等应用程序的一部分使用的。出于这个原因，大多数系统会在 `/usr/lib/uucp/Permissions` 文件中限制 `rmail` 和 `rnews` 程序的执行。

## 检查 uucp 任务状态

用户可以通过 `ustat` 程序检查任何待处理的 uucp 文件传输请求的状态。

1. 登录 UNIX，并在 shell 提示符下输入 `ustat`。
2. 将显示当前队列中的作业列表。这里是一个示例：
```
jupiter 02/14-20:45:00 (POLL) mars 02/14-20:53 S jupiter filename.txt 48871
```
![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)/home/james/docs/sams/uucp/filename.txt




3. 默认情况下，`uustat` 仅显示由执行 `uustat` 命令的用户所排队的任务。要显示所有当前调度的任务，请输入 `uustat -all`。

你可以带有一些可选参数运行 `uustat` 程序，以获取有关单个 uucp 程序性能的额外信息。

# 带参数运行 uustat

1. 输入 `uustat -e` 并按回车。这将提供所有当前排队的程序执行请求的列表。

2. 输入 `uustat -m` 并按回车。该命令将生成连接到远程主机状态的摘要。例如：

```text
remote        05/23 - 10:15    CALLER SCRIPT FAILED dtcg02        05/30 - 11:30     LOGIN FAILED
jupiter         05/30 - 11:30    CONN FAILED (CALLER ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)SCRIPT FAILED)
```

上述代码说明了到三个主机（remote、dtcg02 和 jupiter）失败的 uucp 连接。

## 取消 uucp 请求

你可以使用 `uustat` 程序取消待处理的 uucp 文件传输或程序执行请求。

### 使用 uustat 取消 uucp 请求

1. 登录 UNIX。在 shell 提示符下，通过输入 `vi /usr/lib/uucp/Systems` 编辑 `/usr/lib/uucp/Systems` 文件。

2. 按 `O` 键添加新行，然后输入以下内容：
```text
nohost Never modem 19200 123456
```
定义了一个名为 `nohost` 的新系统，它永远不会被 uucp 程序调用。

3. 通过向已知永远不会发送的 `nohost` 传输请求向 uucp 队列放入消息。输入以下内容并按回车：
```text
uucp /home/uucp_data nohost!/home/uucp_data
```

4. 输入 `uustat`。你会看到类似下面的代码行：
```text
nohostN001 nohost root 03-15 02:25 Sending ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)/home/uucp_data (1864 bytes) to /home/uucp_data ![fc4f3a8aef38b56941e55505c60ecaf.gif](img/fc4f3a8aef38b56941e55505c60ecaf.gif) ![fc4f3a8aef38b56941e55505c60ecaf.gif](img/fc4f3a8aef38b56941e55505c60ecaf.gif)
```
使用 `uustat` 取消时请注意 Lock。命令 `uustat -K`（大写 K）将移除所有当前排队的 uucp 请求。使用 `uustat` 取消任务时，请确保 Lock 键没有被意外设置。

5. 要删除传输请求，输入以下命令：
```bash
uustat -k nohostN001
```

## 通过调制解调器扩展网络 (PPP)

点点协议（PPP）提供了一种通过调制解调器到调制解调器连接传输 IP 包的方法。两个远程主机之间的 PPP 连接为所有远程用户和应用程序提供通过单个调制解调器链路相互访问的方法，而不是将通信限制在任何时刻的单个用户。

通过这种方式，可以使用 PPP 扩展网络，使得远程主机可以像位于同一个本地局域网（LAN）一样协作。但应该，通过拨号线路连接的两个系统之间的通信速度将比 LAN 连接慢一个数量级。

## 配置简单的 PPP 连接

在任何 UNIX 主机上配置 PPP 操作都有三个不同部分：在远程系统（接受接入的系统）上创建 PPP 用户帐户、开发 Chat 脚本以及执行 PPP 守护进程。让我们逐一检查。

### 创建 PPP 用户帐户

1. 建议设置一个专用用户账户来控制 PPP 的执行。以 root 用户身份登录远程系统并创建一个新账户。然后编辑 `/etc/passwd` 文件，使其看起来类似于：
```text
ppp_user:e9prWE5B4fs:501:202:ppp execution account: ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)/tmp:/usr/lib/ppp/ppp-on
```
需要注意的是，GID 和 UID 值将取决于特定系统，你在 `/etc/passwd` 中创建的密码也是如此。



第二个字段。启动程序指示为文件 `/usr/lib/ppp/ppp-on`，这是一个用于开启 ppp 服务的配置脚本。

2.  在开启 PPP 服务之前，你需要在你的调制解调器之间建立连接。这与你之前查看使用 `cu` 程序进行远程登录时类似：在远程系统上输入用户名和密码之前，你必须先连接，让本地调制解调器拨号远程主机的电话号码。`chat` 程序为你提供了一种为 PPP 执行此操作的有效方法。

输入以下内容创建一个新的 PPP chat 脚本：

```bash
vi /usr/lib/ppp/ppp-chat
```

然后按回车键。

3.  输入 `o` 添加以下行，并替换为你系统的正确用户名（通常为 `ppp` 或 `ppp_user`）、密码和电话号码：

```text
ATZ OK ATDT12345678 CONNECT login: ppp word: <password>
```

注意，`chat` 程序使用的语法与你在 `/usr/lib/uucp/Systems` 配置文件中输入的条目非常相似。第一条条目重置调制解调器，调制解调器会发送 `OK`。然后，chat 脚本拨打你远程主机的电话号码。一旦收到 `CONNECT` 消息和登录提示，chat 脚本将发送用户名，并在随后的密码提示处再次发送密码。

4.  按 `Esc` 然后按 `ZZ` 保存并退出新的 `/usr/lib/ppp/ppp-chat` 文件。

4.  通过输入以下命令创建启动 PPP 连接的 shell 脚本：

```bash
vi /usr/lib/ppp/ppp-on
```

并该文件包含以下条目：

```bash
#!/bin/sh
#script to activate ppp connection
pppd connect "chat -f /usr/lib/ppp/ppp-chat"
/dev/cua2 19200
/dev/cua2-detach 130.100.0.5:130.200.0.20 defaultroute
```

注意，在这个示例中，我将 PPP 的拨号设备设置为 `/dev/cua2`，并将本地和远程地址设置为 `130.100.0.5` 和 `130.200.0.20`。你应该修改这些以反映你的配置。完成后，按 `Esc` 键然后按 `ZZ` 保存文件并返回 shell 提示符。

5.  你需要对此文件设置权限，允许 root 用户执行该脚本并激活 PPP 连接。为此，请输入：

```bash
chmod 744 /usr/lib/ppp/ppp-on
```

6.  运行 shell 脚本建立 PPP 链路。

### 停止连接

通过向 `pppd` 进程 ID (PID) 发挂断信号来移除现有的 PPP 连接。`pppd` 进程将其 PID 存储在它在 `/var/lock` 子目录下创建的设备文件中。该文件名将与串口设备相关。对于我的 PPP 配置，我使用了串口设备 `/dev/cua2`，因此我的锁文件名为 `/var/lock/LCK..cua2`。

注意：许多 UNIX 版本提供了基本的 shell 脚本来开启和关闭 PPP 连接。虽然这些文件通常被称为 `ppp-on` 和 `ppp-off`，但它们的目录位置在不同的 UNIX 版本之间差异很大。输入 `find / -name ppp -o* -print` 以在系统中定位这些文件，然后按回车键。

### 移除 PPP 连接

1.  以 root 用户登录并输入 `cat /var/lock/LCK..cua2`。这将在屏幕上显示数字，它是当前使用 `/dev/cua2` 的 `pppd` 的 PID。
2.  通过 `kill -HUP PID` 发送挂断信号告诉 `pppd` 终止，其中 `PID` 是步骤 1 返回的数字。

本章解释了你如何访问连接到你的 UNIX 系统的调制解调器。然而，值得注意的是，在许多 UNIX 版本中，系统设备文件名可能存在细微差异。需要注意的是，在过去的几年里，其他更高效有效的 UNIX 主机间文件传输方法已逐渐取代了 UUCP 的使用。可以说，发现依赖 UUCP 作为文件传输机制的 UNIX 主机已变得相当普通。UUCP 的衰落很大程度上归因于越来越多使用 Sendmail 程序传输电子邮件。但永久连接到互联网的主机日益增多对其发展也没有帮助。如果主机需要通过互联网持续连接，那么采用批处理文件传输方法是有价值的。



在某种程度上，UUCP 的衰落换来了 PPP 的获益，因为启用 PPP 的连接已成为提供 Internet 接入的首选方式。本章阐述了你如何配置 UNIX 主机以建立瞬时的 PPP 连接。但需要注意的是，大多数 PPP 连接是作为持久性连接建立的，且 `ppp-off` 脚本永远不会被运行。

# 第 22 章：访问网络或互联网上的其他系统
作者：James Edwards - 第 563 页

## 一些网络概念
在开始之前，你需要掌握一些基础知识。网络涉及许多需要安装和配置的硬件与软件组件。图 22.1 提供了一个实用的起点，说明了这些组件如何相互结合以提供网络连接性。

![227-0564a.gif](img/5ec3e821a67d5498cf12705c7d78e4.gif) 图 22.1 网络连接的组件。图 22.1 展示了一个 UNIX 主机连接到以太网网络，并使用 TCP/IP 协议与邻近主机通信。这一切是如何结合在一起的？嗯，以太网为我们主机的物理连接提供了基础。在主机连接后，它们就可以通过 TCP/IP 协议进行通信。这些协议为主机提供了相互操作的方法，例如执行远程程序、共享资源和传输文件。第 564 页

TCP/IP 协议族是 UNIX 网络系统的核心。本章将介绍这些协议的操作。尽管这一章不能让你立即成为 TCP/IP 专家，但你将获得足够的信息和指导，让你能够充分使用这些协议并连接到网络。

以太网是迄今最常见的物理网络传输形式。然而，也存在其他形式，包括令牌环（token ring）、FDDI 和异步传输模式（ATM），其中某些可能听起来很熟悉。尽管这些网络类型都采用不同的特性和功能，并且都需要截然不同的配置，但它们之间确实存在某些相似之处。事实上，图 22.1 中概述的相同通用连接组件在所有这些物理网络类型中都适用。本章详细研究了以太网，因为它是你最可能需要交互的网络形式。

### 检查你的网络连接
你首先需要物理上将你的系统连接到网络。这是通过使用网络接口卡，或 `NIC`（读作 *nick*）来实现的。`NIC` 需要物理地安装在你的 UNIX 系统中。系统主板上的若干被称为 `slots`（槽）的连接点是专门为此目的预留的。事实上，许多 UNIX 系统在厂家出厂时已经安装了 `NIC`。

在将 `NIC` 物理安装到你的系统中后，你需要告诉 UNIX 如何识别并与其通信。在 UNIX 中，所有与硬件的通信都通过称为“设备”（devices）的特殊文件处理。这些设备需要在内核中进行配置。因此，当你添加一个新的 `NIC` 时，需要确保内核已有相应的设备文件可用。通常情况下，你的系统会在系统启动时自动检测已安装的 `NIC` 的存在及其当前配置。然而，在某些 UNIX 版本中，有必要运行配置程序来告知系统新添加的 `NIC`。第 565 页

你需要运行的配置程序取决于你正在使用的 UNIX 版本。这些程序通常是菜单驱动的，并引导用户配置新设备。要确保 UNIX 内核已识别新设备条目的一种相对简单的方法是查看系统启动时显示的消息。这些信息可能会飞闪而过，使得检查非常困难。幸运的是，这些信息也会被写入一个特殊的日志，可以使用 `dmesg` 命令进行显示。第 566 页




1. 输入命令 `dmesg | more` 并查找与以太网设备的引用。

2. 根据你系统的启动过程，`dmesg` 的内容可能太大且杂乱，难以翻阅查找以太网驱动程序的引用。如果是这样，输入 `dmesg | grep eth` 来准确定任何定义的设备。列表 22.1 展示了该命令在我的 `dmesg` 文件上的执行结果。

列表 22.1 查找以太网卡。
```
# dmesg | grep eth eth0: WD80x3 at 0x300, 00 00 C0 FE 55 28, IRQ 5, 0xca00
```

3. `dmesg` 的输出显示了已安装 NIC（NIC）的当前配置。在列表 22.1 的示例中，UNIX 设备 `eth0` 对应使用 IRQ 5 安装的 NIC，内存地址为 `ca000`，I/O 通道 `300`。这些值是制造商提供的默认值。如果我想更改其中任何值，必须遵循 NIC 制造商的说明进行操作。

4. 现在你已经知道 UNIX 系统如何引用已安装的 NIC，你可以使用名为 `ifconfig`（读作 *if config*）的接口配置程序对其进行配置。许多（但并非所有）版本的 UNIX 都为我们提供了通过 `netstat` 命令确认设备存在的方法。输入 `netstat -i` 并按回车。此命令显示所有系统接口的状态，任何未配置的接口其设备名称旁边都会有一个星号。

### 检查 IP 地址

每个 NIC 都需要分配一个唯一地址以便 TCP/IP 协议正常工作。分配的 IP 地址取自可用的 32 位二进制地址空间。然而，为了简单易于使用，你可以使用被称为“十进制点表示法”（Decimal Dot Notation）的概念来引用此地址空间。十进制点表示法的操作是将一个 32 位 IP 地址分为四个相等的部分，每部分长 8 位。这些 8 位值中的每一个都可以表示为十进制，每个十进制数之间用点隔开。列表 22.2 说明了这一点；注意当地址被划分并表示为十进制数时，引用它将变得容易得多。

列表 22.2 通过十进制表示法表示 IP 地址。
```
00000110000001100000001000000001 - 32 位二进制值
10.10.2.1 - 分为 4 个等部分的十进制值
```

记住你使用 TCP/IP 协议在网络内的不同主机之间移动数据。要成功实现此点，每个主机都需要唯一的 IP 地址。事实上，一个网络主机对于每个安装的 NIC 可以有多个 IP 地址。你可以使用名为 `ifconfig` 的标准程序为 NIC 分配 IP 地址。以下任务提供了一个快速示例：

1. 以 root 身份登录 UNIX（只有 root 用户可以执行 `ifconfig` 命令）。
2. 在命令行输入以下命令：`ifconfig eth0 130.100.10.1`，将 `eth0` 替换为已安装并配置的 NIC 设备名称，并将 `130.100.10.1` 替换为你想分配给此接口的 IP 地址。
3. 你也可以运行 `ifconfig` 命令来报告任何已安装接口的配置。要做到这一点，输入 `ifconfig -a`。使用 `-a` 开关告诉 `ifconfig` 报告所有安装接口的配置。列表 22.3 提供了一个示例。

列表 22.3 ifconfig 配置详情。
```
#ifconfig -a le0:flags=63<UP, BROADCAST, NOTRAILERS, RUNNING>
  inet 10.252.10.66 netmask fffe0 broadcast 10.252.10.95
eth0:flags=63<UP, BROADCAST, NOTRAILERS, RUNNING>
  inet 130.100.10.1 netmask fffff000 broadcast 130.100.255.255
eth1:flags=63<UP, BROADCAST, NOTRAILERS, RUNNING>
  inet 10.252.10.33 netmask fffe0 broadcast 10.252.10.63
```

注意列表 22.3 中的 `ifconfig` 报告 `eth0` 的 IP 地址为 `130.100.10.1`，掩码值为 `130.100.255.255`。为了理解 IP 地址，你需要意识到该地址同时标识了主机地址和网络地址。掩码值用于指示 IP 地址的哪部分是主机部分，哪部分是网络部分。掩码的构建方式是使用二进制 1 覆盖地址的网络部分，这对于十进制点表示法中的每个十进制数都等于 255。如果我们将提供的掩码应用于任何 IP 地址，它将揭示地址的主机部分和网络部分。列表 22.4 中的后续示例提供了一个掩码如何使用的示例。

列表 22.4 检查掩码值。
```
00000110000001100000001000000001 - 分为 4 个等部分 10.10.2.1 - 每个表示为十进制值
255.255.0.0 - 十进制掩码值
11111111111111110000000000000000 - 二进制掩码值
masked.masked.2.1 - 掩码覆盖了前两个十进制数留下主机地址
10.10.host.host - 掩码覆盖了网络
```



总的来说，IP 地址空间被分为三个主要组，称为地址类。每种类都提供了一个适用于特定网络类型的地址空间。表 22.1 详细列出了这些分类的划分情况，指出了地址范围和典型的网络用途。

### 表 22.1 理解整个 IP 地址空间

| 地址类 | 地址范围 | 默认掩掩码 | 典型用途和功能 |
| :--- | :--- | :--- | :--- |
| A 类 | 1.0.0.0 127.255.255.255 | 255.0.0.0 | A 类地址包含较少量的网络地址，但每个网络可以寻址超过 1600 万个主机。 |
| B 类 | 128.0.0.0 191.255.255.255 | 255.255.0.0 | B 类地址空间为大量中等网络提供了支持，每个网络包含超过 6 万个主机。 |
| C 类 | 192.0.0.0 223.255.255.255 | 255.255.255.0 | C 类地址空间为数百万小规模网络提供了支持，每个网络最多包含 254 个主机。C 类限制 223.255.255.255 以上地址空间被保留并应被忽略。 |

表 22.1 表明，你只需通过地址的第一个十进制数字就可以判断该 IP 地址属于哪一类；通过使用默认掩掩码值，你可以自动确定网络号和主机地址。

在配置 IP 地址时，你可以选择使用默认掩掩码值，或者指定你自己的掩码，从而能够引用更多的网络，每个网络包含更少的主机。这些额外的网络被称为子网络（subnetworks），因为它们地址类的子集，而掩码现在被称为子网络掩码（subnet mask）。你可以使用 `ifconfig` 程序来定义子网络掩码值。

1. 以 root 管理员身份登录 UNIX。输入 `ifconfig a` 来报告系统中安装的所有接口的当前配置。选择一个接口。我将使用接口 `eth0`。你应该将该接口的引用替换为你自己的接口。
2. 输入 `ifconfig eth0 130.100.10.1`，然后按回车。
3. 输入 `ifconfig eth0`，注意掩码值被设置为 B 类的默认值 `255.255.0.0`，或者如果你的系统以十六进制显示，则为 `ffffffff0000`。
4. 输入 `ifconfig eth0 130.100.10.1 netmask 255.255.255.0`，然后按回车。
5. 输入 `ifconfig eth0`，注意掩码被设置为值 `255.255.255.0`，或者如果你的系统以十六进制显示，则为 `ffffffff00`。

`ifconfig` 程序具有许多额外选项，允许用户更改 TCP/IP 协议在给定接口上的运行方式。这些设置的细节超出了本章的范围。要需更详细的功能划分，请参考 UNIX 的 `man` 页面。在退出 `ifconfig` 程序之前，进行最后一次更改是有帮助的：设置广播值。

在 TCP/IP 协议的发展过程中，产生了两种关于接口应如何向任何网络上的所有主机发送数据包的流派。记得我们讨论过的，IP 地址由主机部分和网络部分组成。两种方法都认为 IP 地址的网络部分需要被识别，但其中一种方法决定此网络内的所有主机将通过主机部分中的全 1 来识别，而另一种方法则指定为全 0。随着时间的推移，全 1 占据了主导地位。到目前，它是最常见的设置；然而，由于该选项存在，检查你的接口配置以确保你正在使用正确的设置是非常关重要的。

创建一个任务列表来说说明如何使用 `ifconfig` 程序报告接口配置并记录全 0 广播，然后将其更改为全 1。该列表还说明了 `ifconfig` 命令的完整用法，包括 IP 地址、子网络掩码和广播地址。

1. 以 root 管理员身份登录 UNIX，并输入以下命令（将指定值替换为匹配你的配置和地址需求）：`ifconfig eth0 130.100.10.1 netmask 255.255.255.0 broadcast 130.100.10.0`。然后按回车。
2. 输入 `ifconfig eth0`，注意该接口的广播地址已设置为 `130.100.10.0`。
3. 现在配置接口以全 1 广播（记住这是最常用的设置）。为了实现这一点，输入以下命令：`ifconfig eth0 130.100.10.1 netmask 255.255.255.0 broadcast 130.100.10.255`，并按回车。
4. 输入 `ifconfig eth0`，注意该接口的广播地址已设置为 `130.100.10.255`。

### 为 UNIX 主机命名

通过 IP 地址引用 UNIX 主机可能会很繁琐；通过给你的主机命名可以让事情变得更容易。为了做到这一点，你在 `/etc/hosts` 文件中提供一个条目：

1. 以 root 管理员身份登录 UNIX（更改主机名是只有 root 才能执行的操作之一）。
2. `/etc/hosts` 文件用于将主机名与我们系统的 IP 地址关联。当我们引用此主机名时，系统将引用 `/etc/hosts` 文件来确定对应的 IP 地址。`/etc/hosts` 文件可以扩展以包含对我们需要访问的其他主机的引用。





# 网络工具使用

进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在表达式 `cvar = avar + bvar` 中，加法运算符（+`）将 `avar` 与 `bvar` 相加，得到它们的和 `cvar`。

在 `List.of(arg0, arg1, arg2)` 中，`List` 接口的方法 `of()` 接受一系列元素，返回它们的只读列表。

之后这样调用 `cmd arg0 arg1`：

```bash
if (condVar > someVal) {
    console.log("xxx")
}
```

## 编辑 hosts 文件

3. 编辑 `/etc/hosts` 文件。输入以下命令：`vi /etc/hosts` 然后按 Enter。Listing 22.5 提供了一个 `/etc/hosts` 文件的示例。文件中的排列方式如下。

4. `/etc/hosts` 文件中的每一行都提供主机到 IP 地址的映射。多个主机（作为别名）可以对应同一个 IP 地址。按 `o` 在 `/etc/hosts` 文件中添加新行。输入接口的 IP 地址，按 `Tab` 键输入主机。

5. 在 Listing 22.5 示例中，我为地址 `130.100.50.1` 添加了 `fin.sales.catfish.com` 的条目。按 `Esc` 然后 `Shift+ZZ` 保存并退出 `/etc/hosts` 文件。

Listing 22.5 是 `/etc/hosts` 文件的样本。每个条目对应一个特定的主机。

```text
# include and entry for the loopback interface
127.0.0.1               localhost
# include entries for host machines here
# IP address         hostname            alternative names
#
130.100.10.1        www.catfish.com      web
130.100.10.10       man.catfish.com      manhost     loghost
130.100.50.1        fin.sales.catfish.com
10.100.4.2          mars.catfish.com
# corporate nameserver
10.193.10.1         dns.catfish.com     namsrv
```

## 使用 Ping 测试连接

`ping` 程序是 TCP/IP 网络中最常用的工具。`ping` 用于测试主机之间的连通性。这是通过“控制消息报协议”（简称 `ICMP`）的操作实现的。

`ping` 程序通过向远程主机发送 `ICMP ECHO REQUEST` 包来工作。当主机接收到包时，会返回一个 `ICMP ECHO_RESPONSE` 包。通过这种方式，我们使用 `ping` 工具具有两个用途：确认主机之间的端到端连通性，以及测量往返延迟或到达远程主机的速度。

1. 登录 UNIX。不需要 root 权限，任何人都可以运行 `ping` 命令。
2. 滚动到 `/etc/hosts` 文件中需要添加条目的行。你可以通过按 `j` 键或方向键来实现。在示例中，我移动到 `130.100.50.1` 条目并移动到行尾。
3. 按 `a` 在此行添加新别名。输入新主机名 `accounts`。
4. 可以指示 `ping` 向远程目标发送多少个 `ICMP` 包；在我们的示例中，我们没有指定数量，因此命令需要通过控制中断（Ctrl+C）终止。默认情况下，数据包长度为 56 字节；基础上增加了 8 字节的 `ICMP` 头。远程主机返回 `ECHO_RESPONSE` 包。对于这些包，`ping` 工具将显示递增的序列号、生存时间（`ttl`）值（每经过一个网关减 1）以及以毫秒为单位的往返延迟。
5. 也可以指定主机名而不是 IP 地址。如果这样做，`ping` 在执行连接测试前需要先解析主机。输入以下命令：`ping mars.catfish.com` 然后按 Enter。

```bash
ping 130.100.10.1 (130.100.10.1): 56 bytes data
64 bytes from 130.100.10.1: icmp_seq=0 ttl=252 time=215 ms
64 bytes from 130.100.10.1: icmp_seq=1 ttl=252 time=216 ms
64 bytes from 130.100.10.1: icmp_seq=2 ttl=252 time=217 ms
64 bytes from 130.100.10.1: icmp_seq=3 ttl=252 time=216 ms
64 bytes from 130.100.10.1:
--- ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 215/216/217
```

取决于 UNIX 版本，`aix`、`sco` 和 `linux` 的工作方式与 Listing 22.6 一。此外，其他 PC 系统的 TCP/IP 实现也是这种方式。然而，Solaris 自带的 `ping` 版本如你概述所示所示。





```
64 bytes from 130.100.10.1: icmp_seq=2. ttl=252 time=217. ms
64 bytes from 130.100.10.1: icmp_seq=3. ttl=252 time=216. ms
64 bytes from 130.100.10.1: icmp_seq=4. ttl=252 time=216. ms
^c

---PING STATISTICS-----------------------------------------------
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 215/216/217
```

## 检查域名服务是否正在运行

在前面的节中，我概述了 `/etc/hosts` 文件的操作，并指出了该文件如何提供在 IP 地址和主机名之间进行映射的便捷方法。使用 `/etc/hosts` 文件的局限性之一是你需要确保网络中的所有主机都具有相同的地址映射。随着我们网络主机数量的增加，这显然会带来一些巨大的维护问题。更重要的是，想象一下，如果我们必须在 `/etc/hosts` 文件中为我们想要访问的任何主机创建 IP 地址条目，那么互联网访问将变得多么低效！

`ping` 程序的实现在不同的 UNIX 实现之间有所不同，需要使用不同的开关设置来启用某些功能。例如，如果你在 Sun 工作站上输入 `ping mars.catfish.com`，你会期望响应显示 `mars.catfish.com` 是活跃的。如果你想获得如列表 22.6 和 22.7 所示的统计数据，你需要使用 `-s` 开关并指定数据包大小以及你想发送的 `ECHO_REQUEST` 包的数量。例如，命令 `ping -s mars.catfish.com 56 5` 将告诉 `ping` 向远程主机 `mars.catfish.com` 以五个独立的请求包发送 56 字节的数据。

显然，需要一种替代方案。这种替代方案就是域名系统，或者简单地称为 `DNS`。`DNS` 通过一组分层数据库提供主机名到 IP 地址的映射。在 `DNS` 的帮助下，可以查询单个主机（域名服务器）并定位任何网络主机。现在，域名服务器将跟踪其所属网络内的 IP 地址和主机名，但它知道如何以及向何处转发网络或网域之外的主机请求。通过这种方式，我们就可以定位并维护像互联网这样大型网络的 IP 到主机名的映射了。

所以，有两个问题：1. 我们如何知道我们的主机已配置为使用 DNS？2. 我们如何告诉我们的 TCP/IP 程序去访问此配置？嗯，所有的 TCP/IP 程序只要被提供 IP 地址或主机名，就可以正常工作。然而，如果提供的是主机名，程序首先需要将该名称解析为 IP 地址。此解析过程从检查查找本地 DNS 配置开始；如果查找失败，程序将尝试在 `/etc/hosts` 文件中查找匹配的条目；如果仍然失败，它将发布 `unknown host`（未知主机）的错误信息。

在你的 UNIX 主机上创建一个解析文件。输入 `vi /etc/resolv.conf` 然后按回车。如果 `resolv.conf` 文件不存在，在使用 `vi` 时会创建一个。按 `o` 键开始新的一行，并输入 `domain catfish.com`。然后按回车。你需要在配置文件中包含 DNS 服务器的 IP 地址。要做到这一点，输入关键字 `nameserver`，后跟一个空格和你的网络 DNS 服务器的 IP 地址。保存文件并按 `Esc` 键按 `Shift ZZ` 退出 `vi` 程序。

列表 22.8 展示了我的 `/etc/resolv.conf` 文件，它包含了两个 DNS 服务器的引用：一个主服务器和一个备用（备份）服务器。

### 列表 22.8 一个 /etc/resolv.conf 文件示例。

```
# /etc/resolv.conf
# 默认域设置
domain catfish.com
nameserver 130.100.10.10
nameserver 130.100.10.50
```




重要的是，`ping` 程序并不总是能准确地反映你是否已连接互联网。这是因为某些公司限制了允许从互联网进入的应用程序流量类型。如果你的 `ping` 程序因“主机不可达”（host unreachable）的错误信息失败，请尝试使用 Web 浏览器连接到主要的互联网网站。

如果你仍然无法访问互联网，可能是因为你需要通过代理服务获取访问权限。`proxy` 由安全的第三方代表用户提供应用程序服务。这个第三方被称为 `proxy server`（代理服务器），它通常（但并非总是）集成在互联网防火墙服务器中。使用 `proxy` 意味着单个用户无需与外部设备进行直接通信，从而增加了网络安全性。

如果你的站点正在使用代理，你需要确保你的应用程序如 `Telnet`、`FTP` 和 Web 浏览器已配置为使用代理服务。此配置涉及输入运行代理的主机 IP 地址，以及应用程序运行的端口号。图 22.2 展示了我的 Web 浏览器程序如何配置代理服务器和端口。

![8227-0578a.gif](img/e6b52eaed6cfdcb29635f1575b01c8dd.gif)
图 22.2 配置 Web 浏览器使用代理服务。

# 通过网络登录 UNIX

在建立连接后，你可以开始在网络上执行某些应用程序。下一节将检查若干应用程序的执行情况，并说明可以实现哪些功能。

## 使用 Telnet 登录

1. `Telnet` 程序为我们提供了登录并访问远程主机资源的能力。`Telnet` 程序将远程主机名或 IP 地址作为参数，并尝试打开与指定主机连接。输入以下命令，将指定的主机替换为你自己的主机名：`Telnet www.catfish.com`。然后按回车。

2. `Telnet` 程序将首先尝试解析主机 `www.catfish.com`。注意列表 22.9 中它是如何做的，然后使用 IP 地址连接到远程服务器。一旦连接成功，将显示登录提示。

```
Listing 22.9 An Telnet connection.
# telnet www.catfish.com.
Trying 130.100.10.1...
Connected to www.catfish.com.
Escape character is '^'. (www.catfish.com)
login:
```

3. 输入有效的用户名和密码登录远程主机。登录成功后，输入 `who` 查看还有哪些用户登录在此主机上。要退出，输入 `exit` 并按回车。

4. `Telnet` 程序也可以在交互模式下工作。为了演示这一点，输入 `Telnet` 并按回车。

## rlogin 比 Telnet 更优吗？

`rlogin` 程序是许多用于在 TCP/IP 网络上运行的 r-utilities（`r` 代表远程，远程）之一。该程序与 `Telnet` 程序非常相似，允许用户在远程主机上操作终端会话。然而，与 `Telnet` 不同，`rlogin` 程序不需要我们提供用户名和密码。

`r-utility` 程序引用了两个配置文件：`/etc/hosts.equiv` 以及一个可选存储在用户主目录下的名为 `.rhosts` 的文件。假设我们的网络中有两个主机，一个叫 `jupiter`，另一个叫 `mars`，它们都在 `catfish.com` 域内。

所有网络用户在每个主机上都有账户，用户名构造方式相似（两个用户名都是名字首字母加姓氏的形式，例如 `jedwards`）。通过配置 `/etc/hosts.equiv` 文件，我们可以允许用户仅需登录到本地机器并使用 `rlogin` 程序，即可访问任一机器。以下任务列表说明了如何实现这一目标：

1. 以 root 管理员身份登录 UNIX，输入 `vi /etc/hosts.equiv` 并按回车。

2. 按 `o` 然后按回车向 `/etc/hosts.equiv` 文件添加新的一行。在这一新行上，为你想要提供访问权限的主机添加条目。在我的示例中，我会输入 `jupiter.catfish.com`。保存并退出 `/etc/hosts.equiv` 文件。

3. 注销 root 用户，然后使用另一个用户账户登录到 `jupiter.catfish.com` 服务器。在 shell 提示符下，输入以下命令：`rlogin mars.catfish.com`。然后按回车。`rlogin` 命令会将登录请求转发到远程主机。服务器通过在自己的 `/etc/hosts.equiv` 中查找用户的本地主机名来检查等效性。如果找到匹配项，则允许登录并在远程主机上启动 shell 程序。

此时，我们可以通过在特定用户的主目录中创建 `.rhosts` 文件来启用类似的功能。考虑相同的主机配置。但假设我们没有配置 `/etc/hosts.equiv` 文件，却需要为其中一个用户账户提供主机之间的等效访问权限。

1. 以用户身份登录 `mars.catfish.com` 主机。使用 `vi` 程序在用户主目录下创建一个名为 `.rhosts` 的新文件。这类似于：：`vi $HOME/.rhosts`




2. 按 `o` 开始新行并添加以下条目：`jupiter.catfish.com  jedwards`。第一个条目是远程主机名；第二个是我们将赋予等效权限的主机上的登录账户名。完成后，保存文件并退出 `vi`。

3. 登出 `mars.catfish.com` 主机并使用用户名 `jedwards` 登录 `jupiter.catfish.com`。现在，在 UNIX shell 提示符下，执行命令：`rlogin mars`。然后按回车。再次，由于我们已经在主机之间创建了等效关系，你将自动登录到 `mars` 服务器，而无需提供用户名或密码。

通过这些示例，你应该能看到 `/etc/hosts.equiv` 或 `.rhosts` 的配置都可能成为一项非常强大的资产，但同时也引发了一些严重的安全问题。不诚实的用户可以对这两个文件中的任何一个进行更改，从而访问任何主机账户。以下点为限制滥用主机等效性提供了一些指南：

- 为 `/etc/hosts.equiv` 文件设置有效的权限权限。
- `/etc/hosts.equiv` 文件的权限应设置为仅允许 `root` 编辑。系统的其他用户需要读取访问，但建议不要启用该文件对所有人可读。
- 绝不要在 `/etc/hosts.equiv` 文件中包含加号 (`+`)。
- 加号本身提供对任何及所有主机的等效性，这意味着从所有网络主机都授予对任何同名账户的访问。不诚实的用户要访问远程主机账户唯一需要做的就是在他们的本地机器上创建一个同名的账户。
- 仅包含特定主机的名称，而不包含单个账户。
- 避免允许用户创建 `.rhosts` 文件。通常情况下，之前对 `/etc/hosts.equiv` 文件检查的相同安全规则也需要适用于 `.rhosts` 文件。然而，由于任何用户都可以在自己的家目录下创建 `.rhosts` 文件，要确保每个文件内部的语法将是一场管理上的噩梦。建议通过 `/etc/hosts.equiv` 文件设置任何所需的账户等效关系，不要使用 `.rhosts` 文件。在需要不同名称账户之间存在等效性时，应始终提供账户用户名和密码。

### 跨网络传输文件

`Telnet` 和 `rlogin` 命令提供了远程用户访问系统的方法，但不是一种跨网络传输文件的有效方法。这些缺陷通过文件传输协议（或简称为 FTP）的操作得以缓解。下一节将检查 FTP 的操作，并说明如何使用它在 UNIX 主机之间传输文件。FTP 既可以通过命令行操作，也可以交互式操作。让我们从交互式来看。

1. 以任意用户身份登录 UNIX，但不要登录 `root` 账户。在 shell 提示符下，输入命令 `ftp` 并按回车。
2. `ftp` 程序将进入命令模式并提供提示符 `ftp>`。输入单词 `open` 并按回车。
3. FTP 将提示你想要连接的远程主机名称。在此提示符处，我输入了主机名 `ftp.catfish.com` 来访问我的 FTP 机器。输入你网络内另一个 UNIX 系统的主机名。
4. 如果成功，远程服务器将提示你输入用户名然后是密码。在你的系统上输入这些信息。FTP 将通知你操作成功并返回到 `ftp>` 提示符。我们现在已连接到远程服务器并可以传输文件。列表 22.10 提供了这些任务的插图。

#### 列表 22.10 使用 ftp 访问远程主机

```
# ftp> open (to) ftp.catfish.com.
Connected to ftp.catfish.com. 
220 ftp server (Monday, March 30 12:12:22 EST 1998) ready.
.
Name (ftp.catfish.com. james
331 password required for james.
Password: *******
230 Guest login ok, access restrictions apply.
ftp>
```

#### 列表 22.11 使用 ftp 列出文件

`ftp` 程序允许你显示并移动远程服务器上的文件。输入命令 `ls -l` 并按回车。FTP 提供了 `ftp.catfish.com` 上的文件列表。

```
ftp> ls -l
200 Okay
Opening connection for /bin/ls
total 6
-rw-rw-r-x  1 root     1634 Apr 4 1996 cu_mor
-rw-r--r--  1 root      424 Apr 4 1996 source.c
-rw-rw--r--  1 root     3234 Apr 4 1996 fam.c
-rw-rwxr--  1 root      634 Apr 4 1996 pigsou.c
-rw-rw-r-x  1 root     1634 Apr 4 1996 cracko.4
-rw-r-xrwx  1 root      234 Apr 4 1996 sevent
226 Transfer complete.
ftp>
```

6. 让我们从 `ftp.catfish.com` 将 `source.c` 文件传输到我们的本地主机。在此之前，让我们切换到本地主机上的家目录；我们通过 `ftp` 命令 `lcd` 执行此。输入以下内容，将文件引用替换为你自己的家目录：`lcd /home/james`。





7. 要传输文件，输入 `get source.c` 并按回车。`ftp` 程序将传输该文件，并指示传输何时完成。

## 使用 FTP 传输多个文件

1. `ftp` 程序也可以一次性传输多个文件。让我们通过传输 `ftp.catfish.com` 远程目录中的所有文件来尝试一下。然而，在在此之前，我们我们需要对当前的 `FTP` 会话进行一些调整。

2. 注意列表 22.11，远程子目录中包含的一些文件实际上是可执行文件。因此，我们需要告诉 `ftp` 以 `Binary`（二进制）模式而非 `Text`（文本）模式传输这些程序。这可以通过输入单词 `binary` 并按回车来实现。

3. 此外，我们不需要一个接一个地传输文件，而是可以使用 `mget` 命令一次性传输多个文件。但是，默认情况下，`mget` 程序将在 `Interactive mode`（交互模式）下工作，对每个文件进行提示。我们可以通过关闭 `FTP Interactive mode`（FTP 交互模式）来克服这个问题。输入单词 `prompt` 即可完成。

4. 现在我们准备好从远程主机传输所有文件了。输入命令 `mget` 并按回车。`ftp` 程序将提示要获取的文件。输入 `*.*` 来传输所有文件。`FTP` 将逐个传输文件，指示每次传输何时完成，以及性能统计数据，如传输时间和系统之间复制的字节数。

5. 列表 22.12 提供了这些任务的总结。注意我还添加了 `FTP` 命令哈希值。这会导致 `FTP` 每传输 1024 字节就在屏幕上打印一个哈希标记（`#`）。这可能非常有用，特别是当需要传输大文件时。你应该注意，不同的 UNIX 版本之间哈希标记之间的字节数可能会略有不同。

列表 22.12 使用 FTP 传输多个文件。

```
ftp> binary
200 type set to I.
ftp> prompt
Interactive mode off
ftp> hash
Hash mark printing on
ftp> mget
(remote-files) *.*
local: cu_mar remote: cu_mar
200 Okay
```

```
150 Opening connection for XXX (bytes). 226 Transfer complete.
local: source.c remote: source.c
200 Okay
150 Opening connection for XXX (bytes). ####
226 Transfer complete. 4560 bytes received in 0.0467 secs (9.5e+02 K/sec)
local: frames.c remote: frames.c
200 Okay
150 Opening connection for XXX (bytes). ################################
226 Transfer complete. 11595 bytes received in 0.347 secs (3.3e+02 K/sec)
local: pigsou.c remote: pigsou.c
200 Okay
150 Opening connection for XXX (bytes). #################################################
226 Transfer complete. 1570 bytes sent in 0.01432 secs (1.9e+02 K/sec)
local: cracko.4 remote: cracko.4
200 Okay
150 Opening connection for XXX (bytes). #
226 Transfer complete. 240 bytes sent in 0.00299 secs (1.9e+02 K/sec)
```

注意：可以在 `ftp` 提示符处按问号（`?`）键显示所有可用的 `FTP` 命令。此外，请记住在设置 `prompt`、`hash`、`binary` 等命令时，这些都是切换命令，可以通过再次输入该命令来重置。

`ftp` 工具可将文件从本地主机传输到远程主机。其实现方法与之前类似。然而，不要使用 `get` 和 `mget`，而是使用 `put` 和 `mput`。

## 使用 rcp 传输文件

就像 `rlogin` 为我们提供了使用 `Telnet` 的替代方案一样，另一个 `r-utilities` 也为我们提供了使用 `FTP` 传输文件的替代方案。使用 `rcp` 需要在用户主目录下配置 `.rhosts` 文件。以下示例将在阐述该工具的操作之前，引导我们完成必要的置的 `.rhosts` 配置。

1. 使用普通账户登录远程主机，而不是使用 root 用户。输入以下命令在账户主目录下创建一个新的 `.rhosts` 文件：`vi $HOME/.rhosts`。然后按回车。

2. 按 `o` 在此文件中开启新行，并输入你的本地主机名称以及你想授予访问权限的主机账户名。例如，我的本地主机是 `jupiter.catfish.com`，在该主机上的账户名是 `jedwards`。因此，我在远程主机的 `.rhosts` 文件中了如下条目：`jupiter.catfish.com jedwards`。

3. 保存 `.rhosts` 文件，退出 `vi` 并注销远程主机。现在你准备好执行任何 `r-utilities` 了。




4. 登录到你的本地主机（你在第 2 步中添加条目的那个主机）。输入以下命令创建一个用于测试 `rcp` 实用的新文件：`touch testfile`。然后按回车。输入以下命令运行 `rcp` 实用，将该文件的副本放在远程服务器 `mars.catfish.com` 的主目录下：

```
rcp testfile mars.catfish.com/home/jedwards/testfile
```

5. 传输完成后，登录远程主机并检查文件是否已复制。执行此操作，输入 `rlogin mars.catfish.com`，然后输入 `ls -l$HOME/testfile`。

6. 使用 `rcp` 程序传输文件相比 `ftp` 程序的的一个优势是，它能够对整个目录结构进行递归拷贝。以下命令提供了这方面的示例：

```bash
rsh -r catfish.com:/usr/lib/source /backup/source
```

该命令将子目录 `/usr/lib/source` 及其所有的底层子目录和文件复制到本地子目录 `/backup/source`。使用 `FTP` 实现类似功能的唯一方法是使用 `tar` 将 `/usr/lib/source` 下的所有文件打包，然后传输该文件。显然，`rcp` 为我们提供了更大的灵活性。

# 在网络中的另一个系统上执行命令

`rsh` 程序（有时读作 *rush* 或 *r-s-h*）提供了一种无需先登录即可在远程主机上执行命令的方法。正如程序名称所示，它是 r 系列工具的另一种。因此，在使用该命令之前，需要应用在本章之前介绍过的 `/etc/hosts.equiv` 和 `.rhosts` 配置。

1. 在远程主机的 `.rhosts` 文件中为你的本地 UNIX 主机创建一个条目。在我的情况下，我会通过登录主机 `mars.catfish.com`（我的远程主机）并输入 `vi $HOME/.rhosts`，然后在保存并退出文件之前添加条目 `jupiter.catfish.com`。

2. 注销远程主机并登录本地主机。输入以下命令 `rsh mars.catfish.com /bin/ls` 来执行 `rsh` 命令以便在远程主机上运行 `/bin/ls` 程序。然后按回车。

3. `rsh` 命令将生成远程主机 `$HOME` 目录的文件列表。尝试在远程主机上执行一些可执行文件。以下是一些示例。

4. 输入命令 `rsh mars.catfish.com /bin/sh` 在远程主机上启动一个 UNIX shell。

5. 命令 `rsh mars.catfish.com who` 会显示当前登录到远程主机的用户。

6. 执行 `rsh` 命令时不指定要在远程主机上执行的命令，结果将是用户登录到远程主机，这与我们使用 `rlogin` 命令的结果相同。要尝试这样做，请输入命令 `rsh mars.catfish.com`。

## 结语

本章概述的任务使你能够让主机接入网络。这将为你运行所有常用的网络应用程序和访问远程系统提供基础。

值得注意的是，由于市面上有近 30 种不同的 UNIX 版本，程序操作和语法的一些差异将显而易见。我尝试采用了一种涵盖大多数主流 UNIX 版本方法的方法；如既常，最好参考你系统的帮助页（man pages），以获取本章涵盖的命令和程序的特定版本选项。

# 第 23 章从 Windows 访问 UNIX

作者：James Edwards

## Windows 与 TCP/IP

### 拨号网络

大多数用户在 PC 上运行 Windows 系列操作系统之一。这些用户可能需要与他们网络内部或互联网等公共网络中的 UNIX 主机进行通信。在本章中，我们将介绍为 Windows 95 用户提供访问 UNIX 方法。

### 即插即用

Windows 操作系统以其即插即用功能为傲。这意味着什么？嗯，当 PC 上添加调制解调器等新设备时，Windows 会自动尝试识别并配置它。如果需要任何额外的配置信息，Windows 会自动启动一个简单的程序，引导并提示用户提供完成配置所需的信息。

总的来说，操作系统非常出色地完成了这些任务，特别是与任何版本的 UNIX 相比！但是，有很多“陷阱”是你应该注意，本章将识别其中的一些问题。

### TCP/IP

TCP/IP 协议是网络领域事实上的标准。Windows 为这些协议提供了原生支持，并带有名为*向导*（wizard）的简单程序，引导用户完成必要的安装和配置过程。



为了在 Windows 下局域网连接启用有效的 TCP/IP 网络支持，需要配置三个独立的组件：Microsoft 网络客户端、网络接口卡（NIC）适配器以及 TCP/IP 协议。所有这些配置步骤都依赖 Windows 控制面板中的“网络”图标；以下任务将引导您完成在 Windows 中启用 TCP/IP 网络所需的步骤。

### 启用 TCP/IP 网络

1. **打开控制面板。** 这可以通过点击任务栏上的开始按钮来实现。然后高亮 `Settings` 并点击 `Control Panel` 。控制面板打开后，双击网络图标。

2. **在网络窗口中，点击`Configuration` 标签。** 检查窗口下方“已安装以下网络组件”字样下显示的组件列表。要连接到网络，您必须确保存在三个项目：`Client for Microsoft Networks`、`NIC Adapter` 和 `TCP/IP Network Adapter`。

3. **如果配置中不存在其中任何项目**，可以通过先点击 `Add` 按钮来添加它们。您将看到四个选项：添加客户端、协议、适配器或服务。让我们先逐步添加网络客户端。

### 将协议与适配器关联

当安装了多个网络适配器时，Windows 95 使用箭头将网络协议与特定的网络适配器相关联。如果只配置了一个网络适配器，Windows 则不提供这种关联，而是直接在网络窗口中列出协议名称。

4. 在 `Component Type` 框中选择 `Client`，然后点击 `Add` 按钮。选择 `Microsoft` 为制造商，并在网络窗口下选择 `Client for Networking` 选项。点击 `OK` 确认此选择。

5. **以类似的方式添加`NIC Adapter`：** 点击 `Add` 按钮，选择 `Adapter` 选项，再次点击 `Add` 按钮。高亮您安装的 `NIC` 的制造商；如果没有显示确切的 `NIC`，请点击 `Have Disk` 并按照指示从软盘加载 `NIC` 厂商的驱动程序。点击 `Add` 按钮然后点击 `OK` 按钮确认。

6. **接下来，让 Windows 加载`TCP/IP` 协议**，并配置其在已安装的 `NIC` 上使用。点击 `Add` 按钮，这次选择 `Protocol`。点击 `Add` 按钮，并在可用列表中选择 `Microsoft`。指定 `TCP/IP` 为要添加的网络协议，并通过点击 `OK` 按钮完成操作。

7. **在此阶段，我们已经加载了所有网络组件**，但尚未配置其中任何一个。首先，配置 `NIC`。在“已安装以下网络组件”下的选项窗口中，点击一次您的 `NIC Adapter` 项目。

8. **点击`Properties` 按钮然后点击 Driver type。** 选择 `Enhanced Mode (32 bit and 16 bit)` NDIS 驱动程序选项。点击 `Bindings` 标签，并勾选 `TCP/IP NIC Adapter` （其中 `NIC` 将反映您的 NIC 制造商）。点击 `OK` 按钮完成此配置。

9. **现在配置`TCP/IP` 协议。** 在“已安装以下网络组件”窗口标题栏下，点击一次 `TCP/IP NIC Adapter`，然后点击 `Properties` 按钮。

10. **点击`IP address` 标签。** 如果您已被分配 IP 地址，点击一次 `Specify an IP Address` 选项，然后输入您的 IP 地址和相应的子网掩码。如果您将通过 `DHCP` 服务器分配 IP 地址，请勾选 `Obtain an IP Address Automatically` 选项。

11. **点击`Bindings` 标签**，并勾选 `Microsoft Client` 选项框。点击 `OK` 按钮保存此更改。

12. **所有剩余设置完全是可选的。** 然而，另一个重要选项是 `DNS` 的配置。如果您计划使用 `DNS`（例如为了能够连接互联网），请点击一次 `Enable DNS` 选项按钮。在提供的配置框中，添加您想要作为 PC 名称的主机名以及它的域名（例如 `host` 和 `domain.com`）。

13. **您还必须在`DNS Server Search Order` 下添加 DNS 服务器的 IP 地址**。点击 `Add` 按钮添加 DNS 引用，然后点击 `OK` 按钮保存这些设置。

### 使用 Ping 测试连接




`ping` 工具作为标准 Windows 操作系统的一部分自带的，它是确认我们的 PC 配置和排除网络连接故障的极佳工具。遗憾的是，Windows 自带的 `ping` 版本是一个 DOS 程序，因此必须在 Windows DOS 框中运行。以下任务说明了我们如何使用此命令。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

## 使用 hosts 文件代替 DNS

Windows 支持使用 hosts 文件作为 DNS 的替代方案。该文件位于 Windows 子目录中，其语法与 UNIX 主机上使用的格式完全相同，将单个 IP 地址映射到指定的主机名。如果您无法访问 DNS 服务器，且不想使用 IP 地址引用您的 hosts，`\Windows\hosts` 文件提供了一个非常有用的替代方案。

## 使用 Ping 工具

1. 调出 Windows 任务栏并点击一次“开始”按钮。将光标移动到“运行”选项并点击一次。出现“运行”对话框。在打开提示符处输入以下命令行：`ping 130.100.10.2`（将我的 IP 地址替换为您在自己的接口配置中使用的 IP 地址）。

2. `ping` 程序执行，但由于它是一个 DOS 程序，它会首先打开一个 DOS 窗口。`ping` 向指定的接口发送请求包，要求其立即响应。如果您正确配置了 PC，您应该看到与图 23.2 所示类似的响应。

![8227-0594a.gif](img/8600cea9e4075f1862eae7eef0ec07ec.gif)
图 23.2 探测本地接口以检查连接性。

3. 如果您配置了 `\Windows\hosts` 文件或可以访问 DNS 服务器，可以使用主机名代替 IP 地址。要进行测试，请激活 DOS 框并输入 `ping hostname`（将 `hostname` 替换为您的远程主机名）。

## 查看本地 TCP/IP 设置

Windows 提供了一个允许我们查看当前网络配置详细信息的实用工具。该工具称为 `winipcfg.exe`，位于 `Windows` 子目录中。让我们通过此工具查看某些功能。

### 探测 IP 地址

需要记住，如果您使用主机名，`ping` 程序必须在测试主机连接性之前解析该主机名。如果由于某种原因您指定的名称无法解析，`ping` 将无法报告该主机是否可达。因此，在使用 `ping` 时，指定 hosts IP 地址比指定其主机名更佳。

### winipcfg 工具

1. 调出任务栏并点击一次“开始”按钮，然后点击“运行”菜单选项。这将弹出一个对话框；输入 `\Windows\winipcfg` 作为您想要打开的程序，并按回车键。

2. `winipcfg` 程序启动并显示一个与图 23.3 所示类似的窗口。如图 23.3 所示，`winipcfg` 程序显示了可以帮助排除故障的有用信息。

![8227-0595a.gif](img/48382e7409821e608b1c5.gif)
图 23.3 使用 winipcfg 显示的 TCP/IP 信息。

3. 如果您已为 PC 配置拨号上网网络，点击箭头激活下拉列表并选择 PPP 适配器。`winipcfg` 显示该接口的配置。

4. 点击“更多”按钮；`winipcfg` 将展开并包含许多与您的连接相关的额外信息。图 23.4  PPP 适配器配置的插图。

![8227-0595b.gif](img/57660943c71417818c6f3a39cb617ef.gif)
图 23.4 使用 winipcfg 显示 TCP/IP 详情。

## 使用 ftp 与 UNIX 传输文件

Windows 提供了用于文件传输的 ftp 程序标准实现。与 Windows 版本的 ping 和 telnet 程序一样，ftp 仅作为 DOS 程序提供。然而，它仍然是 Windows 和 UNIX 主机之间传输文件的实用且有效的方法。





## 使用 winipcfg 进行故障排除

如果你的 IP 地址是通过 DHCP 自动分配的，那么使用 `winipcfg` 将证明特别有用。一旦你知道了 IP 地址，就可以更有效地进行故障排除。此外，请注意 `winipcfg` 显示上的两个额外按钮：`Release All`（全部释放）和 `Renew All`（全部更新）。如果接口确实通过 DHCP 获取了 IP 地址，这些按钮将为你提供释放或更新你正在使用的 IP 地址的方法。

## 使用 ftp 传输文件

1. 为了使用 `ftp` 从远程主机传输文件，你必须确保该主机能够接受你的 `ftp` 请求。为了做到，主机必须运行 `ftp` 服务端进程。要确认这一点，请登录到远程主机并输入以下命令：
```bash
cat inetd.conf | grep ftp
```
如果服务器可以处理入站 `ftp` 客户端请求，将显示类似下面的响应：

列表 23.1 检查远程 UNIX 主机上是否运行了 `ftp` 服务器。

```bash
cat /etc/inetd.conf | grep ftp ftp      stream  tcp      nowait  root    /usr/sbin/tcpd
       /usr/sbin/wu.ftpd
```

2. 要激活 `ftp` 程序，将光标移动到任务栏并点击 `Start` 按钮。点击一次 `Run` 菜单，会出现一个对话框，要求你想要执行的程序名称。输入 `ftp` 并按 `Enter`。

3. 出现一个 DOS 窗口，以及 `ftp` 命令提示符 `ftp>`。

4. 输入 `?` 以显示可用命令列表。你必须先与远程主机建立连接。在下面的示例中，我连接到名为 `ftp.catfish.com` 的服务器。输入以下命令，将指示的主机名替换为你的远程服务器名称：`open ftp.catfish.com` 然后按 `Enter`。

5. 如果成功，远程服务器将提示你输入用户名然后是密码。输入这些信息；`ftp` 会在你成功时通知你并返回 `ftp>` 提示符。你现在已连接到远程服务器并能够传输文件。图 23.5 释了这些任务。
![8227-0597a.gif](img/297a8fb7d35278a8893248a45611e42.gif) 图 23.5 使用 ftp 远程 UNIX 主机

6. `ftp` 程序允许你显示远程文件并在远程服务器上包含的文件系统之间移动。输入命令 `dir` 然后按 `Enter`。`ftp` 会显示远程主机当前目录的列表。

7. 要从远程主机传输文件到你的 Windows PC，输入命令 `get filename`（其中 `filename` 是远程主机上的文件名），然后按 `Enter`。`ftp` 程序将传输文件并指示传输何时完成。

8. 同样，你可以从你的 Windows PC 传输文件到远程 UNIX 主机。要做到这一点，输入 `put filename`（其中 `filename` 是要传输的文件名）。这次，当 `ftp` 报告传输完成时，输入 `dir` 并按 `Enter`。生成的目录列表现在也应该包含你刚传输的文件。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) Windows 与 ftp

Windows 版本的 `ftp` 与第 22 章所示的 UNIX 版本相同。第 22 章中概述的额外特性和功能也可以适用于 Windows 版本。

## 关于网络

如果你想登录到跨 TCP/IP 的任何主机，你必须使用 `telnet`。该程序作为 Windows 系统的一部分提供，为 TCP/IP 网络提供终端设施。

## 使用 Telnet 登录 UNIX

1. 要启动 `telnet`，点击 `Start` 按钮并选择 `Run` 选项。在 `Run` 对话框中输入 `telnet` 并点击 `OK` 按钮启动程序。

2. 要连接到远程主机，点击 `Connect` 选项，然后点击 `Remote System` 选项。

3 显示一个 Connect 选项框。输入你的远程 UNIX 主机的主机名或 IP 地址。记住，如果你输入主机名，你必须配置了 DNS，或者在你的 `\Windows\hosts` 文件中有该主机的条目。图 23.6 提供了插图。
![8227-0598a.gif](img/8609a5fdd9d99b80ccd3d10bc642cda2.gif) 图 23.6 登录主机





## 图 23.6 使用 telnet 跨 TCP/IP 连接登录。

4. 点击“连接”（Connect）按钮激活连接。应显示远程主机的登录界面，供您提供用户名和密码。
5. 要断开主机连接，请点击“连接”（Connect）菜单项并选择“断开”（Disconnect）选项。

## 拨号上网

Windows 为您提供了两种通过拨号连接访问 UNIX 主机的选项。一种方案是配置您的 Windows PC，使其能够通过调制调器连接运行 TCP/IP 协议。此选项允许您运行本章在此之前概述的任何基于 TCP/IP 的应用程序，并且通常是为 PC 连接互联网时选择的路径。

另一种方法是配置 Windows 以允许用户具备登录远程主机的能力。此选项允许您访问远程主机上的文件和资源；但该选项的局限性在于，它一次只能访问单个远程主机。接下来的章节将介绍这两种方法。

### 通过互联网访问 UNIX 主机

要通过互联网访问主机，您必须完成四项任务：安装并配置调制解调器、配置调制解调器的物理端口、配置网络设备和协议，以及配置连接脚本，该脚本将拨打您的互联网服务提供商电话并在您配置的设备上启动通信。

以下任务列表提供了该过程的简要指南，从安装和配置调制解调器开始。

#### 通过互联网访问 UNIX 主机

1. 点击任务栏上的“开始”按钮。将光标移动到“设置”（Settings）菜单选项，然后右键点击“控制面板”（Control Panel）选项。当控制面板文件夹打开时，双击“调制解调器”（Modems）图标。如果您已经安装了调制解调器，会弹出“调制解调器属性”对话框。如果是这种情况，请在继续之前右键点击“添加”（Add）按钮。
2. 打开“安装新调制解调器”（Install a New Modem）窗口。点击“下一步”（Next）按钮运行安装向导，Windows 将引导您完成安装过程。点击“下一步”继续此过程。
3. 系统将您是否让 Windows 搜索新安装的硬件；选择“否”（NO）选项并点击“下一步”。从显示的设备类型列表中选择“调制解调器”（Modem）并点击“下一步”。
4. 勾选“不要搜索我的调制解调器，我将从列表中选择”（Dont My Modem, I Will Select It from a List）选项并点击“下一步”按钮。打开一个新窗口；在提供的选项下选择您的调制解调器制造商和型号。
5. 点击“下一步”按钮继续安装，并选择调制解调器将使用的 COM 端口。Windows 尝试安装您的调制解调器——在完成过程中，屏幕可能会空白几秒。完成后，将显示一个窗口报告安装过程成功；点击“完成”（Finish）按钮退出安装向导。
6. 按“完成”按钮将调出“调制解调器属性”（Modem Properties）窗口。为了有效完成安装过程，您必须定义 Windows 如何使用该调制解调器；这通过点击窗口内的“拨号属性”（Dialing Properties）按钮来实现。
7. “拨号属性”（Dialing Properties）屏幕会提示您输入本地拨号区码，以及在拨打任何位置之前是否需要拨打特殊号码。如果您的调制解调器线路通过电话交换机（PBX）连接并需要拨打 `9` 才能访问外部电话线路，可能会出现这种情况。根据您自己的环境对“拨号属性”屏幕进行任何更改。8 点击“确定”（OK）按钮保存并退出“拨号属性”屏幕，再次退出“调制解调器属性”屏幕。

下一步是确保您的 COM 端口设置与您在安装期间为调制解调器配置的设置相对应。这通过访问再次位于控制面板内的“系统”（System）图标来实现。以下任务总结了我们需要做的设置。

#### 配置端口设置

1. 要打开控制面板，点击任务栏上的“开始”按钮。将光标移动到“设置”（Settings）菜单选项，然后右键点击“控制面板”（Control Panel）选项。打开控制面板文件夹；双击“系统”（System）图标。
2. “系统属性”（System Properties）窗口打开；点击“设备管理器”（Device Manager）选项卡，然后双击您连接调制解调器的 COM 端口。点击“端口设置”（Port Settings）选项卡调整显示的值，使其与您为调制解调器配置的值相对应。
3. 点击“确定”保存设置并返回“系统属性”窗口，然后点击“确定”关闭此窗口并返回控制面板文件夹。

在安装好调制解调器和通信端口后，您必须设置并配置 TCP/IP 协议以便能够通过这些设备进行通信。这通过完成以下步骤来实现。

#### 配置 TCP/IP 协议





1. 点击开始按钮，然后选择`Settings`（设置），最后选择`Control Panel`（控制面板）。双击`Network`（网络）图标。

2. 点击`Configuration`（配置）选项卡并检查当前已配置的组件列表。为了配置拨号网络，必须存在以下两个项目：`Dial-up Adapter`和`TCP/IP Dial-up Adapter`。如果缺少其中任何一项，则必须添加。如果你需要添加项目，请点击`Add`按钮。你将看到四种可以添加的选项：客户端、协议、适配器和服务。

如果你需要添加拨号适配器，请点击`adapter`选项并点击`Add`按钮。在`Network Protocols`窗口中，选择`Microsoft`作为制造商，并选择`Dial-up Adapter`。点击`OK`按钮确认操作。

如果你需要添加`TCP/IP`协议的`Dial-up Adapter`选项，请点击`Add`按钮，点击`protocol`选项，然后再次点击`Add`按钮。在网络协议窗口中选择`Microsoft`作为制造商，并选择`TCP/IP`作为网络协议。点击`OK`按钮完成操作。

3. 现在进行 TCP/IP 协议配置：在`The Following Network Components Are Installed`窗口中，点击`Dial-up Adapter`。点击`Properties`按钮，然后点击`Driver Type`选项并选择`Enhanced Mode (32 bit and 16 bit) NDIS Driver`。点击`Bindings`选项卡，然后勾选`TCP/IP Dial-up Adapter`。点击`OK`按钮完成此操作。

4. 在`The Following Network Components Are Installed`窗口中，点击`TCP/IP Dial-up Adapter`，然后点击`Properties`按钮。此屏幕提供了配置 TCP/IP 协议参数的地方。图 23.7 提供示例。

![8227-0602a.gif](img/4cf935ab5ed2a5933b816c603022f84c.gif)
图 23.7 配置 TCP/IP 参数。

5. 需要配置的关键项是 Windows 电脑的 IP 地址。要执行此操作，点击`IP Address`选项卡。如果你已经被分配了使用的 IP 地址，点击`Specify an IP Address`按钮，然后输入你的 IP 地址和子网掩码。如果你还没有分配 IP 地址，点击`Obtain an IP Address Automatically`选项。

6. 如果你的电脑能够使用 DNS，点击`DNS Configuration`选项卡。接下来，勾选`Enable DNS`按钮，以及你的电脑的主机名和域名。然后在在`DNS Search Order`窗口中添加 DNS 服务器的 IP 地址并点击`Add`按钮。

7. 最后，点击`OK`按钮保存配置并退出。你的调制解调器已配置，设备端口和协议也已设置。现在你必须指示 Windows 如何建立连接；这是通过`Dial-up Networking`选项实现的。以下任务说明了必要的配置步骤。

### 配置拨号网络

1. 双击`My Computer`图标、`Dial-Up Networking`文件夹和`Make New Connection`图标。这会启动一个向导程序，引导你设置新的拨号网络会话。

2. 输入一个描述该会话名称，并选择向导应使用的调制解调器。点击`Next`按钮继续。

3. 输入你要拨打的服务器电话号码，根据需要包含国家代码和区号代码。点击`Next`按钮，向导会通知你会话配置已完成。点击`Finish`按钮保存并退出。

4. 你的会话保存在`Dial-up Networking`文件夹中。选择此图标并右键点击，然后选择`Properties`选项，然后选择`Server Type`按钮。显示如图 23.8 所示。

5. 此对话框允许我们指定哪些协议可以在建立的连接上运行。点击`TCP/IP Settings`按钮并输入 TCP/IP 配置。此特定连接的这些信息将覆盖控制面板中指定的值。这允许你为你可能建立的任何特定连接配置不同的 TCP/IP。

![8227-0604a.gif](img/320c23723a6af825d40eed859d883.gif)
图 23.8 为拨号网络指定服务器类型。

6. 要激活此会话，双击 Dial-up Networking 中的 Session 图标。会出现一个对话框，提示输入你的用户名和密码以及要拨打的电话号码。输入你的用户名和密码并点击`Connect`按钮。

7. Windows 将拨打指定的电话号码，并尝试使用你的用户名和密码进行连接。建立连接后，你可以使用任何 TCP/IP 程序通过此连接访问远程服务器。

*通过终端连接访问 UNIX 主机*





# 第 21 章通过调制调器访问其他 UNIX 系统

本文说明了 UNIX 主机如何通过使用调制调器和拨号线路提供远程登录支持。Windows 通过其 `HyperTerminal` 程序提供了类似相当的功能。该程序允许配置 PC，使其能够与远程主机建立终端连接。

## 配置 HyperTerminal 访问 UNIX 主机

1. 要使用 `HyperTerminal` 配置连接，请点击“开始”按钮并将光标移动到“程序”菜单选项。Windows 将显示你 PC 上可用的程序组。选择“附件”，然后选择 `HyperTerminal`。
2. 在 `HyperTerminal` 文件夹中，双击名为 `Hypertrm.exe` 的程序。这会启动 `HyperTerminal` 配置程序，它将引导你完成其余的必要配置步骤。
3. 为新连接输入名称，并从可用列表中为该连接选择一个图标。点击“确定”继续。
4. `HyperTerminal` 会提示你想要连接的远程主机的电话号码。要完成此信息，请通过下拉框添加国家和区号信息。`HyperTerminal` 将帮助你完成这些步骤。
5. 点击“连接方式”窗口末尾的箭头，选择你希望 `HyperTerminal` 使用的调制调器。完成输入这些信息后，点击“确定”按钮继续。
6. `HyperTerminal` 在“连接”对话框中显示你要拨打的号码，以及你拨号的所在地。图 23.9 展示了此示例。
7. 如果你必须更改配置的远程主机电话号码，可以通过点击“修改”按钮来实现。此操作将显示连接的“属性”窗口（参见图 23.10）。
8. 点击“电话号码”选项卡允许你更改远程主机的电话号码，包括国家和区号。该选项卡还允许你通过点击“配置”按钮更改连接调制调器的配置。
9. 点击“设置”选项卡。此屏幕上的可用选项允许你更改终端会话的外观感觉。只要你确保 `仿真` 设置为 `自动检测`，就不需要对这些设置进行任何更改。点击“确定”按钮返回“连接”对话框。

10. 点击“拨号属性”按钮，告诉 `HyperTerminal` 你从哪个位置拨号。如果你经常旅行并需要从不同的位置访问远程主机，此选项特别有用。点击“确定”按钮返回“连接”对话框。
11. 对你的连接设置满意后，点击“拨号”按钮建立远程连接。连接建立后，远程 UNIX 主机将向你显示登录屏幕，在其中输入你的用户名和密码。

## 在远程主机之间传输文件

HyperTerminal 提供了一种简单有效的方法，用于与远程主机之间传输文件。要实现这一点，主机必须采用如 Kermit 等通信服务器软件通过拨号连接下载文件的方法。以下步骤说明了 `HyperTerminal` 用户如何使用该软件传输文件。

### 使用 HyperTerminal 文件

1. 按照之前描述使用 `HyperTerminal` 连接到远程 UNIX 主机，并使用有效的用户名和密码登录。
2. 在远程主机上，输入 `kermit` 启动 `kermit` 文件传输程序。输入 `set file type binary` 并按回车告知远程主机你要从 PC 上传二进制文件，然后输入 `receive` 将主机置于接收你文件的正确模式。按 `Alt+X` 退出回到 `HyperTerminal` 程序。
3. 点击 `HyperTerminal` 程序中的“传输”菜单选项，然后点击“发送文件”选项。弹出的对话框中你可以输入要传输的文件名，或点击“浏览”按钮找到该文件。选择文件后，点击“发送”按钮开始传输。
4. `HyperTerminal` 也可从远程系统接收文件。这可以通过选择“传输”菜单下的“接收文件”选项来设置。使用“浏览”按钮指定传输文件的放置位置，然后使用远程主机上的传输程序将文件发送到你的 `HyperTerminal` 会话。

![图 23.10 更改 HyperTerminal 连接的拨号属性。](img/ed36847-0606b.gif)

## 在 Windows 上通过 Netscape 读取和发送 UNIX 电子邮件




Netscape Communicator 应用程序套件主要是一个浏览器浏览器；然而，它也提供了电子邮件功能。Netscape 应用程序的运行需要 Windows PC 通过 `TCP/IP` 连接到互联网。这可以通过通过 `NIC` 或 `modem`（调制调器）建立的网络连接来实现。

## 配置 Netscape Communicator 用于电子邮件

1.  点击 `Start` 按钮，选择 `Programs` ，滚动到 Netscape 文件夹，然后点击 `Netscape Navigator` 图标来启动 Netscape Navigator。或者，如果你已经创建了该应用程序的快捷方式，只需双击快捷方式图标即可启动。

2.  在 Netscape 选项栏上选择 `Window`，然后选择 `Netscape Mail`。Netscape 会显示电子邮件客户端并提示输入 `user id` 和密码以访问你的远程电子邮件账户。连接后，电子邮件窗口看起来应该与图 23.11 类似。

3.  新邮件会自动放置在你的 `Inbox`（收件箱）文件夹中。点击窗口右上角的 `Inbox` 文件夹；Netscape 会指示未读消息。

4.  `Inbox` 中每条消息的摘要行会显示在该窗口的右侧。你可以通过点击其中任何一条消息来打开它，消息将出现在 Netscape 电子邮件客户端底部的窗口中。

![8227-0609a.gif](img/bd3f7aca161491b0eacc7050610452c2.gif)
图 23.11 Netscape 电子邮件客户端。

5.  将鼠标箭头移动到这三个窗口之间的任何一个分隔符上，移动时你会发现光标形状发生了变化。按住鼠标键并移动鼠标，各个窗口的大小就会改变。

6.  要发送消息，点击 `File`，然后点击 `New Mail Message` 菜单选项。或者，使用快捷键 `Ctrl+M`。

7.  出现 `Message Composition`（消息撰写）框；输入收件人的电子邮件地址，或者点击 `Mail To` 按钮显示通讯录。图 23.12 插图。

![8227-0609b.gif](img/4da739b518ec0c8c74601f4d0eb1.gif)
图 23.12 使用 Netscape Navigator 创建新的电子邮件消息。

8.  点击 `Attachment` 按钮向你的电子邮件添加附件。点击 `Attach File` 按钮以找到文件，点击 `Open` 按钮选中高亮文件，然后点击 `OK` 继续。

9.  点击 `Send` 按钮。如果你没有在主题行中输入任何内容，Netscape 会再次提示你输入邮件主题。如果需要，请输入主题然后按 `OK` 继续。

# 第 24 章 UNIX 与互联网
作者：Gordon Marler

### 在 UNIX 上冲浪网 
### 从互联网下载软件
### 使用基于字符的浏览器 (Lynx)
### UNIX 厂商网站
### 访问 UNIX 技术支持
### 访问免费（非支持的）软件
### 阅读网络

部分首批能够访问万维网（World Web）的机器中运行着 `Mosaic`，这是一个由伊利诺伊大学国家超级计算机应用中心（`NCSA`）开发的 X-Windows 应用程序。它运行在多个版本的 `UNIX` 上，今天仍然可用，尽管它不具备最新一代的一些更优功能。

后来出现了诸如 `Netscape Navigator/Communicator`、`Sun HotJava` 和 `Lynx` 等浏览器。如果你的 `UNIX` 版本没有 X-Windows，或者你没有运行它的适当硬件，你仍然可以运行 `Lynx`，因为它只需要一个哑终端。

表 24.1 运行在 UNIX 上的浏览器及其获取位置。

| 浏览器 | 位置 |
| :--- | :--- |
| Netscape Navigator/Communicator | `http://home.netscape.com/` |
| NCSA Mosaic | `ftp://ftp.ncsa.uiuc.edu/Mosaic/binaries/2.6/` |
| Lynx | `ftp://www.slcc.edu/pub/lynx/release2-8/` |
| Sun HotJava | `http://www.javasoft.com/products/hotjava/` |

表 24.1 中提到的位置可能是你熟悉的格式，因为今天许多公司在广告中放置了统一资源定位符（`URLs`）；这些看起来像这样：`http://www.somecompany.com/`。这些 URL 的 `http` 部分告诉你的 Web 浏览器在与 `http://` 之后指定的 Web 服务器通信时使用哪种协议。

为了帮助你熟悉这些协议以及何时可能想要使用它们，表 24.2 列出并描述了许多常用的协议。





## 表 24.2 URL 协议标识符及其用途。

| 协议 | 目的 |
| :--- | :--- |
| `http://` | 用于指定网页 |
| `https://` | 用于指定安全网页，该网页在发送到你时会进行加密 |
| `ftp://` | 指定使用文件传输协议来上传/下载文件 |
| `news://` | 指定将用作网络新闻 (Usenet) 服务器的主机 |
| `file:/<pathname>` | 允许你将本地文件加载到浏览器中（注意此协议中冒号后只有*一个*斜杠） |
| `gopher://` | 指定提供 Gopher 服务的主机 |

请记住，互联网上的许多 Web 服务器可以针对其网站的不同部分提供表 24.2 中列出的一项、多项或全部服务。许多服务器至少提供前三项服务。通常，如果你想找某公司的网站，可以假设其 URL 会非常接近 `http://www.*companyname.*com`，除非另一家名称相似的公司已经使用了该地址。

### 寻找正确的网站

如果你正在尝试猜测某公司的网站地址，结果却进入了其他公司的网站，你通常会发现一个指向你真正想去的地方的链接。这是一个例子：

你想访问 PC 卡制造商 Diamond Multimedia 的首页。你尝试了 `http://www.diamond.com`，但发现这是 SI Technology, Inc. 的网站。但是！这里有一个指向 Diamond Multimedia 网站的链接：`http://www.diamond.com`。

你会很快发现万维网并不是中心化组织的，信息分布在巨大的区域内。如果你在寻找特定的内容，你要么得知道它在哪里，要么需要帮助来寻找。`search engines`可以为你提供帮助。这些引擎通常是大型 UNIX 服务器，会发送 `spiders`（蜘蛛）或 `robots`（机器人）。它们会寻找、检查并索引它们能找到的每个 Web 服务器上的每一个网页。我在表 24.3 中列出了目前可用的几个引擎。你可以查看它们并选择一个最适合你的。每个引擎都有其自己的方法，让你在其各自的目录中指定想要搜索的内容。某些服务的目录比其他更好，但这会随着时间的推移而变化。每个引擎都有方便的帮助功能，可以帮助你进行基础搜索。高级搜索功能每种服务器类型大约需要一页来解释。

### 表 24.3 几个 Web 搜索引擎。

| | |
| :--- | :--- |
| AltaVista | `http://www.altavista.digital.com/` |
| Yahoo! | `http://www.yahoo.com/` |
| Lycos | `http://www.lycos.com/` |

取决于你的 UNIX 机器所在的位置，你的机器和互联网之间可能存在一个 `firewall`（防火墙）。如果你在公司访问互联网，且你的公司具有任何规模，那么情况很可能是这样。如果你在家里通过互联网服务供应商访问互联网，你可能不需要担心这个问题。

### 自动代理

在某些站点，系统管理员不会给你你的代理服务器的名称，而是会给你一个指向自动代理文件的 URL，你必须将该 URL 输入到浏览器中。该文件包含一个脚本，每当你启动浏览器时都会自动加载，并对你的浏览器进行编程，智能智能地选择代理服务器。这种功能用于具有多个代理服务器的站点，这样你就不需要担心在此刻将浏览器指向哪一个代理。然而，你必须使用支持此功能的浏览器。Netscape Communicator 现在绝对支持它。其他浏览器也在效仿。

如果你确实有一个防火墙，你的系统或网络管理员可能已经设置了 `proxy server`（代理服务器），你必须采取一些特殊步骤让浏览器使用代理服务器，而不是尝试直接通过防火墙并失败。防火墙保护你的网络免受互联网的入侵，但也阻止了你出去。解决办法是建立一个代理服务器，它是唯一允许直接访问或从互联网访问的机器。实际上，你的浏览器将请求代理服务器去获取网页，然后当网页到达时，代理服务器将其交给你的浏览器。不要担心这会很慢；代理服务器从 Web 获取信息的速度通常比你直接获取要快，而且安全得多。





你只需要知道代理服务器的名称和它正在监听的端口。然后你告诉你的浏览器，就可以开始之旅了！唯一棘手的地方可能是，表 `24.1` 中列出的每种协议都可能有自己独立的代理服务器！这在那些拥有海量网络流量的网站非常常见。稍后将展示一个我设置 `Lynx` 浏览器时的示例。

# 从互联网下载软件

你已经在第 24 章中学习了如何通过 `UNIX` 命令行通过 `FTP` 下载文件，但你也可以使用 Web 浏览器来完成相同的操作。使用浏览器要简单得多，因为你只需要做的就是指向和点击。

绝大多数提供你所需软件的 Internet 网站都允许你使用 `anonymous ftp` 来下载你想要的文件。`anonymous FTP` 的惯例是使用 `anonymous` 作为用户名，然后提供你的电子邮件地址作为密码。某些浏览器（如 `Netscape Navigator`）允许你选择一种偏好设置，如果你在 URL 中没有指定用户名，它会自动发送 `anonymous` 作为你的用户名并将你的电子邮件地址作为密码。

如果你没有可以为 `anonymous FTP` 设置偏好选项的浏览器，或者你正在尝试访问一个要求使用特定用户名和密码的 FTP 站点，你可以通过浏览器显式地输入 `FTP` 会话的用户名和密码。URL 的语法如下：

```
ftp://username:password@the.ftp.site.com/
```

### 另请阅读
*有关通过 ftp 传输文件的信息，请参阅第 596 页*
*下载 Lynx。*

对于这个示例，我假设你还没有浏览器。因此，你可能需要使用 `UNIX` 命令行来执行 `FTP` 传输。`Lynx` 的源代码可以在 `www.slcc.edu` 的 `/pub/lynx/release-8/` 目录下通过 `FTP` 获取。由于 `Lynx` 源代码是以 `tarred`, `zipped` 文件（不是压缩或 `gzipped` 文件）格式分发的，你还需要获取一个 `unzip` 工具，而 `UNIX` 默认并不带有该工具。你可以在 `ftp.cdrom.com` 的 `/pub/infozip/UNIX/` 目录下找到为几乎所有版本的 `UNIX` 编译的免费程序。

# 读取和写入 zip 文件

我知道在这一章中不应该讨论压缩，但 `Lynx` 开发者用于压缩其源代码的压缩工具实际上源于 `PKZIP` 工具。因此，该工具并不是 `UNIX` 的一部分，在涵盖 `UNIX` 压缩的章节中也没有讨论过。这意味着标准的 `UNIX` 压缩工具无法读取这些 `PKZIP` 文件。

然而，正如 `UNIX` 中常见的情况一样，有人花时间编写了一个读取/写入这些 `PKZIP` 文件的工具，并免费提供给你。你只需要自己获取并安装它，或者要求你的系统管理员为你操作。我删除了 `FTP` 输出中不是特别帮助的部分。请注意，`FTP` 服务器上的这些消息可能会随时变化，而且经常会变化。

```
% ftp -i ftp.cdrom.com Connected to wcarchive.cdrom.com.
220 wcarchive.cdrom.com FTP server (Version DG-2.12 Tue 24 18:40 ST 98) ready.
Name (ftp.cdrom.com:anonymous):
331 Guest login ok, send your complete email address as password.
Password: username@host.com
230 Welcome to wcarchive-home site for Walnut Creek ROM.
230 There are currently 3000 users out of 3000 possible.
230 Please send mail to ftp-bugs@ftp.cdrom.com if you experience any problems. Please also let us know if there is something we don't have you think we should!
230 Guest login ok, access restrictions apply.
ftp> binary
200 Type set to I.
ftp> hash printing on (8192 bytes/hash mark).
ftp> cd /pub/infozip/UNIX/
250 This directory contains executables for UNIX systems that generally not ship with a C compiler.
250 AIX/ executables for IBM AIX on RS/6000
250 CLIX/ executables for Intergraph CLIX
250 CONVEX/ executables for ConvexOS
250 DEC/ executables for DEC Digital UNIX (OSF/1) and Ultrix
250 FreeBSD/ executables for FreeBSD 2.x on Intel
250 HP/ executables for HP/UX
250 LINUX/ executables for Linux on
250 QNX/ executables for QNX on Intel
250 SCO/ executables for SCO UNIX
```




# Silicon 平台的执行文件

- **SGI/**: 适用于 Silicon Graphics Irix 的执行文件
- **SUN/**: 适用于 SPARC 上 SunOS 和 Solaris 2.x 的执行文件

## 问题报告
请将 `Zip` 和 `UnZip` 的问题报告发送至：`Zip-Bugs@lists.wku.edu`

**最后更新：** 1997 年 12 月 1 日

## FTP 会话
```
CWD command successful.
ftp> cd SUN
```
此目录包含适用于 SPARC 和 Intel x86 硬件的 SunOS 和 Solaris 执行文件。

## 文件列表
| 大小 | 日期 | 名称 | 描述 |
| :--- | :--- | :--- | :--- |
| 1856 | 1997 年 12 月 4 | `README` | 你正在阅读的内容 |
| 240193 | 1996 年 6 月 3 | `gzip124x.tar.Z` | `gzip` 1.2.4, SunOS 执行文件/文档，tar 归档 |
| 195440 | 1994 年 2 月 10 | `gzip124x.zip` | `gzip` 1.2.4, SunOS 执行文件/文档，zip 文件 |
| 208685 | 1997 年 11 月 8 | `unz532x-41x.tar.Z` | `UnZip` 5.32, SunOS 4.x 执行文件/文档，tar 包 |
| 162289 | 1997 年 11 月 8 | `unz532x-41x.zip` | `UnZip` 5.32, SunOS 4.x 执行文件/文档，zip 文件 |
| 207751 | 1997 年 11 月 8 | `unz532x-sol.tar.Z` | `UnZip` 5.32, Solaris/SPARC 2.x 执行文件/文档 |
| 161083 | 1997 年 11 月 8 | `unz532x-sol.zip` | `UnZip` 5.32, Solaris/SPARC 2.x 执行文件/文档 |
| 204513 | 1997 年 11 月 5 | `unz532x-x86.tar.Z` | `UnZip` 5.32, Solaris/x86 2.x 执行文件/文档 |
| 152404 | 1997 年 11 月 5 | `unz532x-x86.zip` | `UnZip` 5.32, Solaris/x86 2.x 执行文件/文档 |
| 94295 | 1997 年 11 月 8 | `zip22x-41x.zip` | `Zip` 2.2, SunOS 4.x 执行文件（无加密） |
| 91733 | 1997 年 11 月 8 | `zip22x-sol.zip` | `Zip` 2.2, Solaris/SPARC 执行文件（无加密） |

## 支持加密的二进制文件
支持加密的二进制文件可通过 `ftp://ftp.icce.rug.nl/info/UNIX/SUN/` 获取：
- 129862 | 1997 年 11 月 9 | `zcr22x-41x.zip` | `Zip` 2.2, SunOS 4.x 执行文件（带加密） |
- 127574 | 1997 年 11 月 15 | `zcr22x-sol.zip` | `Zip` 2.2, Solaris/SPARC 执行文件（带加密） |
- 103685 | 1997 年 11 月 8 | `zcr22x-x86.zip` | `Zip` 2.2, Solaris/x86 执行文件（带加密） |

## 技术说明
`SunOS 4.x` 执行文件已 `SunOS 4.1.4` 和 `Solaris 2.5.1` 下通过测试，其速度与原生 `Solaris 2.x` 二进制文件几乎无异。然而，有报告称它们在 `Solaris 2.4` 下运行并不良好，因此提供了两种版本。

`x86` 二进制文件是在 `Solaris 2.4` 下使用 `SC2.0.1` 编译的。

## 文档与源码
所有的 `Info-ZIP` 包包含文档。源码位于 `../../src`。
- 将 `Zip` 和 `UnZip` 的问题报告发送至：`Zip-Bugs@lists.wku.edu`
- 将 `gzip` 的问题报告发送至：`gzip@prep.ai.edu`

## 安装指南
```
CWD command successful.
ftp> get unz532x-sol.tar.Z
200 PORT command successful.
150 BINARY mode data connection for unz532x-sol.tar.Z (207751 bytes).
########## Transfer complete.
local: unz532x-sol.tar.Z remote: unz532x-sol.tar.Z 207751 bytes received in 3.4 seconds (60 Kbytes/s)
```
现在你已经有了 `unzip` 工具，可以将其通过管道传递给 `gzip` 工具解压，然后从包含的 `tar` 文件中提取信息。完成后，你可能需要将二进制文件拷贝到 `/usr/local/bin`，并将 man 页面拷贝到 `/usr/local/man`，或者让系统管理员为你完成。

```
cat unz532x-sol.tar.Z | gzip -d | tar xvf -
```

## 目录可用文件
- `COPYING`
- `README`
- `WHERE`
- `unzip`
- `unzip.1`
- `unzip.doc`
- `unzipsfx`
- `unzipsfx.1`
- `unzipsfx.doc`
- `zipinfo`（指向 `unzip` 的符号链接）
- `zipinfo.1`
- `zipinfo.doc`
- `zipgrep`
- `zipgrep.1`
- `zipgrep.doc`
- `funzip`
- `funzip.1`
- `funzip.doc`

准备好所有必要的工具后，你就可以下载 Lynx 的源码了。

## Lynx 源码
```
ftp -i www.slcc.edu
Connected to SOL.CCCC. FTP server (UNIX System Release 4.0) ready.
Name (www.slcc.edu:marler): anonymous
Guest login ok, send ident as password.
Password: username@host.com
Guest login ok, access restrictions apply.
ftp> cd /pub/lynx2-8
250 CWD command successful.
ftp> dir
200 PORT command successful.
150 ASCII data connection for /bin/ls (205.172.10.173,48147). total 3786
```
- `CHANGES`
- `features.html`
- `features.txt`
- `index.html`
- `index.txt`
- `lynx2-8` (目录)
- `lynx2-8.zip` (1669681 bytes)
- `lynx2-8.zip-lst` (25671 bytes)
- `ssl.html` (2085 bytes)
- `ssl.txt` (1786 bytes)





# 二进制传输完成

226 二进制传输完成。

本地：`lynx2-8.zip` 远程：`lynx2-8.zip`

在 67 秒内接收了 1669681 字节 (24 Kbytes/s)

Lynx 的源代码位于一个 zip 压缩包中，因此只需对其运行 `unzip` 实用即可。这将创建 Lynx 源码目录并将所有源代码放入其中。

```bash
% unzip lynx2-8.zip Archive:  lynx2-8.zip
   creating: lynx2-8/
   inflating: lynx2-8/COPYHEADER
   inflating: lynx2-8/COPYING
   inflating: lynx2-8/INSTALLATION
   inflating: lynx2-8/LYMessages_en.h
     .....
```

本节包含以下几点假设：

1. 你拥有适用于你版本 UNIX 的 C 编译器套件，或者你安装了 GNU C 编译器。对于大多数用途，首选 GNU 编译器，因为它实际上优于大多数商业编译器。非常棒，尤其是它是免费的。
2. 你拥有随 C 编译器套件一起提供的 `make` 实用，或者你安装了 GNU make 实用。两者之间没有优劣之分。

要了解更多关于 GNU 编译器和 `make` 等 GNU 产品的信息，你可以访问 Free 基金会网站：http://www.gnu.org。你将在那里找到所有 GNU 产品的文档和源代码。它们不仅是免费提供的，而且通常比你版本 UNIX 自带的工具更好用。

与许多当前的 UNIX 发行版一样，Lynx 软件包包含了 GNU `autoconfig` 实用程序，它会分析你的 UNIX 版本并确保进行所有正确的设置，以便能够顺利地编译 Lynx。任何此类包的顶层源码树中都有一个 `configure` 脚本。你只需要运行 `configure`，它就会为你的机器创建相应的 `Makefile`。

```bash
% cd lynx2-8
% ./configure
creating cache ./config.cache
checking host system type... sparc-sun-solaris2.5.1
checking for gcc... gcc
checking whether the C compiler (gcc) works... yes
checking whether the C compiler (gcc) is a cross-compiler... no
checking whether we are using GNU C... yes
.....
updating cache ./config.cache
creating ./config.status
creating makefile
creating WWW/Library/unix/makefile
creating src/makefile
creating src/chrtrans/makefile
creating lynx_cfg.h
```

现在你已经为你的平台配置好了 Lynx 源码，你可以让 `make` 实用程序为你编译它：

```bash
% make
```

如果 Lynx 编译成功，你可以通过输入以下命令来安装它：

```bash
# make install
```

你需要对系统上的 `/usr/local/` 拥有 root 权限，或者让你的系统为你安装 Lynx。

## 使用基于字符的浏览器 (Lynx)

既然你已经费力构建了可以在你机器上运行的 Lynx 二进制文件，你现在终于可以使用它了！

1. 首先，如果你的站点位于防火墙后，你需要确保已设置好使用相应的代理服务器（如果可用）。咨询你的系统管理员查询代理服务器的名称以及通信的端口。如果你不在防火墙后，请跳到第 3 步。
2. 在知道代理服务器名称和端口后（在本例中，我们将服务器称为 `relay.mycompany.com`，端口为 `8080`），在运行 Lynx 之前，你需要设置几个环境变量。为了简单起见，假设你的代理服务器是以下所有协议的代理：HTTP、HTTPS 和 FTP。如果事实不是，你的系统管理员可以告诉你。

如果你使用的是 C Shell，请将以下放入你的登录脚本中：

```
setenv http_proxy http://relay.mycompany.com:8080
setenv https_proxy http://relay.mycompany.com:8080
setenv ftp_proxy ftp://relay.mycompany.com:8080
```

如果你使用的是 Bourne/Korn Shell，请将以下放入你的登录脚本中：

```bash
http_proxy=http://relay.mycompany.com:8080/
export http_proxy
```





```bash
https_proxy=http://relay.mycompany.com:8080/; export
ftp_proxy=http://relay.mycompany.com:8080/; export
```

### 3. 现在你可以运行 Lynx
在命令行中，输入 `lynx`。

使用 Lynx 非常直观。这里是最常用命令的表格。

#### 表 24.4 Lynx 命令简表。

| 命令 | 描述 |
| :--- | :--- |
| `g` | 跳转到 URL，允许你输入一个 URL 进行访问。 |
| `*/pattern` | 在当前网页中搜索模式。 |
| `Up arrow` (向上箭头) | 在当前网页的超链接中向上移动。 |
| `Down arrow` (向下箭头) | 在当前网页的超链接中向下移动。 |
| `Return` (回车) | 进入当前选中的超链接。 |

### UNIX 供应商网站

大多数 UNIX 供应商都活跃在网上，并根据你支付的支持费用多少，允许对网站的技术支持内容进行不同程度的访问。有几个供应商会维护一个独立的站点作为其网站的主入口，另一个站点专门用于 UNIX 支持。

#### 查找支持

我包含了每个供应商网站的主入口，因为这些入口永远不会改变。如果你发现表 24.5 中的 UNIX 支持页面发生了变化，你始终可以确定，只要你进入该供应商的主入口，就能找到指向新 UNIX 支持页面的链接。

#### 表 24.5 UNIX 供应商网站

| 供应商 | 主入口 | 支持 |
| :--- | :--- | :--- |
| Sun Microsystems (SunOS, Solaris) | `http://www.sun.com` | `http://sun.sby.com` |
| Hewlett-Packard (HP-UX) | `http://www.hp.com` | `http://us-support.hp.com` |
| IBM (AIX) | `http://www.ibm.com` | `http://www.rs6000.ibm.com/support/` |
| Silicon Graphics (IRIX) | `http://www.sgi.com` | `http://www.sgi.com/software/` |

### 访问 UNIX 支持

每个 UNIX 供应商都提供多种技术支持。其中一些是免费的，但大多数服务要求你与供应商签订支持合同。本节回顾了每种支持类型以及如何获取它们。虽然每个供应商处理支持的方式略有不同，但以 Sun 的支持系统作为示例。

当你购买 UNIX 系统时，通常可以选择购买硬件和软件的共同支持，这可能包括操作系统、捆绑软件工具，以及你选择购买的任何非捆绑工具，例如特殊的编译器或应用程序。你通常可以选择几个服务级别中的一种，范围从工作时间内的每周五天协助，到每周七天、每天 24 小时的服务。Sun 将这些服务计划称为 SunSpectrum，并并在 `http://www.sun.com/service/support/sunspectrum/index.htm` 上说明了这些计划的运作方式。大多数供应商都有非常相似的服务。

最近，供应商开始提供独立于硬件的软件支持。Sun 将此称为 `Software Only`（仅软件）或 `Software Subscription`（软件订阅）服务。他们在 `http://www.sun.com/service/support/sw_only/index.html` 讨论了该提供的具体组件。随着时间的推移，这种服务可能会变得越来越普遍，因为许多个人和企业只想购买软件支持，并在硬件问题出现时再进行处理。

#### 升级服务电话

如果你发现的问题严重影响了你，技术支持人员没有及时给你回电，或者他们看起来过度缺乏经验，你可以对电话进行 `escalate`（升级）。你这样做的方法是拨回技术支持中心，提供你的服务订单号，并要求与升级经理通话。你可以向他解释糟糕的服务，并要求提高电话的优先级。只有在极端紧急情况下，或者软件支持工程师就是不回你电话时，你才需要这样做。我通常一年只需要这样做一次左右。




谈到网站，供应商正不断通过其支持网站提供越来越多的支持能力。如果你访问 Sun 的网站，你会发现某些支持服务是免费提供的，例如补丁、常见问题解答（FAQ）和文档。

网站的某些部分仅限于拥有支持合同的客户。这里提供的服务包括在补丁数据库上使用搜索引擎的能力，以帮助你找到困扰你特定硬件和软件组合的问题，并指引你找到可以解决该问题的补丁。（关于补丁的更多信息将在稍后的几个章节中介绍。）其他合同服务还包括下载特殊的系统诊断工具，以及查看在线文档，例如白皮书、问题症状和解决方案报告，以及如何从一个操作系统过渡到另一个版本的信息等。

获取技术支持的最后一种通常是最实用的，而且是免费的！我们将在本章最后讨论如何使用 Usenet，但值得提到的是，对于存在过的每种计算机类型和操作系统，都有一组新闻组。通常你会发现专家经常出没这些新闻组，他们通常非常乐意为你提供所需的任何帮助。然而，通常情况下，你可能有的任何问题（特别是如果你是新手）已经有人问过数百次了。如果是这样，它通常会包含在每个新闻组每月左右发送一次的常见问题解答（FAQ）消息中。这是一条单一的消息，包含了自特定新闻组主题创建以来所有被问过且回答过的支持问题。在向新闻组的每个人询问你的特定问题之前，阅读这条消息将为你省去很多麻烦（以及避免收到垃圾邮件）。关于此类新闻组具体名称的更多信息见本章末尾。

## 获取免费（非官方支持）软件

所有供应商都提供一些内部开发的免费软件来监控你的系统。它们之所以是免费的，是因为它们没有官方支持。如果你想报告有关这些软件的问题，必须联系工具的原始作者，根据他们当前的工作量，他们可能可以，也可能做不了。

Sun 的此类工具的一个示例是 SymbEL，最初被称为 Virtual Adrian，可以通过 `http://www.sun.com/sun-on-net/performance/se3/` 获取。它允许你分析操作系统内核的内部运行机制，并报告你可以进行哪些修改以获得更好的性能。你会注意到，文档中明确指出该软件包不受官方支持，但他们感谢通过电子邮件提供的反馈，并会考虑任何增强请求。

此类工具的运行效果实际上非常好。问题在于找到它们，因为非支持的应用程序不会被显著地展示。如果你知道想要的工具名称，只需将这些名称输入 Web 搜索引擎就是一个相当简单的过程，至少可以获得关于从何获取最新副本的提示。值得注意的是，并非所有此类程序都是由供应商创建或提供的。有些是由经验丰富的程序员编写的，他们希望与所有人分享。

Usenet 是另一个可以寻找或在本在本章稍后讨论的此类工具的地方。

## 检查补丁/更新

供应商会免费提供某些补丁。定期检查网站是否有新补丁发布是一个好主意，因为这可以让你保持最新状态。如果你在供应商处有支持，你的处会好得多，因为在更新发布时你会立即通过电子邮件收到通知。如果你有支持，还可以使用 Sun 上一个非常好用的工具（在其他平台上也有类似的工具）来确定应该应用哪些补丁。该工具称为 `patchdiag`，它会将你系统中当前加载的补丁与 Sun 目前建议你加载的补丁进行比较。然后它会生成一份报告，告诉你你加载了什么，应该加载什么。它甚至有专门的章节描述影响应用程序和安全的补丁。

关于 UNIX 机器上的补丁有一点：许多供应商对于永久删除补丁程序替换的任何文件是有必要的谨慎。因此，他们将它们隐藏起来，以防你某天想要撤销补丁。请注意，你可能会因此丢失一些磁盘空间。随着针对同一个问题的不同补丁不断更新，在一个补丁之上再应用另一个补丁会占用越来越多的磁盘空间。如果你有时间但没有剩余磁盘空间，可以在应用新补丁之前删除旧补丁。通常当你升级操作系统时，这些补丁残留会被完全删除，因此你可以找回空间。




# 检查安全公告

针对你所使用的特定版本 UNIX 的安全公告通常会在供应商的网站上非常显眼地显示。通常还会提供免费的历史安全警报存档。每份公告都描述了操作系统中可能被掌握相关信息的人所破坏的部分。它还描述了阻止该威胁所需的补丁或操作。

安全漏洞的补丁几乎总是免费提供的。你可以选择偶尔手动检查新的安全公告，也可以加入每份独立安全公告中都会重点提到的邮件列表。此后，当针对你的特定平台发布公告时，你会自动收到通知。

# 检查千年（2000 年）问题

除非你过去几年一直一直在睡觉，否则你一定听过 2000 年将带给整个计算世界的所有问题。这些问题中的绝大多数都与一个事实有关：许多应用程序和某些操作系统在编写时，将年份的前两位硬编码在到处（即 1999 年中的 "19"）。在数据库和其他存储日期的其他文件中，只有年份的最后两位实际上发生了变化。因此，当 2000 年到来时，这些应用程序会将年份的最后两位改为 00，对它们来说，年份看起来变成了 1900 年。

正如你所想象的，这将导致随着时间推移而依赖日期演变的程序变得有些困惑，并对它们控制的数据进行一些糟糕的操作。像银行记录、账单程序等，除非在 1999 年 12 月 31 日之前发现并修复这些程序，否则可能会受到影响。

整件事之所以发生，是因为开发这些应用程序和操作系统的人并不知道在 2000 年到来时，还会有人使用他们的应用程序，甚至使用同一台计算机。一些开发者仍然留着以相同方式编写处理日期敏感信息程序的坏习惯。

大多数 UNIX 供应商都非常重视这个问题，并花费了大量精力检查他们的系统管理和通用系统程序，以确保它们都符合 2000 年标准。如果你运行的是他们旧版本的操作系统，他们可能提供了你现在就可以应用以修复这些问题的补丁。新版本的 UNIX 声称完全符合 2000 年标准。如果你与 UNIX 供应商签支持合同，这些补丁会在他们的支持网站上显眼显示，并可以直接下载到你的系统中进行应用。如果你没有向 UNIX 供应商购买支持合同，大多数供应商仍通过其支持网页的免费服务部分提供 2000 年补丁，因为这对保持你的系统运行至关重要。

当然，仅对你的 UNIX 操作系统和供应商提供的工具进行补丁可能是不够。你可能从其他供应商那里购买了应用程序，你需要直接向他们查询或访问他们的网站。与 UNIX 供应商一样，大多数应用程序供应商都会在其支持网站的首页声称已提供针对 2000 年问题的解决方案。

# 在 UNIX 上阅读网络新闻

互联网上最老的活动之一是阅读网络新闻（Network News），也称为 Usenet。Usenet 本质上是一个巨大的个人讨论主题集合，范围从职位招聘（`misc.jobs.offer`）到如何管理你的计算机（`comp.sys.sun.admin`），再到如何照顾你的非洲灰鹦鹉（`alt.pets.parrots.african-grey`）。通常，你可以与特定主题的专家交流，如果你是该领域的专家，也可以提供建议。

每个新闻组的内容都非常具体，但只有在新闻组受管理的情况下才会强制执行这一点。受管理的新闻组有一个分配的管理员，他会阅读发送到新闻组的每条消息，以验证它是否属于那里。如果不属于，他就会将其拒绝。未管理的新闻组通常是自由讨论的，但人们通常足够礼貌，固于当前话题。如果小组失去控制，它可能会从整个 Usenet 的所有新闻服务器中被删除。

新闻组按层级结构排列，新闻组名称中的第一个词最不具体，随着你进入新闻组名称后续，它会变得越来越具体。表 24.4 列出并解释了这一惯。

### 表 24.6 若干 Usenet 新闻组层级的顶层

- comp.* 与计算机相关的新闻组（例如，`comp.sys.sun`, `comp.sys.hp`）
- rec.* 娱乐新闻组（例如，`rec.humor`, `rec.gardens.roses`）
- sci.* 与科学相关的新闻组（例如，`sci.math`, `sci.archaeology`）
- alt.* 备选新闻组（例如，`alt.binaries.startrek`）
- misc.* 不属于任何其他地方的杂主题

当你选择一个新闻组进行读取/写入时，被称为“订阅”该新闻组。当你发送一条消息以包含在新组中时，被称为“向新闻组发帖”。当你这样做时，大约需要一天的时间才能过滤到全球所有的新闻服务器，然后人们很可能会对你写的内容进行回复。过去，你必须每天扫描新闻组，手动寻找对你原始问题/评论的任何回复。坦率地说，如今的大多数新闻阅读器都提供了一种名为“线程”（threading）的功能，它能找到原始帖子并将对它们的任何回复按时间顺序紧跟在原始帖子之后。你会发现 `trn`（线程化阅读新闻）和 Netscape 提供了此功能，尽管 Netscape 将新闻组称为讨论组，并将你用于阅读新闻的浏览器部分称为 Collabra Discussions。




仅有一个新闻阅读客户端是不够让你能够读取和发布 Usenet 消息的。你需要访问新闻服务器的权限。如果你在一个大型站点，你的系统管理员可能已经设置了新闻服务器，或者与其他站点安排了提供这项服务。无论什么情况下，你的系统管理员都可以告诉你该服务器的名称，以便你连接它。如果你的 UNIX 机器是独立的，并且你通过互联网服务提供商访问互联网，你可以询问他们他们的新闻服务器名称是什么。在知道新闻服务器的名称后，设置环境变量 `NNTPSERVER` 使其指向该服务器。大多数新闻阅读客户端在启动时都会寻找此环境变量，并使用它来识别应该连接的新闻服务器。

# NNTP

`NNTPSERVER` 代表网络新闻传输协议服务器（Network News Transfer Protocol SERVER）。

1.  你想使用 `trn` 读取网络新闻。首先，确保 `trn` 可用。如果没有，请你的系统管理员为你安装它（或等效程序）；或者，如果你是独立操作，可以下载它的源代码并自行编译。安装完成后，你就可以进行下一步。
2.  从系统管理员或互联网服务提供商处获取你的新闻服务器名称，并相应地设置你的 `NNTPSERVER` 环境变量。在本示例中，假设新闻服务器名称为 `news.mycompany.com`。

### 对于 Bourne、Bash 和 Korn Shell 用户
```bash
NNTPSERVER=news.mycompany.com; export NNTPSERVER
```

### 对于 C Shell 用户
```bash
setenv NNTPSERVER news.mycompany.com
```

3.  现在运行 `trn` 并订阅所有的 `comp.sys.sun.*` 新闻组。在命令行中输入 `trn`。（以下输出中行尾的加粗术语反映了你作为响应输入的内容。）

```
 |
|
```
使用模式或 `g newsgroup.name` 添加新组。如需移除你不感兴趣的新闻组，请使用 `u` 命令。`noread` 不读取已订阅新闻组中的消息。订阅新闻组请使用 `g<newsgroup>` 命令。

```
End of newsgroups -- what next? a comp.sys.sun
Newsgroup comp.sys.sun.admin not in newssrc -- subscribe? y
Put newsgroup where? $
unread articles in comp.sys.sun.admin -- now? y
```

4.  当你输入 `comp.sys.sun` 时，你指示 `trn` 在整个新闻组列表中搜索标题中包含 `comp.sys.sun` 的任何组，并逐一询问你是否想要订阅每一个。如果说是，它会询问你想将该新闻组放在当前订阅新闻组列表的什么位置。按下美元符号 ($) 将此新闻组放在你当前列表的末尾。在你添加所有新闻组后，你将获得机会阅读每个组中的消息。
5.  如果你想向任何新闻组发布消息，可以在 `trn` 内的任何地方通过输入 `!P` 来操作。系统会询问你想向哪个新闻组发送消息。如果你愿意，可以通过逗号分隔新闻组名称来一次指定多个新闻组。
6.  在 `trn` 中任何时候按下 `h` 键都将向你显示帮助菜单。

如前讨论的，新闻组处理特定版本的 UNIX。阅读针对你所用版本的特定组非常有帮助，而且当你需要提问时会更有帮助，因为你是在一个只处理该主题的论坛中发言。但你需要了解这些新闻组是什么。好消息是，新闻组的名称遵循特定的模式。表 24.7 显示了主要的 Sun 新闻组及其用途。

### 表 24.7 Sun 特定的新闻组

| 新闻组 | 目的 |
| :--- | :--- |
| comp.sys.sun.announce | 使用 Sun 计算机的人感兴趣的主要公告 |
| comp.sys.sun.admin | 关于 Sun 计算机系统管理的信息 |
| comp.sys.sun.apps | 关于在 Sun 计算机上运行的的信息 |
| comp.sys.sun.hardware | 关于 Sun 计算机硬件的信息 |
| comp.sys.sun.misc | 不符合任何其他新闻组的 Sun 计算机杂杂 |
| comp.sys.sun.wanted | 通常是对 Sun 硬件的请求，有时也包括软件 |

如果你使用的是惠尔惠谱（Hewlett-Packards），不要放弃。只需将上表中的 `sun` 替换为 `hp`，你的平台就有相同的新闻组。其他版本的 UNIX 也有类似的新闻组。




# 由 Gordon Marler 

## 编写/执行简单脚本
- 创建/使用自定义变量
- 与用户交互
-在命令行上提供脚本输入 (`$1`)
- 根据测试结果执行代码 (`if`)
- 执行算术计算 (`expr/bc`)
- 特殊 Shell 变量
- 结束脚本并设置退出状态 (`exit`)

Bourne shell 是标准 shell，可以在存在过的每一种 UNIX 变体中找到。尽管它可以被认为是 Korn shell 的子集，但许多人仍然使用 Bourne shell 编写脚本，因为其在不同版本的 UNIX 之间具有保证的移植性。

你已经看到 shell 可以作为 UNIX 的命令行界面使用，但它也包含编程结构，使你能够将重复的命令序列提取并在脚本中实现自动化。这方面的一个例子是找到你当前在系统中运行的所有程序并将它们报告给你。你还可以让脚本与你交互，并根据你的输入做出决策。这方面的例子是：脚本询问你一个特定的用户名，然后找到系统中所有属于该用户的程序并将它们报告给用户。

在我们开始之前，有一个简单的规则：井号（`#`）字符表示其后的后续字符都是注释的一部分，除非 `#` 是第一行的第一个字符，否则 shell 将不会解释它们。你稍后就会明白为什么。

### 编写/执行脚本
你可以从创建一个非常简单的 Bourne 脚本开始，它可以打印 Hello World 并退出。

1. 首先，你需要创建一个存放脚本的空文件。将此文件命名为 `testscript`。输入 `touch testscript`。
2. 为了确保该文件被视为可执行脚本，你必须开启该文件的执行权限。输入 `chmod +x testscript`。
3. 现在，你需要在文件中放入一些内容让 UNIX 知道这是一个 Bourne 脚本。大多数 UNIX 版本都能识别 `#!` 符号。如果文件的前两个字符是 `#!`，UNIX 将将文件第一行的其他所有内容视为解释器（通常是 shell），用于执行该文件的内容。在这种情况下，我们希望 Bourne shell 执行我们的文件内容，因此我们将使用 `vi` 或其他编辑器输入 `testscript` 文件的第一行：`#!/bin/sh`。
4. 打印“Hello World”通过输入文件的第二行来实现：`echo "Hello World."`。
5. 你可以通过运行脚本来测试它：
```bash
./testscript Hello World
```
6. 你完成后的脚本看起来应该是这样的：
```bash
#!/bin/sh
echo "Hello World"
```
有关操作脚本的更多信息，请参阅第 28 页。

### 创建/使用自定义变量
你经常发现，将脚本中运行的命令输出存储起来供稍后使用非常方便。或者，你可能想编码某些信息（例如长路径），但你不想在每次在脚本中使用它时都输入整个路径。如果此路径以后需要更改，如果可以在脚本中仅一处进行更改并在整个脚本中生效就太好了。要实现这一点，你必须创建一个变量。shell 以任何字母或下划线（`_`）开头，后跟零或多个数字、字母或下划线。

要给变量赋值，你使用等号（`=`）以及你想要赋值给变量的值。注意，不能在等号前后使用空格。请学习这些示例：

```bash
LocalBinaries=/usr/local/bin
TMP=/tmp
_mybinaries=/home/gmarler/bin
rocket_0=apollo
```





- `0_rocket=mercury`
- 无效的首字符不能为数字
- `myvar = myvalue`
- `=` 符号周围存在非法空格

要检索存储在变量中的值，可以在变量名前面加上一个美元符号 (`$`)。也可以通过用大括号 (`{...}`) 包围变量名并在整个表达式前面加上一个美元符号 (`$`) 来实现。稍后你就会看到这种情况下何时是必要的。

让我们写一个脚本来设置变量并打印它的值：

1. 遵循 `Writing/Executing a Simple Script` 章节中的第 13 步，但文件名命名为 `testscript2`。
2. 在脚本的第二行，将名为 `tmp_dir` 的变量设置为 `/tmp`。输入：`tmp_dir=/tmp`。
3. 在下一行，打印变量 `tmp_dir` 的值。输入：`echo " Variable tmp_dir contains: $tmp_dir.`。
4. 保存你的脚本文件。它现在应该包含以下内容：
```bash
#!/bin/sh
tmp_dir=/tmp
echo "Variable tmp_dir contains: $tmp_dir"
```
5. 测试你的脚本：`./testscript2`
`tmp_dir contains: /tmp`

我提到过当你想要检索存储在变量中的值时，可能需要使用 `${variable}` 语法。当你打算以如下方式使用变量值时，这是确实成立的：`mv ${filename}${OLD}`

在这里，我们的意图是两次使用存储在变量 `filename` 中的文件名：第一次是引用原始文件名，第二次是为原始文件创建一个新名称，并在末尾加上 `OLD`。你可能会犯一个错误，尝试像这样写：`mv $filename$OLD`

这会尝试将变量 `filename` 所引的文件移动到变量 `filenameOLD` 所引的名字，而该变量并不存在。从这个例子中，你可能看出，养成始终使用 `${variable}` 形式引用变量内容的习惯是好的，因为因为它总是有效的。

### 使用反引号设置变量

与其手动设置所有变量的值，你可以运行一个程序并将其输出存储在变量中。你可以通过反引号（`` `` `）包围想要捕输出的命令来运行它。这被称为命令替换，因为 shell 会获取你在反引号中输入的命令，将其作为一个独立的程序运行（就像你在命令行中输入它一样），然后获取输出并替换整个反引号表达式。反引号与键盘上的波浪号 (`~`) 位于同一个键上。

你可以通过编写一个脚本来收集你的用户名、运行脚本的计算机名称以及当前日期并打印信息信息来测试此功能。

#### 测试设置变量的反引号方法

1. 遵循 `Writing/Executing a Simple Script` 的第 1-3 步，但将文件命名为 `system_info`。
2. 将 `date` 程序的输出存储在变量 `today` 中。输入：`date`。
3. 通过运行 `whoami` 查找你的登录身份并存储在变量 `identity` 中。输入：`whoami`。
4. 查找机器名称并将其存储在变量 `machine` 中。输入：`hostname`。
5. 以优的格式打印出来。输入 `echo "Hello, today is $date. I am logged in as $identity on machine $machine."`。
6. 保存你的脚本。它看起来应该是这样的：
```bash
#!/bin/sh
today=`date`
identity=`whoami`
machine=`hostname`
echo "Hello, today is $date. I am logged in as $identity on machine $machine"
```
7. 测试脚本：`./system_info`
Hello, today is Thu Mar 12 01:03:27 PST 1998. I am logged in as gmarler on machine proteon`

### 使用引号





如果反引号中的命令将产生多行输出，你必须确保将反引号中的命令括在双引号中。否则，输出中的换行符将被剔除，你将得到一行非常长且难看的内容！如果你打算在将此类命令的输出存储在变量后使用 `echo` 打印它，双引号也是必要的。

你需要确保你想要通过反引号执行的命令实际上可以被你的 shell 脚本找到。你可以通过在脚本内部显式地设置 `PATH` 环境变量来实现这一点。你之所以这样做是因为没有设置此变量的脚本将继承运行脚本的用户 `PATH`。如果该用户的路径与你（脚本作者）不相同，脚本在为该用户运行时可能会莫名其妙地运行失败。

### 另请参考
- *有关更多关于设置路径以及查找要运行的程序实际路径的信息，请参阅第 97 页和第 100 页*

### 使用 whoami 和 hostname
你想编写一个运行 `whoami` 和 `hostname` 命令的脚本，并且你非常确定无论由谁运行该脚本，它都能实际找到这两个命令。方法如下：

1. 找到这些命令所在的目录。在 Solaris 上，`whoami` 位于 `/usr/ucb/whoami`，而 `hostname` 位于 `/usr/bin/hostname`。
2. 现在你已经知道需要在脚本中创建一行（最好是第一行），指定你希望在 `PATH` 中包含 `/usr/ucb` 和 `/usr/bin`。该行看起来应该是这样的：`PATH=/usr/ucb:/usr/bin`
3. 以下是整个脚本的示例：

```bash
#!/bin/sh
PATH=/usr/ucb:/usr/bin
myhost=`hostname`
myidentity=`whoami`
echo "My username is $myidentity, and machine name is $myhost"
```

字体 与用户交互
本节演示了在本章之前讨论的一些命令，并向你的命令集中添加了一些新命令。

#### 显示标题和提示符 (echo)
你已经使用 `echo` 命令来输出脚本操作的结果。然而，你也可以用它来打印任何你想让用户看到的输出。默认情况下，`echo` 会打印你提供的信息加上换行符，因此除非另作指定，否则你会被强制到下一行。

`echo` 命令允许使用以下转义字符，帮助你创建标题、标题和提示符：
- `\c`: 打印到此处的文本而不跳到下一行。适用于输入提示符。
- `\n`: 换行。适用于强制让其后的文本在下一行打印。
- `\t`: 制表符。适用于格式化标题和提示符。
- `\\`: 用于在行中插入反斜杠字符。
- `\0xx`: 用于插入不可打印的控制字符。`0xx` 是 ASCII 字符的八进制表示。这个零是必须的。

#### 利用已知知识打印有关用户的信息
1. 首先，为你的信息表打印一个标题。在标题前使用几个制表符使其大致居中，并在其后留一个额外的空行，以与表格的其他部分隔开。由于 `echo` 已经强制你换到下一行，你只需要在末尾再添加一个换行符：
   ```bash
   echo "\t\tCURRENT USER INFORMATION\n."
   ```
2. 你需要运行脚本的用户的用户名供后续命令使用；因此你将其保存在变量中：
   ```bash
   identity=`whoami`
   ```
3. 现在你将打印一些关于用户的信息。注意反引号命令被直接用在输出的行内。这些命令会被执行，并且它们的输出会在打印前被替换到文本中：
   ```bash
   echo "My Unix username is: `whoami`"
   echo "My Unix machine name is: `hostname`"
   echo "My current directory is: `pwd`"
   ```




4. 最后，你打印出当前运行此脚本的用户在系统中正在运行的所有程序列表。注意行中间的换行符（`\n`）。这强制该 `echo` 命令的后续输出从下一行开始显示。行的剩余部分是一个反引号命令，它获取系统中所有正在运行的程序列表（`ps -ef`），并将该输出传递给 `grep` 命令，以搜索运行该脚本的用户正在运行的所有程序。注意，这里必须使用双引号；否则反引号命令的多行输出将显示为一整行。

```
echo "Programs I am currently running: \n `ps -ef | grep $identity`"
```

5. 这是完整的脚本：

```bash
#!/bin/sh
echo "\t\tCURRENT USER INFORMATION\n"

identity=`whoami`

echo "My Unix username is: `whoami`"
echo "My Unix machine name is: `hostname`"
echo "My current directory is: `pwd`"
echo "Programs I am currently running: \n `ps -ef | grep $identity`"
```

通常，你还可能想使用 `echo` 让用户知道你期望某些输入。当你这样做时，可以在某行上打印提示符并让用户在下一行输入其响应，也可以允许用户在与提示符相同的行内输入响应。

这行代码将打印 Please enter your password，然后将光标移动到下一行。

```bash
echo "Please enter your password"
```

这行代码将打印 Please tell me your name:、一个空格，然后在空格后留出光标。如你所见，`\c` 格式字符防止光标跳到下一行。

```bash
echo "Please tell me your name: \c"
```

现在你已经打印了提示符，让我们下一节查看如何读取用户的响应。

### 将用户输入读入 Shell 变量 (read)

现在你已经知道如何向用户输出，是时候学习如何接受用户输入并在脚本中使用它了。`read` 函数就此此目的。关于这个函数需要记住的是它只接受一种类型的输入：任意长度的文本（最多 1024 个字符），并且必须紧跟回车键。在按下回车键之前，`read` 函数对用户输入的内容不会任何操作。

以下步骤显示了如何要求用户输入任何用户名，然后报告该用户当前运行的程序。

#### 报告运行中的程序

1. 首先，提示用户输入用户名，并将光标留在同一行：`echo enter a username: \c`。
2. 现在，将响应读入名为 `username` 的变量中：`read username`。
3. 现在打印一个格式化的页头，并使用 `username` 变量找到该用户正在运行的所有程序。我们将该信息存储在变量 `programs` 中：
   ```bash
   echo "\n\t\tCURRENT USER INFORMATION\n" programs="`ps -ef | grep $username`"
   ```
4. 我们现在再次使用 `username` 变量打印一行，随后是两个回车符和 `program` 变量的内容：
   ```bash
   echo "User $username is running the following programs: \n\n $programs"
   ```

5. 这是完整的脚本：

```bash
#!/bin/sh
echo "Please enter a username: \c"
read username
echo "\n\t\tCURRENT USER INFORMATION\n"
programs="`ps -ef | grep $username`"
echo "User $username is running the following programs: \n\n $programs"
```

关于 `read` 的另一个要点是，它可以用于将值读入多个变量。

```bash
echo "Please enter your firstname, lastname, age and weight" read lastname age weight
```

然而，如果用户输入的值多你读取的变量数量，则 `read` 命令中的最后一个变量将接收所有额外值。在以下示例中，如果用户响应提示输入了 John Smith 20 160，那么变量 `firstname` 将包含 John，而变量 `lastname` 将包含 Smith 20 160。这可能不是你想要的结果。

### 在命令行上提供脚本输入 ($1)





到为止，我们创建的脚本要么完全不需要用户的任何输入，要么在每次运行时都必须与用户直接交互。你通常会发现，在启动脚本时提供它所需的所有信息非常方便，这样它在运行过程中就不会向你提问任何问题。如果你打算在后台运行脚本，这一点尤为重要，因为你没有机会给此类脚本提供额外输入，因为后台运行会使其与终端断开。当另一个脚本将运行你的脚本并为其传递信息时，这种方法也有用。

当你运行脚本并像这样为其传递参数时：

`myscript arg1 arg2 arg3 ...`

在你的脚本内部，特殊变量 `$1`、`$2` 和 `$3` 分别被设置为 `arg1`、`arg2` 和 `arg3`。这种机制一直有效到 `$9`。如果你需要处理超过九个参数，则需要使用另一种涉及 `for` 指令的方法。该指令将在几几节后进行讨论。

值得注意的是的是，`$0` 被设置为你的脚本的实际名称（在本例中为 `myscript`）。当你想要打印信息消息并在其中包含脚本名称时，可能会发现这非常方便。

### 根据测试结果执行代码 (if)

所有编程语言都有某种方法根据条件是否真来决定是否执行代码。Shell 通过 `if` 语句为你提供。`if` 语句的完整格式如下：

```bash
if conditional then
    command
    ...
elif conditional
then
    command
    ...
else
    command
    ...
fi
```

这是它的工作原理：在所有情况下，`conditional` 都是你可以执行的任何命令。如果命令的退出状态为零 (0)，意味着它执行成功，那么紧接着 `conditional` 之后的命令将被执行，直到遇到下一个 `else`、`elif` 或 `fi`。如果命令的退出状态不是零，意味着命令以某种方式失败了，那么 `conditional` 之后的命令将被跳过，直到遇到下一个 `else`、`elif` 或 `fi`。

`elif` 语句如果存在，代表 else if（否则如果），它允许你在进入 `else` 语句或退出整个 `if` 语句之前测试另一个条件。语句的这部分不是必须的，提供以备你需要时使用。`else` 语句如果存在，则仅在之前的 `conditional` 不为真时执行。语句的这部分也不是必须的。

如果你不把关键字 `then` 单独放在一行，只要使用分号将其与 `conditional` 分隔，就可以将其与 `if` 或 `elif` 关键字同一行。

```bash
if conditional; then
elif conditional; then
```

你会注意到条件可以是任何命令，但它通常是 `test` 命令。让我们来看看它是如何工作的。

#### 检查文件类型、大小或权限

`test` 命令允许你做的之一是检查文件系统对象（文件或目录）的多个属性，并根据这些属性在脚本中做出决策。下表不是 `test` 用于文件系统对象的选项完整列表，但它涵盖了最常用的。

**表 25.1 用于文件系统对象的 test 选项。**

| 选项 |  |
| :--- | :--- |
| `-d file` | 文件是目录吗？ |
| `-f file` | 文件是普通文件吗？ |
| `-r file` | 该文件可被此脚本读取吗？ |
| `-w file` | 该文件可被此脚本写入吗？ |
| `-x file` | 该文件可被此脚本执行吗？ |
| `-s file` | 文件长度是否大于零？ |

让我们创建一个文件并对其运行若干次测试。首先，让我们创建一个文件并设置权限：

```bash
touch /tmp/test
chmod 755 /tmp/test
```

现在我们可以编写脚本了。让我们从使用两个独立的 `if` 语句开始：

```bash
MYFILE="/tmp/test" if test -d $MYFILE then
    echo "My file is a directory!"
fi
if test -f $MYFILE then
    echo "My file is an ordinary file!"
fi
```

如果你原样保存并运行它，你应该会得到如下输出：

```
% ./testif My file is an ordinary file!
```

这是你预期的。现在让我们创建一个名为 `testif2` 的新脚本。在这里我们将使用 `elif` 和 `else` 语句：

```bash
MYFILE="/tmp/test" if test -d $MYFILE then
    echo "My file is a directory!"
elif test -f $MYFILE then
    echo "My file is an ordinary file!"
fi
```





```bash
then
    echo "My file is an ordinary file!"
    if test -w $MYFILE
    then
        echo "This file is writeable too!"
    else
        echo "This file is not writeable"
    fi
    if test -r $MYFILE
    then
        echo "This file is readable!"
    else
        echo "This file is not readable"
    fi
fi
```

注意，你可以将一个 `if` 语句放在另一个 `if` 语句内部。按照当前的文件权限，该脚本应该输出如下：

```bash
./testif2 My file is an ordinary file!
This file is writeable too!
This file is readable!
```

4. 现在让我们稍微修改一下文件的权限，关闭它的写入权限，以便我们测试脚本。

```bash
chmod -w /tmp/testfile
```

5. 现在再次运行脚本：

```bash
./testif2 My file is an ordinary file!
This file is not writeable
This file is readable!
```

### 另另参考
相关相关信息请参阅第 286 页。

值得注意的是，你不需要为每个想要测试的条件都编写一个独立的 `if` 语句。如果对你要完成的任务方便，你可以将多个 `test` 命令组合在同一行。在下表中，`exp` 代表 `test` 命令的任何选项。

#### 表 25.2 组合 test 命令的运算符

| 表达式 | 说明 |
| :--- | :--- |
| `test exp[1] && test exp[2]` | 如果 `exp[1]` 和 `exp[2]` 都为真，则整个命令为真。 |
| `test exp[1] \| test exp[2]` | 如果 `exp[1]` 或 `exp[2]` 为真，则整个命令为真。 |
| `test ! exp[1]` | 如果 `exp[1]` 结果为真，则现在变为假，反之亦然。 |

### Test 命令的另一个示例

1. 现在我们可以写一个短一点的脚本，命名为 `testif3`。让我们先把文件的权限改回来。

```bash
chmod +w /tmp/testfile
```

2. 我们将测试该文件是否是一个普通文件、是否可写以及是否可读：

```bash
MYFILE="/tmp/testfile" if test -f $MYFILE && test -w $MYFILE && test -r $MYFILE
then
    echo "My file is an ordinary file, and it is writeable and readable!"
fi
```

3. 现在，如果文件里什么都没有，即使开启了执行位，尝试将其作为程序运行也是没有意义的对吧？让我们让脚本测试这种情况并告诉我们。请注意，`-s` 测试只有在文件大小大于 0 时才返回真 (0)，如果文件大小恰好为 0 则返回假 (1)。因此，我们通过使用 `!` 运算符来反转测试含义。这使得语句的逻辑如下：如果文件是可执行的*且*文件长度为 0，则打印消息。

```bash
if test -x $MYFILE && test ! -s $MYFILE then
    echo "This file is empty! Why would you try to execute it?"
fi
```

4. 让我们脚本的输出：

```bash
./testif3 My file is an ordinary file, and it is writeable and readable!
This is empty!
```

另一种编写 `test` 命令的方法可以让它在脚本中更具可读性，并使用方括号（``）：`[ -x file ]`。

不要忘记空格。当你在脚本中使用这种形式的 `test` 时，你必须确保在左方括号（`[`）*之后*加上空格，并在右方括号（`]`）*之前*加上空格。否则，这会导致语法错误。`[ -x file ]` 等于 `test -x file`。

从现在起，我们将对 `test` 命令使用 `[...]` 语法。

### 检查变量内容

除了检查文件属性外，你还可以使用 `test` 查看变量中的内容，并根据其内容做出决策。对于想要解释为字符串的变量以及想要解释为整数的变量，有单独的运算符。

#### 表 25.3 test 的字符串运算符

| 表达式 | 说明 |
| :--- | :--- |
| `-n *string` | 如果 `string` 有值（不为空）则返回真 |
| `-z *string` | 如果 `string` 无值（为空）则返回真 |
| `*string1 = string2` | 如果 `string1` 与*string2* 相同则返回真 |
| `*string1 != string2` | 如果 `string1` 不与 `string2` 相同则返回真 |




几个示例可以清楚地说明这些是如何工作的。你可以使用这些语句中的任何一个脚本中 `if` 语句的条件部分。你应该记住，传递给 `test` 的任何变量都应该用双引号括起来。

### 检查值

首先，我们可以检查一个变量是否有任何值。

```bash
myvar= if [ -z "$myvar" ]; then
   echo "This variable has no value"
fi
```

然而，上一个示例可能会让你碰钉，如果变量 `myvar` 包含某些非字母数字字符，例如等号（`=`），因为 `test` 会认为你正试图给一个变量赋值！为了确保这种情况永远不会发生，你可以使用另一种结构，你会发现这种结构在 shell 脚本中非常常见。

```bash
myvar= if [ X = X"$myvar" ]; then
   echo "This variable has no value"
fi
```

你看到它是如何工作的了吗？如果 `myvar` 没有值，该语句将简化为：`X` 等于 `X` 吗？这显然是真。。

### 字符串比较

现在让我们对字符串变量进行一些比较。

```bash
animal1="pig" animal2="cow"
if [ $animal1 = $animal2 ]; then
   echo "These animals are the same"
elif [ $animal1 != $animal2 ]; then
   echo "These animals are different"
fi
```

### 整数比较

如果存储在变量中的字符串是数字，你需要使用另一组运算符将它们视为数字处理。你需要区分这种区分，正如你从以下示例中看到的那样。记住，这些运算符只对整数有效。它们不理解带有小数点的数字。

**表 25.4 用于 test 的整数运算符。**

| 运算符 | 描述 |
| :--- | :--- |
| `int1 -eq int2` | `int1` 等于 `int2` |
| `int1 -ne int2` | `int1` 不等于 `int2` |
| `int1 -gt int2` | `int1` 大于 `int2` |
| `int1 -ge int2` | `int1` 大于等于 `int2` |
| `int1 -lt int2` | `int1` 小于 `int2` |
| `int1 -le int2` | `int1` 小于等于 `int2` |

```bash
value1="6" value2="00005"
if [ "$value1" -ne "$value2" ]; then
   echo "values are not equal"
fi
if [ "$value1" -eq 6 ]; then
   echo "value1 is equal to 6"
fi
if [ "$value2" -eq 5 ]; then
   echo "value2 is equal to 5"
fi
```

现在，如果你在最后两个测试中使用字符串运算符 `=` 而不是整数运算符 `-eq`，你将无法收到任何一个的输出。那是因为 `value1` 中的 `6` 后面有一个空格，而 `value2` 中的 `5` 之前有四个零，字符串运算符寻找的是精确字符匹配，而不是数值匹配。

### 检查命令结果

我知道我说 `if` 语句的条件部分通常是 `test` 命令的形式，但你可以使用任何在成功完成时返回零 (0)、在失败时返回其他任何数字的命令或程序。

例子是，如果你想知道系统中是否有人运行 `vi` 文本编辑器。实际上，这个脚本将定位系统中运行的任何 `vi` 程序，以及由 `ps -ef` 生成的包含 "vi" 字样的任何内容。

```bash
if ps -ef | grep "vi"; then
   echo "Yep, someone is running vi"
else
   echo "No one is running vi at this time"
fi
```

注意我们运行了 `ps -ef`，将其输出通过到 `grep`，并告诉它查找任何以最后两个字符 vi 结尾的行。如果 `grep` 搜索成功，它将返回零状态码，并返回确认 `vi` 运行在系统某处的行。注意，只检查*条件*部分中运行的最后一个命令的状态码。

让我们看看上述的输出：

```
1234 pts/0    S    0:00 0:00 vi
```
是的，vi 正在运行
```

发生了什么？嗯，第一行输出是由运行 `ps -ef | grep "vi"` 产生的。如果你不想让运行脚本的人看到*条件*程序的输出，你可以将此类程序的输出重定向到 `/dev/null`。修改后的行看起来像这样：

```bash
if ps -ef | grep "vi" > /dev/null; then
```

只要你在*条件*中运行的程序向*标准输出*发送了任何信息，那就是没问题的。然而，如果它们还向*标准错误*发送了任何信息消息或错误，如果你不想看到这些消息混杂在你的输出中，你就必须更改该行以将它们都发送到 `/dev/null`。在这种情况下，该行将变为：

```bash
if ps -ef | grep "vi" > /dev/null 2>&1; then
```



你实际上不需要使用 `if` 就能获得这些结果。你可以使用 `&&` 和 `||` 运算符来连接你想要在特定条件下执行的一系列命令。首先，让我们来看如何查看这些运算符。

你可以将 `command1 && command2` 理解为：当且仅当 `command1` 执行成功时，才执行 `command2`。你可以将 `command1 || command2` 理解为：如果 `command1` 没有执行成功，则执行 `command2`。

你可以使用这些运算符连接你认为必要的任意数量命令。这里有一个常见任务的示例：将日志文件复制到另一个位置以备日后检查，然后再清空当前日志文件。你不希望在确定到另一个位置的复制成功之前允许当前日志文件被清空。

```bash
cp ${logfile} ${logfile}.1 && cp /dev/null ${logfile}
```

你可以重写这段代码，给出一个友好的短消息，通知用户脚本无法复制日志文件。括号的作用是确保由 `&&` 连接的命令在 `echo` 可能运行之前已经过完全评估。如果前两个命令都成功，则 `echo` 将永远不会执行。

```bash
(cp ${logfile} ${logfile}.1 && cp /dev/null ${logfile}) || echo "Could not copy ${logfile} to ${logfile}.1"
```

这比写等价的内容短一点（但没有那么易读）：

```bash
if cp ${logfile} ${logfile}.1; then
    cp /dev/null ${logfile}
else
    echo "Could not copy ${logfile} to ${logfile}.1"
fi
```

### 执行计算

你可能已经注意到，到为止所有的示例都严格处理文本，没有提到如何处理数值计算。这是因为 shell 认为一切都是文本；它只将数字视为 ASCII 字符。如果你需要执行任何类型的数值计算，你必须使用 shell 外部的程序并通过反引号（backquote）来为你完成。这些程序的输出可以赋值给变量，或者通过 `echo` 命令直接打印。如果你只需要执行整数计算，可以使用表达式评估程序 `expr`。

#### 表 25.5：`expr` 中使用的数学运算

| 表达式 | 运算操作 | 结果 |
| :--- | :--- | :--- |
| `result=`expr 5 + 4`` | 加法 | `result=9` |
| `result=`expr 5 - 4`` | 减法 | `result=1` |
| `result=`expr 5 \* 4`` | 乘法 | `result=20` (注意星号 `*` 必须用反斜杠转义) |
| `result=`expr 4 / 2`` | 除法 | `result=2` |
| `result=`expr 5 % 4`` | 余数（模） | `result=1` (即 5 除以 4 余 1) |
| `result=`expr 5 / 4`` | 除法 | `result=1` (记住，`expr` 除了整数计算外什么也做不了) |

如果你需要在脚本中使用浮点数数学运算，你可以使用 `bc` 来进行计算。你必须确保在每次使用 `bc` 时都为它指定的小数位精度。

#### 转义 `expr` 命令

`expr` 中的乘法使用星号 (`*`)，但你必须用反斜杠对其进行转义。为什么？因为如果你这样做，星号将被解释为通配符，并匹配目录中的所有文件。

为了获得两位小数，我们必须使用 `bc` 中的 `scale` 指令。为了获取兆字节数，我们将千字节数除以 1024。注意我们使用双引号来保护命令不被 shell 解释：

```bash
diskspace_mb=`echo "scale=2; $diskspace_kb/1024" | bc` echo $diskspace_mb
```

在这种情况下，你应该得到以下输出：

```
1765.69
```





为了方便起见，shell 预定义了一些变量，其中一些会脚本的运行而改变，另一些则在脚本的生命周期内固定设置。

### 检查指定的命令行参数数量 (`#`)

当有人运行你的脚本时，确保他或她传递了正确数量的参数总是很有好的。当你的脚本运行时，shell 会将 `$#` 设置为该数字。你可以使用已经讨论过的整数比较操作符对其进行检查。

如果你知道你必须向脚本传递三个选项，例如，你可以这样检查：

```bash
if [ "$#" -ne 3 ]; then
   echo "Sorry, you did not pass the necessary 3 arguments to this script"
fi
```

通常情况下，你会在脚本执行任何其他操作之前进行此测试。

### 检查上一个命令的状态 (`$?`)

在运行一个命令后，确保它执行正常并采取相应的行动是一个非常好的主意。每当在 UNIX 上执行命令时，它在停止运行时都会返回一个退出状态码。shell 会捕获该退出状态码的值并将其存储在特殊变量 `$?` 中。然而，你必须立即检查这个变量，因为一旦执行下一个命令，它就会被重置。此外，不要尝试对 `$?` 变量运行测试；这样做会重置它的值！除非你只想将其打印给用户，否则请先保存到临时变量中。

通常，如果命令执行成功，变量的值为零 (0)，如果执行失败，则为任何非零数字（通常为 1）。

在第一个示例中，我们将尝试在将原始日志文件设置为零长度并压缩副本之前，将日志文件复制到另一个位置：

```bash
cd /adm cp messages.1
STATUS=$?
if [ "$STATUS" -eq 0 ]; then
   compress messages.1 & # Run the compress in the background
else
   echo "not make a copy of the original file"
fi
```

如果上示例中的 `cp` 命令失败，是因为发生了错误，例如文件系统满了，或者磁盘本身真的有问题。并不是所有命令在这种失败情况下都会返回非零值。正如你所看到的，测试命令根据比较是否有效来返回零或一。

```bash
firstname="john" lastname="smith"
[ "$firstname" = "$lastname" ]
echo $? # 这将打印 1，因为它们不相等
[ "$firstname" = "john" ]
echo $? # 这将打印 0，因为它们相等
```

### 使用非冲突的临时文件 (`$$`)

如果你编写了一个许多人认为很有用的脚本，那么可能有许多人会同时运行它。如果这个脚本在运行时需要打开临时文件，你需要采取措施，防止一个脚本副本覆盖另一个同时运行的脚本副本的临时文件。幸运的是，`$$` 变量允许你做到这一点。每当你运行一个脚本时，`$$` 会被设置为该脚本的进程 ID (PID)。

这使得一个脚本的 `$$` 变量不太与同一系统中运行的该脚本的任何副本相同。因此，你可以将此变量作为脚本需要创建的任何临时文件名的一部分。

假设你想编写一个脚本，它接收一个文件，使用 `nl` 命令对其中的每一行进行编号，临时保存该文件的修改版本，然后将临时文件的内容打印到屏幕上：

```bash
if [ "$#" -ne 1 ]; then
   echo "This script wants 1 argument"
   exit
else
   nl $1 > /tmp/$$ # Run the nl command on the file
   cat /tmp/$$ # Print the contents of the temp file to the screen
fi
```

### 将所有参数传递给另一个命令 (`*`)

现在你知道如何使用 `$#` 计算传递给脚本的参数数量，那么如何获取参数本身的列表呢？特殊变量 `$*` 包含了该列表。

如果你想让脚本使用 `ls` 对你在命令行上指定的任何文件进行长列表显示，你可以这样写：

```bash
if [ "$#" -eq 0 ]; then
   echo "This script takes at least one argument"
   exit
fi
listing=`ls -l $`
echo "$listing"
```

如你所见，`ls` 获取了你传递给脚本的所有命令行参数。因此，如果脚本名为 lister，并且你这样运行它：

```bash
./lister core /tmp/test
```

它等同于输入以下内容：

```bash
ls -l core /tmp/test
```





# 结束脚本并设置完成状态 (`exit`)

当你的脚本完成工作并准备终止时，显式地返回一个退出状态比让 shell 猜测退出状态应该是什么样的要好。特别是当你是因为错误条件退出时，这一点尤为重要，因为你想通知任何可能调用你脚本的脚本。通常情况下，如果你的脚本正常退出，给出一个退出状态零 (0) 是很好的，这样任何可能调用你的脚本都可以检查你的退出状态，并确信一切正常。

我们在之前的几个示例中使用过 `exit` 命令，但从未带过参数。你传递给 `exit` 的任何参数将作为你脚本的退出状态。这里有一个简单的示例，展示了如何根据几次测试的结果顺利或非顺利地退出脚本。

```bash
if cp ${filename} ${filename}.1; then
    echo "Compressing ${filename}.1"
    compress ${filename}.1
    cp /dev/null ${filename}
    exit 0      # 噢！顺利退出，任务完成
else
    echo "Could not copy ${filename} to ${filename}.1"
    exit 1      # 哎！非顺利退出
fi
```

# 提供正确的 UNIX 使用错误提示

你可能已经注意到，当你使用错误的数量或错误的类型的参数运行 UNIX 命令时，命令会向你发送一条简短的消息，让你知道它所需的参数数量和顺序。到目前为止的示例，我们只打印了一条消息说输入的信息错误。我们没有给用户关于他应该输入什么的提示。

这里有一个示例，展示了你应该每个脚本第一个测试中放置什么。在这个示例中，脚本的第一部分将文件复制到归档位置，压缩归档文件，然后删除原始文件。它要求你至少提供一个文件名来执行此操作。

```bash
if [ $# -eq 0 ]; then
    echo "Usage: $0 ..."
    echo "Please enter filename(s) to be archived"
    exit 1
fi
```

# 遍历每个命令行参数 (`for`)

你经常会在脚本中有一列表项目，需要对其执行特定的操作。`for` 循环结构可以帮助实现。它的通用格式如下：

```bash
for variable in list-of-items... do
    command
done
```

其中，`variable` 被设置为 `list-of-items` 中的每个值，并且每当 `variable` 变化时都会运行 `command`。

记得我们讨论过 `$1`, `$2`, ... `$9` 变量，我们说明过你只能通过它们引用程序的前九个参数。使用 `for` 循环，你可以访问任意数量的参数。你刚刚知道了 `$*` 变量的用途，所以让我们使用 `for` 循环来打印传入如下运行的脚本的所有命令行参数：

`myscript dog cat horse`

现在 `$*` 应该包含 `dog cat horse`。在 `myscript` 内部代码如下：

```bash
for arg in $* do
    echo $arg
done
```

因此，脚本的输出是每个命令行参数打印在单独的一上：

```
dog
cat
horse
```

让我们用同样的思想写一个脚本，获取命令行给出的所有文件名并对其进行压缩（如果存在）。

```bash
if [ "# -eq 0 ]; then
    echo "This command requires at least one argument"
    echo "$0: filename-to-compress..."
    exit 1
fi
for FILE in $* do
    if [ -f "$FILE" ]; then
        echo "Compressing $FILE now"
        compress $FILE
    else
        echo "Sorry, filename $FILE does not exist"
    fi
done
```

# 调试你的脚本

如果脚本没有按照你的预期运行，或者某个变量似乎没有你认为它应该有的值，你可以做几件事来调试问题。最简单的方法是对 Bourne shell 使用 `-x` 选项。你可以通过修改脚本的第一行使其看起来像这样：

```bash
#!/bin/sh -x
```

或者，你可以直接带 `-x` 选项对你的脚本运行 shell，如下：

`sh -x scriptname`

这两种方法实现相同；shell 被指示逐行打印脚本中的每一行，展开任何变量以显示它们包含的值，并运行任何反引号命令，显示它们的结果。在这样打印每一行之后，它实际上会被执行。这里有一个示例脚本，我们将开启调试模式运行它：

```bash
#!/bin/sh
1.machine=`hostname`
2.identity=`whoami`
```



3. `date=`date``
4. `echo "Hello, today is $date"`
5. `echo "I am logged in as user $identity on machine $machine"`

![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)

开启调试模式运行 `info`：

```bash
sh -x ./info
```

1. + hostname
2. machine=proteon
3. + whoami
4. identity=gmarler
5. + date
6. date=Sat Mar 21 19:22:28 PST 1998
7. + echo Hello, today is Sat Mar 21 19:22:28 PST 1998
8. Hello, today is Sat Mar 21 19:22:28 PST 1998
9. + echo I am logged in as user gmarler on machine proteon
10. I am logged in as user gmarler on machine proteon

### 调试脚本。

1. 脚本的第一行由调试输出的第 1 和 2 行表示。注意，反引号包裹的 `hostname` 命令在第 1 行被标记为加号 (+)，告知你这是一个外部执行的命令。第 2 行显示了结果。变量 `machine` 现在的值为 `proteon`，即机器名称。

2. 脚本的第二行在调试输出的第 3 和 4 行中执行。第 3 行显示正在执行外部命令 `whoami`，第 4 行显示该命令的输出被赋值给变量 `identity`。

3. 脚本的第三行显示在调试输出的第 5 和 6 行中。第 5 行显示正在执行外部命令 `date`，第 6 行显示其输出被赋值给变量 `date`。

4. 脚本的第四行显示在调试输出的第 7 和 8 行中。注意第 7 行展开了 `date` 变量。第 8 行是你即使不以调试模式运行脚本也会看到的输出。

5. 脚本的第五行显示在调试输出的第 9 和 10 行中。第 9 行展开了 `identity` 和 `machine` 变量的值，第 10 行打印了你通常从该脚本看到的输出。你也可以使用 `-xv` 选项，它会产生更详细的脚本输出。另一种更困难或至少更繁琐的调试方法是使用大量的 `echo`，打印你在脚本中设置的变量值（例如传递给脚本的命令行参数），以确保你获取了你认为应该的信息。

### 遍历项目列表 (*)

你可以使用 `for` 手动输入想要遍历的整个项目列表：

```bash
for x in 1 2 3 4 5 do echo $x done
```

你也可以直接在脚本中创建想要遍历的项目列表，或者通过反引号操作符让外部程序为你完成。

### 处理目录中的所有文件

在之前的示例中，我们编写了一个脚本，可以在运行脚本时压缩你指定的文件。你也可以编写一个脚本，获取目录中的所有文件并对它们进行处理（例如压缩），这样你就不需要在命令行上指定任何内容，除非是包含文件的目录。让我们试试这个：

```bash
if [ "$#" -eq 0 ]; then
  echo "This command requires at least one argument"
  echo "$0: directory-containing-files-to-compress ..."
  exit 1
fi
for DIR in $*
do
  if [ ! -d "$DIR" ]; then
    echo "Sorry, directory $DIR does not exist"
    exit 1
  fi
  for FILE in `ls $DIR`
  do
    if [ -d "$FILE" ]; then
      echo "Yikes!, this is a directory"
    else
      echo "Compressing $FILE"
      compress $FILE
    fi
  done
done
```

如你所见，我们不需要测试文件是否存在，因为脚本生成了文件列表。我们只需要确保指定的目录确实存在。我们还需要检查目录是否也包含其他目录。

### 处理目录树中的所有文件

现在我们已经处理了目录中的所有文件，如果目录本身包含另一个目录，以此类推呢？我们可能希望也处理所有子目录中的文件。这里有一个处理这种情况的示例。

#### 处理文件

1. 一如常，开始脚本前确保输入了正确数量的参数。在这种情况下，一个参数就足够了，但它是必须的。

```bash
if [ "$#" -eq 0 ]; then
  echo "This command requires at least one argument"
  echo "$0: directory-containing-files-to-compress ..."
  exit 1
fi
```

2. 现在，获取命令行上提到的每个目录并确保它们确实存在。

```bash
for DIR in $*
do
  if [ ! -d "$DIR" ]; then
    echo "Sorry, directory $DIR does not exist"
    exit 1
  fi
```

3. 我们使用 `find` 命令生成每个目录下的完整文件列表。然后我们可以检查 `find` 返回的每一行，查看它描述的是否文件（它可能描述子目录、符号链接或管道），如果是文件，则对其进行压缩。





```bash
for FILE in `find $DIR -print` do
    if [ -f "$FILE" ]; then
        echo "Compressing $FILE now"
        compress $FILE
    else
        echo "Yikes, This is not a file"
    fi
done
```

# 从项目列表中选择项 (case)

如果你希望脚本能为用户提供一组菜单选项，并根据其响应采取操作，`case` 语句是一种非常方便的实现方法。它的格式如下：

```bash
case value in
    pattern1 )
        command ...
        command;;
    pattern2 )
        command ...
        command;;
    ...
    patternx )
        command ...
        command;;
esac
```

其中 `value` 是任何将与模式 `pattern[1], pattern[2], ..., pattern^x` 进行比较的文本字符串。匹配到 `value` 的第一个模式之后的 `command` 列表将被执行。通常会使用一个全捕模式（如 `*`）作为最后一个模式，用以捕获任何未预料到的或用户输入错误的内容。请注意每个模式部分的最后一个命令后必须使用双分号（`;`）。不要忘记这些；否则，你执行的命令将比预期的多！

下面的示例涵盖了一个允许你压缩、详细列出或删除文件的脚本。

### 压缩、列出或删除文件

1. 首先，你需要打印出菜单供用户选择。注意使用 `\c` 字符以确保抑制换行，光标将停留在冒号后等待输入。
```bash
echo "What would you like to do:
1. Compress a file
2. Do a long listing of a file
3. Delete a file
select one of the above (1-3): \c"
```

2. 现在你可以在用户输入后读取其选择，并将其传递 `case` 语句。
```bash
read selection
case "$selection" in
```

3. 现在你已经有了他的选择，`case` 语句将涵盖每种情况。第一个是要选择压缩的文件。你会提示文件名，确保它确实存在，然后对其压缩。
```bash
1)  echo "Enter filename to compress: \c"
    read filename
    if [ -f "$filename" ]; then
        compress $filename
    else
        echo "Bad filename"
    fi;;
```

4. 第二种可能的选择是对文件执行详细列出。同样地提示文件名，确保它存在，然后执行列出。
```bash
2)  echo "Enter filename to list: \c"
    read filename
    if [ -f "$filename" ]; then
        ls -l $filename
    else
        echo "Bad filename"
    fi;;
```

5. 现在是第三个要删除的文件。你提示文件名，确保它存在，然后将其删除。
```bash
3)  echo "Enter filename to delete: \c"
    read filename
    if [ -f "$filename" ]; then
        rm $filename
    else
        echo "Bad filename"
    fi;;
```

6. 最后，你想要执行全捕操作，并将其报告为菜单中的错误选择。然后结束 `case` 语句。
```bash
*)  echo "Incorrect selection";
esac
```

# 第 26 章编写 awk 脚本
作者 David B. Horvath, CCP

## 何时使用 awk

## awk 的特性
### 基础
### 动作 (Actions)
### 高级输入与输出
### 函数
### 编写报告
### 瞬时命令



`awk` 有多个版本：原始的 `awk`、`nawk`、`POSIX awk` 和 `gawk` (GNU awk)。`nawk` 创建于 1985 年，是 *The awk Programming Language* 一书中描述的版本（参见本章末尾“总结”部分对该书的完整引用）。`POSIX awk` 定义在《信息技术标准，可移植操作系统接口第 2 部分：Shell 和工具第 2 》中，该标准由 ANSI 于 1993 年 4 月 5 日批准（IEEE 是电气与电子工程师协会）。`gawk` 基于 `POSIX awk`。

`GNU` 缩写代表 `GNU is Not UNIX`（GNU 不是 UNIX）。它是一系列在 UNIX 环境中常见的有用软件包的名称，由 MIT 的 GNU 项目分发。这些软件包通常是免费的，可以在互联网的各个地方获取（如果你想在软磁盘或磁带等物理介质上获取副本，则需要支付费用）。这些软件包的开发是一个协作过程，由许多志愿者完成。这项工作在很大程度上由 Richard M. Stallman（`emacs` 编辑器的开发者之一）领导。

### 什么是 awk
`awk` 语言（所有版本）是一种功能强大的模式匹配和处理语言。它会搜索文件（或多个文件）中匹配指定模式的记录。当找到匹配项时，会执行指定的动作。作为程序员，你不需要担心打开文件、循环文件、读取每条记录、处理文件结束符或在完成后关闭文件。这些细节都会自动为你处理。创建一个简短的 `awk` 程序很容易，因为许多细节都由语言自动处理了。它还有许多用于处理文件的功能。

### 何时使用 awk
`awk` 有许多可能的用途，包括从文件中提取数据、统计文件中的出现次数以及创建报告。`awk` 语言的基本语法与 `C` 编程语言匹配；如果你已经熟悉 `C`，你就熟悉了大部分 `awk`。在很多方面，`awk` 是 `C` 的更简单版本，因为它处理字符串和数组的方式是（动态的）。如果你还不认识 `C`，学习 `awk` 会让学习 `C` 变得稍微容易。`awk` 对于快速原型设计或尝试将要在 `C` 等其他语言实现的想法也非常有用。你不需要担心一些细微的细节，内置的自动化功能会处理它们。你只需要关注基本功能。

### 何时不使用 awk
`awk` 适用于文本文件，而不是二进制文件。因为二进制数据可能包含像记录终止符（换行符）的值，或者完全没有，`awk` 会产生困惑。如果你需要处理二进制文件，请查看 `Perl` 或使用传统的编程语言如 `C`。

### awk 的特性
作为 UNIX 环境的一部分，`awk` 非常灵活，包含预定义变量、自动化许多编程任务、提供常规变量、支持 C 格式输出并且易于使用。它允许你结合 shell 脚本和 C 编程的优处。

### awk 中的变量
在 `awk` 中通常有许多不同的方法来完成同一个任务。程序员可以决定哪种方法最适合他们的应用程序。通过内置变量和函数，许多常规编程任务会自动执行。`awk` 会自动读取每条记录，将其拆分为字段并在需要时进行类型转换。变量的使用方式决定了它的类型；不需要（也没有方法）声明任何类型的变量。当然，`awk` 支持标准的 `C` 编程结构，如 `if/else`、`do/while`、`for` 和 `while`。`awk` 不支持 `switch/case` 结构。它支持用于格式化输出的 `C printf()`，还有一个用于简单输出的 `print` 命令。

### awk 基础
与其他 UNIX 工具（`shell`、`grep` 等）不同，`awk` 需要一个程序（称为 `awk` 脚本）。这个程序可以简单到一行，也可以复杂到几千行（我曾开发过一个 `awk` 程序，可以在多个层级通过多个控制断点总结数据；它差差 1000 行）。



`awk` 程序可以通过多种方式在命令行或程序文件中输入。`awk` 可以接受来自文件的输入、从另一个程序的管道的输入，甚至可以直接从键盘输入。输出通常发送到标准输出设备，但可以将其重定向到文件或管道到另一个程序。输出也可以直接发送到文件，而不是标准输出。

## 从命令行使用 awk

使用 `awk` 最简单的方法是在命令行上编写程序，接受来自标准输入设备（键盘）的输入，并将输出发送到标准输出设备（屏幕）。列表 26.1 显示了这种最简单的形式；它会打印输入记录中的字段数量以及该记录本身。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 关于列表 26.1 及其他的一些说明

`Ctrl+D` 是显示你应该按下（并按住）`Ctrl`（或 Control）键然后按下 `D` 的一种方式。这是 UNIX 的默认文件结束键。如果这在你的系统上不起作用，请使用 `stty -a` 来确定应该按哪个键。该操作或键在屏幕上的另一种显示是 `^d`。

整个 `awk` 脚本包含在单引号 `' '` 中，以防止 shell 解释其内容。这是操作系统或 shell 的要求，而不是 `awk` 语言的要求。

#### 列表 26.1 awk 最简单的用法。

```awk
awk '{print NF ":$0}'
```
6: Now is the time for all
7: Good Americans to come to the Aid
3: of Their Country.
不要问你能为 awk 做什么，而要问 awk 能为你做什么。
16: 不要问你能为 awk 做什么，而要问 awk 能为你做什么。

#### 如何运行本章中的示例

所有示例将展示如何作为实现 `awk` 语言的 UNIX 命令使用 `awk`。你的机器可能同时拥有 `awk` 和 `nawk`，仅有 `awk` 命令（实现旧的 `awk`、`nawk`、`POSIXawk` 甚至 `gawk`），或者只有 `gawk`。你必须使用适用于你机器的命令。

`NF` 是预定义变量，设置为每条记录的字段数。`$0` 是该记录。单个字段可以引用为 `$1`、`$2` 等。

你也可以将 `awk` 脚本存储在文件中，并通过 `-f` 标志在命令行上指定该文件名。如果你这样做，就不需要将程序包含在单引号中。

`gawk` 以及其他符合 POSIX 标准的 `awk` 版本通过使用多个 `-f` 选项支持指定多个程序。这允许你对同一份输入执行多个 `awk` 程序。个人而言，我倾向于避免这样做，因为这会变得有点混乱。

```bash
$
```
```bash
awk '{print NF ":$0}' < inputs
```

可以通过直接在命令行上列出多个文件来指定，它们将按照指定的顺序进行处理。输出可以通过正常的 shell 功能重定向以发送到文件或管道到另一个程序：

```bash
awk '{print NF ":$0}' > outputs | more
```

当然，输入和输出可以同时进行重定向。

### 脚本命名

我倾向于用 `.awk` 文件类型（后缀）保存我的 `awk` 脚本，以便在查看目录列表时一目了然。我最常用的使用 `awk` 的方式之一是通过将另一个命令的输出管道到 `awk` 来处理其输出。如果我想创建一个包含文件名和权限的自定义文件列表，我会执行这样的命令：





```bash
ls -l | awk '{print $NF, " ", $1}'
```

`$NF` 是最后一个字段（即文件名，我偷懒了不想数字段个数来确定它的数字）。`$1` 是第一个字段。`ls -l` 的输出被传递给 `awk`，由它为我进行处理。

输入 `awk` 命令时请要小心。

如果你在程序文件名之前忘记了 `-f` 选项，你的程序将被视为数据。

如果你在命令行中编写 `awk` 程序，但将其置于数据文件名之后，它也将被视为数据。

如果我将 `awk` 脚本放入一个文件（命名为 `lser.awk`）并将其输出重定向到打印机，我将得到如下所示命令：

```bash
ls -l | awk -f lser.awk | lp
```

请参本章稍后的“实时执行”（On-the-Fly）章节，获取更多使用 `awk` 脚本处理管道数据的示例。

## 处理（模式与动作）

每个 `awk` 语句由两部分组成：模式（pattern）和动作（action）。模式决定了何时执行动作，当然，动作是程序员希望发生的行为。如果没有模式，动作将始终执行（该模式可以被认为默认为真）。

有两个特殊的模式（也称为块）：`BEGIN` 和 `END`。`BEGIN` 代码在从文件中读取第一条记录之前执行，用于初始化变量和设置如控制断点等内容。`END` 代码在到达文件末尾后执行，用于任何清理工作（例如在报告中打印最终总计）。其他模式则对从文件中读取的每条记录进行测试。

通用的程序格式是将 `BEGIN` 块放在顶部，紧接着是任何模式/动作对，最后将 `END` 块放在末尾。这并不是语言的要求，这只是大多数人的习惯做法（主要是为了可读性考虑）。

### 使用 BEGIN 和 END 的贴士

`BEGIN` 和 `END` 块是可选的；如果你使用它们，每个最多一个。不要编写两个 `BEGIN` 块，也不编写两个 `END` 块。

动作包含在大括号（`{ }`）中，可以由一个或多个语句组成。如果你省略模式部分，它将默认为真，这会导致对文件的每一行都执行动作。如果你省略动作，它将默认为 `$0`（打印整个记录）。

模式在动作之前指定。它可以是一个正则表达式（包含在一对斜杠 `/` 之间），用于匹配输入记录的一部分，也可以是一个包含比较运算符的表达式。它也可以是由表达式和正则表达式组合而成的复合或复杂模式、范围模式。

## 正则表达式

`awk` 使用的正则表达式与 `grep`、`egrep` 以及 UNIX 编辑器 `ed`、`ex` 和 `vi` 使用的相似。它们是用于指定和匹配字符串的符号。正则表达式由字符（如字母 `A`、`B` 或 `c`）组成，这些字符在输入中匹配自身，还包括元字符。元字符是具有特殊（元）含义的字符；它们不匹配自身，而是执行某些特殊功能。表 26.1 显示了元字符及其行为。

#### awk 中的正则表达式元字符

| 元字符 | 含义 |
| :--- | :--- |
| `\` | 转义序列（下一个字符具有特殊含义，`\n` 是换行符，`\t` 是制表符）。任何被转义的元字符将匹配到该字符（仿佛它不是元字符）。 |
| `^` | 匹配字符串的开头。 |
| `$` | 匹配字符串末尾。 |
| `.` | 匹配任意单个字符。 |
| `[ABC]` | 匹配 A、B 或 C 中的任意一个。 |
| `[A-Ca-c]` | 匹配 A、B、C、a、b 或 c 中的任意一个（范围）。 |
| `[^ABC]` | 匹配 A、B、C 以外的任何字符。 |
| `Desk\|Chair` | 匹配 Desk 或 Chair 中的任意一个。 |
| `[ABC][DEF]` | 拼接。匹配 A、B 或 C 中的任意一个，后面紧跟 D、E 或 F 中的任意一个。 |
| `*` | `[ABC]*` 匹配 A、B 或 C 的零次或多次出现。 |
| `+` | `[ABC]+` 匹配 A、B 或 C 的一次或多次出现。 |
| `?` | `[ABC]?` 匹配空字符串或 A、B 或 C 中的任意一个。 |
| `()` | 组合正则表达式。例如，`(Blue\|Black)berry` 匹配 Blueberry 或 Blackberry。 |





# 尝试组合

所有这些模式都可以组合形成复杂的搜索字符串。

典型的搜索字符串可以用于搜索特定的字符串（例如 `Report Date`）、不同格式的字符串（例如五月的不同拼写方式，如 `may`、`MAY`、`May`），或作为字符组（任何拼出五月月份的大写和小写字母组合）。这些看起来如下所示：

```awk
/Report Date/ { print "something" } /(may)(MAY)(May)/ { print "something else" } /[Mm][Aa][Yy]/ { print "something completely different" }
```

## 比较运算符与模式

awk 使用的比较运算符与 C 语言和 UNIX Shell 中的运算符相似。它们是用于指定和比较值（包括字符串）的记法。单靠正则表达式将匹配输入记录的任何部分。通过将比较操作与正则表达式相结合，可以对特定字段进行测试。

表 26.2 显示了比较运算符及其行为。

### 表 26.2 awk 中的比较运算符。

| 运算符 | 含义 |
| :--- | :--- |
| `==` | 等于 |
| `<` | 小于 |
| `>` | 大于 |
| `<=` | 小于或等于 |
| `>=` | 大于或等于 |
| `!=` | 不等于 |
| `~` | 匹配正则表达式 |
| `!~` | 不匹配正则表达式 |

使用比较运算符可以允许你对字段执行特定的比较，而不是针对整个记录。记住，你也可以使用 `$0` 而不是特定字段对整个记录执行操作。典型的搜索字符串可以用于搜索第一个字段中的名称（`Bob`）并用正则表达式与特定字段比较：

```awk
$1 == "Bob" { print "Bob stuff" } $2 ~ /(may)(MAY)(May)/ { print "May stuff" } $3 !~ /[Mm][Aa][Yy]/ { print "other May stuff" }
```

## 复合模式运算符

awk 使用的复合模式运算符与 C 语言和 UNIX Shell 中的运算符相似。它们是将其他模式（表达式或正则表达式）组合成复杂逻辑形式的记法。

表 26.3 显示了复合模式运算符及其行为。

### 表 26.3 awk 中的复合模式运算符。

| 运算符 | 含义 |
| :--- | :--- |
| `&&` | 逻辑与 |
| `\|` | 逻辑或 |
| `!` | 逻辑非 |
| `()` | 用于分组复合语句的括号 |

如果你想执行某些操作（例如，如果第一个字段包含值 `Bob` 且第四字段包含值 `Street`），你可以使用如下所示的复合模式：

```awk
$1 == "Bob" && $4 == "Street" {print "message"}
```

## 范围运算符

范围模式比类型类型复杂：它在第一个模式被匹配时设置为真，并直到第二个模式变为真为止保持为真。关键在于文件需要按照范围模式匹配的字段进行排序。否则，它可能会过早设置为真或提前结束。范围模式中的各个模式由逗号（（`,`）分隔。如果你目录中有 A 到 Z 命名的 26 个文件，你可以像列表 26.2 所示显示文件的范围。

```bash
ls | awk '$1 == "B", $1 == "D"'
B C D
ls | awk '$1 == "B", $1 <= "D"'
B ... continues
```

### 列表 26.2 续。

```bash
ls | awk '$1 == "B", $1 > "D"'
B C D E _
```

第一个示例显而易见——显示了 B 和 D 之间所有的记录。其他示例不那么直观，但要记住的关键是模式在第二个条件为真时完成。第二个 `awk` 命令只显示 B，是因为 C 小于或等于 `D`（使得第二个条件为真）。第三个 `awk` 显示从 B 到 E，因为 E 是第一个大于 `D` 的项（使得第二个条件为真）。

## 处理输入




当 `awk` 读取每条记录时，它将其分解为字段，然后搜索匹配的模式以及要执行的相关操作。它假设每条记录占据一行（根据定义，换行符表示记录的结束）。仅包含空白或空（仅有换行符）的行也被视为记录，只是字段非常少（通常为零）。

### 流程控制
你可以使用 `next` 语句强制 `awk` 读取文件的下一条记录（停止搜索模式匹配）。`next` 类似于 C 语言中的 `continue` 命令，控制权返回到最外层循环。在 `awk` 中，最外层循环是自动读取文件。如果你决定完全退出程序，可以使用 `exit` 语句。`exit` 的作用就像到达了文件末尾，并将控制权传递给 `END` 块（如果存在）。如果 `exit` 位于 `END` 块中，程序将立即退出。

### 字段分隔符
默认情况下，字段由空格分隔。对于 `awk` 来说，有一个空格还是多个空格都并不重要；当发现第一个非字符时，下一个字段便开始。你可以通过将变量 `FS` 设置为该字符来更改字段分隔符。要将字段分隔符设置为冒号（`:`），即 `/etc/passwd` 中的分隔符，请编写以下代码：

```awk
BEGIN { FS = ":" }
```

文件的通用格式如下：
```text
david:!:207:1017:David B Horvath,CCP:/u/david:/bin/ksh
```

如果你想列出系统中所有人的姓名，请使用以下：
```bash
gawk --field-separator=: '{ print $5 }' /etc/passwd
```
你将看到所有人的名字列表。在这个示例中，我通过 `gawk` 命令行选项（`--field-separator=`）在命令行设置了字段分隔符变量（`FS`）。我也可以使用 `-F :`，所有版本的 `awk` 都支持它。

第一个字段是 `$1`，第二个是 `$2`，依此类推。整条记录包含在 `$0` 中。你可以通过引用 `$NF` 获取最后一个字段（如果你懒得数的话）。`NF` 是记录中的字段数量。

### 编写你的程序
`awk` 的妙之处在于，除少数例外外，它像 C 语言一样是自由格式。空行会被忽略。语句可以放在同一行，也可以按你喜欢的任何形式拆。`awk` 识别空白字符，就像 C 一样。以下两行本质上是相同的：

```awk
$1=="Bob"{print"stuff"}
$1 == "Bob" { print "stuff"}
```

引号内的空格是有意义，因为它们将出现在输出中或用于比较。其他空格则没有。你也可以拆分操作（但你必须将左大括号与模式放在同一行）：

```awk
$1 == "Bob" { print "stuff" }
```

你可以在操作中包含多个语句。如果你将它们放在同一行，则需要使用分号（`;`）来分隔它们（这样 `awk` 就能判断一个语句何时结束，另一个何时开始）。打印多行看起来所示：

```awk
$1 == "Bob" { print "Bob stuff"; print "more stuff"; print "last stuff"; }
```

你也可以将语句放在不同的行上。当你这样做时，就不需要编写分号，代码看起来如下：

```awk
$1 == "Bob" {
    print "Bob stuff"
    print "more stuff"
    print "last stuff"
}
```

### 注释
充分利用注释。行中井号（`#`）之后的任何内容都会被 `awk` 忽略。这些是为程序员阅读设计并帮助理解程序代码的注释；通常，程序中放置的注释越多，越容易维护。

个人而言，我习惯在每个语句后编写分号，因为我在 C 语言中必须这样做。对于 `awk` 来说，下面的示例与上一个相同（但你可以看到分号）：

```awk
$1 == "Bob" {
    print "Bob stuff";
    print "more stuff";
    print "last stuff";
}
```

### 操作
程序的操作是告诉 `awk` 在匹配到模式时执行什么部分。如果没有模式，它默认为真。没有操作的模式默认为 `{print $0}`。




# Actions
所有动作都包含在花括号 (`{ }`) 之中。左大括号应该与模式出现在同一行；除此之外外，没有其他限制。一个动作由一个或多个动作组成。

# 变量
除了简单的查找和打印类程序外，你将需要保存数据。这是通过使用变量来实现的。在 `awk` 中，有三种变量：字段变量、预定义变量和用户定义变量。你已经见过前两种的示例：`$1` 是包含输入记录中第一个字段的字段变量，而 `FS` 是包含字段分隔符的预定义变量。

### 用户定义变量
用户定义变量是你创建的变量与其他许多许多语言不同，`awk` 不需要要求你在在使用变量之前对其进行定义或声明。在 `C` 中，你必须声明变量所包含的数据类型（如 `int`、`float`、`char` 等）。在 `awk` 中，你只需使用该变量。`awk` 会尝试根据变量的使用方式来确定变量中的数据。如果你在变量中放入字符数据，它会被视为字符串；如果你放入数字，它会被视为数值。

`awk` 还会在数据类型之间进行转换。如果你在变量中放入字符串 `123` 稍后对其进行计算，它将被视为数字。这种做法的危险在于，当你对字符串 `abc` 进行计算时会发生什么？`awk` 会尝试将字符串转换为数字，得到转换错误，并将该值视为数值零！这种逻辑错误可能很难调试。

```awk
BEGIN {total = 0.0; loop = 0; first_time = "yes";}
```

忘记像这样在 `BEGIN` 动作中初始化你的变量。像 `C` 语言一样，`awk` 要求变量以字母或下划线开头。字母可以是大写也可以是小写。变量名的其余部分由字母、数字或下划线组成。对于你自己以及任何在你离开后需要维护代码的人来说，让变量名具有意义且具有描述性会很好。虽然你可以将变量名全部写为大写，但这是一个坏习惯，因为预定义变量（如 `NF` 或 `FS`）是大大写的。将预定义变量输入为小写（例如 `nf` 或 `fs`）是一个常见的错误；`awk` 不会产生任何错误，这个错误可能很难调试。变量的行为将与正确的拼写不同，你将得预期的期的。

# 预定义变量
`awk` 提供了若干预定义（也称为内置）变量。这些变量用于为你的程序提供有用数据；它们也可以用于通过将它们设置为特定值来更改 `awk` 的默认行为。表 26.4 总结了 `awk` 中的预定义变量。早期版本的 `awk` 不支持所有的变量。

### 表 26.4 awk 预定义变量
| 变量 | 含义 | 默认值（如果有） |
| :--- | :--- | :--- |
| `ARGC` | 命令行参数的数量 | |
| `ARGIND` | 当前处理文件在 `ARGV` 中的索引 | |
| `ARGV` | 命令行参数数组 | |
| `CONVFMT` | 数字的转换格式 | `%.6g` |
| `ENVIRON` | UNIX 环境变量 | |
| `ERRNO` | UNIX 系统错误消息 | |
| `FIELDWIDTHS` | 以空格分隔的输入字段宽度字符串 | |
| `FILENAME` | 当前输入文件的名称 | |
| `FNR` | 当前记录数 | |
| `FS` | 输入字段分隔符 | 空格 |
| `IGNORECASE` | 控制大小写敏感性 | 0 |
| `NF` | 记录中的字段数 | |
| `NR` | 读取的记录数 | |
| `OFMT` | 数字的输出格式 | `%.6g` |
| `OFS` | 输出字段分隔符 | 空格 |
| `ORS` | 输出记录分隔符 | 换行 |
| `RS` | 输入记录分隔符 | 换行 |
| `RSTART` | match 函数匹配的字符串的起始位置 | |
| `RLENGTH` | match 函数匹配的字符串长度 | |
| `SUBSEP` | 下标分隔符 | `\034` |

`V` 是支持变量的第一个实现。`A` = `awk`，`N` = `nawk`，`P` = `POSIX awk`，`G` = `gawk`。

`ARGC` 变量包含传递给程序的命令行参数数量。`ARGV` 是一个包含 `ARGC` 个元素的数组，包含命令行参数本身。第一个是 `ARGV[0]`，最后一个是 `ARGV[ARGC-1]`。`ARGV[0]` 包含正在执行的命令名称 (`awk`）。`awk` 命令行选项不会出现在 `ARGV` 中——它们由 `awk` 自身解释。





数字的默认转换（输入）格式存储在 `CONVFMT`（转换格式）中，默认格式字符串为 `%.6g`。有关格式字符串含义的更多信息请参见标题为 `printf` 的章节。

`ENVIRON` 变量是一个数组，包含了为你的 UNIX 会话定义的环境变量。下标是你想要获取值的环境变量的名称。

如果你想让程序根据环境变量中的值执行特定的代码，可以使用以下语句：

```awk
ENVIRON["TERM"] == "vt100" {print "Working on a Video Tube!"}
```

如果你正在使用 VT100 终端，你将获得消息 `Working on a Video Tube!`。请注意，只有在你使用字面量时，才在环境变量周围加上双引号。如果你有一个名为 `TERM` 且其包含字符串 `TERM` 的变量，则应省略双引号。

如果在在重定向、读取或关闭文件期间发生系统错误，`ERRNO` 变量将包含相应的 UNIX 系统错误信息。

`FIELDWIDTHS` 变量提供了一种固定长度字段的功能，而不是使用字段分隔符。要指定字段的大小，你可以将 `FIELDWIDTHS` 设置为一个字符串，该字符串包含由空格或制表符分隔的每个字段的。设置此变量后，`gawk` 将根据指定的宽度拆分输入记录。要恢复使用字段分隔符，可以给 `FS` 赋一个新值。

`FILENAME` 变量包含当前输入文件的名称。由于命令行上可以指定不同的（甚至是多个）文件，这为你提供了确定正在处理哪个输入文件的方法。

`FNR` 变量包含当前记录在当前输入文件中的行数。它会在命令行指定的每个文件被重置。它包含的值始终小于或等于变量 `NR`。

用于分隔字段的字符存储在变量 `FS` 中，默认值是空格。你可以通过命令行选项或在程序内部更改此变量。如果你知道你的文件将使用空格以外的某个字符作为字段分隔符（例如使用冒号的 `/etc/passwd` 文件），你可以在程序中使用 `BEGIN` 模式来指定它。

你可以通过 `IGNORECASE` 变量控制 gawk 正则表达式的大小敏感性。当设置为默认值 0 时，模式匹配会检查正则表达式中的大小写。如果你将其设置为非零值，则会忽略大小写（字母 `A` 将匹配字母 `a`）。

`NF` 变量在每个记录被读取后被设置，包含字段的数量。字段由 `FS` 或 `FIELDWIDTHS` 变量决定。

`NR` 变量包含读取的记录总数。它永远不会小于 `FNR`，`FNR` 在每个文件会被重置为零。

数字的默认输出格式存储在 `OFMT` 中，默认格式字符串为 `%.6g`。有关格式字符串含义的更多信息请参见标题为 `printf` 的章节。

输出字段分隔符包含在 `OFS` 中，默认值是空格。当你在 `print` 语句中使用逗号时，就会输出这个字符或字符串，例如如下所示：

```awk
print $1, $2, $3;
```

该语句打印文件的前三个字段，并用空格隔开。如果你想用冒号分隔它们（例如对于 `/etc/passwd` 文件），只需将 `OFS` 设置为新值即可：`OFS=":"`。

你可以通过将 `ORS` 设置为新值来更改输出记录分隔符。`ORS` 默认值为换行符（`\n`）。

`match()` 函数调用匹配的任何字符串的长度存储在 `RLENGTH` 中。它与预定义变量 `RSTART` 配合使用以提取匹配字符串。

你可以通过将 `RS` 设置为新值来更改输入分隔符。`RS` 默认值为换行符。

更改输入字段（`$1`、`$2` 等）或输入记录（`$0`）会导致其他预定义变量发生变化。如果你原始输入记录有两个字段而你设置了 `$3="third one"`，那么 `NF` 将从 2 变为 3。

`SUBSEP` 变量包含用于分隔多维数组下标的值。默认值为 `\034`，即双引号字符（`"`）。

### 字符串





`awk` 支持两种通用类型的变量：数值型（可以由字符 0 到 9、`+` 或 `-` 以及小数点 `.` 组成）和字符型（可以包含任何字符）。包含字符的变量通常被称为字符串。字符字符串可以包含有效数字、单词等文本，甚至可以是格式化的电话号码。如果字符串包含有效数字，`awk` 可以自动将其转换并像数值变量一样使用；如果你尝试将一个包含格式化电话号码的字符串作为数值变量使用，`awk` 将尝试将其转换并作为包含值为零的数值变量来使用。

### 字符串常量

字符串常量始终包含在双引号 `""` 中，长度可以从零（一个 `empty` 字符串）到多个字符。具体的最大长度随 UNIX 版本而异；就个人而言，我从未达到过这个上限。双引号不会存储在内存中。一个典型的字符串常量可能如下：

```awk
"Using UNIX"
```

#### 在比较中使用字符串常量

在本章之前的章节，你已经看到过字符串常量在比较和 `print` 语句中的用法。

### 字符串运算符

实际上只有一个字符串运算符，那就是连接。你可以通过仅将多个字符串（常量或变量的任意组合）放在在一起来组合它们。列表 26.1 使用 `print` 语句实现了这一点，字符串 `:` 在输入记录（`$0`）之前。列表 26.3 显示了连接字符串的几种方法。

#### 列表 26.3 连接字符串。

```awk
BEGIN{x="abc"; y="ghi"; z=x y; z2="A"x"y"C"; print x, y, z, z2}
```
变量 `x` 设置为两个连接字符串；打印结果为 `abcdef`。变量 `y` 设置为一个字符串供变量 `z` 使用。变量 `z` 是两个变量的连接，打印为 `abcdefghi`。最后，变量 `z2` 显示了字符串常量和变量的连接，打印为 `AabcdefghiC`。如果你在 `print` 语句中省略逗号，所有字符串将连接在一起，如下所示：

```awk
abcdefabcdefghiAabcdefghiC
```

### 内置字符串函数

除了这一个字符串操作（连接）之外，`awk` 还提供了许多处理字符串的函数。表 26.5 总结了 `awk` 中的内置字符串函数。早期版本的 `awk` 不支持所有这些函数。

#### 表 26.5 *awk* 内置字符串函数。

| 函数 | 用途 |
| :--- | :--- |
| `gsub(*reg*, *string*, *target*)` | 每当匹配到正则表达式 `reg` 时，就替换 `target` 字符串中的 `string` |
| `index(*search*, *string*)` | 返回 `search` 字符串在 `string` 中的位置 |
| `length(*string*)` | `string` 中字符的数量 |
| `match(*string*, *reg*)` | 返回 `string` 中匹配正则表达式 `reg` 的位置 |
| `printf(*format*, *variables*)` | 根据 `format` 写入格式化数据；`variables` 是你想要的数据 |
| `split(*string*, *store*, *delim*)` | 根据分隔符 `delim` 将 `string` 拆分为 `store` 中的元素 |
| `sprintf(*format*, *variables*)` | 根据 `format` 返回一个包含格式化数据的字符串；`variables` 是你想要在字符串中的数据 |
| ` `(*format*, *timestamp*)` | 根据 `format` 返回格式化的日期或时间字符串；`timestamp` 是由 `systime()` 函数返回的时间 |
| `sub(*reg*, *string*, *target*)` | 在第一次匹配到正则表达式 `reg` 时，替换 `target` 中的 `string` |
| `substr(*string*, *position*, *len*)` | 返回从 `position` 开始长度为 `len` 个字符的子字符串 |
| `tolower(*string*)` | 返回 `string` 中的字符的等小写形式 |
| `toupper(*string*)` | 返回 `string` 中的字符的等大写形式 |

`V` 是第一个支持变量的实现。`A` = `awk`，`N` = `nawk`，`P` = `POSIX awk`，以及 `G` = `gawk`。





## Awk 函数

`index(search, string)` 函数返回 `search` 字符串在 `string` 中首次出现的位置（从左侧计数）。如果省略了 `string`，则返回 0。

`length(string)` 函数返回 `string` 中字符的计数。`awk` 在内部跟踪字符串的长度。

`match(string, reg)` 函数确定 `string` 是否包含由 `reg` 定义的字符集。如果匹配，则返回匹配的位置，并设置变量 `RSTART` 和 `RLENATH`。

`printf(format, variables)` 函数根据 `format` 字符串将 `variables` 转换并写入格式化数据。该函数与 C 语言中的 `printf()` 函数非常相似。关于此函数和格式字符串的更多信息，请参阅本章后面标题为 `printf` 的节。

`split(string, store, delim)` 函数根据 `delim` 字符串将 `string` 分拆为数组 `store` 中的元素。返回 `store` 中元素的数量。如果省略了 `delim` 字符串，则使用 `FS`。要将一个由斜杠（/）分隔的日期拆分为其组成部分，请编写以下代码：

```bash
split("08/12/1962", results, "/")
```

函数调用后，`results[1]` 包含 08，`results[2]` 包含 12，`results[3]` 包含 1962。与 `split` 函数使用时，数组从第一个元素开始。这同样适用于包含文本的字符串。

`sprintf(format, variables)` 函数的行为与 `printf` 函数相似，但它返回结果字符串而不是写入输出。它根据 `format` 字符串将 `variables` 转换并产生格式化数据。该函数与 C 语言中的 `sprintf()` 函数非常相似。关于此函数和格式字符串的更多信息，请参阅本章后面标题为 `printf` 的节。

`strftime(format, timestamp)` 函数根据 `format` 字符串返回格式化的日期或时间；`timestamp` 是自 1970 年 1 月 1 日午夜以来的秒数。`systime` 函数返回这种形式的值。格式与 C 语言的 `strftime()` 函数相同。

`sub(reg, string, target)` 函数允许你用另一组字符替换 `string` 中第一次出现的另一个字符（以正则表达式 `reg` 的形式定义）。该函数返回替换的次数。如果省略了 `target`，则输入记录 `$0` 为目标。这模仿了 `ed` 编辑器中的 `substitute` 命令。

`substr(string, position, len)` 函数允许你根据起始位置 `position` 和长度 `len` 提取子字符串。如果省略 `len` 参数，则返回剩余字符串。

`tolower(string)` 函数将 `string` 中的大写字母转换为小写返回。任何其他字符将直接返回，不进行任何转换。

`toupper(string)` 函数将 `string` 中的小写字母转换为大写返回。任何其他字符将直接返回，不进行任何转换。

## 特殊字符串常量

`awk` 支持从键盘输入或具有特殊含义的特殊字符串常量。如果你想让双引号（"）作为一个字符串常量（`x = "\""`），如何防止 `awk` 认为第二个（你真正想要的那个）是字符串的结束？答案是使用转义，或者告诉 `awk` 下一个字符具有特殊含义。这是通过与 UNIX 其他部分相同的反斜杠（\）字符实现的。表 26.6 显示了 `awk` 支持的大多数常量。

### 表 26.6 awk 特殊字符串常量

| 表达式 | 意义 |
| :--- | :--- |
| `\\` | 包含反斜杠的意思 |
| `\a` | 警报或铃声字符 |
| `\b` | 退格 |
| `\f` | 换页 |
| `\n` | 换行符 |
| `\r` | 回车 |
| `\t` | 制表符 |
| `\v` | 垂直制表符 |
| `\"` | 双引号 |
| `\xNN` | 表示 `NN` 是十六进制数 |
| `\0NNN` | 表示 `NNN` 是八进制数 |

## 数组

当你有多个相关数据时，你有两个选择：创建多个变量，或者使用数组。数组允许你将一组相关数据保留在一起。你通过在方括号（[]）中包含下标来访问数组中的单个元素。通常，你可以在任何可以使用普通变量的地方使用数组元素。`awk` 中的数组具有大多数其他语言缺乏的特殊能力：它们是动态的；稀疏的；而且下标实际上是字符串。你不需要声明一个变量为数组，也不需要在第一次使用元素时定义最大元素数量，它是动态创建的。因为这样，最初不会分配内存块；在标准的编程实践中，如果你想累积一年中每月的额，将分配 12 个元素，即使你目前只处理十二月。`awk` 数组是稀疏的；如果你正在处理十二月，那么只有该元素会存在，而其他 11 个（空）月份不存在。





根据我的经验，最后一种能力是最用的：下标可以是字符串。在大多数编程语言中，如果你想根据字符串累积数据（例如按州或国家计算销售总额），你需要两个数组：州或国家名称（字符串）和数值销售数组。你需要搜索州或国家名称以找到匹配项，然后使用销售数组中的相同元素。`awk` 会替你完成这些工作。你可以使用州或国家名称作为下标在销售数组中创建一个元素，并像下面一样直接访问：

```
total_sales["Pennsylvania"] = 10.15
```

然而，`awk` 并不直接支持多维数组。

## 数组函数

从 `nawk` 开始的 `awk` 版本提供了几个专门用于数组的函数：`in` 和 `delete`。`in` 函数测试元素是否在数组中。`delete` 函数用于从数组中删除元素。

如果你有一个以州为下标的数组，并想确定某个州是否在列表中，可以将以下内容放入条件测试中（关于条件测试的更多信息，请参见“条件流”章节）：

```
"Delaware" in total_sales
```

你还可以在循环中使用 `in` 函数来遍历数组中的元素（特别是当数组是稀疏或关联数组时）。这是 `for` 循环的一种特殊情况，在 `for` 语句章节中有描述。

要删除数组元素（例如特拉华州），你可以编写以下代码：

```bash
delete total_sales["Delaware"]
```

当数组元素被删除时，它已从内存中移除。该数据将不再可用。在完成对元素的使用后，删除数组元素或整个数组是一个良好的习惯。虽然内存很便宜且容量充足（特别是使用虚拟内存的情况下），但如果不清理，你最终会耗尽内存。

你不能一条语句删除数组中的所有元素。你必须遍历所有元素并逐个删除。你不能直接删除整个数组；以下操作是无效：

```
delete total_sales
```

## 多维数组

尽管 `awk` 不直接支持多维数组，但它提供了一种模拟这些数组的机制。对于程序员来说，这种区别非常微不足道。你可以以 C 程序员熟悉的格式（方括号内）指定多个维度：

```
array[5,3] = "Mary"
```

这被存储在一个单维数组中，下标实际上存储为 `5SUBSEP3` 的形式。预定义变量 `SUBSEP` 包含下标组件的分隔符值。它默认是双引号，因为下标本身不太可能出现引号。记住，引号用于包含字符串；它们本身不会作为字符串的一部分被存储。如果你需要在多维数组下标中使用引号字符，则可以随时更改 `SUBSEP`。

如果你想按城市和州（或国家）计算销售总额，你将使用一个二维数组：

```
total_sales["Philadelphia","Pennsylvania"] = 10.15
```

你可以在条件语句中使用 `in` 函数：

```
("Wilmington","Delaware") in total_sales
```

你还可以在循环中使用 `in` 函数来遍历不同的城市。

## 内置数值函数

`awk` 提供了许多用于计算特殊数值的数值函数。表 26.7 总结了 `awk` 中的内置数值函数。早期版本的 `awk` 不支持所有这些函数。





### 表 26.7 `awk` 内置数值函数

| V | 函数 | 目的 |
| :--- | :--- | :--- |
| A | `atan2(x, y)` | 返回 `y/x` 弧度值的反正切值 |
| N | `cos(x)` | 返回 `x` 弧度值的余弦 |
| A | `exp(x)` | 返回 `e` 的 `x` 次方 |
| A | `int(x)` | 返回截断为整数的 `x` |
| A | `log(x)` | 返回 `x` 的自然对数 |
| N | `rand()` | 返回 0 到 1 之间的随机数 |
| N | `sin(x)` | 返回 `x` 弧度值的正弦 |
| A | `sqrt(x)` | 返回 `x` 的平方根 |
| A | `srand(x)` | 初始化（种子）随机数生成器；如果省略 `x`，则使用 `systime()` |
| G | `systime()` | 返回自 1970 年 1 月 1 日午夜以来的当前秒数 |

V 是支持变量的第一种实现。`A` = `awk`，`N` = `nawk`，`P` = `POSIX awk`，`G` = `gawk`。

### 算术运算符

`awk` 支持多种数学运算。表 26.8 汇总了这些运算符。

### 表 26.8 `awk` 算术运算符

| 运算符 | 目的 |
| :--- | :--- |
| `x^y` | 将 `x` 升幂 `y` 次 |
| `x**y` | 将 `x` 升幂 `y` 次（与 `x^y` 相同） |
| `x%y` | 计算 `x/y` 的余数（模） |
| `x+y` | 将 `x` 加到 `y` |
| `x-y` | 从 `x` 中减去 `y` |
| `x*y` | `x` 乘以 `y` |
| `x/y` | `x` 除以 `y` |
| `-y` | 取 `y` 的反数（切换 `y` 的符号）；也称为单元负 |
| `++y` | 将 `y` 加 1（前缀增） |
| `y++` | 使用 `y` 的值然后加 1（后置增） |
| `--y` | 将 `y` 减 1（前缀减） |
| `y--` | 使用 `y` 的值然后减 1（后置减） |
| `x=y` | 将 `y` 的值赋予 `x`。`awk` 也支持运算符赋值（`+=`, `-=`, `*=`, `%=`, `^=`, `**`） |

`awk` 中的所有数学计算均使用浮点数（即使你将其视为整数）。

### 条件流

从本质上讲，`awk` 程序中的动作是有条件的。如果其模式为真，则执行该动作。你也可以通过使用 `if` 语句让条件程序在动作内部流转。

`if` 语句的一般流程如下：

```
if (condition)
    为真时执行的语句
else
    为假时执行的语句
```

`condition` 可以是表 26.2 和 26.3 中所示任何有效模式组合。`else` 是可选的。如果你有多个语句要执行，需要将语句封装在大括号（`{ }`）内，就像 C 语法一样。

你也可以根据需要堆叠 `if` 和 `else` 语句：

```
if ("Pennsylvania" in total_sales)
    print "我们有宾夕法尼亚的数据"
else if ("Delaware" in total_sales)
    print "我们有特拉华的数据"
else if (current_year < 2010)
    print "天王星仍然是一个行星"
else
    print "没有一个条件被满足。"
```

### 空语句

根据定义，`if` 需要一个（或多个）语句来执行；在某些情况下，逻辑可能非常直接，即你想执行的代码在条件为假时发生。当反转逻辑以在条件为真时执行代码变得困难或难看时，我使用了这种方法。

解决这个问题的办法很简单：只需使用空语句，即分号（`;`）。空语句满足了 `if` 执行所需的语法要求；它只是什么都不做。

你的代码看起来会像下面：

```
if (($1 <= 5 && $2 > 3) || ($1 > 7 && $2 < 2)) ;    # 空语句
else
    我真正想要执行的代码
```

### 条件运算符

`awk` 有一个运算符实际上有三个参数：条件运算符。该运算符允许你在代码的任何地方应用 if-测试。

条件语句的一般格式如下：

```
condition ? 真-结果 : 假-结果
```

尽管这看起来像是 `if` 语句的重复，但它可以让你的代码更易于读。如果你有一个由员工姓名和请假天数组成的数据文件，你可以使用以下内容：





```awk
{ print $1, "has taken", $2, $2 != 1 ? "s" : "", "of ![arrow.gif](img/4505ed21b36efb4ebf4df5206fc03bad.gif)sick time" }
```

如果员工只请了一天病假，该命令将输出“day；如果员工请了零天或多于一天的病假，则输出“days”。生成的句子更具可读性。使用 `if` 语句编写相同的示例会更复杂，且如下所示：

```awk
if ($2 != 1)
    print $1, "has taken", $2, "days of sick time"
else
    print $1, "has taken", $2, "day of sick time"
```

### 循环

从本质上说，`awk` 程序是一个大循环，它读取输入文件中的每条记录并处理相应的模式和动作。在动作内部，经常会有重复的需求。`awk` 通过 `do`、`for` 和 `while` 语句支持循环，这些语句与 C 语言中的语句相似。

注意块语句（大括号）。

在条件语句和循环语句中，忘记给多条语句加上大括号是一个常见的编程错误。与 `if` 语句一样，如果你想在循环中执行多条语句，必须将它们包含在大括号中。

### do 语句

`do` 语句提供了一个至少执行一次的循环结构。条件或测试在循环内容执行完毕后进行。

#### do do while

`do` 语句有时也被称为 `do while` 语句。它的形式如下：

```awk
do statement while (condition)
```

`statement` 可以是一条语句，也可以是包含在大括号中的多条语句。`condition` 是任何有效的测试，类似于在 `if` 语句中使用的测试。通常，你必须在循环内部更改条件中变量的值。如果不这样做，你将陷入死循环，因为测试结果永远不会改变（也就不会变为假）。

### 循环控制 (break 和 continue)

如果你需要，可以提前退出循环（而无需给条件中的变量分配某个虚假值）。`awk` 提供了两种实现方法：`break` 和 `continue`。

- `break` 导致退出最内层循环。它的行为就像测试立即判定为假一样。循环中 `break` 之后的剩余代码都不会执行。这在你需要尽早处理某些错误时非常有用。
- `continue` 导致当前循环返回测试阶段。循环中 `continue` 之后的剩余代码都不会执行。这在你有某些想要暂时跳过的代码时非常有用。

### for 语句

`for` 语句适用于对项目进行计数。它有两种通用形式：

```awk
for (loop = 0; loop < 10; loop++) statement
for (subscript in array) statement
```

第一种形式初始化变量（`loop = 0`），执行测试（`loop < 10`），然后执行循环内容（`statement`）。随后修改变量（`loop++`）并再次测试。只要测试为真，`statement` 就会执行。





你可以使用许多不同的方法修改循环控制变量。这里展示了自增运算符（`loop++`），因为它是最常用的运算符（例如，用于遍历数组）。任何有效操作都可以此处此处，甚至是像这样的操作：`loop = loop * 2 + another_variable`。

在第二种形式中，`statement` 在执行时，下标 `subscript` 会被设置为 `array` 中的每一个下标。这使得你即使在不知道下标值的情况下，也能遍历数组。这对于多维数组非常有效。

`statement` 可以是一条语句，也可以是用大括号括起来的多个语句。条件 `(loop < 10)` 是任何有效的测试，类似于在 `if` 语句中使用的测试或用于触发动作的模式。

第 700 页

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 注意事项

通常情况下，你不希望在循环体内修改循环控制变量（`loop` 或 `subscript`）。让 `for` 语句为你完成这项工作，否则你可能会得到难以调试的行为。

对于第一种形式，变量的修改可以是任何有效操作（包括函数调用）。在大多数情况下，它是自增或自减。

`for` 循环是遍历未知大小数据的好方法：

```awk
for (i=1; i<=NF; i++) print $i
```

当前记录中的每个字段都将单独打印在一行。作为程序员，我编写代码时并不知道记录中有多少个字段。变量 `NF` 会会在程序运行时告诉我结果。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

后置还是前置？

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

这个示例展示了后置自增。无论使用后置（`loop++`）还是前置（`++loop`），结果都是样的。只需保持一致即可。

### while 语句

最后的循环结构是 `while` 循环。它是最通用的，因为只要条件为真它就会执行。其通用形式如下：

```awk
while(condition) statement
```

`statement` 可以是一条语句，也可以是用大括号括起来的多个语句。`condition` 是任何有效的测试，类似于在 `if` 语句中使用的测试或用于触发动作的模式。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

#### 修改条件的值

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

通常，你必须在循环内修改条件中变量的值。如果不这样做，你将陷入无限循环，因为测试（`condition`）永远不会改变（变为变为假）。如果在遇到 `while` 之前条件为假，则循环的内容将不会执行。这与 `do` 不同，`do` 至少会执行循环一次。

#### 高级输入输出

除了 `awk` 提供的简单输入输出外，你可以利用许多高级功能进行更复杂的处理。默认情况下，`awk` 会自动读取并遍历你的程序；你可以更改这种行为。你可以强制输入来自不同的文件，导致循环提前回收（不执行任何动作就读取下一记录），甚至读取下一记录。你甚至可以从其他命令的输出中获取数据。

第 701 页

在输出端，你可以格式化输出并将其发送到文件（标准输出设备以外）或作为另一个命令的输入。

##### 输入

你不需要在 `awk` 中编写标准的输入循环过程。它读取记录，然后搜索模式匹配并执行相应的动作。如果在命令行上指定了多个文件，它们将按顺序处理。只有在你想要改变这种行为时，才需要进行任何特殊的编程。

#### next 和 exit

`next` 命令会导致 `awk` 立即读取下一记录并执行模式匹配和相应的动作执行。通常情况下，它会执行你任何匹配模式的动作中的所有代码。`next` 会导致忽略此记录的任何额外的匹配模式。





在除 `END` 之外的任何动作中，`exit` 命令的行为就像到达了文件末尾。所有模式/动作中的代码执行将停止，并执行 `END` 模式中的动作。在 `END` 模式中出现的 `exit` 是一个特殊情况；它会导致程序结束。

## getline

`getline` 语句用于显式地读取一条记录。如果你有一个看起来像两个物理记录的数据记录，这种方法会特别有用。它会执行标准的字段拆分（设置 `$0`、字段变量、`FNR`、`NF` 和 `NR`）。如果读取成功，返回值 `1`；如果失败，返回零（到达文件末尾）。如果你想显式地读取整个文件，可以编写如下代码：

```
{ while (getline == 1)  {
    # 处理输入的字段
}
}
```

你还可以使用 `getline *variable` 的形式让 `getline` 将输入数据存储在字段中，而不是利用标准的字段处理。当这样使用时，`NF` 被设置为 0，而 `FNR` 和 `NR` 会加 1。

### 从文件输入

你可以使用 `getline` 从特定文件输入数据，而不是命令行列出的文件。通用形式为 `getline < *filename`。当这样编写代码时，`getline` 会执行标准的字段拆分（设置 `$0`、字段变量和 `NF`）。如果文件不存在，`getline` 返回 `-1`；成功返回 `1`，失败返回 `0`。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

如果你使用 `getline > "filename"` 将数据读取到程序中，`FNR` 和 `NR` 都不会改变。

你可以将数据从指定文件读取到变量中。你也可以将 `filename` 替换为 `stdin` 或包含文件名的变量。

### 从命令输入

使用 `getline` 语句的另一种方法是接受 UNIX 命令的输入。如果你想对系统中的每个人执行某些处理（例如，向他或她发送一条消息），可以编写如下代码：

```
while ("who -u" getline) {
    # 处理来自 who 命令的每一行
}
```

`who` 命令只执行一次，它的每一行都由 `getline` 处理。你也可以使用 `getline variable` 的形式。

### 结束文件或命令

每当你使用 `getline` 从指定的文件或命令获取输入时，在处理完数据后应该将其关闭。awk 允许打开的文件数量有一个最大限制；这个数字随操作系统的配置而异（命令输出被视为一个文件）。在用完文件后关闭它们，可以减少达到限制的概率。

关闭文件的语法如下：

```
close("*filename")
```

`filename` 是在 `getline` 中指定的（它也可以是 `stdin`、包含文件名的变量，或与 `getline` 使用的精确命令）。

## 输出

输出有几个高级功能：格式化输出、将输出发送到文件以及将输出作为其他命令的输入进行管道。`printf` 命令用于格式化输出，而不是查看 awk 决定使用的任何默认格式（那种格式通常很难看），你可以指定它的外观。

### 格式化输出 (printf)

`print` 语句为你生成简单的输出。如果你希望能够对数据进行格式化（例如产生固定列），你需要使用 `printf`。`printf` 的优点是它使用的语法与 C 语言中的 `printf()` 函数非常相似。`printf` 的通用格式如下所示（只有在包含表达式时才需要括号）：

```
printf(format-specifier, variable1, variable2, ..., variableN)
```

变量是可选的，但 `format-specifier` 是强制的。经常会有包含 `format-specifier` 的 `printf` 语句（用于打印不变量的消息）：

```
printf("Program Starting\n") printf("\f")  # 输出换页
```

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

习惯使然




个人而言，我使用第二种，因为我习惯了用 C 语言编码。

`format-specifier` 可以由文本、转义字符或实际的打印说明符组成。说明符以百分号（`%`）开头，后面跟着一个可选的数值用于指定字段大小，然后是格式类型（描述变量类型或输出格式）。如果你想在输出中打印百分号，则使用 `%%`。

字段大小可以由两个用小数点（`.`）隔开的数字组成。对于浮点数，第一个数字是整个字段的大小（包括小数点）；第二个数字是小数点右侧的位数。对于其他类型的字段，第一个数字是最小字段大小，第二个数字是最大字段大小（实际打印的字符数）；如果你省略了第一个数字，它将取最大字段大小的值。

打印说明符决定了变量的打印方式；还有修饰符可以改变说明符的行为。表 26.9 显示了打印格式说明符。

### 表 26.9 `awk` 的格式说明符。

| 格式 | 含义 |
| :--- | :--- |
| `%c` | ASCII 字符 |
| `%d` | 整数（十进制） |
| `%i` | 整数，与 `%d` 相同 |
| `%e` | 使用科学计数法的浮点数 (1.00000E+01) |
| `%f` | 浮点数 (10.43) |
| `%g` | `awk` 在 `%e` 或 `%f` 显示格式之间选择（较短的那个），并抑制不重要的零 |
| `%o` | 无符号八进制（基 8）数（整数） |
| `%s` | 字符串 |
| `%x` | 无符号十六进制（基 16）数（整数） |
| `%X` | 与 `%x` 相同，但使用 ABCDEF 代替 abcdef |

如果你尝试使用 `%c` 打印数值，它将作为字符打印（该值对应的 ASCII 字符）。

修饰符改变说明符的默认行为。列表 26.4 显示了各种说明符和修饰符的使用。

### 列表 26.4 `printf` 格式说明符和修饰符。

```c
printf("%d %3.3d %03.3d %.3d %-.3d %3d %-3d\n", 64, 64, 64, 64, 64, 64, 64)
printf("%c %c %2.2c %-2.2c %2c %-2c\n", 64, "abc", "abc", "abc", "abc", "abc")
printf("%s %2s %-2s %2.2s %-2.2s %.2s %-.2s\n", "abc", "abc", "abc", "abc", "abc", "abc", "abc")
printf("%f %6.1f %06.1f %.1f %-.1f %6f\n", 123.456, 123.456, 123.456, 123.456, 123.456, 123.456)
```
**输出：**
```
64   64  064  64 -64   64  64
@  a  a  a   a  a
abc abc abc ab  ab ab ab
123.456000  123.5 0123.5 123.5 123.5 123.456000
```

- 使用整数或十进制（`%d`）说明符时，字段大小默认为所打印值的大小（数值 64 为两个数字）。如果你指定的字段大小比该值大，则会自动获得填充字段。所有数值字段都是右对齐的，除非你使用减号（`-`）修饰符，该符号会导致其变为左对齐。如果你只指定了字段大小并希望填充字段剩余部分，必须使用零修饰符（在字段最小大小之前）。
- 使用字符（`%c`）说明符时，无论你使用的字段最小或最大大小是多少，无论值包含多少字符，都只从输入中打印一个字符。注意，作为字符打印的值 64 显示为 `@`。
- 使用字符串（`%s`）说明符时，除非你指定了字段最大值，否则将打印整个字符串。默认情况下，字符串是左对齐的，除非你使用减号（`-`）修饰符，该符号会导致其变为右对齐。
- 使用浮点（`%f`）说明符时，字段大小默认为 .6（小数点左侧和右侧各 6 位）。如果你在格式的小数后指定数字，则小数点右侧将打印相应位数且`awk` 会对数字进行四舍五入。所有数值字段都是右对齐的，除非你使用减号（`-`）修饰符，该符号会导致变为左对齐。如果你希望字段零填充，必须使用零修饰符（在字段最小大小之前）。

### 输出到文件

你可以将输出（来自 `print` 或 `printf`）发送到文件。以下操作创建一个新文件（或清空现有文件），其中包含打印的消息：

```bash
printf("hello world\n") > "datafile"
```

如果你多次执行此语句或其他重定向输出到 `datafile` 的语句，输出将保留在文件中。文件的创建/清空仅在程序第一次使用该文件时发生。




要向现有文件追加数据，你需使用以下命令：

```bash
printf ("hello world\n") >> "datafile"
```

### 输出到命令

除了将输出重定向到文件外，你还可以将程序的输出作为另一个命令的输入。你可以编写类似如下的代码：

```bash
printf ("hello world\n") | "sort -t`
```

任何其他将数据管道到同一命令的输出语句，在管道符（`|`）之后都会指定完全相同的命令，因为 `awk` 正通过这种方式跟踪哪个命令正在接收来自你程序的哪些输出。

### 关闭输出文件或管道

每当你将输出发送到文件或管道时，都应该在处理完数据后将其关闭。`awk` 允许打开的文件数有一个上限。这个数字随操作系统版本或个人账户配置而异（管道被视为一个文件）。通过在完成工作后关闭文件，可以减少达到限制的几率。

关闭文件的语法如下：

```bash
close("filename")
```

`filename` 是输出语句中指定的名称（也可以是 `stdout`、包含文件名的变量，或与管道一起使用的精确命令）。

### 函数

除了内置函数（如 `gsub` 或 `srand`），你还可以编写自己的函数。用户定义函数是创建在代码中多处访问的代码块的手段。它们还可以用于构建一个常用例程的库，这样你就不必重复编写相同的算法。

用户定义函数不是原始 `awk` 的一部分；它们被添加到 `nawk` 中并在较新版本中得到了支持。使用函数包含两个部分：定义和调用。函数定义包含要执行的代码（函数本身），而调用则将执行从主代码临时转移到函数。命令执行通过两种方式传回主代码：隐式返回和显式返回。当 `awk` 到达函数末尾（右大括号 `}`）时，它会自动（隐式地）将控制权返回给调用例程。如果你想在底部之前离开函数，可以显式地使用 `return` 语句提前退出。

#### 函数定义

`awk` 函数定义的通用形式如下：

```awk
functionname(parameter list) { the function body }
```

你编写函数的方式就像编写任何其他动作集一样，并将其放置在任何可以放置模式/动作集的地方。如果你仔细考虑，定义中的 `functionname(parameter list)` 部分可以被视为一种模式，而 `function body` 可以被视为动作。

`gawk` 支持另一种函数定义形式，其中 `function` 关键字缩写为 `func`。其余语法相同。

使用用户定义变量时要加小心。在使用用户定义函数时，调用时必须在函数名后立即紧跟包含参数列表的括号。当你使用内置函数时，这并不是强制要求的。

#### 26.5 定义和调用函数

```awk
BEGIN { print_header() }

function print_header() {
    printf("This is the header\n");
    printf("this is a second line of the header\n");
}
```




函数内部的代码仅在从 `BEGIN` 动作调用该函数时执行一次。该函数使用了隐式返回方法。

## 函数参数

与 C 语言一样，`awk` 通过值传递参数给函数。换句话说，它会创建原始值的副本并将副本传递给被调函数。即使函数更改了该值，原始值也会保持不变。

任何参数都在函数定义中列出并用逗号分隔。如果你没有参数，可以留参数列表（括号内）为空。

列表 26.6 是列表 26.5 的扩展版本；它展示了 `awk` 函数参数的值传递特性。

### 列表 26.6 传递参数。

```awk
BEGIN {
    pageno = 0;
    print_header(pageno);
    printf("the page number is now %d\n", pageno);
}

function print_header(page) {
    page++;
    printf("This is the header for page %d\n", page);
    printf("this is a second line of the header\n");
}
```
输出:
This is the header for page 1
this is a second line of the header
the page number is now 0

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

`awk` 不执行参数验证。

当你调用函数时，列出的参数可以比预期的多或少。任何多余的参数会被忽略，任何缺失的参数默认为零或空字符串（取决于如何使用）。页码在第一次调用 `print_header` 之前初始化，并在函数内部递增。在函数调用后打印时，它仍然保持原始值。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

你可以利用缺乏函数参数验证的特点。它可以被用来在被调函数内部创建局部变量，即在函数定义中列出的变量比函数调用中使用的变量多。我强烈建议注释说明这些额外的参数实际上被用作局部变量。

被调函数有几种方法可以通过显式返回或直接使用调用程序中的变量来调用程序中的变量（这些变量通常已经是全局变量）。

## 函数的显式返回（return 语句）

如果你想返回一个值或提前退出函数，需要编写一个 `return` 语句。如果你没有编写，函数将在右大括号（`}`）处结束。我个人倾向于将它们写在底部。

如果调用代码期望从你的函数获取返回值，你必须以以下格式编写 `return` 语句：

`return variable`

扩展列表 26.6 以允许函数更改页码，列表 26.7 展示了 `return` 语句的使用。

### 列表 26.7 返回值。

```awk
BEGIN {
    pageno = 0;
    pageno = print_header(pageno);
    printf("the page number is now %d\n", pageno);
}

function print_header(page) {
    page++;
    printf("This is the header for page %d\n", page);
    printf("this is a second line of the header\n");
    return page;
}
```
输出:
This is the header for page 1
this is a second line of the header
the page number is now 1

更新后的页码被返回给调用函数的代码。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

`return` 语句允许你仅向调用程序返回一个值。

## 编写报告

在 `awk` 中生成报告涉及一系列步骤，每一步都为下一步产生输入。编写报告通常是一个三步过程：选取数据、排序数据以及美化输出。





# 复杂报告

使用 `awk` 可以快速创建复杂的报告。相比于用其他语言（如 `C`）编写，进行字符串比较、动态构建数组以及利用关联数组要容易得多。不需要在数组中搜索与文本键匹配的项，而是可以将该键直接作为数组的下标。

我曾使用 `awk` 生成过具有三级控制间符（control breaks）的报告，同一个控制间符内包含多个报告部分，并有多个汇总页。每个级别的控制符都有一个汇总页，最后再加上一个总页；如果某个控制符没有特定类型的数据，则汇总页也不会包含该数据。如果某个控制符只有一个成员，则不会创建该级别的汇总页。（这在实际上只有一层控制符——即最高层——时节省了大量的纸张。）

该报告最终包含了超过 1000 行 `awk`（具体来说是 `nawk`）代码。它的运行时间比同等的 `C` 程序稍长，但创建它花费的程序员时间少得多。因为它容易创建和修改，所以我通过原型设计进行开发。用户简要描述他们想要的内容，我生成报告。他们决定需要更多的控制间符，于是我添加了它们；接着他们意识到汇总页上浪费了大量纸张，因此按照描述对报告进行了修改。

## 响应用户变化

在未知最终结果的情况下进行增量式开发，这让我觉得更容易也更有趣。通过对用户变化做出响应，用户非常开心！

## 提取数据

正如本章开头提到的，许多系统并不产生所需格式的数据。在处理存储在关系型数据库中的数据时，有两种提取数据的方法：使用带有 `SQL` 的查询工具，或者编写一个程序从数据库获取数据并以所需的格式输出。`SQL` 查询工具的格式化能力有限，但可以提供快速方便的数据访问访问。

我发现的一种非常有用的技术是将数据从数据库提取到文件中，然后通过 `awk` 脚本对文件进行处理，以生成所需的精确格式。需要时，`awk` 脚本甚至可以创建用于查询数据库的 `SQL` 语句（指定要选择的行的键值）。当查询工具在数值字段前放置一个空格，而某个要在其他系统中使用该数据的程序（如 `COBOL`）必须移除该空格时，可以使用以下示例：

```
{ printf("%s%s%-25.25s\n", $1,$2,$3);}
```
当 `awk` 将输入记录拆分为单独字段时，它会自动移除字段分隔符（空格字符），且 `printf` 中的格式化字符串说明符是连续的（它们之间没有任何空格）。

## 动态生成命令

将一个命令的输出管道到另一个命令的能力非常强大，因为第一个命令的输出变成了第二个命令可以处理的输入。单行 `awk` 程序的一个频繁用法是列表创建命令。`find` 命令可以产生符合其条件的文件列表，或者它可以执行一个接受单个命令行参数的单一命令。你可以通过以下命令查看目录（及子目录）中符合特定条件的文件：

```
$ find . -name "*.prn" -print
./exam2.prn ./exam1.prn ./exam3.prn
```

或者通过以下命令打印这些文件的内容：

```
find . -name "*.prn" -exec lp \;
```

`find` 命令会将单独的文件名插入 `{}` 位置并执行命令。如果你想执行一个需要两个参数的命令，或者执行多个命令，仅通过 `find` 是无法实现的。你可以创建一个接受单个参数并在多处使用的 Shell 脚本，或者创建一个单行的 `awk` 程序：

```
$ find . -name "*.prn" -print | awk '{print "echo bak " $1; print "cp " $1 " " $1".bak"}'
echo bak ./exam2.prn
cp ./exam2.prn ./exam2.prn.bak
echo bak ./exam1.prn
cp ./exam1.prn ./exam1.prn.bak
echo bak ./exam3.prn
cp ./exam3.prn ./exam3.prn.bak
```

为了让命令实际执行，你需要将这些命令管道到其中一个 Shell 中。以下示例使用了 Korn Shell；你可以使用你喜欢的任何：

```
$ find . -name "*.prn" -print | awk '{print "echo bak " $1; print "cp " $1 " " $1".bak"}' | ksh
```




在每次复制发生之前，都会显示消息。如果你想在多个子目录的文件中搜索字符串（使用 `grep` 命令），这也会非常方便。许多版本的 `grep` 命令不会显示所搜索的文件名，除非你使用通配符（或在命令行上指定了多个文件名）。以下示例了如何使用 `find` 搜索 C 源文件，使用 `awk` 创建 `grep` 命令来查找错误信息，并使用 shell 的 `echo` 命令来显示正在搜索的文件：

```bash
find . -name "*.c" -print | awk '{print "echo " $1; print "grep error-message " $1;}'
```

同样的技术可以用于对一系列子目录中的源代码进行 lint 检查。我定期在 shell 脚本中执行以下命令来检查所有的 C 代码：

```bash
find . -name "*.c" -print | awk '{print "lint " $1 " > " $1".lint"}'
```

某个系统上的 lint 版本会将代码错误作为标题行打印，然后将问题的代码以列表的形式列在下方。`grep` 显示标题，但不会显示详细行。`awk` 脚本会打印从标题到第一行空行（lint 章节结束）的所有内容。

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

如果有疑问 . . .

如果有疑问，在将输出管道到 shell 执行之前，可以先将输出传给 `more` 或 `pg` 以查看所生成的命令。

### 最后一个内置函数：system

还有一种不属于字符或数字类型的内置函数：`system`。`system` 函数执行传递给它的参数作为字符串。这允许你在 `awk` 代码有需要时即时执行命令或脚本。你可以编写一个报告，并在完成后自动打印到纸上。代码类似于列表 26.8 “使用 `system` 函数”所示。

```awk
BEGIN {
    pageno = 0;
    pageno = print_header(pageno);
    printf("page number is now %d\n", pageeno);
}
# 报告的生成代码将写在这里
END {
    close("report.txt");
    system("lpr -Pprinter report.txt");
}

function print_header(page) {
    page++;
    printf("This is the header for page %d\n", page) > "report.txt";
    printf("this is a second line of the header\n") > "report.txt";
    return page;
}
```

这是第 1 页的标题
这是标题的第二行
页码现在是 0

输出结果与列表 26.6 相同，不同之处输出显示在打印机上而不是屏幕上。在打印文件之前，你必须先关闭它。

### 结语

本章介绍了各种实现下的 `awk` 编程语言。这是一门非常强大且实用的语言，允许你搜索数据、从文件中提取数据、即时创建命令，甚至创建整个程序。作为一种原型语言，它非常有用，你可以快速创建报告。在展示给用户后，可以快速进行修改。虽然它的效率不如 C 语言编写的程序，但远未低到无法创建生产环境程序的程度。如果 `awk` 程序的效率是一个问题，可以将其转换为 C。

更多信息，请参考以下内容：Aho, Alfred V., Brian. Kernighan and Peter J. Weinberger. *The awk Programming Language.* Addison-Wesley, 1988 (copyright AT&T Bell Lab). 另另你系统上 `awk`、`nawk` 或 `gawk` 的 man 页面。

### 第 27 章编写 Perl 程序
作者 Pitts

#### 编写/执行简单的 Perl 脚本
#### 与用户交互
#### 特殊 Perl 变量
#### 控制结构
#### Perl 中常用的函数
#### 数组操作
#### 文件操作
#### 系统操作




本章将为你介绍如何编写 Perl 脚本。本教程使用 Perl 5 版本编写。本章中提到的某些内容无法在 Perl 4 版本中运行。其目的是为 Perl 初学者提供足够的信息，使其能够编写自己的程序，以提高在现实世界中的性能。本章主要涉及三个领域：用户输入、处理和输出，并重点关注用户输入和处理。基础输出将以向输出到标准输出（显示器）和文件的形式涵盖。

## 什么是 Perl？

首先，Perl 是什么？Perl 是一种几乎适用于任何场景的编程语言。Perl 的作者拉里·沃尔（Larry Wall）说，它代表“病态折衷的垃圾列表器”（Pathologically Eclectic Rubbish Lister）。在你有机会使用 Perl 一段时间后，我认为你也会同意一个更好的定义是“实用提取与报告语言”（Practical Extraction and Reporting Language）。习惯于 C 语言的人会发现它的语法与此相似，但更好。你还会发现，由于不需要 C 语言相关的编译，工具的设计和更改变得快速而简单。这是没错的；Perl 不是编译的。Perl 是一种解释型语言。Perl 在运行时编译，因此速度几乎与编译后的 C 程序相当，但编写代码像编写 Shell 程序一样简单。对于习惯了 awk 或 sed 的人来说，Perl 利用正则表达式提供了模式匹配。基本上，Perl 已经成为 C、Shell 脚本、TCL 以及其他与系统管理相关的编程语言和技术的替代品。

幸运的是，Perl 并不止于此。它是一门完整的语言，准备好处理编程社区的复杂需求。Perl 已用于基因组项目中的 DNA 制图；最流行的邮件列表管理器 Majordomo 就是用 Perl 编写的。Perl 被用于数千（字面上意义）其他项目。有关如何使用 Perl 的更多信息，请参见全面 Perl 存档网络 (www.perl.com)。

## 编写/执行简单的 Perl 脚本

我上过的每一门编程课程都是从设计 Hello World 程序开始的。本章也不例外。我们可以从命令行显式地运行 Perl 脚本开始。假设 Perl 可执行文件的位置在你的路径中，以下程序：

```
perl -e 'print "Hello world!\n";
```

将输出以下内容：

```
Hello world!
```

`-e` 告诉 Perl 执行其后的内容。这种方法限制为 80 个字符。如果你需要超过 80 个字符的内容，你需要将行放在文本文件中。该文件将完成两件事：首先告诉计算机要做什么（调用 Perl 解释器），其次告诉 Perl 解释器要解释什么。

你可能会问这是如何实现的？正如你从 Shell 脚本经验（如果有的话）中所知，你使用脚本的第一行来告诉计算机调用哪个程序。例如，如果我要调用 ksh 程序，我的第一行看起来如下：

```
#!/bin/ksh
```

在 Perl 中，情况是类似的。你有一个井号（!），后面跟着解释器的位置。因此，你新程序的第一行应该像这样：

```
#!/bin/perl
```

此行之后的所有内容都将作为参数发送给程序（在此例中为 Perl）。因此，Hello World 程序可以像这样的文件：

```
#!/bin/perl print "Hello World!\n";
```

诚然，这算不上什么程序。然而，它足以确保 Perl 运行并且你对文件拥有正确的权限。为了让 Perl 读取并执行脚本，脚本必须为运行程序的人设置了读取和执行权限。`-r-x------` 将允许脚本所有者运行 Perl 程序，而 `-------r-x` 将允许任何人运行程序。

### 关于终止符的快速说明

每行代码必须以某种形式的终止符结束。Perl 中有两种终止符。第一种是分号（`;`）。它用于结束一行代码。第二种是右大括号（`}`）。它用于结束一个代码块。许多初学者（甚至是专家）都会忘记终止符。

当你忘记终止符时会发生什么？程序仍然会尝试编译，但几乎会在缺少分号的下一行报错，或者在程序结束处因缺少大括号而报错。

为什么终止符如此重要？终止符的作用用于告诉 Perl 一行或一个代码块何时结束，这样它就知道如何处理该代码。对于 Perl 来说，硬回车没有意义。例如，以下两组代码在 Perl 视角来看是相同的。第二组对我们人类来说更容易读：

```
$first_name="David";
$last_name="Pitts";
$work="Best Consulting";
```

```
$first_name="David"; $last_name="Pitts"; $work="Best Consulting";
```

因此，格言说：要终止，否则就会被终止！

## 与用户交互




拥有一个可以输出内容的程序是可以的。该流程的下一步是允许程序与用户进行交互。实现这种交互有多种方法：可以向程序传递参数，也可以从命令行获取输入。

在继续之前，让我花一点时间说明一下 Perl 中使用的主要数据类型。它们是字面量、包括字符串、数组和哈希引用的变量、文件句柄以及 here-iss。接下来的章节将对这些每种类型给出简要描述和示例。

## 字面量

`Literals` 是实际的值。`Literals` 名如其名。例如，有数值字面量 `1`、`2`、`3`、`4` 等。还有字符串字面量 `abc`、`xyz`、`Fred`、`Sylvia` 等。某些字符不是字面量，而是元字符。这些字符匹配除自身以外的内容。这些元字符是 `\ ( ) [ ] { } ^ $ * + ?`。

在一个章节内没有空间详细解释所有这些内容的含义。如果你有任何正则表达式的经验，大部分对你来说应该熟悉。一个需要理解的重要点是反斜杠。反斜杠（`\`）可以将元字符转换为字面字符。它也会将某些字面字符转换为元字符；例如，`\n` 是换行，`\t` 是制表符。

## 变量

`Variables` 是用于存储值的命名存储位置。该值可以是一个数字、字符、数字和字符的字符串，或者程序认为合适的任何内容。以下是一些变量的示例。

- `$var`: 一个简单的标量变量。
- `@var`: 在标量上下文中整个数组，即数组中元素的数量。
- `$var[4]`: 数组的第五个元素（和大多数计算机一样，数组的第一个元素是第 0 个元素，而不是第一个）。
- `$d = @var`: `$d` 是指向数组的引用。
- `$d[4]`: 由 `$d` 引用的数组的第五个元素。
- `$var[-1]`: 数组 `@var` 的最后一个元素。
- `$var[$x][$y]`: 数组 `@var` 中第 `$x` 个元素的第 `$y` 个元素。
- `$#var`: 数组 `@var` 的最后一个索引。
- `%var`: 在标量上下文中整个哈希，如果哈希有元素则为真（哈希被称为关联数组）。
- `$var{'Name'}`: 来自哈希 `%var` 的一个值。
- `$d = %var`: `$d` 是指向哈希 `%var` 的引用。
- `$d{'Name'}`: 由 `$d` 引用的哈希中的值。
- `@var{'x','y'}`: `%var` 的切片；相当于 ($var{'x'},$var{'y'})。默认情况下，所有变量都是全局变量。这意味着如果你在程序的某个部分或子程序中使用变量，然后在其他部分使用它，它仍然指向同一个位置，并且在一个地方对其进行的任何更改都会影响另一个地方的变量。声明局部变量有两种方法。我在这里不会讨论它们的区别，但有一个例外：局部声明的变量会将值传递到从当前子程序调用的另一个子程序中，而 `my` 则不会。使变量变为子程序局部的两种方法是使用 `my` 和 `local` 标识。这意味着子程序获得了这些变量的自己的副本，对这些变量的任何操作都不会影响该程序外部同名的变量。以下示例展示了如何使用 `my` 和 `local` 标识。

```perl
my $name = "David"; local @brothers_family = ("John", "Kathy", "Pat", "Emily");
my ($John, $Kathy, $Pat, $Emily) = @brothers_family;
```



注意，以下不是将变量 `$x` 和 `$y` 初始化为局部变量正确方法：

```perl
my $x, $y = 1;
```

这等同于以下写法：

```perl
my $x; $y = 1;
```
这会将 `$x` 初始化为局部变量，并将 `$y`（全局地）设置为 1。

第 723 页

## 代码引用
代码引用指的是子程序（subroutines）。子程序是一段代码，可以从程序的不同位置被调用，用以处理程序目标的某部分。如果子程序返回有意义的值，它也被称为函数。子程序包含两个部分：首先是实际的代码段；其次是调用该代码的内容。

子程序使用保留字 `sub` 定义，后面跟一个空格，然后是子程序的名称。整个子程序包含在 `begin` 和 `end` 括号（`}{}`）中，如下子程序所示。

使用井号（`#`）开始注释。注释从井号开始一直延伸到行尾。因此，如果你想写行注释，必须在每行的开头放置一个井号。

```perl
sub weekday { # determine day of week
$y=$year;
$d=$mday;
$m=$month;
@d= (0,3,2,5,0,3,5,1,4,6,2,4);
@day=(Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday);
$y-- if $m < 3;
$weekday = $day[($y+int($y/100)+int($y/400)+$d)%7];
# end of sub weekday
```

要调用子程序，需要在子程序名称前加上取符符号（`&`）。例如，要调用 `weekday` 子程序，你可以这样做：

```perl
&weekday
```

也可以通过将参数放在括号内传递给子程序。

```perl
&subroutine(list);
```
这等同于向程序传递参数列表。因此，我将关于这点的讨论推到本章稍后的“将输入作为参数”章节。

## 文件句柄
文件句柄（filehandle）赋予文件、管道、套接字或设备的一个符号名称。在对文件、管道、套接字或设备进行操作时，你使用的是文件句柄而不是实际名称。下面的示例显示了文件句柄的一种用法。

```perl
open(FILE, "$filename"); @file = <FILE>;
close FILE;
```
第一行打开与变量 `$filename` 关联的文件。现在该文件将使用文件句柄 `FILE` 来引用（它可以是任何名称；我使用 `FILE` 是为了提醒自己这是一个文件；同样，如果我打开一个目录列表，我会使用 `DIR`）。第二行将整个文件保存为名为 `@file` 的数组。最后，第三行通过关闭文件句柄关闭与变量 `$filename` 关联的文件。

表 27.1 显示了如何根据不同目的打开文件。

| 命令 | 说明 |
| :--- | :--- |
| `open(FILE, "<")` | 从现有文件读取 |
| `open(FILE, ">")` | 创建并打开文件（覆盖现有文件） |
| `open(FILE, ">>")` | 向文件追加（不覆盖现有文件） |
| `open(FILE, \|")` | 设置输出过滤器 |
| `open(FILE, "|")` | 设置输入过滤器 |

第 724 页

如你所见，文件句柄可以命名为任何名称。打开后，可以使用文件句柄访问文件，直到它被显式关闭。

## Heroc
Heroc 是一种面向行的引用形式。它通常用于打印多行内容。使用带有 heredoc 的单个打印语句比逐个打印每一行要快。引用 heredoc 的是使用两个小于号（`<<`），后面紧跟一个用于结束引号内容的字符串（小于号和字符串之间不要有空格）。忘记在语句末尾加上分号，以便 Perl 知道语句何时结束。以下是使用 heredoc 打印多行的示例。

```perl
print<<"Print_to_here";
My name is $f_name $l_name
I live at:
   $street
$city, $state $zip
Print_to_here;
```

如果在两个小于号后加上空格，或者没有使用字符串来结束引号内容，打印语句将一直打印到遇到空行为止。因此，如果我在第一行的 `<<` 和字符串之间放了一个空格，那么打印出来的将只有第一行，而不是整个内容。

## 特殊 Perl 变量




Perl 具有几个特殊的内置变量。这些变量具有特定的值，或者在无需程序指示的情况下采用特定的值。表 27.2 列出并描述了这些特殊变量。

### 表 27.2 特殊 Perl 变量

| 变量 | 用途或功能 |
| :--- | :--- |
| `$_` | 默认输入和模式搜索空间。 |
| `$.` | 与最后读取的文件句当前行相关的行号。 |
| `$/` | 输入记录分隔符。 |
| `$,` | 打印操作的输出字段分隔符。 |
| `$` | 字符串中插值数组元素的连接符。 |
| `$\` | 打印运算符的输出记录分隔符。 |
| `$#` | 打印数字的输出格式。 |
| `$*` | 设置为 1 以在字符串内多行匹配。 |
| `$?` | 上一次 `...` 命令、`close`、`pipe` 或系统操作返回的状态。 |
| `$]` | Perl 版本号。 |
| `[` | 数组第一个元素的索引，以及子字符串第一个字符的索引。 |
| `$;` | 用于模拟多维数组的下标运算符。 |
| `$@` | 上一次 `eval` 或 `do` 命令返回的错误信息。 |
| `$!` | 如果在字符串上下文中，产生相应的错误字符串；在数值上下文中，产生 `errno` 的当前值。 |
| `:$` | 字符串后可以断开以填充格式中延续字段的字符集。 |
| `$0` | 正在执行的 Perl 脚本的文件。 |
| `$$` | 运行当前脚本的 Perl 解释器的进程 ID。 |
| `$<` | 当前 Perl 进程的实际用户 ID。 |
| `$>` | 当前 Perl 进程的有效用户 ID。 |
| `$(` | 当前 Perl 进程的实际组 ID。 |
| `$)` | 当前 Perl 进程的有效组 ID。 |
| `$^A` | 行和写操作的累加器。 |
| `$^D` | 使用 `-d` 传递给 Perl 的调试标志。 |
| `$^F` | 最高的系统文件描述符。 |
| `$^I` | 使用 `-i` 传递给 Perl 的就地编辑扩展。 |
| `$^L` | 格式中使用的分页符。 |
| `$^P` | 内部调试标志。 |
| `$^T` | 当前 Perl 程序启动的时间。 |
| `$^W` | 传递给 Perl 的 `-w` 选项的值。 |
| `$^X` | 调用此 Perl 解释器的名称。 |
| `$%` | 当前选定输出通道的页码。 |
| `=$` | 当前输出通道的页长度。 |
| `$-` | 当前页剩余的行数。 |
| `~$` | 当前报告格式的名称。 |
| `$^` | 当前页首格式的名称。 |
| `$` | 如果设置为非零（默认为 0），则强制在当前选定的输出通道上的每次打印或写入后进行刷新。 |
| `$ARGV` | 从 `< >` 读取时当前的文件名。 |
| `$&` | 上一次成功匹配的字符串。 |
| `$'` | 上一次成功匹配之前的字符串。 |
| `` ` `` | 上一次成功匹配之后的字符串。 |
| `$+` | 上一次搜索匹配的最后一个括号。 |
| `$1..$9` | 包含上一次匹配模式中对应括号组的子模式。 |
| `@_` | 子程序的参数数组；如果不是数组上下文，也由 `split` 使用。类似于 `$_`。 |
| `@ARGV` | 脚本的命令行参数。 |
| `@EXPORT` | 包默认导出的方法名称。 |
| `@EXPORT_OK` | 包在显式请求时可以导出的方法名称。 |
| `@INC` | 包含 `do` 和 `require` 评估脚本的路径列表。 |
| `@ISA` | 包的基类列表。 |
| `%ENV` | 环境变量。 |
| `%INC` | 使用 `do`、`require` 和 `use` 包含的文件列表。 |
| `%OVERLOAD` | 可用于重载包中的运算符。 |
| `%SIG` | 用于设置各种信号的信号处理器。 |

许多程序允许在实例化时传递参数。程序必须足够聪明，以知道如何处理这些参数。Perl 中调用的任何例程也是如此。坦率地说，Perl 有一个内置数组，可以捕获从命令行传递它的任何参数。该数组就是 `@argv` 数组。在任何语言中，数组元素的编号从零（0）开始。因此，如果向程序传递两个参数，第一个值将是数组的第 0 个元素，第二个参数将是数组的第一个元素。

`@argv` 数组是默认数组。有几种方法可以从数组获取信息。正如前面提到的，可以引用元素。如果使用这种方法，值将保留在数组中。获取信息的另一种方法是将其移出数组。使用 `shift` 命令，我们可以一次移除数组上的元素，并将数组中的所有其他元素向下移动一个。

例如，假设你有如下数组：

```
@argv = (1,2,3,4);
```

你可以像这样将数组第一个元素的值赋给变量：

```perl
$number = $argv[0];
```



这会将 `$number` 赋值为 "1"，而 `@argv` 的值为 (1,2,3,4)。接下来的示例将 `$number` 赋值为 "1"，但此时 `@argv` 的值将变为 (2,3,4)。

```perl
$number = shift @argv; # 这等同于仅对 @argv 数组执行 shift = shift。
```

## 在命令行上提供脚本输入

在实例化程序时，并不一定需要向程序传递变量。也可以从命令行读取输入。这是通过使用尖角运算符（angle operator）实现的。尖角运算符使用一个名为 `STDIN` 的特殊文件句柄。通过将输入句柄放在小于号和大于号之间，我们可以从命令行获取输入。该值必须赋值给变量，并且包含了输入数据时使用的硬回车符。下一行代码获取标准输入并将其保存到变量 `$input` 中。

```perl
$input = <STDIN>; chomp($input);
```
第二行删除了字符串末尾的硬回车符。

## 控制结构

`Control structures` 为程序提供了根据标准做出并并操作的能力。Perl 基本上有两种类型的控制结构：条件结构和交互结构。条件结构基于这样的概念：如果某事为真，则执行一次操作。交互结构（也称为循环）基于这样的概念：如果某事为真，则持续执行某些操作直到其不再为真。这引出了一个问题：什么是真？

### 什么是真？

这是一个困扰了哲学家千年的问题。幸运的是，我们是程序员而不是哲学家，我们知道什么是真。真可以分为两种。观察真的第一种方法是简单值。如果该值等于 nil 或零，它就是假的；否则，它是真的。因此，在前面的示例中，如果 `$value` 是任何非 nil 或零的值（即它具有某些值），就会被打印；否则不会。以下是一些使用这种基本格式的示例，展示了真与假之间的区别。

```perl
$value = ""; if ($value) { print $value }
```
什么都没有被打印，因为 `$value` 是 nil。

```perl
$value = "David"; if ($value) { print $value }
```
打印了 David，因为 "David" 既不是 nil 也零。

另一种观察真的方法是使用真值表来观察一个值如何与另一个值比较。要查看这些真值表，我们必须先理解 Perl 中是如何进行比较的。取决于比较的是字符串还是数字，比较方式有所不同。表 27.3 显示了数字和字符串的关系运算符及其含义。

表 27.3 数字和字符串的关系运算符

| 数字 | 字符串 | 含义 |
| :--- | :--- | :--- |
| `>` | `gt` | 大于（假时返回 ""，真时返回 1）。 |
| `>=` | `ge` | 大于等于（假时返回 ""，真时返回 1）。 |
| `<` | `lt` | 小于（假时返回 ""，真时返回 1）。 |
| `<=` | `le` | 小于等于（假时返回 ""，真时返回 1）。 |
| `==` | `eq` | 等于（假时返回 ""，真时返回 1）。 |
| `!=` | `ne` | 不等于（假时返回 ""，真时返回 1）。 |
| `<=>` | `cmp` | 比较（左侧小于右侧时返回 -1，相等时返回 0，左侧大于右侧时返回 1）。 |

使用上表，我们可以写出一些复杂的 `if` 命令。

```perl
if ($value == 24) { print $value } if ($value == 24 && $name eq "David") { print $name } if ($value == 24 || $name eq "David") { print $value }
```
第一行可能是容易理解的：如果 `$value` 的值为 24，则打印 `$value` 的值。接下来的两行使用逻辑运算符允许复杂的检查 set 来判断真假。双和符号 `&&` 是逻辑与（AND），双管道符号 `||` 是逻辑或（OR）。在逻辑与中，`&&` 两侧的值都必须为真，整个语句才为真。在逻辑或中，只需一侧为真即可。它们使用以下基础真值表。

| 比较 | 值 | True && True | True || False | True && False | False || False |
| :--- | :--- | :--- | :--- | :--- | :--- |
| True && True | True | True | True | | |
| True || False | True | True | True | | |
| True && False | False | | True | False | |
| False || False | False | False | False | False |





# 根据测试结果执行代码 (if)

现在我们已经获取了输入（无论是来自命令行还是标准输入），我们就可以对其进行处理了。对输入最常见的处理方式是测试结果，并且如果结果符合特定条件，则执行某些操作。这种测试结果通过 `if` 命令完成。`if` 命令的语法是动词 `if` 后跟一个真值语句。在真值语句之后，如果该语句评估为真，则执行一个代码块；否则，将跳过该代码。一个简单的 `if` 语句看起来如下：

```perl
if ($value) {print $value}
```

## 决策 (if-else)

具备检查某事真假的能力是可以的，但在许多过程中，我们希望更进一步：即如果某事为真，则执行某件事；如果为假，则执行另一件事。这在 Perl 中可以通过 `if-else` 语句轻松实现。

```perl
if ($value eq "True") {
  do something
} else {
  do something
}
```

这是最基础的操作了：一个简单的“是”或“否”问题，每个选项都接收一组独立的指令。当然，通过 `elsif` 动词，可以根据某些条件执行分级工作（即：如果第一个条件为假，则检查下一个条件）。下面的示例显示，如果该值为真，则执行某些操作；如果为假，它会检查另一个值，并根据该值执行若干种操作中的一种。

```perl
if ($value eq "True") {
  do something
} elsif ($range <= 22) {
  do something
} elsif (($range > 22) && ($range <= 44)) {
  do something
} elsif (($range > 44) && ($range <= 70)) {
  do something
} else {
  do something
} # end
```

## 遍历每个命令行参数 (for)

`if` 语句有助于在存在选择时确定该做什么。当你想要按照特定次数循环一系列代码时，就会使用 `for` 命令。例如，你想执行某项任务，直到某个变量（如 `counter`）达到某个特定值。用英语描述，你的做法可能如下所示：![4f3a8aef3b56941e5550c604caf.gif](img/4f3a8aef3b56941e5550c604caf.gif) 将 `counter` 初始化为 0。如果 `counter` 小于或等于 10，则运行系列命令。当 `counter` 大于 10 后，继续执行程序的剩余部分。

Perl 的 `for` 循环语法与 C 语言相同。格式如下：

```perl
for(initial_value;while true;change_value) {
  do ![arrow.gif](img/450ed21b36ef4f4df520fc03bad.gif)stuff
}
```

这是一个带有实际变量的示例，有助于理解上述内容：

```perl
for ($counter=0; $counter <= 10; $counter++) {
  do stuff
}
```

注意，`for` 循环有三个部分。首先，你有 `for` 循环的初始状态（`$counter = 0`）。其次，你定义了在什么条件下执行代码（当 `counter` 小于或等于 10 时）。最后，你有一个用于修改循环状态的表达式（增加 `$counter`）。只要真值条件为真（`$counter <= 10`），循环就会继续执行。

你可能已经发现 `for` 循环在本质上与 `while` 循环是相同的。语法不同，但概念是一的。不过，为了完整起见，这里有一个使用 `while` 循环实现的相同循环以便以便观察区别：

```perl
while ($counter <=10) {
do stuff
}
```

两者之间的主要区别在于，`do stuff` 代码中必须存在对状态变量的变化，否则你将陷入死循环。

## 遍历整个对象 (foreach)

`foreach` 循环类似于 `for` 循环。`foreach` 循环用于对整个标量值（如数组）执行一组指令。语法非常简单；我将再次用通白英语给出，然后用 Perl 给出。




用通俗易懂的话来说，你可以认为对于我集合中的每个实体，执行这些指令。听起来很简单吧？事实它也确实如此。以下是 `foreach` 命令的 Perl 版本：

```perl
foreach $value(@array) { do stuff }
```

在前面的示例中，数组 `@array` 的每个元素都被赋值给变量 `$value`。然后，执行代码块。没有必要在这里定义该变量（`$value`）。如果缺失了它，在循环执行时，特殊变量 `$_` 将包含每个元素的值。这里有一个真实世界的示例，可能有助于你理解这一点。

例如，假设你想打开一个文件，将其内容保存到数组中，并检查每行是否包含 `\n`，然后将其替换为 `<br>`。这是一个很好的循环示例。判断这是一个循环函数的关键在于“检查每行”的句语句。这样的程序看起来可能像这样：

```perl
#!/site/bin/perl 
open (FILE,"filename") die "File not found: $!\n";
@file=<FILE>;
close(FILE);
foreach (@file) {
    $_ =~ s/\\n/<br>/g;
    push (@temp, $_);
} # end of foreach (@file)
open (FILE< ">filename");
print FILE @temp;
close FILE;
```

## Perl 中常用的函数

虽然可能需要一百页或更多的内容才能简要描述 Perl 的所有函数，但列出一些处理数组、列表和标量的常用函数就足够了；这让初学者能够制作非常强大且复杂的工具。因此，本节将对一些最常用的函数进行简要描述并提供示例。在此之前，需要对泛指函数说明几点。

函数可以作为表达式中的项使用。其中一些函数接受一个 `list` 作为参数。这种列表可以是标量和列表值的任何组合，但整个列表将被视为一个单维的列表值。列表中的元素必须用逗号分隔，或者用 `=>`（逗号的简写形式）分隔。

函数的参数不需要加括号。许多程序员在参数周围使用括号，以帮助将其与函数名区分开，并指示它们是参数。然而，必须小心，因为位置错误的括号往往会导致许多意想不到的结果。下面的示例将有助于这一点这一点：

```perl
print 1+1+1;      # 输出 "3"
print (1+1)+1;    # 输出 "2"
print +(1+1)+1;   # 输出 "2"
print ((1+1)+1);  # 输出 "3"
```

如你所见，空格的影响很小或没有影响，但括号的影响很大。我们将看到的函数属于以下几类：数组、文件、哈希和变量。这些函数可以分为这些类别，尽管其中某些确实属于多个类别：

- **数组操作**：`pop`, `push`, `shift`, `unshift`, `splice`
- **文件操作**：`open`, `close`
- **哈希操作**：`each`, `keys`, `values`
- **系统操作**：`time`, `localtime`, `system`
- **变量操作**：`++`, `--`, `chomp`, `split`, `join`

一个准确的观察者会注意到，其中某些并不是真正的函数（`.`, `++`, `--`），但它们足够重要，会被包含进来。

## 数组操作

数组可以被视为栈。因此，可以从栈的末端添加或删除内容。通过从数组的开头和结尾添加和删除内容的能力，我们可以执行先进先出（FIFO）和后进先出（LIFO）的功能。也可以从栈的中间删除内容。考虑到这一点，我们来看以下函数。

### Pop 和 Push

下面的示例使用 `foreach` 语句读取数组的每行。然后对每行进行搜索和替换，并将该行的结果推（push）到一个名为 `@temp` 的数组。

```perl
foreach $line(@stuff) {
    $line =~ s/$search/$replace/g;
    push (@temp, $line);
} # end of foreach $line
print @stuff,"\n",@temp;
```

### Pop

如果省略了 `ARRAY`，函数将弹出 `@ARGV` 或 `$_`。下面的示例从数组中弹出每个元素，执行与前例相同的搜索和替换程序，并将结果推入第二个数组中。

```perl
while (@ARGV) {
    $argument = pop;
    $argument =~ s/$search/$replace/g;
    push (@temp, $argument);
} # end of while (@ARGV)
```




```perl
print @temp, "\n\n", @ARGV;
```

## 这两个示例之间有什么区别？

有两个区别。让我们来看 print 语句的输出。在两个示例中，`$search = "David"` 和 `$replace = "John"`，传递的参数都是 "David was here."

push 示例的输出如下：
```
Johnwashere.
Johnwashere.
```

pop 示例的输出如下：
```
here.wasJohn
```

区别在于，在 pop 示例中，`@ARGV` 失去了所有的值，因为它们从列表中被弹出（移除），而在第二个示例中，每个值只是被引用了。第二个区别是，在 pop 示例中，输出与输入相反。你能猜出为什么吗？

## Shift and Unshift

Shift 和 unshift 与 push 和 pop 相似，它们作用于数组的另一侧。push 和 pop 在数组的末尾添加和删除项，而 unshift 和 shift 在数组的开头添加和删除项。我们将使用与 push 和 pop 类似的示例，并看看有什么区别。不过，首先是它们的语法：

```perl
unshift ARRAY, LIST
```

记住，`unshift` 将项插入数组前面，这意味着它将它们添加到数组的开头。

```perl
foreach $line (@ARGV) {
    $line =~ s/$search/$replace/g ;
    unshift(@temp, $line);
} # end of foreach $line (@stuff)

print @temp,"\n\n",@ARGV;
```

**示例输出：** 
```
here.wasJohn
Johnwashere.
```

注意，`@temp` 与输入参数 ![arrow.gif](img/4505ed21b36ef4fdf520fc03bad.gif)"David was here." 是反的。

shift

与之对应，如果给了 ARRAY，`shift` 会从 `@ARGV` 中移除项。

```perl
while (@ARGV) {
    $argument=shift;
    $argument~ s/$search/$replace/g;
    unshift(@temp, $argument);
}
while (@ARGV)
print @temp, "\n\n",@ARGV;
```

**示例:**
```
here.John
```

注意，尽管它是先从栈顶获取项，但它又先将它们放回开头。因此，新数组 `@temp` 现在按顺序包含了所有参数。

## Splice

有时，我们想要获取数组较大的一部分，或者想要从中间取出某些东西。这就是 `splice` 的用途。事实上，我们可以用 `splice` 代替 `shift`、`unshift`、`pop` 和 `push`。`splice` 的语法如下：

```perl
splice ARRAY, OFFSET, LENGTH, LIST
splice ARRAY, OFFSET, LENGTH
```

该函数从数组中删除由 `OFFSET` 和 `LENGTH` 指定元素，并用 `LIST` 中的元素（如果有）替换它们。`Splice` 返回从数组中移除的元素。如果省略 `LENGTH`，它将移除 `OFFSET` 之后的所有内容。

下表显示了如何使用 `splice` 代替 `push`、`pop`、`shift` 和 `unshift` 来移除数组中间的一部分。

| Splice | 等效操作 |
| :--- | :--- |
| `splice(ARRAY, OFFSET, 0, LIST)` | `unshift(ARRAY, LIST)` |
| `splice(ARRAY, ##, LENGTH, LIST)` | `push(ARRAY, LIST)` |
| `splice(ARRAY, 0, LENGTH)` | `shift(ARRAY)` |
| `splice(ARRAY, -1, 1)` | `pop(ARRAY)` |
| `splice(ARRAY, OFFSET, LENGTH, LIST)` | `ARRAY[OFFSET] = LIST` |

你看到那个看起来很特殊的变量 `$#array` 吗？该值返回数组中最后一个元素的索引。通过给它加 1，我们得到了 `OFFSET` 值（数组从 0 开始计数；OFFSET 从 1 开始计数）。





对文件进行最常见的两种操作是打开和关闭。关闭文件非常简单，我们将首先讨论这一点。打开文件取决于你打算对该文件做什么，因此需要花一点额外的时间来解释它。

## Close

在 Perl 5 之前的版本中，关闭文件句柄（filehandle）并不是一个必要步骤。当程序结束或用具有相同 `FILEHANDLE` 名称打开一个新文件时，文件会自动关闭。但无法保证这在 Perl 的未来版本中仍然依然有效，而且，关闭你所打开的任何文件也是良好的编程规范。如果你不记得文件句柄是什么，请参阅讨论它们的上一个章节。其语法非常简单：

```perl
close FILEHANDLE;
```

我在这里给您提供一个例子，尽管这应该是显而易见的：

```perl
open (FILE, $file); $file=<FILE>;
close FILE;
```

## Open

打开文件是通过打开文件并赋予其一个文件句柄完成的。然后在程序中引用该文件句柄。打开文件有多种原因：为了读取、写入或追加。下表显示了打开文件的不同方式。

| 命令 | 功能 |
| :--- | :--- |
| `open (FILE, "filename")` | 从现有文件读取 |
| `open (DAVID, "<filename")` | 显式打开文件（与上述相同） |
| `open (church, ">filename")` | 创建文件并打开进行写入（覆盖现有文件） |
| `open (log,">>filename")` | 追加到文件（不覆盖现有文件） |
| `open(file, "| output-pipe-command")` | 设置输出过滤器 |
| `open(file, "input-pipe-command")` | 设置输入过滤器 |

如你所见，知道你打算对文件做什么非常重要；否则，你可能会意外删除现有文件，或向你本想覆盖的文件中追加内容。

## Hash Manipulation

哈希数组（Hash arrays）与普通数组不同。哈希数组是一种关联数组。普通数组是索引列表，每个项通过其索引数字引用，而哈希是一个键值对（value pairs）列表。在键值对中，第一个项（key）引用第二个项（value）；当引用第一个项时，返回的就是第二个项的值。你可以通过以下代表周期的哈希数组轻松地理解这一点：

```perl
%day_of_the_week = (0, Sunday, 1, Monday, 2, Tuesday, 3, Wednesday, 4, Thursday, 5, Friday, 6, Saturday);
```

哈希也可以这样这样定义：

```perl
%day_of_the_week = (0 => 'Sunday', 1 => 'Monday', 2 => 'Tuesday', 3 => 'Wednesday', 4 => 'Thursday', 5 => 'Friday', 6 => 'Saturday');
```

注意，最后一对后面的逗号必须存在。现在我们已经有了哈希，可以查看 `each`、键和值，并看看它们与 `%day_of_week` 的关系。

`each` 返回一个包含两个元素的列表，由哈希中下一个键和值组成。`each` 函数的独特之处在于，你可以通过连续调用 `each` 来遍历整个哈希。在遍历哈希时，你不向其中添加元素，但可以从中删除元素。

`keys %hash` 返回哈希的所有键（keys）。

`values %hash` 返回哈希的所有值（values）。





此函数返回哈希中的所有值。

此示例列出了我们 `%day_of_the_week` 哈希中的每一个值。

```perl
while (($key, $value) = each %day_of_the_week) {
    print "$key has value $value\n";
}
```

该程序的运行结果如下：

```
0 has value Sunday
1 has value Monday
2 has value Tuesday
3 has value Wednesday
4 has value Thursday
5 has value Friday
6 has value Saturday
```

# 系统操作

对于这些函数来说，“系统操作”并不是一个准确的术语。基本上，它们是从系统中读取某些内容，或者执行一次系统调用。我们也可以在这里包含其他函数（例如 `exec`、`fork`、`kill` 和 `times`），但这些是最基本的。

### time

`time` 返回自 UNIX 诞生（1970 年 1 月 1 日世界时）以来的秒数。它可以用于确定文件自上次访问以来已经多久，或者完成一项任务需要多久。`time` 的一个常见功能是作为 `localtime` 的参数。关于如何使用此函数的示例请参见 `localtime` 函数章节。

### localtime

此函数返回一个包含当前时区修正后时间的九元素列表。这九个元素如下表所示，以及它们可能的值。

| 元素 | 可能的值 |
| :--- | :--- |
| seconds | 0..59 |
| minutes | 0..59 |
| hour | 0..23 |
| day | 1..31 |
| month | 0..11 |
| year | 当前年份减去 1900 |
| day of the week | 0..6 |
| day of the year | 0..364 |
| 是否为夏令时 | 0..1 |

以下示例获取当前日期并打印时间、日期、星期、一年中的第几天以及是否为夏令时。你会注意到为了处理以零开头的值而的一些修改。此外，夏令时被更改为了 True 或 False。

```perl
#!/usr/bin/perl
($sec, $min, $hour, $mday, $year, $wday, $yday, $isdst) = localtime(time);
$year+=1900;
$yday++;
if ($sec < 10) { $sec = "0".$sec; }
if ($min < 10) { $min = "0".$min; }
if ($hour < 10) { $hour = "0".$hour; }
if ($isdst) {$isdst = "True"} }else { $isdst = "False" }
%tday = (
    0 => 'Sunday',
    1 => 'Monday',
    2 => 'Tuesday',
    3 => 'Wednesday',
    4 => 'Thursday',
    5 => 'Friday',
    6 => 'Saturday',
);
%tmonth = (
    0 => 'January',
    1 => 'February',
    2 => 'March',
    3 => 'April',
    4 => 'May',
    5 => 'June',
    6 => 'July',
    7 => 'August',
    8 => 'September',
    9 => 'October',
    10 => 'November',
    11 => 'December',
);
print "Time:  $hour:$min:$sec\n";
print "Today:  $tmonth{$mon} $mday,$year\n";
print "Day of the week: $tday{$wday}\n";
print "Day of the year: $yday\n";
print "Daylight Savings?: $isdst\n";
```

正如你所想象的，`time` 和 `localtime` 函数非常适合日志、报告以及其他需要知道事件发生时间的应用程序。

```perl
system(` `)
```





`system` 命令允许 Perl 程序访问系统。调用系统有两种方法：第一种是使用 `system` 命令；第二种是将命令放在反引号（back-ticks）之间。进行系统调用的问题在于它极大地限制了代码的可移植性。`system` 命令的优点之一是它会阻塞 `SIGINT` 和 `SIGQUIT`，防止程序被杀死。此外，通过 `system` 调程序执行结果可以保存到变量中，允许程序检查结果并根据结果执行任何必要的步骤。这里列出了非常简单的示例。幸运的是，Perl 内部有执行此任务的方法；因此，你可以保持程序的移植性。

```perl
$cur_dir = `ls`;
```

实际调用系统命令看起来如下：

```perl
$cur_dir = system (ls); # 括号不是必须的。
```

Perl 假设你清楚自己在做什么，因此它允许你随心所欲。像 `$remove = \`rm -r \` 这样的命令可能会毁掉整个系统！

## 变量操作

变量操作被分为几不同的组。首先是自增和自减符号（`++` 和 `--`）、点（`.`），然后是 `split` 和 `join`。最后是 `chomp` 命令。我们将按照这个顺序讨论这些主题。

### ++ 和 --

这两个符号将变量的值加一或减一。以下示例展示了将变量 `$penny` 增加一，然后减去一。

```perl
$penny++; $penny--;
```

你会发现这比下面的写法快得多：

```perl
$penny += 1;
$penny = $penny - 1;
```

### .

点（`.`）用于连接字符串。给定以下字符串：

```perl
$string1 = "University of Kentucky"; $string2 = "are the best players ever!";
$string3 = $string1.$string2;
```

在打印时会产生以下输出：
University of Kentuckyare the best players ![](img/4505ed21b36efb4eb4df5206fc03bad.gif)ever!

连接时没有在字符串之间留空格；因此，我们必须手动添加。可以这样做：

```perl
$string3 = $string1." ".$string2;
```

在打印时会产生以下结果：
University of Kentucky are the best players ![](img/4505ed21b36efb4eb4df5206fc03bad.gif)ever!

如果连接数字字符串，它们会像文本一样拼接在一起；这并不是相加。例如，以下行会生成 123456：

```perl
$a=123; $b=456;
$c=$a.$b;
print $c;
```

### split

`split` 用于将分隔符字符串转换为列表。

```perl
split /PATTERN/,EXPR,LIMIT;
split /PATTERN/,EXPR;
split /PATTERN/;
```

该函数扫描由 `EXPR` 提供的字符串，寻找由 `/PATTERN/` 指定的分隔符。然后将该字符串分割为一组子字符串。如果 `LIMIT` 设置为非零正整数，则字符串被分割成不超过于该数量的子字符串。在此过程中，匹配到的 `/PATTERN/` 部分会消失。

以下示例展示了如何将 `/etc/passwd` 文件分割成七不同的字段。账户行是以冒号分隔的，因此我们根据冒号模式进行搜索。

```perl
($user,$password,$uid,$gid,$gcos,$home,$init_prog) = split (/:/, @passwd);
```

因此，`split` 将大字符串拆分为较小的字符串。`join` 函数则取小字符串并将它们连接成大字符串。

### join

```perl
join EXPR,LIST;
```

`join` 获取字符串并将它们连接成单个字符串，并使用 `EXPR` 作为分隔符。这与 `split` 函数相反。以下示例获取了与密码条目相关的七个元素，并使用冒号作为 EXPR 将它们连接在一起。

```perl
$entry = join (':',$user,$password,$uid,$gid,$gcos,$home,$init_prog);
```




# chomp

`chomp VARIABLE`; `chomp LIST`; `chomp;`

`chomp` 用于移除所选字符串（或）末尾的换行符。如果省略了 `VARIABLE` 或 `LIST`，它将处理 `$_`。`chomp` 的一个常见用途是移除来自键盘输入的换行符。

```perl
print "Spell out the answer to this math problem: 2 + 2= Answer: ";
$answer = <STDIN>;
chomp $answer;
if ($answer eq "four" || $answer eq "Four") { 
    print "Right! The answer is four (4)" 
}
else { 
    print "Sorry! The answer is four (4)" 
}
```

如果你注释掉 `chomp $answer` 这一行，那么无论你输入什么答案，结果都将为假，因为我们的 if 语句正在寻找的是 "four" 或 "Four"，而这两个字符串中都不包含换行符。

## 调试你的脚本 (-d)

Perl 调试器并不是一个独立的程序。相反，你通过带有 `-d` 选项调用 Perl 来进入调试模式（Debug mode）。在调试模式下，你能够检查源代码、设置断点、转储函数调用栈、修改变量值等。本节并不会详述调试器的所有功能，也不会提供所有可用命令。本节的作用是向你介绍基础调试命令，并展示如何获取更多信息。具体来说，这里展示的内容包括如何设置、列出和删除断点；如何单步执行程序；如何检查和修改变量的值；如何获取帮助。

我将使用以下短程序作为描述调试器的基础。该程序名为 `rep.pl`，用于在文件中搜索并替换字符串。你会注意到我添加了 `-d` 选项，以便 Perl 在调试模式下运行。

```perl
#!/usr/bin/perl -d
# 打开文件，替换字符串的所有出现处。
# Usage: rep string string2 file
$file = @ARGV[2];
$search = @ARGV[0];
$replace = @ARGV[1];
if ($file eq "") {
    print "Usage: rep.pl [search] [replace] [file]\n";
}
else {
    open(FILE, "$file") or die "File not found: $!";
    @stuff = <FILE>;
    close FILE;
    foreach $line (@stuff) {
        $line =~ s/$search/$replace/g;
        push(@temp, $line);
    }
    open(FILE, ">$file");
    print FILE@temp; close FILE;
}
```

当我运行这个程序时，Perl 会以调试模式启动。这意味着代码会被编译。如果存在编译错误（例如缺少分号），调试器将不会运行。假设没有编译错误，调试器将会启动，并看起来如下所示：

```
Loading DB routines from perl5db.pl version 1 Emacs support available.
Enter h or h' for help.
main::./rep.pl:6): $file = @ARGV[2];
DB<1> By the way, I ran the program with the following command:
rep.pl david
```
在我们查看某些字符串的值以及程序本身的最终输出时，这将非常重要。

### 列出代码 (-l)

我想做的第一件事是列出我的代码。输入字母 l 即可列出代码。这会产生以下内容：

```
DB<1> l 6> $file = @ARGV[2];
7:   $search = @ARGV[0];
8:   $replace = @ARGV[1];
9:   if ($file eq "") {
10:    print "Usage: rep.pl [search] [replace] [file]\n";
11: }
12: else {
13:    open(FILE, "$file") or die "File not found: $!";
14:    @stuff = <FILE>;
DB<1>
```

调试器用 `==>` 指向当前行（第 6 行）。你会注意到它跳过了程序开头的注释并到了第 6 行。默认情况下，调试器列出 10 行代码。你可以通过放置一个起始行号，加上一个连字符和你想打印的行数来指定任何范围。因此，如果我告诉它我想打印程序的前三行，它看起来像这样：

```
DB<2> l 1-3
#!/usr/bin/perl -d
2    #
3    # 打开文件，替换字符串的所有出现处。
```

### 执行一行代码 (-n)

在我列出代码之后，现在我想 own 执行第一行。我通过输入字母 n 来执行第一行。这告诉调试器执行该行并进入下一行。产生了以下内容：

```
main::./rep.pl:7):    $search = @ARGV[0];
DB<3>
```

### 打印变量值

在此时，我告诉它执行接下来的两行代码。这给了我其他可以处理的内容。现在我想知道变量 `$_`、`$ARGV[0]`、`$ARGV[1]` 和 `$ARGV[2]` 的值。

```
DB<3> print $_
DB<4> print $ARGV[0]
david
DB<5> print $ARGV[1]
DB<6> print $ARGV[2]
DB<7>
```




正如我所料的，`$_` 的值是空的。`$ARGV[0]` 的值是 `"david"`，而 `$ARGV[1]` 和 `$ARGV[2]` 也是空的。我想把 `$ARGV[1]` 的值改为 David 而不是空。

我通过告诉变量它应该是什么来实现此点的，如下所示：

```perl
DB<7> $ARGV[1]="David"
DB<8> print $ARGV[1]
David
```

事实上，你可以从调试器命令行执行任何 Perl 命令，它将影响你正在运行的程序。唯一的限制是，每个提示符只能输入一条命令，并且在命令末尾不需要加分号。

### 断点 (Breakpoints)

你可以使用断点在程序中设置一个或多个停止点。断点一旦设置，它就会告诉调试器在运行到这一行时停止执行。在我们的示例中，我想在第 10 行设置一个断点。我希望程序停止在 `if` 语句处，这样我就可以确定具体的值了。要设置断点，你使用字母 `b` 后加上行号。可选的是，你还可以在那里放置一个条件。如果放置了条件，只有当运行到该行且条件为真时，断点才会停止程序执行。因此，我想做的是设置一个当 `$file` 等于 `""` 时停止程序的断点。该命令看起来如下：

```perl
DB<5> b 10 $file eq "" DB<6> l 6-15
6=> $file = $ARGV[2];
7  $search = $ARGV[0];
8  $replace = $ARGV[1];
9
10 b if ($file eq "") {
11 print "Usage: rep.pl [search] [replace] [file]";
12
13 else {
14 open(FILE, "$file") die "File not found";
15 @stuff = <FILE>;
```

你注意到第 10 行看起来不同吗？它的行号旁边有一个 `b`。这就是调试器指示断点的方式。现在我想让调试器运行到遇到断点的地方。我通过输入字母 `c` 来实现。我在 `c` 后面跟着一个 `w`，这样我就可以看到当前行周围的代码窗口。

```perl
DB<7> c main::./rep.pl:10): if ($file eq "") {
DB<7> w
7  $search = $ARGV[0];
8  $replace = $ARGV[1];
9
10=>b if ($file eq "") {
11 print "Usage: rep.pl [search] [replace] [file]";
12
13 else {
14 open(FILE, "$file") die "File not found";
15 @stuff = <FILE>;
16 close FILE;
```

现在我想再看一眼我的变量 `$ARGV[0]` 和 `$ARGV[1]`，所以我输入了以下命令：

```perl
DB<7> print $ARGV[0] $ARGV[1];
```

记得，我说过过每行一条命令。在这里我写了两个命令。我告诉它打印两个值。这里是命令的结果：

```text
Scalar found operator expected at (eval) line 2, at end of line
eval('@@, $, /, @W) = @saved;package main; $@ = $@DB::db_stop;
print $ARGV[0] $ARGV[1];
called at /usr/lib/perl5/perl5db.perl line 153
DB::eval called at /usr/lib/perl5/perl5db.perl line 1062
DB::DB called at ./rep.pl line 10
(Missing operator before ?)
eval('@@, $, /, @W) = @saved;package main; $@ = $@DB:
Segmentation fault
```

嗯，这告诉我了两点。首先，每行使用一条命令。其次，它告诉我如果发生错误，就会发生段错误（segmentation fault）， Perl 程序将会崩溃。所以，我重启重试。我重新添加了断点，以便保持与之前相同的条件。但我现在意识到，我不想要那个断点。我现在需要删除它。要删除断点，你输入小写的 `d`。如果 `d` 后面跟着行号，则会移除该行的断点。大写的 `D` 将删除所有断点。

```perl
DB<2> d 10
6  $file = $ARGV[2];
7  $search = $ARGV[0];
8  $replace = $ARGV[1];
9
10 if ($file eq "") {
11 print "Usage: rep.pl [search] [replace] [file]";
12
13 else {
14 open(FILE, "$file") die "File not found";
15 @stuff = <FILE>;
```

我在第 10 行的断点现在消失了。我添加了一些断点，现在我想列出它们。我通过大写的 `L` 来实现，如下：

```perl
DB<7> L ./rep.pl:
6  $file = $ARGV[2];
  break if (1)
11 print "Usage: rep.pl [search] [replace] [file]";
  break if (1)
```

似乎我设置了三个断点：第 6 行、11 行和 15 行。用一个大写的 `D` 将删除它们所有的，我就准备就绪了。

```perl
DB<7> D Deleting all breakpoints...
```




调试器还可以做很多事情。要详细介绍其中所有的功能需要用一整个章节的内容。因此，在我们结束关于调试器的章节之前，让我向你介绍一个进一步理解调试器的来源。这个来源就是内置在调试器内部的帮助功能。如果你只输入一个 `h`，你将获得一个所有可用命令选项的详细列表。如果你像我一样，阅读速度快到跟不上它在屏幕上滚动的速度。因此，如果你输入 `h h`，它将以不同的格式提供相同的列表。这种格式是双列列表，应该可以适应单个屏幕。每个命令后面都有一个关于该命令功能的简短描述。我看到 `v` 显示模块的版本，例如：

```
DB<10> v 'Term/ReadLine.pm' => '/usr/lib/perl5/Term/ReadLine.pm'
'dumpvar.pl' => '/usr/lib/perl5/dumpvar.pl'
'perl5db.pl' => '1 from /usr/lib/perl5/perl5db.pl'
```

最后，当你完成时，只需输入 `q` 即可退出程序。

# 结语

Perl 是一种功能完备且强大的语言，它结合了 C 语言的力量和 Shell 编程的易用性。然而，Perl 并不止于此。Perl 支持面向对象。Perl 可以与其他语言结合，包括 C、TK 和 Java。它易于使用，并且有强大的后端支持。

有关 Perl 的更多信息，请访问 Perl 官网 www.perl.com。你可以在那里找到 Perl 的最新版本以及 Perl 存档网络（CPAN），其中有大量的代码，大部分代码与 Perl 本身采用相同的版权许可。你还可以在那里找到常见问题解答（FAQs）。如果你遇到困难，也可以去 `comp.lang.perl.misc` 新组并在那里提问。

# 附录 A UNIX 命令

注意：`[` `]` 表示可选字段。

- `=` - 设置 变量
  - 用法：`variable=new-contents`
  - 标准输入：未使用
  - 标准输出：未使用
  - 另请：`apropos`（第 54 页）

- `apropos` - 等于 `man -k`

- `at` - 在指定的日期/时间运行命令
  - 标准输入：用于输入一个或多个以 EOT 键（通常为 `Ctrl+D`）结束的命令
  - 标准输出：未使用
  - 另请：（第 313 页）
  - 注意：为了防止显示 `Usage`，请编辑 `/usr/lib/cron/at.allow` 和 `at.deny`

- `awk` - Aho, Weinberger, 和 Kernighans 的类 C 编程语言
  - 标准输入：仅在给出 `list-of-files` 时使用
  - 标准输出：用于显示结果
  - 注意：在某些系统上，请使用 `nawk` (new awk) 或 `gawk` (GNU awk)。
  - 从命令行使用 `awk` 显示选行：
    - `awk '$n == "string"'`（如果字段 `n` 等于字符串，则显示该行）
    - `awk '$n > 3.5'`（如果字段 `n` 大于该值，则显示该行）
    - `awk '$n ~ /R.E./'`（如果字段 `n` 包含 `R.E.`，则显示该行）
    - 另请：（第 407 页）
  - 使用 `awk` 显示字段：
    - `awk '{print $1, $5, $0}'`
    - `awk '{if ($5 > 20000) $5=20000} {print "file: " $9}'`
    - `awk '{printf("Name: %16s, Size: %5d, Blocks: %6.2f\n", $9, $5, $5/512)}'`
  - 从命令行使用 `awk` 替换字符串：
    - `awk '$3 == "acme" {gsub("R.E.", "repl")}'`
    - `awk '$n > 3.5 {gsub("R.E.", "repl")}'`
    - `awk '$n ~ /R.E./ {gsub("R.E.", "repl")}'`



更多信息，请参阅第 429 页。

### awk
在命令行中使用 `awk` 移除字符串：
```bash
awk '$3 == "acme" { gsub ("R.E.","") } {print}'
```
[list-of-files]

另请
更多信息，请参阅第 429 页。

### banner
以横幅标题大小显示文字
用法：`banner [要显示的单词]`
- **标准输入**：仅在命令行未提供单词时使用
- **标准输出**：用于显示结果

第 759 页

### 另请
更多信息，请参阅第 167 页
**注意**：除非对空格进行了转义或引用，否则会将不同的单词放在不同的行上。每行会在 10 个字符处截断。

### batch
当系统忙时运行
用法：`batch`
- **标准输入**：用于输入一个或多个命令
- **通过 `EOT` 键结束（通常为 `Ctrl+D`）**
- **标准输出**：未使用

另请
更多信息，请参阅第 35 页
**注意**：要防止使用，请编辑 `/usr/lib/cron/at.allow` 和 `at.deny`。

### bc
计算计算器
可以进行无限算术。
- 两位小数，输入 `scale=2`。
- 退出，输入 `quit`。

### bg
在后台启动挂起的任务
用法：`bg [JOBID]`
- **实用**：同于 `Korn shell`、`Bourne shell` (`sh`) 和 `C shell` (`csh`) 下的 `kill`。

### cal
显示日历
用法：`cal [year]`
- **标准输入**：未使用
- **标准输出**：用于显示结果
- **注意**：`98` 与 `1998` 不是同一个年份。

### cancel
取消打印作业
用法：`cancel JOBID`
- **标准输入**：未使用
- **标准输出**：未使用

### cat
合并文件
用法：`cat [file]`
- **标准输入**：在未提供文件时使用
- **标准输出**：用于显示结果

另请
更多信息，请参阅第 23 页
**实用选项**：
- `-n` 在输出中包含行号
- **nb** 仅对非空行计数
- `-v` 将控制字符显示为打印字符

另请
更多信息，请参阅第 164 页。




## `cd` - 切换目录

**用法:** `cd dirname`

**标准输入:** 不使用
**标准输出:** `CDPATH` 外均不使用（参见下文备注）

**相关**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息请参阅第 42 页

**备注：** 如果未给出 `dirname`，将带你回到主目录。如果 `dirname` 是一个基名（basename），`cd` 将检查 `dirname` 是否为 `CDPATH` 中任何父目录的子目录。如果是，`cd` 将切换到该目录并将其完整路径输出到标准输出。

## `chgrp` - 修改文件的所属组

**用法:** `chgrp newgroup list-of-files`

**标准输入:** 不使用
**标准输出:** 不使用

只能由文件所有者或 root 用户执行。

第 761 页

## `chmod` - 修改文件的模式（权限）

**用法:** `chmod perms list-of-files`

**标准输入:** 不使用
**标准输出:** 不使用

只能由文件所有者或 root 用户执行。权限可以通过两种方式指定：
- 符号模式：`[ugoa][+-][rwx]`
- 绝对值或数值：`read=4+write=2+execute=1`，`owner*100+group*10+other`, `4000=SUID`, `2000=SGID`, `1000=sticky`

## `chown` - 修改文件的所有者

**用法:** `chgrp newowner list-of-files`（注：原文用法处写成了 `chgrp`）

**标准输入:** 不使用
**标准输出:** 不使用

只能由文件所有者或 root 用户执行。

## `cmp` - 比较任意类型的两个文件

**用法:** `cmp file1 file2`

**标准输入:** 如果 `file1` 或 `file2` 为连字符 `-`，则不使用
**标准输出:** 用于显示结果

**备注：** `cmp` 在发现第一个差异后就会停止。无输出意味着文件相同。

**相关**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息请参阅第 67 页
有用选项：
- `-l` 列出所有差异

## `col` - 从管道中过滤控制字符

**用法:** `col options`

**标准输入:** 为 `col` 提供输入
**标准输出:** 用于显示结果

第 762 页

**相关**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息请参阅第 167-168 页
有用选项：
- `-b` 过滤掉退格键
- `-x` 不将空格转换为制表符

## `comm` - 显示两个排序文件之间的唯一行

**用法:** `comm file1 file2`

**标准输入:** 仅当 `file1` 或 `file2` 为连字符 `-` 时使用
**标准输出:** 用于显示结果

**备注：**
- `col 1` 显示仅于 `file1` 的行
- `col 2` 显示仅于 `file2` 的行
- `col 3` 显示共同行





## compress
压缩文件

用法：`compress filename`
标准输入：未使用
标准输出：未使用

另请
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *更多信息，请参阅第 219 页*

备注：在压缩后的文件名后添加 `.Z`

有用选项：
- `-H` 允许在 SCO UNIX 上获得更好的压缩率。

## copy
特殊文件拷贝

第 73 页

并非所有系统均可用

用法：`copy source dest`
`cp file1 file2`
`cp list-of-files dest-dir/`
标准输入：未使用
标准输出：未使用

另请
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *更多信息，请参阅第 181 页*

有用选项：
- `-m` 设置目的地的修改时间和最后访问时间与源文件一致。
- `-o` 设置所有者和组与源文件一致。
- `-r` 递归拷贝目录，因此所有子目录都会被拷贝。

## cpio
拷贝入/出，特别是到磁带

用法：生成文件名
cpio 选项
标准输入：用于向 `cpio` 提供路径列表
标准输出：通常重定向到磁带设备

另请
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *更多信息，请参阅第 355 页*

第 764 页

主要选项：（必须是其中之一第一个选项。）
- `-o` 意味着在 `cpio` 存档中写入（保存）文件。
- `-it` 在磁带上列出文件而不恢复它们。
- `-i` 意味着从 `cpio` 存档中恢复。
- `-p` 将子目录传递到另一个目录。

另请
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) *更多信息，请参阅第 189 页*

使用 `cpio` 备份的选项：
- `-a` 意味着将每个文件的最后访问时间重置为 `cpio` 访问文件之前的时间。
- `-B` 意味着每记录阻塞 10 个块（5120 字节）。
- `-c` 意味着写入字符头以提高对其他 UNIX 系统的移植性。可能与 `-H odc` 同时使用。
- `-C XX` 意味着将磁带块大小设置为 `XX` 字节。





## 通用选项

- `-H odc` 意味着 SVR4 系统将写入预-SVR4 系统可以读取的 `cpio` 磁带。可能与 `-c` 选项配合使用。
- `-L` 意味着跟随符号链接（AIX 上不支持）。
- `-v` 意味着详细输出，在复制每个文件时列出它们。
- `-V` 意味着在备份每个文件时仅显示一个点。

## 使用 cpio 恢复的选项

- `-A` 意味着抑制开头的斜杠，以便将绝对路径文件恢复到其他目录（SCO）。
- `-c` 意味着查找字符头，以提高其他 UNIX 系统具有更好的可移植性。某些 UNIX 系统将自动检测归档文件或磁带是否使用此选项写入。在其他系统上，如果磁带是使用 `-c` 写入的，则在恢复时必须包含 `-c`。
- `-d` 意味着根据需要创建目标目录。
- `-k` 意味着跳过磁带上的损坏区域并尝试恢复读取文件。
- `-m` 意味着保持每个文件的最后修改日期/时间与源目录一致。
- `-t` 意味着不恢复任何文件；仅显示磁带的目录内容。
- `-u` 意味着无条件覆盖任何现有的目标文件，否则旧文件将不会覆盖新文件。
- `-v` 意味着详细输出，在复制每个文件时列出它们。
- `-V` 意味着在备份每个文件时仅显示一个点。

另见 ![arrow.gif](img/ad91af06ad9657f0a338bded4c2e.gif)*有关更多信息，请参阅第 18 页

## 使用 cpio 传递文件的选项

- `-a` 意味着将每个文件的最后访问时间重置为 `cpio` 访问该文件之前的时间。如果包含了 `-m` 选项，则可能使用。
- `-d` 意味着根据需要创建目标目录。
- `-L` 意味着跟随软链接（见下一节），以便复制指向的文件而非指针文件。
- `-m` 意味着保持每个目标文件的最后修改日期/时间与源目录一致。如果包含了 `-a` 选项，则可能使用。
- `-u` 意味着无条件覆盖任何现有的目标文件，否则旧文件将不会覆盖新文件。
- `-v` 意味着详细输出，在复制每个文件时列出它们。
- `-V` 意味着在备份每个文件时仅显示一个点。

## crontab - 为此用户提交全新的 cron 表

- 用法 `crontab NEWTABLE` # 提交新表
- `crontab -l` # 列出当前表
- 标准输入：未使用
- 标准输出：用于显示 `-l` 选项的输出结果

另见 ![arrow.gif](img/ad91af06ad9657f0a338bded4c2e.gif)*有关更多信息，请参阅第 30 页
注意：为了防止使用，请编辑 `/usr/lib/cron.allow` 和 `cron.deny`。

## crypt - 加密或解密文件或管道

- `-l` 列出当前表
- 用法：`crypt < filename`
- 标准输入：从管道重定向
- 标准输出：用于显示结果

另见 ![arrow.gif](img/ad91af06ad9657f0a338bded4c2e.gif)*有关更多信息，请参阅第 17 页
注意：解密需要与加密时相同的密钥。

## csh - 运行 C shell

## csplit - 按上下文将文件拆分为较文件

- 用法：`csplit options filename [prefix]`




较小文件将为 `prefix00`、`prefix01`、`prefix02`。
默认前缀为 `xx`。
标准输入：未使用
标准输出：未使用

### 另
更多信息请参阅第 227 页

### 有用的选项：
- `-k` 即使发生错误（如使用 99 作为重复计数），也保留已创建的文件。

### 示例：
```bash
csplit -k filename '/Chapter/' '{99}'
csplit filename '/boundaryword/' '/boundaryword/'
```

### cut - 切并保留输出的列或字段
### 用法
cut options [list-of-files]
标准输入：在未提供 list-of-files 时使用
标准输出：用于显示结果

#### 有用的选项：
- `-c5-16,42` 指定输出中要保留的列。
- `-dX` 将 `X` 设置为分隔符。
- `-fn` 切割并保留第 `n` 个字段。

#### 另
相关信息请参阅第 37 页

### date - 显示系统日期和时间
### 用法
日期格式 `+%X`，其中 `X` 可以：
- `S` 秒 (09)
- `M` 分 (09)
- `I` 小时 (12)
- `p` am 或 pm
- `H` 小时 (23)
- `T` 时间 (hh:mm:ss)
- `Z` 时区
- `A` 星期名称
- `a` 星期字母
- `w` 星期几 (06)
- `d` 月份几号 (31)
- `j` 年中的第几天 (366)
- `U` 周 (53)
- `m` 月份 (12)
- `b` 月份字母
- `h` 月份（三个字母）
- `B` 完整的月份
- `y` 年（两位数字）
- `Y` 年（四位数字）
- `D` MM/DD/YY
- `c` 日期/时间

#### 另
相关信息请参阅第 40 页

### df - 显示磁盘空闲块




### 另请
更多信息，请参阅第 262 页

### 有用选项：
- `-b` 表示忽略末尾空格，并将连续的空格视为单个空格。

### 另请
更多信息，请参阅第 262 页

### diff3 - 比较 3 个文本文件
**用法：** `diff3 file1 file2 file3`
- **标准输入：** 无
- **标准输出：** 用于显示结果
**注：** 在结果中，`===` 表示所有三个文件均不同，如所示。`==n` 表示文件 `n` (1、2 或 3) 与其他不同，如所示。

第 769 页

### 另请
更多信息，请参阅第 264 页

### du - 显示磁盘占用率

### echo - 显示文本
- `-n` 用于抑制行尾换行符
- 在某些系统上使用 `echo -n text`
- 在其他系统上使用 `echo "some text"`

### egrep -  grep，但支持额外的 R.E. 通配符
查看 grep。查看通配符、正则表达式

### expr - 评估简单计算
例如：`CNT=`expr $CNT + 1``
`VALUE=`expr $2``

### fg - 将后台作业移至前台
**用法：** `fg %JOBID`
同于 Korn shell 下的 `%JOBID` 的 `kill`

### fgrep - grep，但不支持任何 R.E. 通配符
查看 grep

### file - 显示文件类型
**用法：** `file-of-files`
- **标准输入：** 无
- **标准输出：** 用于显示结果
**注：** 如果没有数字，它将根据文件开头进行最佳猜测。
文件名: 通配符

第 70 页

### find - 根据搜索选项查找文件
**用法：** `find start-dir actions`
- **标准输入：** 无
- **标准输出：** 用于显示结果
**注：** find 会搜索起始目录的所有子目录。

### 另请
更多信息，请参阅第 153 页





# 查找选项

- `-ctime [+-]ndays` 仅选择索引（inode）在 `ndays` 天前修改的文件。选项 `+` 表示大于 `ndays`，`-` 表示少于 `ndays`，否则表示恰好在 `ndays` 天前。
  - 另请参：更多信息请参阅第 252 页

- `-depth` 意味着在列出目录本身之前列出目录的内容。从非根账户恢复数据时有时有用。

- `-group GROUP` 意味着仅选择组为 `GROUP` 的文件。

- `-inum NUM` 意味着仅选择索引号为 `NUM` 的文件。
  - 另请参：更多信息请参阅第 195 页

- `-mount` 意味着仅选择与起始目录同一文件系统中的文件。

- `-mtime [+-]ndays` 意味着仅选择最后修改于 `ndays` 天前的文件。选项 `+` 表示大于 `ndays`，`-` 表示少于 `ndays`，否则表示恰好在 `ndays` 天前。
  - 另请参：更多信息请参阅第 252 页

- `-name FNAME` 仅选择基名为 `FNAME` 的文件。
  - 第 771 页：`FNAME` 可以包含通配符，但必须放在引号内。

- `-newer filename` 仅选择比 `filename` 更新的文件（即修改时间更晚）。
  - 另请参：更多信息请参阅第 252 页

- `-perm DDD` 仅选择八进制权限为 `DDD` 的文件。

- `-perm -DDDD` 仅选择开启了与 `DDDD` 权限的文件。它会忽略 `DDDD` 中关闭的权限。

- `-size [+-]nblocks` 意味着仅选择大小为 `nblocks` 的文件。选项 `+` 表示大于 `nblocks`，`-` 表示少于 `nblocks`，否则表示大小恰好为 `nblocks`。
  - 另请参：更多信息请参阅第 259 页

- `-type TYPE` 仅选择类型为 `TYPE` 的文件，其中 `TYPE` 可以是：
  - `f` 表示普通文件
  - `d` 表示目录
  - `c` 表示字符设备
  - `b` 表示块设备

- `-user USER` 仅选择由 `USER` 所有的文件。

### 逻辑分组
- 如果你指定了两个选项，则两者都为真才能选中文件。
- `-o` 表示逻辑或（OR）。
- `\( \)` 可用于分组。
- `!` 表示反向测试（否定）。

### 有用的操作
- `-print` 意味着显示选中的名称。在某些 UNIX 系统中，如果没有指定任何操作，默认会执行此操作。
- `-exec` 为每个文件执行后续 UNIX 命令。命令中的 `{}` 表示文件名放置的位置。命令必须以 `;` 结尾。
  - 第 772 页：更多信息请参阅第 252, 259 页。

- `finger` - 显示一个用户或所有登录用户的信息。
- `fsck` - 文件系统检查
  - 另请参：更多信息请参阅第 296 页

### 有用的选项：





## 命令参考

### 选项
- `-b` 表示如果在检查根文件系统时对磁盘执行了重大修改，则重启（重要）。
- `-s` 表示无条件地重建空闲列表。

### grep
`grep` - 全局查找正则表达式 (R.E.) 并打印（显示）该行。

**用法：** `grep R.E.pattern [list-of-files]`

- **标准输入：** 仅在未提供 `list-of-files` 时使用
- **标准输出：** 用于显示结果。

**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 380 页

#### 有用的选项：
- `-c` 表示仅显示文件名和包含模式的行数。

**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 386 页

#### 模式 (grep)
- `-i` 表示忽略大小写。 | 第 73 页
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 382 页

- `-l` 表示仅显示包含模式的文件名。
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 386 页

#### 模式 (grep)
- `-n` 表示在显示的每行中包含行号。
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 385 页

- `-v` 表示反转测试，显示不包含模式的行。
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 385 页

### gzip
- `-y` 与 `-i` 相同，但仅适用于旧版系统。
- `gzip` - 压缩文件。

**用法：** `gzip filename`

- **标准输入：** 不使用
- **标准输出：** 不使用
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 219 页

**备注：** 在压缩后的文件名后添加 `.gz`。

### head
`head` - 显示文件或管道的初始行。

**用法：** `head options [list-of-files]`

- **标准输入：** 仅在未提供 `list-of-files` 时使用
- **标准输出：** 用于显示结果。
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 215 页

#### 选项：
- `-n` 表示仅 `n` 行。
- `id` - 显示您的用户和组。
- `jobs` (Korn shell) - 显示您的后台作业。
- **标准输入：** 不使用
- **标准输出：** 用于显示结果。
**另请**
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 322 页

### join
`join` - 根据连接字段连接两个文件的行。

**用法：** `join options file1 file2`





## 命令概述
- **标准输入 (Std input)**：仅在提供为连字符 (`-`) 的文件时使用。
- **标准输出 (Std output)**：用于显示结果。

### 另请
更多信息请参阅第 224 页。

### 有用选项：
- `-aN`表示包含文件 `N` 中的所有行。
- `-jN`表示使用字段 `N` 而不是 1 作为连接字段。
- `-jN M`表示使用文件 `N` 中的字段 `M` 作为连接字段。
- `-o A.B`表示显示文件 `A` 中的字段 `B`。
- `-t`表示将字段分隔符设置为后续字符。

---

## kill (Bourne shell) - 终止 UNIX 进程

### 使用方法
`kill -SIG PID`

- **标准输入 (Std input)**：未使用
- **标准输出 (Std output)**：未使用

### 另请
更多信息请参阅第 320 页。

### 有用选项：
`-SIG`表示向进程发送信号。如果省略，则发送 `SIGTERM`（终止）或替换为 `15`。

### 通过 `kill` 发送的其他信号：
- `SIGHUP` (`SIG = 1`)：终端或父进程终止。
- `SIGINT` (`SIG = 2`)：按下中断键（`Ctrl+C` 或 Del）。
- `SIGQUIT` (`SIG = 3`)：按下退出键。
- `SIGKILL` (`SIG = 9`)：强制终止

---

## kill (Korn shell) - 终止后台进程

### 使用方法
`kill -SIG PID`（同前述 `kill` [Bourne shell]）或 `kill %JOBID`

- **标准输入 (Std input)**：未使用
- **标准输出 (Std output)**：显示进程行

### 另请
更多信息请参阅第 325 页。

### 有用选项：
- `%JOBID`表示编号为 `JOBID` 的作业。
- `%+`表示最近一次放入后台的作业。
- `%%`等同于 `%+`。
- `%-`表示倒数第二个放入后台的作业。
- `%CMD`表示命令以 `CMD` 开头的作业。
- `%?CMD`表示所有命令包含 `CMD` 的作业。

---

## ksh (Korn shell)- 重定向

### Shell 选项：
- `>filename` -覆盖 `noclobber` 并重定向到现有文件。
- `noclobber` - 防止重定向到现有文件。
- `/etc/profile` - 在 `/etc` 目录启动。
- `.profile` - 在 `home` 目录运行。
- `less` - 每次显示一屏文件。

### 使用方法
`less [list-files]`

- **标准输入 (Std input)**：仅在给出 `list-files` 时使用。
- **标准输出 (Std output)**：用于结果。

### 另请
更多信息请参阅第 160 页。

### 注意：
在大多数商业 UNIX 系统上不可用。每个屏幕末部的提示符为行 `XXX`。

### 进入 less 后的有用命令：




- `h` 显示帮助菜单。
- `space` 或 `f` 或 `Ctrl+f` 跳到下一页。
- `b` 或 `Ctrl+b` 跳到上一页。
- `G` 跳到最后一页。
- `1G` 跳到第一页。
- `nf` 向前移动 n 页。
- `nb` 向后移动 n 页。
- `nG` 跳转到第 n 行。
- `/string` 跳转到该字符串的下次出现位置。
- `n` 重复上一次搜索。
- `d` 或 `Ctrl+D` 向下移动半屏。
- `r` 或 `Ctrl+R` 或 `Ctrl+L` 重新显示当前页面。
- `!CMD` 作为子 shell 执行 UNIX 命令，完成后恢复到 less 模式。

### ln
创建软链接/符号链接或硬链接
- **用法**: `ln [-s] existing-file link-file`
- **标准输入**: 不使用
- **标准输出**: 不使用
- **另请**: 第 193 页
- **常用选项**:
    - `-s` 表示创建软链接/符号链接而非硬链接。
- 第 777 页

### lp (System V)
打印文件或管道
- **用法**: `lp options [list-of-files]`
- **标准输入**: 仅在未提供 list-of-files 时使用
- **标准输出**: 不使用
- **另请**: 第 172 页
- **常用选项**:
    - `-n` 表示打印份数。
    - `-d` 表示输出到打印机。如果未提供 `-d`，则打印到默认打印机。如果没有默认打印机，则报错。

### lpr (BSD)
打印文件或管道
- **用法**: `lpr options [list-of-files]`
- **标准输入**: 仅在提供了 list-of-files 时使用
- **标准输出**: 不使用
- **另请**: 第 172 页
- **常用选项**:
    - `-#` 表示打印份数。
    - `-P` 表示输出到打印机。如果未提供 `-P`，则打印到系统默认打印机。如果没有默认打印机，则报错。

### lpstat
显示打印后台打印状态
- **用法**: `lpstat options`
- **标准输入**: 不使用
- **标准输出**: 用于显示结果
- **另请**: 第 171 页
- **备注**: 如果未提供选项，则显示队列中等待的打印请求。
- 第 778 页
- `-p -D` 表示哪些打印机可用及其描述（如果有）。

### ls
列出目录中的文件
- **用法**: `ls options [list-of-files-or-directories]`




## 命令参考

- **标准输入**: 未使用
- **标准输出**: 用于显示结果
- **备注**: 如果没有指定目录，则列出当前目录。

### 有用选项
- `-a` 表示显示所有文件，包括隐藏文件、非隐藏文件和双点目录（..）。
- `-b` 表示显示文件名中的任何控制字符。
- `-c` 表示如果是长格式，则显示 inode 最后一次更改的日期/时间。
- `-C` 表示以列的形式输出输出。

### 另请
- 更多信息，请参阅第 46 页

- `-d` 表示显示目录名称而非目录的内容。

### 另请
- 更多信息，请参阅第 148 页

- `-F` 表示通过添加符号来显示文件类型：目录添加斜杠（`/`），可执行文件添加星号（`*`），符号链接添加 `@` 符号（`@`）。
### 另请
- 更多信息，请参阅第 46 页

- `-i` 表示将 inode 节点作为每行的第一个字段。
### 另请
- 更多信息，请参阅第 195 页

- `-l` 表示以长格式列出文件，包括最后修改的日期/时间。第 779 页
### 另请
- 更多信息，请参阅第 252 页

- `-L` 表示跟踪符号链接并显示指向的文件信息。

- `-r` 表示按反向顺序列出文件。
### 另请
- 更多信息，请参阅第 252 页

- `-R` 递归列出子目录。

- `-t` 表示按时间/日期而非名称的顺序列出文件。
### 另请
- 更多信息，请参阅第 252 页

- `-u` 表示如果是长格式，则显示最后访问的日期/时间。
### 另请
- 更多信息，请参阅第 252 页

## `mail/mailx`
读取和发送邮件

## `man`
显示在线手册页
用法：`man unixcmd`
- **标准输入**: 未使用
- **标准输出**: 用于显示结果
### 另请
- 更多信息，请参阅第 89 页

### 有用选项
- `-a` 表示显示包含此命令的所有章节，而不只是第一个。
- `-k` 表示显示描述包含 `WORD` 的名称。
- `-M` 表示创建新目录。

## `dirname`
用法：`dirname`
- **标准输入**: 未使用
- **标准输出**: 未使用
第 780 页
### 另请
- 更多信息，请参阅第 51 页





## 有用选项
- `-p` 表示创建 `dirname` 所需的任何父目录。
- `more` - 每次一屏显示文件或管道。

### 使用方法
`more [list-of-files]`

- **标准输入 (Std input)**：仅在未提供 `list-of-files` 时使用。
- **标准输出 (Std output)**：用于显示结果。

### 相关
更多信息请参阅第 160 页。

### 注意事项
每个屏幕末尾提示符为 `--`。

### 进入 more 环境后的后的用命令：
- `h` 显示帮助菜单。
- `space` 或 `f` 跳到下一页。

在某些 UNIX 版本中，如果通过管道传递 `more` 命令，以下某些命令在 `more` 中不可用：
- `Ctrl+B` 回到上一页。
- `G` 跳到末页。
- `1G` 跳到第一页。
- `nf` 向前移动 n 页。
- `nb` 向后移动 n 页。
- `nG` 跳转到第 n 行。
- `/string` 跳转到该字符串下一次出现的位置。
- `n` 重复上次搜索。
- `d` 向滚动半屏。
- `Ctrl+L` 重新显示当前页。
- `!CMD` 作为子壳执行 `CMD`，完成后退出。

---

## mt - 磁带命令
### 使用方法
`mt -f /dev/XXX`

- **标准输入 (Std input)**：不使用。
- **标准输出 (Std output)**：不使用。

参见 `tape` 命令。

### 相关
更多信息请参阅第 336 页。

### 有用命令：
- `rewind retention`

---

## mv - 移动/重命名文件
### 使用方法
`mv file1 file2`
`mv list-of-files dest-dir/dir2`

- **标准输入 (Std input)**：不使用。
- **标准输出 (Std output)**：不使用。

### 相关
更多信息请参阅第 181 页

### 有用选项：
- `-f` 表示如果文件有写权限但对目录没有写权限，强制移动而不请求确认。
- `-i` 表示与用户交互，并在覆盖现有文件前请求权限。

---

## nice - 以低优先级启动作业
### 使用方法
`nice -VAL UNIXCMD`

- **标准输入 (Std input)**：不使用。
- **标准输出 (Std output)**：由于 `UNIXCMD` 使用它们，因此也使用。

### 相关
更多信息请参阅第 317 页

### 有用选项：
- `-VAL` 表示将优先级降低 VAL 个点。
- `--VAL` 表示将优先级提高 VAL 个点（仅限 root）。





# nl
`nl` - 在文件输出或管道中显示编号。

## 使用
`nl [list-of-files]`

- **标准输入**: 仅在未提供 `list-of-files` 时使用。
- **标准输出**: 用于显示结果。

### 另请
更多信息请参阅第 164 页。

### 有用选项：
- `-ba` 表示对所有行编号，包括空行。

# nohup
`nohup` - 启动注销后不会终止的后台进程。

## 使用
`nohup UNIXCMD &`

- **标准输入**: 不使用。
- **标准输出**: 因为 `UNIXCMD` 会使用标准输出。

### 另请
更多信息请参阅第 320 页。

# od
`od` - 以八进制转格式显示。

## 使用
`od [list-of-files]`

- **标准输入**: 仅在提供 `list-of-files` 时使用。
- **标准输出**: 用于显示结果。

### 另请
更多信息请参阅第 165 页。

### 有用选项：
- `-b` 表示以字节显示输出，而不是字。
- `-c` 表示显示任何可打印字符。
- `-d` 表示以十进制显示输出。
- `-x` 表示以十六进制显示输出。

# passwd
`passwd` - 修改你的密码。

# paste
`paste` - 在每行中并排显示文件。

## 使用
`paste list-of-files`

- **标准输入**: 仅当将横线 (`-`) 作为文件名时使用。
- **标准输出**: 用于显示结果。

### 另请
更多信息请参阅第 223 页。

# perl
`perl` - 实用提取和报告语言。

- **标准输入**: 仅在提供 `list-of-files` 时使用。
- **标准输出**: 用于显示结果。

## 从命令行使用 perl 显示选定的行：
```
perl -ne'print if /R.E./xi' [list-of-files]
```
- `/x` 表示忽略 `R.E.` 中的空格以提高可读性。
- `/i` 表示忽略大小写。

### 另请
更多信息请参阅第 404 页。

## 从命令行使用 perl 进行替换或删除：
```
perl -pe's/R.E./replacement/gx' [list-of-files]
perl -pe's/R.E./replacement/' [list-of-files]
```
- 仅在行中找到 `R.E.` 模式时执行。
- `/x` 表示忽略 `R.E.` 中的空格以提高可读性。
- `/g` 表示全局替换，而不只是每行仅替换一次。

### 另请
更多信息请参阅第 425 页。

### 有用选项：
- `-e` 表示 Perl 脚本在命令行中。

第 784 页
另请





## 选项

- `-n` 表示处理标准输入或指定文件的每一行，但除非另有指示否则不显示这些行。（更多信息，请参阅第 404 页）
- `-p` 表示处理标准输入或指定文件的每一行并在处理后显示每一行。（更多信息，请参阅第 404 页）

## pg
`pg` - 一页一次显示文件或管道

### 用
`pg [list-of-files]`

- **标准输入**: 仅在未提供 `list-of-files` 时使用
- **标准输出**: 用于显示结果

### 相关
（更多信息，请参阅第 425 页）

### 注意事项
屏幕底部的提示符是冒号（`:`）。

进入 pg 后的可用命令：
- `h` 显示帮助菜单。
- `Enter` 进入下一页。
- `-` 返回上一页。
- `$` 跳到最后一页（处理巨大的管道时可能会导致系统崩溃！）。
- `1` 跳到第一页。
- `+n` 向前移动 `n` 页。
- `-n` 向后移动 `n` 页。
- `nl` 跳到第 `n` 行。
- `/string` 跳到该字符串的下一个出现处。
- `/` 重复上一次搜索。
- `/string/b` 将找到的字符串放在底部，以便捕捉所有出现处。
- `d` 向下移动半屏。
- `d` 显示当前页。
- `!CMD` 作为子壳执行 `CMD`，完成后恢复 `pg`。

## pr
`pr` - 格式化输出以打印

### 用
`pr options [list-of-files]`

- **标准输入**: 仅在未提供 `list-of-files` 时使用
- **标准输出**: 用于显示结果

### 相关
（更多信息，请参阅第 175 页）

### 有用选项
- `-COLS` 意味着使用 `COLS` 中的数字作为页面上创建输出的列数。截断任何超过列宽的行。
- `-e` 表示将制表符扩展为空格。如果提供了 `SIZ`，则使用该值作为每个制表符字符数，否则使用 8。
- `-f` 表示在每页末尾插入分页符。
- `-HEAD` 意味着在页面顶部使用文件名。
- `-l` 意味着每页行数。
- `-n` 意味着正文字符数。如果提供了 `SIZ`，则使用长度，否则使用 5。
- `-p` 意味着在页结束后发出响声并等待 Enter 键。

## ps
`ps` - 显示进程状态

- **标准输入**: 未使用
- **标准输出**: 用于显示状态

### 相关
（更多信息，请参阅第 317 页）

## pwd
`pwd` - 打印工作目录




## pwd
### 使用
`pwd`

- **标准输入**: 未使用
- **标准输出**: 用于显示结果
- **相关参考**: 更多信息，请参阅第 43 页

## qcan - 在 AIX 上取消作业
### 使用
`qcan options`

- **标准输入**: 未使用
- **标准输出**: 未使用
- **相关参考**: 更多信息，请参阅第 174 页

### 选项
- `-P PTR -x JOBID` 表示取消 `PTR` 的作业 ID。
- 正则表达式通配符：见 Wildcard

## renice - 降低运行作业的优先级
### 使用
`renice -VAL PID`

- **标准输入**: 未使用
- **标准输出**: 未使用
- **相关参考**: 更多信息，请参阅第 38 页

### 选项
- `-VAL` 表示降低优先级 `VAL`。
- `--VAL` 表示提高优先级 `VAL`（仅限 root）。

## rm - 删除文件
### 使用
`rm list-of-files`

- **标准输入**: 未使用
- **标准输出**: 未使用
- **注意**: 如果 `list-of-files` 包含目录且未给出 `-r` 选项，将报错。
- **相关参考**: 更多信息，请参阅第 191 页

### 选项
- `-f` 表示在文件不可写时无需询问直接删除。
- `-i` 表示交互模式，在删除每个文件前均会确认。
- `-r` 表示如果 `list-of-files` 包含目录，则递归删除该目录及其所有子目录和文件。**警告**：操作非常危险！出错后无法撤回！
- **相关参考**: 更多信息，请参阅第 53 页

## rmdir - 删除目录
`rmdir`

要删除的目录除点 (`.`) 和双点 (`..`) 之外必须为空。

## sed - 流编辑器
### 使用
`sed cmd list-of-files`

- **标准输入**: 仅当提供了 `list-of-files` 时使用
- **标准输出**: 用于显示结果
- **常用命令**:
    - `q` 表示退出。
    - `s` 表示替换。
- **相关参考**: 更多信息，请参阅第 215 页




# 另请
更多信息请参阅第 412 页。

## 在命令行中使用 sed 替换输出中的字符串：

```bash
sed 's/R.E./repl/g' [list-of-files]
```

- `sed 's:R.E.:repl:g' [list-of-files]` # 可以更改分隔符
- `sed '5,23 s/R.E./repl/g' [list-of-files]` 仅更改第 5 至 23 行，$ 表示行尾
- `sed '/acme/ s/R.E./repl/g' [list-of-files]` 仅更改包含 acme 的行
- `sed '/s1/,/s2/ s/R.E./repl/g' [list-of-files]` 仅更改从首次出现 s1 直到下一次出现 s2 之间的行
- `sed 's/.*acme.*/ *** canceled *** /` 替换整行

## 另请
更多信息请参阅第 412 页。

## 在命令行中使用 sed 删除输出中的字符串：

```bash
sed 's/R.E.//g' [list-of-files]
```

## 另请
更多信息请参阅第 12 页。

- 运行 Bourne shell 反引号（`` ` ``）。
- 注释以空格开头，然后是井号（`#`）。

## 另请
更多信息请参阅第 24 页。

## 文件名通配符
参见 通配符

## 重定向
- `> file` 或 `1> file` 重定向标准输出。
- `2> file` 重定向标准错误。
- `>> file` 或 `2>> file` 追加输出或错误。
- `2>&1` 表示将标准错误重定向到标准输出所在的地方。
- 参见 tee 管道。

Shell 启动运行 `/etc/profile`，然后运行用户目录下的 `.profile`。

## 特殊变量
- `CDPATH` - 常用目录的父目录可选列表。
- `PATH` - 搜索命令时使用的目录列表。

## 另请
更多信息请参阅第 54 页。

## shutdown (BSD 版本) - 关闭系统
- 标准输入：未使用
- 标准输出：未使用

## 另请
更多信息请参阅第 300 页。

## 注意：需要 root 权限
常用选项：
- `-h` 表示停止系统。
- `-r` 表示关机并重启。
- `now` 表示不要等待关机。
- `+MIN` 表示在关机前等待 `MIN` 分钟。

## shutdown (System V 版本) - 关闭 UNIX 系统
- 标准输入：未使用
- 标准输出：未使用




## 通用信息
标准输出：未使用

### 另请
更多信息，请参阅第 300 页

### 注意事项
需要 root 权限

### 有用选项
- `-g MIN` 表示广播警告并在关闭前等待 `MIN` 分钟的宽限期。
- `-i STATE` 表示进入运行级别 `STATE`。
- `-y` 表示在宽限期结束后不再询问用户确认关机。

## sleep
`sleep` - 使程序暂停 `n` 秒

## sort
`sort` - 对文件或管道进行排序

### 使用方法
`sort options [list-of-files]`
多个文件在排序前会进行合并。
标准输入：仅当 `list-of-files` 中包含横杠 (`-`) 或未提供 `list-of-files` 时才使用。
标准输出：用于显示结果

### 另请
更多信息，请参阅 202, 223 和 29

### 有用选项
初始选项适用于所有键。跟在排序键后的选项仅适用于该键。
- `-b` 表示忽略排序字段开头的空格。
- `-d` 表示忽略开头的标点符号。
- `-f` 表示忽略大小写合并比较。
- `-k` 表示使用新方法定义排序：`-k opts, n`。
- `-n` 表示按数值排序。
- `-o` 表示输出到后续的文件中。
- `-r` 表示按反序排序。
- `+m` 表示每行跳过 `m` 个字段，然后开始排序。
- `+n` 定义行内的排序键。

### 另请
更多信息，请参阅第 204 页
更多信息，请参阅第 208 页
更多信息，请参阅第 207 页
更多信息，请参阅第 207, 259 页
更多信息，请参阅第 209, 259 页
更多信息，请参阅第 210 页

## split
`split` - 将文件拆分为行数相同的小文件

### 使用方法
`split options [filename] [prefix]`
较小文件将命名为 `prefixaa`、`prefixab`、`prefixac` 等。
标准输入：仅在未提供文件名或提供横杠 (`-`) 作为文件名时使用。





## strings
**标准输出**: 未使用

**另需**
更多信息，请参阅第 226 页

**常用选项：**
- `-N` 创建每份 `N` 行的较小文件（最后一份除外）。默认值为 1000。
- `strings` - 显示任意类型文件中的可打印字符串

**用法**: `strings options [list-of-files]`
**标准输入**: 仅在未给出 `list-of-files` 时使用
**标准输出**: 用于显示结果

**另需**
更多信息，请参阅第 165 页

**常用选项：**
- `-n LEN` 意味着设置报告的可打印序列最小长度 `LEN`。

## stty
### 设置/显示终端特性
第 79 页

**常用选项：**
- `-a` 意味着显示所有 `stty` 选项，如果关闭则在前面加上减号 (`-`)。

**常用选项：**
- `erase` 意味着设置/显示 `erase` 键。
**另需**
更多信息，请参阅第 103 页

- `intr` 意味着设置/显示 `interrupt` 键。
**另需**
更多信息，请参阅第 111 页

- `topstop` 意味着当后台作业开始任何输出时暂停其运行。
**另需**
更多信息，请参阅第 32 页

## sum
- `su` 成为超级用户或其他用户
- `sum` 计算文件或管道的校验和
**用法**: `sum [list-of-files]`
**标准输入**: 仅在未给出 `list-of-files` 时使用
**标准输出**: 用于显示结果
**备注**: 校验和匹配表示数据相同的相同的概率极高。
**另需**
更多信息，请参阅第 267, 269 页

- `-r` 意味着计算循环校验和，该校验和可以检测顺序以及内容的差异。
**另需**
更多信息，请参阅第 267, 269 页

## tail
显示文件或管道的最后几行
**用法**: `tail [filename]`
**标准输入**: 仅在给出 `filename` 时使用
第 93 页
**标准输出**: 用于显示结果
**另需**
更多信息，请参阅第 216 页

**常用选项：**
- `-f` 意味着追踪，即持续显示附加到文件的任何数据，直到按下回车键。
 `-n` 意味着仅显示 `n` 行。（警告：`n` 的大值可能会被忽略。）
- `+n` 意味着从第 `n` 行显示到文件末尾。

## tape
发布磁带命令





# 使用
`tape cmd /dev/XXX?`

- **标准输入**: 未使用
- **标准输出**: 未使用
- 请参阅 `mt` 命令。

## 相关
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 336 页

## 有用命令
- `rewind`
- `reten`
- `tar` - 磁带归档

## 另
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 340 页

## 备份时的常用选项
- `-c` 表示创建备份（必须是第一个选项）。
- `-b` 表示设置磁带块大小。
- `-f` 表示指定设备或文件。
- `-h` 表示符号链接 (AIX)。
- `-L` 表示符号链接 (SCO)。
- `-v` 表示详细模式。

## 第 79 页
### 恢复时的常用选项
- `-x` 表示从备份中提取文件（必须是第一个选项）。
- `-A` 表示忽略文件名开头的斜杠 (SCO)。
- `-m` 将最后修改时间设置为恢复执行的时间，否则设置原始磁带文件的最后修改时间。
- `-v` 表示详细模式。

### tee - 将标准输入保存到文件并将相同信息发送到标准输出
用法：`tee filename`
- **标准输入**: 用于读取输入
- **标准输出**: 用于显示当前输出

相关
![sarrow.gif](img/ad91af06ad96c57f0a338bded4c42f0e.gif) 更多信息，请参阅第 16 页

## 有用选项
- `-a` 表示追加到文件，而不是覆盖。

### test - 评估条件为真或假
用法：`test condition [condition]`

#### 文件测试
- `-f name`: name 是否为普通文件？
- `-d name`: name 是否为目录？
- `-r name`: name 是否可读？
- `-w name`: name 是否可写？
- `-x name`: name 是否可执行？
- `-c name`: name 是否为字符设备？
- `-b name`: name 是否为块设备？
- `-s name`: name 是否为大小大于 0 的文件？

#### 第 95 页
- `-h`: name 是否为符号链接？

#### 字符串测试
- `-n`: 字符串不为空
- `-z`: 字符串为空
- `s1 = s2`: 两个字符串是否相同？
- `s1 != s2`: 两个字符串是否不同？

#### 数值测试
- `v1 -eq v2`: v1 是否等于 v2？
- 我们也可以测试 `-ne`, `-gt`, `-ge`, `-lt`, `-le`。

#### 组合测试





## 逻辑运算符
- `-a` 表示逻辑与（AND）。
- `-o` 表示逻辑或（OR）。

## touch
`touch` - 更新文件的最后访问和修改日期/时间。
- 如果文件不存在，它将创建一个空文件，但不会影响已存在的内容。

## tr
`tr` - 翻译字符。
- **用法**: `tr "list1" "list2" < file1 > file2`
- **标准输入**: 始终使用，不接受文件名。
- **标准输出**: 用于显示结果。
- **备注**: 如果在 `list1` 中找到 `char`，则将其替换为 `list2` 中对应的字符。
- **另请**: 更多信息请参阅第 441 页。
- **常用选项**:
    - `-d` 表示删除列表 1 中找到的字符。
- **常用示例**:
    - `tr "[A-Z]" "[a-z]" < file1 > file2` # 将大写转换为小写
    - `tr "\001-\376" "\001-\177" < file1 > file2` # 关闭第 8 位
    - `tr '\001-\010\037\177'^* < file1 > file2` # 将大多数控制字符翻译为 ^

## type
`type` - 显示命令的路径。
- **用法**: `type unixcmd`
- **标准输入**: 不使用。
- **标准输出**: 用于显示结果。
- **另请**: 更多信息请参阅第 100 页。
- **备注**: 在 Bourne shell 和 Korn shell 中均可用。

## tty
`tty` - 显示当前系统 tty 端口名称。

## umask
`umask` - 显示当前的文件创建权限掩码。

## uname
`uname` - 显示类型和名称。

## uniq
`uniq` - 删除重复行。
- **用法**: `uniq [list-of-files]`
- **标准输入**: 仅在提供 `list-of-files` 时才使用。
- **标准输出**: 用于显示结果。
- **另请**: 更多信息请参阅第 445 页。
- **常用选项**:
    - `-d` 表示仅显示重复行。
    - `-u` 表示仅显示唯一的行。
    - `-c` 表示显示每行重复内容的计数。

## uucp
`uucp` - 通过串口和调制解调器在 UNIX 到 UNIX 之间拷贝。

## uuencode/uudecode
`uuencode/uudecode` - 将文件转换/恢复为打印文本。
- **用法**: `uuencode binary dest text`
- **标准输入**: 仅在提供 `binary` 时才使用。
- **标准输出**: 用于显示结果。
- **用法**: `uudecode text`
- **另请**: 更多信息请参阅第 221 页。

## vi
`vi` - 可视化编辑器。
- **另请**: 更多信息请参阅第 449, 471 页。
- **启动 vi**:





# vi 命令参考

## 选项
- `vi -r` 显示可以恢复的文件。
- `view` 表示以只读模式运行。

## 冒号命令
- `:abbrev word` 定义新短语。
- `:!cmd` 在子壳中运行 `cmd`，然后恢复 `vi`。
- `:f` 显示当前行和文件名。
- `:map c string` 将字符 `c` 映射到字符串 `string`。
- `:q!` 不保存并退出。
- `:w` 写入磁盘。
- `:w file` 保存到文件 `file` 中。
- `:wq` 写入（保存更改）并退出。

### 设置模式、缩写及还原
- `:set autoindent`, `:set ai`, `:set noai`
- `:set ignorecase`, `:set ic`, `:set noic`
- `:set number`, `:set nu`, `:set nonu`
- `:set showmode`, `:set noshowmode`
- `:set wrapmargin=10`，通过设置为零来关闭

## 冒号模式下的替换
- `!! cmd` 用 `cmd` 的输出替换当前行。
- `!a cmd` 从光标处到标记 `a` 应用 `cmd`。
- `!a sed 's/st1/st2/g'` 将从光标到标记 `a` 找到的字符串 `st1` 替换为 `st2`。
- `%! sed 's/st1/st2/g'` 替换整个文件的 `st1`。`st1` 可以包含表达式通配符。

## 复制、粘贴以及删除与粘贴
- `ya` 复制到包含标记 `a` 的行开头。
- ``a` 复制到标记 `a`。
- `y...` 在 `y` 后接移动命令，以指示要复制和保存的文本范围。
- `ay...` 复制并保存到命名缓冲区 `a` 中。
- `p` 将无名缓冲区粘贴到当前光标处。
- `ap` 将命名缓冲区粘贴到当前光标处。
- `np` 粘贴 `n` 次前删除的内容。

## 删除命令
- `dd` 删除行。
- `x` 删除字符。
- `D` 删除到行尾。
- `da` 删除到包含标记 `a` 的行开头。
- ``a` 删除到标记 `a`。
- `d...` 在 `d` 后接移动命令，以指示要删除的内容。
- `ad...` 删除并保存到命名缓冲区 `a` 中。

## 插入文本命令
- `i` 在光标处或左侧插入，直到按 Esc。
- `I` 在行首插入，直到按 Esc。
- `a` 在光标后插入，直到按 Esc。
- `A` 在行尾插入，直到按 Esc。
- `o` 在下方打开一行并插入，直到按 Esc。
- `O` 在上方打开一行并插入，直到按 Esc。

## 其他命令
- `J` 合并 `n` 行。
- 大多数 vi 命令允许前加计数。
- `u` 撤销上一次插入/删除/修改。
- `U` 将行恢复到首次进入该行的状态。
- `.` 重复上一次插入/删除/更改。

## 修改文本
- `C` 修改到行尾并输入，直到按 Esc。





# 编辑器命令

- `CC` 意味着修改当前行直到 `Esc`。
- `r` 意味着替换字符。
- `R` 意味着替换直到 `Esc`。

## 移动光标

- `0`、`^`、`$` 表示行首、第一个可打印字符、行尾。
- `h`, `j`, `k`, `l` 等同于左、下、上、右方向键。
- `H`, `M`, `L` 意味着移动到当前屏幕的高、中、低位置。
- `Gn` 意味着跳转到第 `n` 行；`G` 意味着跳转到文件末尾。
- `Ctrl+F`/`Ctrl+B` 向前/后移动一屏。
- `Ctrl+D`/`Ctrl+U` 向下/向上半屏。
- `W`, `B`, `E` 意味着向前、向后或移动到单词末尾。
- `w`, `b`, `e` 与前面的说明相同，但跳转到下一个连续单词或非单词。

## 标记 (Marks)

- `mc` 意味着设置标记 `c`。
- `'c` 意味着跳转到包含标记 `c` 的行首。
- ``c`` 意味着跳转到标记 `c`。

## 搜索

- `/string` 向前移动到 `string` 的下次出现处。
- `?string` 向后移动到 `string`。
- 允许使用正则表达式。
- `/` 若不带字符串则重复上一次搜索。
- `n` 或 `N` 也重复之前的搜索。
- `fc` 意味着移动到字符 `c`。
- `;` 意味着重复上一个 `f` 命令。
- `%` 意味着查找匹配的闭合符号，例如 `[{ }]`。

## 命令

### whence
`whence` - 显示命令的路径
- 用法：`whence unixcmd`
- 标准输入：未使用
- 标准输出：用于显示结果
- 另 `which`
- 注意：在 Korn shell 中有效，但在 Bourne shell 中无效。

### which
`which` - 显示命令的完整路径
- 用法：`which unixcmd`
- 标准输入：未使用
- 标准输出：用于显示结果
- 另 `whence`
- 注意：在 Bourne shell 中有效，但在 Korn shell 中无效。

### who
`who` - 显示谁在使用系统以及其他系统信息
- 用法：`who options`
- 标准输入：未使用
- 标准输出：用于显示结果

### reboot
- `b` 显示上次重启的时间。
- `r` 显示当前进入的运行级别。
- 另 `wildcard`

### 文件名生成
- `*` 意味着零或多个任意字符，斜杠（/`）和开头的点除外。





# 包含模式 (*)

`?` 表示除斜杠 `/` 和开头的点之外的任意单个字符。

另请
更多信息，请参阅第 232 页

# 位置 (?)

`[...]` 表示列出的备选项中恰好选择一个，但排除 `/` 和开头的点除外。

另请
更多信息，请参阅第 239 页

`[!... ]` 表示除列出的备选项之外的任意字符，且不能匹配斜杠 `/` 或开头的点。

另请
更多信息，请参阅第 241 页

# 位置 ([!...])

`[!!]` - 通配符正则表达式 (R.E.)

另请
更多信息，请参阅第 243 页

模式开头的 `^` 表示行首。

第 802 页

另请
更多信息，请参阅第 388 页

模式末尾的 `$` 表示行尾。

另请
更多信息，请参阅第 389 页

`.` 表示任意的单个字符。

另请
更多信息，请参阅第 390 页

`[...] ]` 表示列出的备选项中恰好选择一个。

另请
更多信息，请参阅第 395 页

`[^...]` 表示除列出的备选项之外的任意字符。

另请
更多信息，请参阅第 396 页

`{n}` 表示前一个元素恰好出现 `n` 次（`grep` 和 `sed` 支持，`egrep` 不支持或在 Perl 中使用 `{n}`）。

另请
更多信息，请参阅第 397 页

`{n,}` 表示前一个元素出现 `n` 次或更多（`grep` 和 `sed` 支持，`egrep` 不支持或在 Perl 中使用 `{n,}`）。

另请
`{n,m}` 表示前一个元素出现 `n` 到 `m` 次（包含两者）之间（`grep` 和 `sed` 支持，`egrep` 不支持或在 Perl 中使用 `{n,m}`）。

另请
`*` 表示前一个元素出现 0 次或多次。

另请
更多信息，请参阅第 398 页

它匹配最长的跨度。

第 803 页

另请
更多信息，请参阅第 424 页



- `*` 匹配最短的跨度（仅限 perl）。另参见：更多信息请参阅第 426 页。
- `.*` 表示任意字符出现 0 次或多次。
- 这仅仅是 `*` 通配符的一个示例。
- `+` 表示前一个元素出现 1 次或多次（支持 `egrep`、`perl` 和 `awk`，但 `grep` 和 `sed` 不支持）。另参见：更多信息请参阅第 403 页。
- 匹配最长的跨度。另参见：更多信息请参阅第 424 页。
- `+?` 匹配最短的跨度（仅限 perl）。另参见：更多信息请信息请参阅第 426 页。
- `?` 表示前一个元素出现 0 次或 1 次（支持 `egrep`、`perl` 和 `awk`，但 `grep` 和 `sed` 不支持）。另参见：更多信息请参阅第 403 页。
- `|` 允许搜索备用模式（支持 `egrep`、`perl` 和 `awk`，但 `grep` 和 `sed` 不支持）。另参见：更多信息请参阅第 403 页。
- `()` 允许备用模式分组（支持 `egrep`、`perl` 和 `awk`，但 `grep` 和 `sed` 不支持）。另参见：更多信息请参阅第 403 页。
- `\( \)` 记住匹配括号内模式的字符（支持 `grep` 和 `sed`，`egrep` 或 `awk` 不支持；perl 使用 `()`）。第 804 页。
- `\1`、`\2` 指代被记住的字符串 1 或 2。
- `\b` 表示单词边界（仅限 perl）。另参见：更多信息请参阅第 405 页。
- `\B` 表示非单词边界（仅限 perl）。另参见：更多信息请参阅第 405 页。
- `\X` 在任何通配符 `X` 之前加上反斜杠 (\)，以便将其作为字符串中的字文字使用。

### xargs
使用传递的参数执行另一个 UNIX 命令
`xargs cmd [opts]`
- 标准输入：用于传递给 `cmd` 的参数列表。
- 标准输出：`cmd` 使用它的输出。
- 有用的选项：
    - `-n NUMB` 限制每个 `cmd` 上的参数数量。第 405 页。

### 术语表
- `[]` 中括号。
- `{}` 花括号。
- `$HOME` 指向登录目录的环境变量。
- `$PATH` 包含用于搜索 UNIX 命令的目录列表的 shell 环境变量。




| 扩展名 | 说明 |
| :--- | :--- |
| `.bmp` | 位图图形文件。 |
| `.c` | C 源代码。 |
| `.gif` | GIF 图形文件。 |
| `.gz` | 使用 GNU gzip 工具压缩的文件。 |
| `.h` | C 头文件。 |
| `.htm` | HTML 文档。 |
| `.html` | HTML 文档。 |
| `.o` | 编译后的对象文件。 |
| `.ps` | PostScript 文件。 |
| `.tgz` | Gzipped 的 tar 包。 |
| `.tif` | TIFF 图形。 |
| `.txt` | 文本文档。 |
| `.Z` | 使用 `compress` 命令压缩的文件。 |
| `/` | 根目录。 |
| `/dev/null` | 发送你不感兴趣的输出的地方；也是在你没有输入（但程序或命令需要输入）时获取输入的地方。这被称为“位桶”（旧比特位死亡的地方）。 |
| `/dev` | 设备目录。 |
| `/etc/group` | 该文件包含关于组的信息、其中包含的用户以及访问所需的密码。密码实际上可能在另一个文件（shadow 文件）中，以防止免受攻击。 |
| `/etc/ittab` | 该文件包含 UNIX 将为其发布提示符的活动终端列表。它还包含一个需要初始化的后台进程列表。某些某些版本的 UNIX 使用其他文件，例如 `/etc/tty`。 |
| `/etc/motd` | 日消息；通常包含系统管理员认为你应当了解的重要信息。该文件在用户登录系统时显示。 |
| `/etc/passwd` | 包含用户信息和密码。密码实际上可能在另一个文件（shadow 文件）中，以防止免受攻击。 |
| `/etc/profile` | 包含所有 Bourne 和 Korn shell 用户通用的 shell 环境特性的文件。 |
| `/usr/local` | 本地开发的公共可执行文件所在目录。 |
| `/var/spool` | 各种打印缓冲目录。 |

绝对路径名是一种引用文件的方法，其中指定了从根目录开始的所有目录。绝对路径始终以斜杠开头，表示它从根目录开始（例如，`/reports/abc` 指向 `reports` 子目录下的 `abc` 文件）。

目录的行政控制：对目录具有写权限的用户对该目录拥有有效的行政控制。除了创建文件外，他们还可以删除和重命名其他用户的文件，即使他们没有修改这些文件的权限。如果设置了目录粘滞位（sticky bit），拥有写权限也不会赋予对目录的行政控制权。

ANSI 美国国家标准协会。





## API (应用程序接口)
计算机操作系统、应用程序或第三方工具所规定的特定方法，程序员在编写应用程序时可以通过该方法向操作系统提出请求。也称为应用程序设计员接口（Application Programmers Interface）。

## 应用程序数据文件
通常是多个文件中的一个，包含该应用程序的数据。

## 应用程序
一种软件程序，通常是许多程序之一，为应用程序提供部分编程功能。

## 应用程序
一个或多个提供特定功能的软件程序，例如会计应用程序。

## Arguments
参见 *parameters*。

## ARPA
参见 *DARPA*。

## ASCII
美国信息交换标准代码。用于在大多数计算机的内存中表示字符。

## AT&T UNIX
在 AT&T 贝尔实验室开发的 UNIX 原始版本，后来被称为 UNIX 系统实验室。许多当前的 UNIX 版本都是其后代；即使是 BSD UNIX 也是源自早期的 AT&T UNIX。

## awk
由 A.V. Aho、P.J. Weinberger 和 Brian W. Kernighan 开发的编程语言。该语言构建在 `C` 之，包含了 `grep` 的正则表达式搜索，并添加了 `C` 语言中缺失的高级字符串和数组处理。`nawk`、`gawk` 是该语言的版本。

## 后台作业
你启动但独立于你的键盘和屏幕运行的任务，以便你可以做其他事情。许多重要的 UNIX 进程作为后台作业运行，等待用户请求或其他事件（这些通常被称为系统守护进程）。参见 *Foreground job*。

## 备份
将 UNIX 系统、应用程序和数据文件存存储在可移动介质上以备将来取用的过程。

## Basename
路径中不包含斜杠 `/` 的最长右侧部分（例如，在 `/usr/fred/reports/acme` 中，`acme` 是该路径的 basename）。basename 可以是任何类型的文件，包括目录。此外，书中使用的 `basename` 也可以指代没有斜杠且没有目录部分的文件。

## Bash
代表 GNU Bourne Again Shell（GNU 再次 Bourne 壳），包含了大多数 Bourne shell (`sh`) 和 Korn shell (`ksh`) 的增强功能。

## Boot 或 boot up（启动）
启动操作系统（UNIX）的过程。

## Bourne shell
所有 UNIX 系统上的标准 shell，支持基础编程但很少提供用户便利性。

## BSD UNIX
由伯克利软件发行版（Berkeley Software Distribution）开发并在加州大学伯克利分校编写的 UNIX 版本。

## Berkeley Software Distribution（伯克利软件发行版）

## C
由 Brian W. Kernighan 和 Dennis M. Ritchie 开发的编程语言。`C` 语言具有高度移植性，适用于包括主机、PC 以及的 UNIX 系统在内的许多平台。

## CAD
计算机辅助设计。

## Cast（类型转换）
用于强制类型转换的编程结构。

## CD-ROM
紧凑光学只读存储。存储在与音乐 CD 相同物理形式上的计算机可读数据。容量大、价格廉、速度比硬盘慢，且仅限于读取。存在某些版本是可写入的（`CD-R`，可录光型），以及其他可以写入一次或多次的格式。

## C shell
由 Bill Joy 在伯克利编写的 UNIX 用户界面。它具有类似于 `C` 语言编程的语法。





# 术语表

- **CGI**: 通用网关接口。在 Web 页面与服务器上执行的程序或脚本之间传输数据的方法。这些程序可以处理数据，并通过动态创建 HTML 将结果返回给用户的浏览器。

- **字符设备 (Character)**: 用于与字符型 I/O 设备（如终端、打印机或网络通信线路）通信的设备文件。所有 I/O 访问都被视为一系列字节（字符）。

- **字母字符 (Characters, alphabetic)**: 字母 `A` 到 `Z` 以及 `a` 到 `z`。

- **字母数字字符 (Characters, alphanumeric)**: 字母 `A` 到 `Z`、`a` 到 `z`，以及数字 `0` 到 `9`。

- **控制字符 (Characters, control)**: 任何不可打印字符。这些字符用于控制设备、分隔记录以及在打印机上出页。

- **数字字符 (Characters, digits)**: 数字 `0` 到 `9`。

- **数值字符 (Characters, numeric)**: 数字 `0` 到 `9`。

- **校验和 (Checksum)**: 通过累加文件内所有字符产生的数值。该总和允许你快速检查文件是否与另一个文件匹配。通过比较校验和，你可以快速检查两个文件可能包含相同的内容，或者一个文件的内容是否仍与其计算校验和时的内容相同。通常在添加每个字符后，会对总和进行移位或旋转（类似于乘以 2）。这被称为旋转校验和，它可以检测数据相同但顺序不同的文件。校验和的目标是：两个文件之间的微小差异应产生校验和之间的巨大差异。如果两个文件的校验和相同，那么它们极可能包含相同的内容。如果它们的校验和不同，则这两个文件一定不相同。

- **子目录 (Child directory)**: 与子目录相同。

- **子进程 (Child process)**: 由另一个进程或任务启动的进程或任务，被称为父进程。

- **子进程 (Child process)**: 见 `subprocess`。

- **子 Shell (Child shell)**: 见 `subprocess`。

- **类 (Class)**: 具有属性（数据）和行为（代码或函数）的对象模型。它也被视为抽象形式的对象的集合。

- **命令替换 (Command substitution)**: Shell 的一种功能，允许使用包含另一个 UNIX 命令的反引号（`` ``）将该命令的输出替换为当前命令中的单词。

- **命令行编辑 (Command-line editing)**: UNIX Shell 支持调回之前输入的命令、对其进行修改，然后执行新版本。命令历史可以在会话之间保留（你昨天执行的命令在今天登录时可以使用）。某些 Shell 支持命令行编辑模式，该模式使用 `vi` 或 `emacs` 编辑器的子集进行命令的调回和修改。

- **命令行历史 (Command-line history)**: 见 `Command-line editing`。

- **命令行参数 (Command-line parameters)**: 用于指定传递给执行程序或过程的参数。也称为命令行参数。

- **注释 (Comment)**: 为人类读者准备的解释性文字。通常注释有特殊的起始字符，以便计算机会忽略它们。在 UNIX Shell 编程中，使用井号（#）来开始注释。其他编程语言可以使用其他起始字符作为注释。

- **配置文件 (Configuration files)**: 用于初始化和设置特定命令及程序环境的信息集合。Shell 配置文件用于设置用户环境。

- **包含单词 (Contained words)**: 在 `vi` 中，包含单词是任何字母和数字的组合。它们通过标点符号、空格、制表符和行尾与其他单词隔开。例如，`abc-def=3` 包含三个单词：`abc`、`def` 和 `3`。见 *分隔单词* (Separated words) 和 *非单词* (Non-words)。





### CPU
CPU 中央处理单元。计算机的大脑，即计算引擎和逻辑控制器。

### 当前目录
作为任何相对路径基准的目录。如果没有没有指定目录，许多 UNIX 命令将假定此目录。使用 `cd` 命令更改你的当前目录。

### 守护进程 (Daemon)
一种与系统相关的后台进程，通常以 root 权限运行并处理来自其他进程的服务请求。

### DARPA（美国国防部）
国防高级研究计划局。资助了 TCP/IP 和 ARPAnet（互联网的前身）的发展。

### 数据库服务器
参见 *Server, database*。

### 默认目录
与当前目录相同。

### 设备文件
用于实现物理设备访问的文件。这为 UNIX 下访问存储介质提供了一种统一的方法；数据文件和设备（如磁带和通信设施）都被实现为文件。对于程序员来说，它们之间没有本质区别。

### 设备节点
用于访问磁带驱动器或软磁盘等硬件的一种文件。

### 数字 (Digit)
0 到 9 之间的字符之一。数字始终是一个单个字符。一个或多个数字组成一个数字。

### 目录
组织和收集文件的一种手段。目录本身是一个文件，由其包含的文件列表组成。根目录 `/` 是最顶层，所有其他目录都包含在其中（直接或间接地）。目录可能包含其他目录，这些称为子目录。

### 目录导航
在目录之间移动的过程被称为导航。你的当前目录被称为工作目录。你的登录目录被称为默认目录或主目录。使用 `cd` 命令，你可以在目录树结构中上下移动。

### Dirname
路径名中从开始到最后一个内部斜杠 `/` 的部分。例如，在 `/usr/fred/reports/acme` 中，`/usr/fred/reports` 就是 `dirname`。如果路径名中没有斜杠 `/`，则其 `dirname` 由点 `.` 表示，代表当前目录。参见 *Basename*。

### DNS
域名服务器。用于在互联网上的机器名称（`name.domain.com`）与数字型 IP 地址（`123.45.111.123`）之间进行转换。

### DOS
磁盘操作系统。基于使用磁盘存储命令的操作系统。它也是个人计算机上 MS-DOS 和 PC-DOS 的通用名称。MS-DOS 是微软销售的版本，PC-DOS 是 销售的版本。两者都基于微软的代码。

### Page
8

### Double
双精度浮点数。

### dpi
每英寸点数。

### 电子邮件
通过电子介质而非本地邮政发送的消息。有许多设计用于处理局域网（LAN）环境中邮件的专用系统；其中大多数也可以通过互联网发送。大多数互联网（开放）电子邮件系统使用 MIME 来处理附件数据（可以是二进制的）。

### EBCDIC
扩展二进制编码进制交换码。用于大型机计算机内存中表示字符的编码。

### Ed
一种用于行文本编辑的常用工具。

### Elm
交互式邮件程序。

### emacs
一种免费提供的编辑器，现在是 GNU 软件发行的一部分。最初由 Richard M. Stallman 在 20 世纪 70 年代末在麻省理工学院编写，适用于许多平台。它具有极强的扩展性并有自己的编程语言；该名称代表使用宏进行编辑（editing with macros）。





# F

### 封装 (Encapsulation)
将数据（属性）和函数（以代码形式的行为）组合成对象的过程。数据和函数在对象内部紧密耦合。这并不是所有程序员都能按照自己的方式访问结构中的数据，而是必须使用与该数据关联的代码。这促进了代码复用和处理数据的标准化方法。

### 环境变量 (Environment variables)
参见 `Variables, environmental`。

### 转义字符 (Escaped characters)
前面带有反斜杠（`\`）的字符。通常我们转义一个字符是为了消除它的特殊含义，但有时我们转义普通字符是为了赋予其特殊含义。

### 以太网 (Ethernet)
一种网络方法，系统连接到单一共享总线，且所有流量对每台机器都可见。数据包包含接收者的标识符，只有该机器应该处理该数据包。

### 表达式 (Expression)
常量、变量或操作数与运算符的组合。用于设置值、执行计算或设置比较模式（正则表达式）。

### FIFO
先进先出。参见 `Pipe, named`。

### 文件压缩 (File compression)
对数据应用数学公式的过程，通常会导致数据占用空间更小的形式。压缩文件可以解压，恢复原始文件。

### 索引文件 (File, indexed)
基于文件结构的文件，可以根据特定的键（名称、员工编号等）或按顺序检索数据。键存储在索引中。`UNIX` 操作系统不直接支持此；通常由程序员实现或使用来自 ISV 的工具。一种典型形式被称为 `ISAM`。

### 行顺序文件 (File, line sequential)
参见 `File, text`。

### 顺序访问文件 (File, sequential)
这个短语可以指只能按顺序访问（而非随机访问）的文件，也可以指没有记录分隔符的文件（通常是固定长度，但 `UNIX` 不知道长度是多少，也不关心）。

### 文件字节 (File bytes)
存储在设备（通常是磁盘或磁带）上的字节集合。可以是源代码、可执行二进制文件或数据。

### 文本文件 (File, text)
带有记录分隔符的文件。可以是固定长度或可变长度；`UNIX` 工具可以处理这些文件，因为这些工具可以判断记录何时结束（通过分隔符）。

### 文件名 (Filename)
用于标识数据集合（文件）的名称。如果没有 `pathname`，则假设它在当前目录下。

### 文件名生成 (Filename Generation)
通配符命令行中模式词可以使用的特殊字符。Shell 将模式词替换为匹配该模式的现有文件列表。不要将这些通配符与正则表达式通配符混淆。

### 全限定文件名 (Filename, fully qualified)
用于标识数据集合（文件）及其位置的名称。它包含文件的路径和名称；通常，`pathname` 是完全指定的（绝对路径）。参见 `Pathname` 和 `Pathname, absolute`。

### 文件系统 (Filesystem)
构建在磁盘驱动器部分或磁盘结构（如 `RAID`）中的分级目录系统。非根文件系统在访问之前必须挂载到目录上（有时在根目录下）。对挂载点目录的所有访问都是在访问文件系统所在的磁盘扇区。这与 `DOS` 将磁盘分区指定为 `D:` 或 `E:.` 的惯例不同。文件系统通常无法增长，因此你系统上的某些目录可能已满，而其他目录仍有未使用的磁盘块。文件系统存储在磁盘分区中，有时被称为磁盘分区。参见 `Mount` 和 `Mount point`。

### 指令 (Finger)
用户信息查询程序。





# 防火墙
一种用于从外部（通常是互联网）为内部网络提供受控入口的系统。这用于防止外部或未经授权的系统访问你内部网络上的系统。该功能取决于具体的软件包，但典型特性包括过滤数据包和过滤数据报文、系统（名称或 IP 地址）别名，以及拒绝来自某些 IP 地址的数据包。在理论上，它提供了防止来自外部恶意程序或人员的保护。它还可以防止内部系统访问外部互联网。该名称源于连接建筑之间或单个建筑内部的物理屏障，这种屏障旨在防止火从一个地方蔓到另一个地方。

## Flags
参见*选项*（Options）。

## Float
单精度浮点数。

## 前台作业
一个正在运行并占用你的键盘和屏幕的任务。参见*后台作业*（Background job）。

## FSF
自由软件基金会。

## FTP
文件传输协议或文件传输程序。一种在通过 `TCP/IP` 连接的系统之间传输文件的平台无关方法。确保即使在传输过程中发生错误，文件也能正确传输。通常可以处理字符集转换（`ASCII`/`EBCDIC`）和记录终止符解析（`UNIX` 的换行符，MS/PC-DOS 的回车符加换行符）。

## 全路径
与绝对路径相同。

## 网关
一种硬件、软件和网络连接的组合，提供一种架构与另一种架构之间的链接。通常，网关用于连接 `LAN` 或 `UNIX` 服务器与大型主机（使用 `SNA` 进行网络，因此被称为 `SNA 网关`）。网关也可以是内部和外部网络之间的连接（通常称为防火墙）。参见*防火墙*（Firewall）。

## GID
组 ID 号。

## 通配符（Globbing）
参见*文件名生成*（Filename generation）。

## GNU
GNU 代表 Not UNIX，是 `UNIX` 环境中常见的自由软件包的名称，这些软件包由 MIT 的 GNU 项目分发，很大程度上归功 Richard Stallman 的努力。这个递归缩写（GNU 包含该缩写作为其中一个单词）是对 Richard Stallman 的玩笑。一本关于操作系统设计的教科书书名为：`GNU`：`GNU` 不是 `UNIX`，且 `GNU` 遵循那条路径。

## GPL
通用公共许可证。

## grep
一种在文件中搜索模式的常用工具。`egrep` 允许使用扩展（因此有 `e` 前缀）正则表达式；`fgrep` 使用有限表达式（因此有 `f` 前缀）进行搜索。

## GUI
图形化用户界面。

## 在此文档（Here document）
`<<` 重定向运算符，被称为在此文档，允许将程序的键盘输入（`stdin`）包含在脚本中。

## 隐藏文件
文件名以点（`.`）开头的的文件或目录。某些工具默认不会处理隐藏文件（例如 `ls` 和文件名生成通配符）。隐藏文件通常是系统文件和配置文件，在处理数据文件时不应包含它们。

## HTML
超文本标记语言。用于描述万维网网页。它是用于通过标签定义在互联网上可用的页面的文档语言。浏览器解释 HTML 以显示所需的信息。

## I-node
用于描述文件及其存储。目录包含 i-node 与路径/文件名之间的交叉引用。也称为 `inode`。磁盘数据结构中的文件条目（通过 `ls -i` 查看）。

## ICMP
网络控制消息协议。`TCP/IP` 的一部分，提供网络层管理和控制。





# 继承
一种面向对象的软件复用方法，通过使用现有的属性和行为并在此基础上扩展，基于现有类开发新类。如果基对象是汽车（具有引擎、四个轮子和轮胎等属性；以及加速、转向、减速等行为），那么跑车就会修改这些属性：引擎可能比默认的更大或马力更高，四个轮子可能包括合金轮毂和高速轮胎；行为也会被修改：更快的加速、更小的转弯半径、更快的减速。

# 初始化级别
与运行级别（run level）相同。

# inode 节点号
给定文件在 inode 表中的条目编号。参见 `Inode`。每个文件系统都有自己的 inode 表，因此如果两个不同的文件位于同一系统的不同文件系统中，它们可能会有相同的 inode 节点。参见 `Filesystem`。

# inode 表
参见 `Inode`。

# inode
一种表条目，存储了关于文件的所有信息，但文件名和实际文件数据除外。inode 包含文件所有者、组、权限、最后访问/修改的日期/时间等字段。每个 UNIX 文件系统都包含一个 inode 表，用于跟踪磁盘上该区域的所有文件。参见 `Filesystem`。内存中也有一个 inode 表，用于跟踪所有当前正在引用的文件。

# Int
整数。

# 互联网服务提供商
专门连接您到互联网的公司。

# 互联网
不同网络的集合，提供了在它们之间移动数据的能力。它构建在 `TCP/IP` 协议之上。最初由 DARPA 开发，后由 NSF 接管，现已脱政府控制。

# IRC 继聊天
基于服务器的应用程序，允许组人员通过文本对话进行同时通信。IRC 类似于民用频段无线或某些公告板上的聊天室。某些聊天可以是私密的（仅限受邀请人员）或公开的（任何人都可以加入）。IRC 现在支持音频和文本；对于文件交换也有用。

# ISAM
索引访问方法。在 UNIX 和其他系统中，ISAM 指一种以键或顺序方式访问数据的方法。UNIX 操作系统不直接支持 ISAM 文件；它们通常是附加产品。

# ISO
国际标准组织。

# ISP
参见 `Internet service provider`。

# ISV
独立软件供应商。对除您的硬件供应商之外的软件供应商的通用称呼。

# K&R
Kernighan 和 Ritchie。

# 内核
操作系统的核心，处理内存分配、设备输入输出、进程分配和用户访问等任务。与其它操作系统相比，UNIX 的内核通常较小。

# 键
这些是触发某些功能而不是显示字符的键。文件结束键（EOF）告诉 UNIX 不再有输入；它通常是 `Ctrl+D` 键。

# Korn shell
一种具有广泛脚本（编程）支持的 UNIX 用户界面。由 David G. Korn 编写。该 shell 具有命令行编辑功能，并能接受为 Bourne shell 编写的脚本。

# L LAN
局域网（Local area network）。网络硬件、软件、台式计算机、服务器和主机直接连接的集合。一个局域网可以是整个大学校园。

# 限制
参见 `Quota`（配额）。

# LISP
列表处理语言。

# 登录
用户获取 UNIX 系统访问权限的过程。这也可以指在登录提示符处输入的用户 ID。





- `lp`: 行式打印机。
- `lpc`: 行式打印机控制程序。
- `lpd`: 行式打印机守护进程。
- `lpq`: 打印机打印队列检查程序。
- `lprm`: 打印机打印队列作业删除程序。
- `ls`: 列出目录命令。

## M

- **Magic number（魔数数）**: 嵌入在某些文件中的数字，允许系统通过查阅魔数表来确定该文件内容的类型。
- **Man page（手册页）**: `man` 命令的输出，显示来自 UNIX 在线手册的页面，告知你如何使用大多数 UNIX 命令以及该命令提供的可用选项。
- **Memory, real（物理内存）**: 系统内部正在使用的存储空间（硅基器件；过去是磁铁芯存储器）。
- **Metacharacter（元字符）**: 对 shell 具有特殊含义的字符。它会被 shell 或命令转换为其他内容。
- **Filename Wildcard（文件名通配符）**: 例如，`*` 会被 shell 转换为当前目录下所有文件的列表。
- **MIME Multipurpose Internet Mail Extensions（多用途互联网邮件扩展）**: 一套协议或方法，用于在电子邮件中附加二进制数据（可执行程序、图像、声音文件等）或额外的文本。
- **motd**: 日期消息（Message of the day）。
- **Mount（挂载）**: 将预定义的磁盘驱动器或磁盘子系统分区（例如 RAID）变为系统可用的行为。系统维护一个当前挂载文件系统的内部挂载表。
- **Mount commands（挂载命令）**: 通常在系统启动时自动运行。见 filesystem（文件系统）和 Unmount（卸载）。
- **Mount directory（挂载目录）**: 与挂载点相同。
- **Mount point（挂载点）**: 一个标准的 UNIX 目录（本但不包含文件和子目录），`mount` 命令将其作为另一个磁盘驱动器或磁盘子系统（例如 RAID）中文件系统的访问点。挂载后，挂载点目录中的文件和目录将消失。相反，挂载文件系统的文件和目录似乎出现在挂载点目录中。挂载点目录内的任何访问或更改实际上都发生在挂载的文件系统中。见 *Filesystem（文件系统）* 和 *Mount（挂载）*。
- **Multitasking operating system（多任务操作系统）**: 支持多个作业并发运行的操作系统，特别是单个用户可以启动多个并发运行的作业。
- **Multi-user operating system（多用户操作系统）**: 支持多个用户连接到系统的操作系统。
- **mwm**: Motif 窗口管理器。

## N

- **Netnews（网络新闻）**: 这是一个松散控制的讨论组集合。消息（类似于电子邮件）发布在特定区域，然后人们可以进行评论，公开地回复同一处（发布响应）供他人看到。同一主题的消息集合称为线程（thread）。有些小组经过了审核，这意味着未经所有者批准不发布任何内容。大多数小组不是，且组名不能保证讨论内容与之相关。此的正式术语是 Usenet news。
- **NFS Network file system（网络文件系统）**: 一种将挂载到远程系统的磁盘连接到本地系统的方法，就像它们物理连接在一起一样。
- **NNTP Netnews Transport Protocol（网络新闻传输协议）**: 用于在 TCP/IP 之上传输 Netnews 或 Usenet 消息。关于传输消息的更多信息，请参阅 *Netnews（网络新闻）*。




### 非单词 (Non-words)
在 `vi` 中，非单词是指任何标点符号组。例如，`abc---def=3` 包含两个非单词：`---` 和 `=`。参见*包含的单词*和*分离的单词*。

### 对象 (Object)
从本质意义上说，对象是指具有物理属性的东西，例如汽车、橡胶球和云。这些东西具有属性和行为。它们可以被抽象为数据（属性）和代码（行为）。它们不再仅仅是通过函数来处理数据，而是被封装在一个被称为对象的包中。

### 运算符 (Operator)
对值或变量执行函数的元字符。加号（`+`）是一个将两个整数相加的运算符。

### 选项 (Options)
特定程序或命令的指示器，用于控制该程序的行为。有时称为标志（flags）。`ls` 命令的 `-a` 选项显示以 `.` 开头的文件（如 `.profile`、`.kshrc` 等）。如果没有它，无论使用什么通配符，这些文件都不会显示。这些用于命令行。另见*参数 (Parameters)*。

### OSF
开放软件基金会 (Open Software Foundation)。

### 参数 (Parameters)
通过命令行传递给命令或程序的数据。这些可以是控制命令工作方式的 `options`。某些参数根据其在命令行上的位置具有特殊含义。

### 父目录 (Parent directory)
包含另一个目录的目录被称为该子目录的父目录。

### 父进程 (Parent process)
创建或派生称为子进程的子任务的进程或作业。

### 父 shell (Parent shell)
控制另一个 shell 的 shell（通常是登录 shell），通常被称为子 shell 或子外壳。参见*Shell*。

### 密码 (Password)
用于与用户 ID 结合使用以获得 UNIX 系统权限的安全代码。

### 路径名 (Pathname)
一种包含斜杠的文件引用方法——即指明包含该文件的目录。参见*相对路径 (Relative)*和*绝对路径 (Absolute pathnames)*。

### Perl
由 Larry Wall 开发的编程语言。（Perl 代表 Practical Extraction and Report Language 或 Pathologically Eclectic Rubbish Language；两种解释均同样有效）。该语言提供了 shell 编程、`awk` 和 `sed` 的功能以及许多增强功能。它通常用于为 UNIX 和 Windows 编写 CGI Web 脚本。

### 权限 (Permissions)
当应用于文件时，它们是控制文件访问的属性。有三个访问级别：所有者（文件创建者）、组（属于系统确的相关组的人员）和其他（所有人）。权限通常用 `r` 表示读取，`w` 表示写入，`x` 表示执行。执行标志也用于搜索目录。

### PGP
极好的隐私系统 (Pretty Good Privacy)。

### PID
进程 ID 数字 (Process ID Number)：UNIX 下的每个作业或进程都列在一个名为进程表的表中。该表中的作业条目即为其 ID 数字或 `PID`。

### Pine
交互式邮件程序。

### 管道 (Pipe)
将一个 UNIX 命令的输出重定向并作为第二个 UNIX 命令的输入的方法或动作。这消除了使用文件存储临时结果的需要。管道会自动调节其流量，因此其占用的磁盘空间远小于临时文件所需的空间。

### 管道文件 (Pipe file)
参见*命名管道 (Pipe, named)*。

### 管道符号 (Pipe sign)
竖线字符（`|`）。

### 命名管道 (Pipe, named)
普通管道（将一个命令的输出重定向到另一个命令的输入）的扩展功能。




（一个程序成为另一个程序的输入）。与其其将 `stdout` 连接到 `stdin`，不如将一个程序的输出发送到命名管道，而另一个程序从同一个文件中读取数据。这是通过一种被称为管道文件或 `FIFO` 的特殊文件实现的。操作系统确保了数据的正确顺序。管道文件中实际上存储了很少或没有数据；它仅充当两者之间的连接。

### Pipeline（管道线）
一组通过管道相互链接的 UNIX 命令序列。参见*Pipe*（管道）。

### Piping（管道操作）
使用管道的行为。参见*Pipe*（管道）。

### POSIX
可移植操作系统接口，UNIX。`POSIX` 是基于 UNIX 的开放系统标准族。该名字归功于理德·斯尔曼（Richard Stallman）。由 IEEE 工作组 1003.2 (`POSIX.2`) 开发的 `POSIX` Shell 和工具标准侧重于命令解释器接口和实用程序。

### PostScript
Adobe 系统公司（Adobe Systems, Inc.）打印机语言。

### PPID
父进程 PID：启动正在考虑的当前进程或作业的进程 `PID`（参见 `PID`）。

### PPP
点对点协议。串行链路（调制解调器）上的互联网协议。

### pppd
点对点协议守护进程。

### Present
同于当前目录。

### Print
能力数据库。（注意：根据上下文，可能意指“打印能力数据库”）

### Process（进程）
UNIX 下的离散运行程序。用户的交互式会话是一个进程。进程可以调用（运行）并控制另一个程序，该程序被称为子进程。最终，程序所做的一切都是操作系统的子进程。

### Process identifier（进程标识符）
在 `ps` 命令标题中显示为 `PID`。分配给系统中运行的每个进程的唯一数字。

### pwd
打印工作目录命令。

### Quota（配额）
对用户或进程实施的系统限制的一般描述。它可以适用于磁盘空间、内存使用、CPU 使用、最大打开文件数以及许多资源。

### Quoting（引用）
使用单引号和双引号来否定正常的命令解释，并将引号内的所有单词和空格拼接为单段文本。

### R
正则表达式（regular expression）的缩写。这个短语在技术上是冗的，因为正则表达式本身就是一种模式。更高级的 UNIX 用户应该省略这个词，直接称为正则表达式。

### R.E.
通配符（wildcard）的缩写。参见*Regular expression*（正则表达式）。

### RAID
廉价/独立磁盘冗余阵列。`RAID` 子系统允许你将多个磁盘组合成一个更大的结构，提供条带化（通过均衡磁盘负载来提高性能）、镜像（以防止介质或驱动器故障）或校验（以便在无需双倍数据驱动器数量的情况下提供冗余）。

### RCS
版本控制系统。

### Recursively processing（递归处理）
递归处理一个目录意味着其所有的子目录也会被处理，这些子目录的子目录也会被处理，以此此类推。这意味着无论距离起始目录有多少层，所有的子目录都将被处理。

### Redirection（重定向）
将数据流从默认值引导的过程。输入可以重定向以从文件获取数据或另一个程序的输出。标准输出可以发送到另一个程序或文件。错误可以发送到另一个程序或文件。




### 正则表达式
可能包含一个或多个正则表达式通配符的模式。也是大型正则表达式中子模式元素的名称。参见`正则表达式通配符`。

### 正则表达式通配符
这些是特殊字符，允许我们以通的方式在文件和管道中指定模式。这些通配符模式被 `grep`、`sed`、`awk` 和 `Perl` 等工具用于查找要显示或修改的所需文本。请勿将其与文件名生成通配符（Filename Generation Wildcards）混淆。

### 普通文件
包含用户或系统数据、文本、编程等的 UNIX 文件，它与目录、设备节点、命名管道、信号量或共享内存文件有所区别。这是 UNIX 系统上常见的文件类型。

### 相对路径
一种引用文件的方法，其中文件名的目录部分指示为相对于当前目录的相对路径。相对路径从不以斜杠开头，例如，`reports/abc` 指向当前目录下 `reports` 子目录下的 `abc` 文件。参见`相对路径`。

### 备注
与注释（comment）含义相同。

### RFC
意见请求（Request For Comment）。用于创建 Internet 和 TCP/IP 相关标准的文档。

### rlogin
远程登录。提供与 `Telnet` 相同的功能，但增加了不需要受信任客户端提供密码的功能，这可能引发安全问题。参见`Telnet`。

### 根目录
包含所有其他目录和文件的主系统目录。它由单个斜杠 `/` 表示。

### root 用户
UNIX 系统管理员，也称为超级用户（superuser）。root 被视为所有文件的共同所有者，因此拥有访问系统上所有文件的权限。

### 路由
在两个不同网络之间移动网络流量的过程；当两台机器之间存在多个连接时，决定采取哪条路径。它可以绕过中断发送流量。

### RPC
远程过程调用。提供了从本地调用运行在远程系统上的函数或子程序的能力。

### RPM
红帽软件包管理器（Red Hat Package Manager）。

### 运行级别
在 System V 中，一个从 0 到 6 的数字，用于描述系统状态。

### 脚本为为 UNIX 工具编写的程序，包括 shell、`awk`、`Perl`、`sed` 等。参见`Shell 脚本`。

### SCSI
小型计算机接口（Small computer interface）。

### sed
一种用于流编辑的常用工具，具有 ed 语法。

### 分隔
在任何由空格、制表符或换行符分隔的字符组中。也称为定界符。参见`delimited`。

### 服务器数据库
关系型数据库软件，如 Oracle、Sybase。其他系统连接到此数据库获取数据。

### SGID
设置 ID（Set ID）。

### Shell
UNIX 中处理用户输入并调用其他程序的部分。包括一种编程语言（例如 Bourne shell、C shell、Korn shell、tcsh 和 bash）。

### Shell 环境
shell 程序（Bourne, Korn, C, tcsh 和 bash）的调用选项和预设变量，这些变量定义了 UNIX 命令行和程序执行界面的特性、功能和特征。

### Shell 命令提示符
UNIX shell 显示的单个字符或字符集，用户可以在其中输入一个或多个命令。





- **Shell 脚本**：使用 Bourne、Korn 或 C shell 等支持的 shell 语言编写的程序。
- **信号 (Signal)**：一种特殊的标记或中断，用于操作系统和其他程序向程序通信特殊事件。
- **进入目录 (Sit in a directory)**：对进入当前目录或切换到某个目录的非正式说法。（例如，如果你位于 `/tmp` 目录，访问这些文件将变得更容易。）
- **SLIP**：串行链路互联网协议。通过串行链路（调制解调器）上网。该协议负责分帧和控制线路上 `TCP/IP` 数据包的传输。通常 `PPP` 比 `SLIP` 更好。
- **SNA**：系统网络架构。IBM 的网络架构。
- **特殊文件 (Special files)**：同设备节点。
- **Spool 文件 (Spool files)**：用于排队等待打印的文件临时副本，一直保留直到打印完成。该术语也适用于许多其他系统进程（如 `uucp`）所持有的临时文件。
- **stderr**：程序的标准错误输出，默认发送到屏幕。可以重定向到文件。
- **stdin**：程序的标准输入，默认从键盘读取。可以重定向到文件或另一个程序的输出。
- **stdout**：程序的标准输出，默认发送到屏幕。可以重定向到文件或另一个程序的输入。
- **流 (Stream)**：数据的顺序集合。对于 `UNIX` 操作系统而言，所有文件都是流。对它来说，文件没有结构；结构是由应用程序（如 `ISAM` 软件包或关系型数据库）所施加的。
- **子目录 (Subdirectory)**：包含在另一个目录中的目录。如果你指的是某个给定目录的所有子目录，那么你指的不仅是它的直接子目录，还包括其子目录的每一个子目录。请参见 `Directory`。
- **子网 (Subnet)**：网络中共享共同 IP 地址组件的部分。出于安全和性能考虑而使用。
- **子进程 (Subprocess)**：在另一个进程（通常称为父进程）控制下运行的进程。参见 `Process`。
- **子 shell (Subshell)**：在另一个 shell（通常称为父 shell，即登录 shell）控制下运行的 shell。参见 `Shell`。
- **子树 (Subtree)**：由一个目录及其每一个文件、子目录，以及它们的每一个文件和子目录（尽可能延伸）组成的 `UNIX` 树的一部分。
- **SUID**：设置用户 ID (Set user ID)。
- **超级用户 (Superuser)**：通常指 root 操作员。
- **系统管理员 (System administrator)**：负责维护 `UNIX` 系统和用户管理事务员。也称为系统经理 (system manager)，尽管该术语在 DEC VAX 安装中常见。
- **系统经理 (System manager)**：参见 `System administrator`。
- **tar**：磁带归档工具。
- **TCP**：传输控制协议。
- **TCP/IP**：传输控制协议/互联网协议。这一对协议，也是构成互联网基础的工具和协议组的通用名称。最初开发用于将系统连接到 `ARPAnet`。
- **tcsh**：一种类似于 C shell 的用户界面，具有命令行编辑功能。




- **Telnet Protocol**: 用于通过交互式（字符用户界面）终端访问远程系统。使用 `Telnet` 协议的终端模拟器通常被称为 `telnet` 或 `tnvt100`。
- **telnet**: 远程登录程序。
- **Termcap**: 终端能力数据库。
- **Terminal**: 一种硬件设备，通常包含一个阴极射线管（屏幕）和键盘，用于人类与计算机系统的交互。不支持图形或图像。
- **Text processing languages**: 文本处理语言是在文本编辑器中开发文档的方法，其中嵌入了处理格式的命令。文件通过一个执行这些嵌入命令的处理器，生成格式化的文档。这些包括 `roff`、`nroff`、`troff`、`RUNOFF`、`TeX`、`LaTeX` 甚至是大型机的 `SCRIPT`。
- **TFTP**: 简单文件传输协议或简单文件传输程序。一种在通过 `TCP/IP` 连接的系统之间传输文件的系统无关方法。它与 `FTP` 的不同在于它不保证文件传输的性，不对用户进行身份验证，并且缺少许多功能（例如 `ls` 命令）。
- **Tin**: 交互式新闻阅读器。
- **Truncate**: 截断/删除超出某些限制的末尾部分（例如，限制为 14 个字符）。
- **UDP**: 数据报协议。`TCP/IP` 的一部分，用于不需要交付的控制消息和数据传输。在这种情况下，应用程序必须确保数据传输。
- **UID**: 每个登录用户都有一个标识数字，称为 `UID`，列在 `/etc/passwd` 中。参见 User ID。
- **UIL**: Motif 界面语言。
- **umount**: 执行卸载操作的命令。参见 Unmount（卸载）。
- **Unmount**: 从系统挂载表中移除文件系统的操作，这将导致系统无法访问其内容（直到再次挂载）。这还将挂载点目录转换回普通目录，其原有内容现在可用。参见 Filesystem（文件系统）、`Mount（挂载）和 Mount point（挂载点）。
- **URL**: 统一资源定位符。指定互联网材料的协议、格式、登录（通常省略）和位置的方法。
- **Usenet**: 参见 Netnews。
- **UUCP**: UNIX 到 UNIX 复制程序。用于构建早期的、非正式的网络，以传输文件、电子邮件和 Netnews。
- **Variables, attributes**: 设置变量类型的修饰符。变量可以可以是字符串或整数、左对齐或右对齐、只读或可更改，以及其他属性。
- **Variables, environmental**: 环境变量。在 shell 控制的区域内存储数据和值（字符串和整数）的地方，以便当前进程和子进程可以使用。它们可以是当前 shell 局部的，也可以供子 shell 使用（已导出的）。
- **WAN**: 广域网。一种某些网络连接涉及电话公司的网络（例如数字线路、`ISDN` 或 `T1`）。
- **Web**: 参见 World Wide Web（万维网）。
- **Whitespace**: 一个或多个空格和制表符，通常用于分隔命令和命令参数（例如，除非包含引号内，否则文件名）。
- **World Wide Web**: 互联网上运行软件并使用通用协议 (`HTTP`) 进行通信的服务器和服务的集合。



用户无需记住这些资源的位置，通过 URL 从一个 Web 页面链接到另一个。

- **工作目录**：与当前目录相同。
- **WWW**：参见*世界维网 (World Wide Web)*。
- **WYSIWYG**：所见即所得。

### **X**
- **X Window System**：由 MIT 开发的窗口和图形系统，用于客户端/服务器环境。
- **X11**：参见*X Window System*。
- **X**：参见*X Window System*。

### **Y**
- **yacc**：另一种编译器。

### **索引（INDEX）页** 第 82 页
- **符号（Symbols）**：
    - `&`，运行后台作业，319
    - `*`，星号
    - `crontab` 通配符，312
    - 文件名生成通配符，232-233
    - 检查主页，for，234-236
    - 忽略目录，237
    - 列出其他目录中的文件，239
    - 列出符合多种模式的文件，237-238
    - 列出隐藏文件，238
    - 减少长名称的输入，236
    - 反引号，生成文件名，245-247
    - 反斜杠，721
    - 主页中的 `^H`（退格键），168
    - `^`（脱字符符号）正则表达式通配符，389-390
    - `^$`（脱字符符号和美元符号）正则表达式通配符，391-392
    - `}`（大括号，右），720
    - `--` 变量值减（Perl），745
    - `$` 正则表达式通配符，390-391

### **UNIX 提示符（prompt）**，82
- 双引号，419
- `++` 变量值增（Perl），745
- `<<`（小于号，引用，here-iss, Perl），725
- `&&`（逻辑与），使用 awk 查找行，408




- `#` (井号)
- Bourne 和 Korn shell 提示符, 82
- UNIX shell 中的 `#` 注释, 86-87
- Perl 中的 `#` 注释, 723
- `%` (百分号)
- `%` C shell 提示符, 82
- `sed` 命令中的 `%` 分隔符, 416-417
- `.` (点)
- Perl 中的 `.` 字符串拼接, 746
- `.` 目录, 47
- `.` 正表达式, 395-396
- `.` vi 编辑器, 472-475
- `?` (问号) 文件通配符, 232-240
- `?` 固定长度命名, 240-241
- `?` Perl, 426-427
- `()` 单引号, 419
- `/` (斜杠)
- `/` 命令, 93
- `sed` 命令中的 `/` 分隔符, 416-417
- `^` (方括号) 正表达式, 397-398
- `[]` (方括号) 字符, 232-244
- `[]` (方括号) 字符, 232-243, 396-397
- `|` (竖线) 管道传输, 31, 107
- `|` 4-mm DAT 磁盘驱动器, 332
- `|` 8-mm Exabyte 螺旋扫描磁带驱动器, 333
- `|` 9 磁半英寸磁带磁盘驱动器, 333
- `A`
- `A` (`vi` 编辑器) 命令, 458
- `A` 字符串缩写, 489
- `A` 中止, `vi` 编辑器, 455
- `A` 绝对, 44-45
- `A` 绝对文件名, 解决方案
- `A` `cpio` 命令, 363-364
- `A` `tar` 命令, 349-350
- `A` 绝对路径, 39, 44-46, 148-149, 180, 184. *另参见* 全路径；路径；相对路径




- 使用 `cpio` 命令检查, 362
- 使用 `tar` 命令检查, 346-348
- 第 824 页
- `awk` 脚本中的动作, 675-676, 682
- 数组函数, 693-694
- 数组, 692-693
- 多维, 694
- 循环, 698
- 数值函数, 695
- 运算符
- 算术, 695-696
- 条件, 697-698
- 字符串, 688
- 语句
- break, 698-699
- continue, 698-699
- do, 698
- for, 699-700
- if, 696-697
- null (), 697
- while, 700
- 字符串常量, 688, 692
- 字符串函数, 689-691
- 变量, 682-683
- 定义, 684-687
- 字符串, 687-688
- `vi` (vi 编辑器)。参见 `autoindent` (vi 编辑器) 命令
- `AIX` 操作系统 (IBM), 20
- CDE GUI, 126
- 设备文件名, 331
- 软磁盘驱动器, 338
- 磁带驱动器, 333-336
- 系统关机, 302
- 脚本, 305-306
- 系统启动脚本, 306-307
- alias 命令, 506
- 字母顺序，排序文件或管道, 202




由于提供的原始文本包含大量的 HTML 表格碎片和重复占位符，作为高级文档工程师，我已提取了其中的核心语义信息，并按照要求进行了格式化排版。

### 字符与符号索引
- ASCII 字符值，202-204
- AltaVista, 614
- Ampersand (`&`)，运行后台作业，319
- AND 逻辑与，159
- 角度运算符，Perl, 729
- 匿名 ftp， 615
- Answer Books CDE 应用程序，133-134
- App Manager CDE 应用程序，133-134
- 在行末尾追加文本，`vi` 编辑器，458
- 应用程序，13
- CDE, 132-134

### CDE 应用程序列表
- Answer Books, 133-134
- App Manager, 133-134
- Audio（音频），133-134
- Calculator（计算器），133-134
- Calendar（日历），133-134
- Clock（时钟），133-134
- Console（控制台），133-134
- File Manager（文件管理器），133, 140-142
- Help（帮助），132-134
- Icon Editor（图标编辑器），133-134
- Image Viewer（图像查看器），133-134
- Mailer（邮件发送器），133-134, 142-144
- Performance Meter（性能计数器），133-134
- Program Manager（程序管理器），132-134
- Snapshot（快照），133-134
- Style Manager（样式管理器），133-134
- Terminal（终端），132-135
- Text Editor（文本编辑器），132-140
- Web Browser（网页浏览器），133-34

### 命令与工具
- `apropos` 命令，95
- archives（归档）：数据副本，328
- 列出目录 (TOC)
- `cpio` 命令，360-361, 367-368
- `tar` 命令，343-353





- 参数列表过长错误，244-245
- 使用 `xargs` 命令解决，249
- `ARGC` 预定义变量 (awk)，684-685
- `ARGIND` 预定义变量 (awk)，684-685
- 参数。另见参数
- 添加到命令，84-86
- 添加到选项，88-89
- 命令行，646-647
- 检查给定的数字，658
- 循环遍历，662-663
- 列出，660
- 使用空格与选项和命令分离，86
- `@argv` 数组， Perl，728-729
- `ARGV` 预定义变量 (awk)，684-685
- 算术计算。另见数学计算
- 算术运算符，awk，695-696
- 数组，692-694
- 函数，awk，693-694
- 使用 Perl 函数进行操作
- `pop`，736
- `push`，736
- `shift`，737-738
- `splice`，738-739
- `unshift`，737-738
- `@argv`，728-729
- `hash`，741-742
- 方向键，命令错误，103
- ASCII 字符值，排序文件或管道，202-204
- 基于行内字段，209-210
- 基于主/次排序键，210-214
- 忽略开前的空格，204
- 第 825 页
- 忽略标点符号，208-209





- 忽略大小写，207
- 数字，按大小，204-206
- 倒序，207-208
- 将结果保存到原始文件，206-207
- 汇编语言，17
- 星星号 `*`
- crontab 通配符，312
- 文件名生成通配符，232-233
- `检查 man pages，对于，234-236`
- 忽略目录，237
- 列出其他目录中的文件，239
- 列出符合多个模式的文件，237-238
- 列出隐藏文件，238
- 减少长名称的输入，236
- `at` 命令，313-315
- 启用/禁用用户权限，316
- AT&T UNIX 操作系统，UNIX SVR3 和 SVR4，19, 26
- `atan()` awk 函数，695
- ATM（异步传输模式）网络，565
- Audio CDE 应用，133-134
- 自动保存的文件，514-515
- `autoconfig` 实用，GNU，621-622
- `autoindent` (vi 编辑器) 命令，488
- 自动代理服务器，614
- 任务自动化。*参见*脚本
- `awk` 语言，672
- 根据所选文件显示字符串，431
- 将字段格式化为列，433-436
- 特性，673
-查找查找，406-408
- 根据字段值替换字符串，432
- 基于字段，429-431
- 有用性，673
- 版本，672, 675





- `awk scripts`, 673-674
- `action`, 675-676, 682
- `arithmetic operators`, 695-696
- `array functions`, 693-694
- `arrays`, 692-693
- `break statement`, 698-699
- `conditional operators`, 697-698
- `continue statement`, 698-699
- `do statement`, 698
- `for statement`, 699-700
- `if statement`, 696-697
- `loops`, 698
- `multidimension arrays`, 694
- `null () statement`, 697
- `numeric functions`, 695
- `predefined variables`, 684-687
- `string constants`, 688, 692
- `string functions`, 689-691
- `string operators`, 688
- `strings`, 687-688
- `user-defined function parameters`, 709
- `variables`, 682-683
- `while statement`, 700
- `coding`, 681-682
- `commands`
- `find`, 712-713
- `from line`, 674-675
- `grep`, 713
- `functions`
- `built-in`, 713-714
- `user-defined`, 707-710
- `input`, 701
- `from commands`, 702-703
- `from files`, 702-703
- `handling`, 680-681
- `operators`





- `comparison`, 678
- `compound pattern`, 678-679
- `range pattern`, 679-680
- `output`, 703
- `to commands`, 706
- `to files`, 706-707
- `to pipes, ending`, 706-707
- `patterns`, 675-676
- `regular expression`, 676-677
- `reports`
- `complex`, 710-711
- `data extraction`, 711
- `statements`
- `getline`, 701-702
- `printf`, 703-706
- `B`
- `b` 块设备文件类型字母, 149
- ``ticks`. 另见 ``
- `Perl`, 744-745
- `background jobs`
- `killing`, 320-322
- `under Korn shell`, 325
- `listing`, 323
- `moving to foreground`, 323-325
- `not killing at logoff`, 320
- `starting`, 319
- `suspending output`, 325-326
- `backing up`, 328-329
- `cpio` 命令
- `directories or files`, 358-359
- `directory subtrees`, 356-358
- 第 826 页
- `listing archive TOC`, 360-361
- `restoring files/directories`, 361
- `restoring files/directories to different directory`, 367
- `restoring files/directories to original directory`, 365-366
- `restoring selected files/directories`, 367-368





- emacs 文件，自动地，514-515
- tar 命令
- 目录或文件，343
- 目录子树，341-342
- 列出归文件目录 (TOC)，343-344
- 恢复文件/目录，344-350
- 将文件/目录恢复到不同的目录，352-353
- 将文件/目录恢复到原始目录，351-352
- 恢复文件/目录，353
- 质写保护，329
- 反引号 (``), 641-642。参见反引号 (`)
- 生成文件名，245-247
- 在命令中的误用，104-105
- 结合正则表达式搜索，392-393
- 反斜杠 (`\`)，将元字符转换为字面量，Perl, 721
- 退格键 (Backspace Key)，修正命令错误，103-104
- 主页面中的退格符 (`^`)，168
- banner 命令，167, 494
- basenames，43
- 查找文件，153-157
- 根目录，49-51
- bash (GNU Bourne-Again) 壳，28, 83
- BASIC 编程语言，13, 17
- bath 命令，315-316
- 批处理，16
- vi 编辑器中的错误鸣声，453
- BEGIN 块，675-676
- 行首 (emacs)，535
- 伯克利软件发行版 (BSD) 系统，20-21
- BSD 脚本 (AIX)
- 系统关闭，302, 305-306
- 系统启动，306-307
- BSD UNIX，25-26
- bg 命令，323-325
- /bin 目录，41





![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 二进制文件 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 转换为简单文本，221-223 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 文本，165-166 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| `strings`，166-167 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 绑定键，515-518 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 块设备节点文件，149-150, 330 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 块 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| awk 脚本，`BEGIN` 和 `END` 块，675-676 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| Perl 脚本，结束块，720 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 尺寸 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| `cp` 命令，368 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| `tar` 命令，354-355 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 启动系统，296. | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 使用 `fsck` 检查根文件系统，297-298 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 加载 UNIX 内核文件，297 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 多用户模式，299 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 第一个子系统，296 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 诊断模式，297 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 子系统启动，297 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 移除启动介，296 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 单用户模式，298 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| System V (SCO) 运行级别，299 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| Bourne shell，28-29, 82-83, 638 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| Bourne shell 脚本，638-639 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 检查文件/目录属性，648-652 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 命令行参数，646-647 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 检查给定值，658 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 循环遍历，662-663 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 命令行替换，641-642 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 命令 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| `checking results`，654-656 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| `exit`，661 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 调试，663-665 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 循环遍历项目列表，665 | | |
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| 处理所有目录文件，666-667 | | |





# 索引（第 827 页）

- 返回用法错误，661-662
- 从菜单项中选择，668-670
- 语句，if，647-648
- 用户输入，645-646
- 用户输出，643-645
- 变量
    - `CDPATH`,54
    - 检查内容，652-654
    - 检查上一个命令的状态，658-569
    - 创建，639-641
    - 列出参数，660
    - 使用不冲突的文件，659-660
- Bourne/Korn shell，Lynx 的登录脚本，623
- break 语句，awk，698-699
- 断点，调试 Perl，751-754
- 浏览互联网，612-614
- Lynx，622-623
- USEN 新闻组，629-633
- BSD (伯克利软件发行版) ，20-21
- 脚本 (AIX)
    - 系统关机，302, 305-306
    - 系统启动，306-307
- UNIX，25-26
- 缓冲区，509
- 内置函数，awk，713-714
- 字符设备类型，149
- C 套件，621
- C 编译器，GNU，621
- C 编程语言，13, 17
    - 与 awk 的相似性，673
- C shell，28-29, 82
- 登录 ID，别名，184
- 登录脚本，针对 Lynx，622
- C++ 编程语言，14
- 计算器 CDE 应用，133-134





- Caldera OpenLinux 操作系统 (Caldera), 20
- Calendar CDE 应用程序, 133-134
- Call-UNIX 程序。见 `cu` 程序
- `cancel` 命令， 174
- `capitalize-word` 函数 (emacs), 535
- 插入符符号 (caret)，参见 `circumflex`
- 情况 (case)
- 使用 `tr` 命令更改, 442
- 在搜索中忽略
- `emacs`, 525-526
- `grep`, 382
- 替换字符串, 490
- `Perl`, 428
- 命令的敏感性, 84
- 错误, 101-102
- case 语句 (case statement), 668-670
- `cat` 命令, 223-245
- `cat -n` (行号), 165
- 显示小文件， 160
- 查看文件 (catting files)，参见显示 (displaying)
- `cd` 命令, 42-49, 85
- CD-ROM 驱动器, 13
- 启动系统前移除, 296
- 支持的 CDE (通用桌面环境)应用程序, 132-134
- 问答手册 (Answer Book), 133-134
- 管理器 (App Manager), 133-134
- 音频 (Audio), 133-134
- 计算器 (Calculator), 133-134
- 日历 (Calendar), 133-134
- 时钟 (Clock), 133-134
- 控制台 (Console), 133-134
- 文件管理器 (File Manager), 133, 140-142
- 帮助 (Help), 132-134
- 图标编辑器 (Icon Editor), 133-134





- 查看器, 133-134
- 邮件发送器, 133-134, 142-144
- 性能计数器, 133-134
- 程序管理器, 132-134
- 快照, 133-134
- 样式管理器, 133-134
- 终端, 132-135
- 文本编辑器, 132-140
- 网页浏览器, 133-134
- 复制文件/目录, 140-142
- 编辑文件, 136-140
- 帮助, 134
- Motif 窗口
- 可用控件, 129-131
- 在...之间移动文本, 131-132
- 读/发送邮件, 142-144
- 运行命令, 135
- UNIX 标准, 25
- `CD` 变量, 54-56
- 字符节点文件, 149-150, 330
- 字符型终端, 62-63
- 字符。另见通配符字符
- 关闭第 8 位, 443
- 切换大小写, 442
- 删除
- 按位置, 437-438
- 在文件/管道中, 440-441
- 选择性地, 443
- 第 828 页
- 查找, vi 文本编辑器, 467
- 匹配
- 使用点号 (.) 正则表达式通配符, 395-396
- 使用方括号 ([ . .]) 正则表达式通配符, 396-397
- 替换, vi 文本编辑器, 459
- 将控制转换为一个错误, 444
- 检查拼写, vi 文本编辑器, 461





- `chgrp` 命令，284, 290
- `chmod` (更改模式) 程序，285-289
- `chmod` 命令，287
- `chomp` 函数 (Perl), 747
- `chown` 命令，290
- 插入符号 (`^`) 正则表达式通配符，389-390
- 插入符号和美元符号 (`^$`) 正则表达式通配符，391-392
- CDE 应用，133-134
- `close` 命令, Perl, 739-740
- `关闭文件`, Perl, 739-740
- `cmp` 命令，比较内容类型，267
- `COBOL` 编程语言，13, 17
- `代码引用`, Perl, 723-724
- `编写 awk` 脚本，681-682
- `col` 命令，167-169
- 排序序列，202-204
- `基于行内字段`，209-210
- `基于主/次键`，210-214
- `忽略`-`前导空格`，204, 207
- `标点符号`，208-209
- 大/小写，207
- `按大小排序数字`，204-206
- `逆序`，207-208
- `将结果保存到原始文件`，206
- 冒号 (`:`) 分符，`sed` 命令，416-417
- `合并文件`
- `基于连接字段`，224-226
- `多个`，223
- `接一个`，223
- `并排`，223
- `comm` 命令，比较共同/唯一的文本行，266-267
- `命令行`
- `参数`，646-647
- *检查给定的数字*，658




- 循环，662-663
- awk 脚本，674-675
- 编辑，498
- Korn shell，历史，498-500
- 使用 vi 命令，502-506
- 解释器，参见 Shell (UNIX) 符
- Perl 脚本，使用角号运算符输入，729
- 替换，641-642
- 模式，vi 命令，502-506
- 命令未找到错误，96-97
- 命令。另见函数；实用程序
- 别名 (alias)，506
- apro，95
- 作为构建模块，33
- 在，313-315
- 启用/禁用用户权限，316
- awk
- 结束输入，702-703
- 退出 (exit)，701
- find，712-713
- grep，713
- 输入，702
- 输出，706
- 横幅 (banner)，167, 494
- 批，315-316
- bg（后台），323-325
- 取消，174
- 大小写敏感，84
- 错误，101-102
- cat，223, 245
- -n (行数)，165
- 显示小文件，160
- cd，42-49, 85
- 检查 man 页以查看文件列表和通配符支持情况，234-236
- 检查结果，654-656
- 检查状态，658-659




| 命令 | 描述 | 参考页码 |
| :--- | :--- | :--- |
| `chgrp` | | 284, 290 |
| `chmod` | | 287 |
| `chown` | | 290 |
| `cmp` | 按内容类型比较文件 | 267 |
| `col` | | 167-169 |
| `comm` | 比较共同/唯一的文本行 | 266-267 |
| 命令行编辑 | | 502-506 |
| `compress` | | 219-221, 375-376 |
| `cp` | | 235 |
| | 确定目录 | 185-187 |
| | 在当前目录 | 182-184 |
| | 在不同目录 | 184-185 |
| | 将文件列表复制到目录 | 187 |
| `cpio` | | 339-340, 355 |
| | 选择性地备份目录或文件 | 358-359 |
| | 备份目录子树 | 356-358 |
| | 块大小 | 368 |
| | 复制目录子树 | 189-191 |
| | 列出存档目录 (TOC) | 360-361 |
| | 恢复文件/目录 | 361, 365-368 |
| `crontab` | | 308-312 |
| 通配符 | | 312 |
| 每日备份 | | 313 |
| 启用/禁用用户权限 | 316 |
| `crypt` | | 217-219, 493-494 |
| `csplit` | | 227-229 |
| `cut` | | 437-438 |
| `date` | | 72-73, 84 |
| `df` | | 74-77, 181 |
| `diff` | | 262-263 |
| | 三文件比较 | 264-266 |
| `dmesg` | | 566 |
| `du` | | 373 |
| `echo` | | 246, 643-645 |
| `edquota` | | 375 |





# egrep

- 可用的正则表达式通配符，402
- 指定 0 次或多次出现，403
- 指定 1 次或多次出现，403
- emacs，498
- 在另一个系统上执行，rsh 程序 program，587
- exit，84, 661
- fc，498-500
- fg，323-325
- file，内容类型，150-151, 165
- find，88, 373-374
- 按访问日期比较文件，255-262
- 带有文件名的文件，153-157
- 带有逻辑 AND、OR 和 NOT 的文件，159
- 内容中包含单词的文件，158-159
- fine-exec (exec)，打印，157-158
- finger，67-68
- 跟踪符号链接，199-200
- grep，31, 158-159, 247, 321-322
- 选择模式，384-385
- 删除行，445-447
- 显示匹配模式的文件名，386-387
- 查找行，385-392, 395-399, 402
- 起源，392
- 管道至其他命令，383-384
- 保存输出，382-383
- 正则表达式中的 shell 替换，392-393
- 正则表达式周围的单引号 (),393-394
- 组，280
- gunzip，221
- gzip，219-221
- head，215-216, 235
- id，61
- jobs，323
- join，224-226
- kill，320-322, 325





# 索引

- `less`, 160-164
- `line`, 参见 `command-line`
- `In`, 多个文件名, 193-199
- `logout`, 84
- `Ip`, 89, 169-173, 237-238, 245-246
- `Ipmove`, 174-175
- `Ipr`, 169-173
- `Iprm`, 174
- `Ipstat`
- `检查打印队列`, 173-174
- `打印名称`, 171-172
- `is`, 31, 42-43, 46, 87, 90, 238, 279-283
- `按最后日期比较文件`, 252-255, 259
- `文件类型`, 148-153
- `查找文件的硬链接`, 195-197
- `is /dev/cua/`, 542
- `is /dev/ttyS/`, 542
- `Lynx`, 623
- `man`, 92, 234
- `mesg`, 68
- `最小击键次数`, 33-34
- `mkdir`, 51
- `more`, 152, 160-164
- `mount`, 293, 370-371
- `mv`
- `确定目标目录`, 185-187
- `在当前目录`, 182-184
- `在不同目录`, 184-185
- `列出目录到目录`, 187
- `重命名目录`, 188-189
- `覆盖`, 188
- `newgrp`, 284
- `nice`, 317-319
- `nispasswd`, 277
- `nl`, 165
- `nohup`, 320





| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | od | 165-166 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | passwd | 71, 277 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | paste | 223 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | Perl | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `close` | 739-740 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `for` | 733-734 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `foreach` | 734 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `if` | 732 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `open` | 740 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `system` | 744-745 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `pg` | 31, 152, 160-164 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `pr` | 175-177 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `ps` | 317, 321-322 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `ef` | 78-79 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `pwd` | 43-44 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `qcan` | 174 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `quota` | 374 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `read` | 645-646 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `renice` | 318-319 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `repquota` | 374-375 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | returning usage errors | 661-662 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `rm` | 53-54, 84-86, 233-234, 237-245 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | deleting substrees | 192 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | deleting files from current directory | 191-192 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | deleting hard links to files | 197 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | overwrite permissions | 188 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `rmdir` | 52 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | running on local systems, with cu program | 553-554 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | running on remote hosts, with uux program | 556 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `sed` | 235-236 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | comparing text by side | 263-264 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `sed` | 215-216 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | changing line indentations | 484 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | characters matched by regular expression wildcards | 421-423 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | deleting strings | 417-418 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | delimiters | 416-417 |




- 消除搜索模式以外的所有内容，423-424
- 匹配最长跨度，424-425
- 不替换 0 次或多次出现的内容，421
- 替换字符串，412-414
- 替换行，445
- 替换字符串并保存输出，415
- 条件替换字符串，480-484
- 有选择地替换字符串，415-418
- 使用正则表达式通配符替换字符串，414-415
- 使用 shell 变量，420
- 使用特殊字符，419
- 使用空格分隔选项和参数，86
- shell
- fmt，461-462
- 从 CDE 运行，135
- shell (UNIX) 提示符，82
- 添加参数，84-86, 88-89
- 添加注释，86
- 将当前目录添加到 PATH，99-100
- 将新软件添加到 PATH，100
- 添加选项，86-88
- 添加 PATH 变量，97-98
- 命令未找到错误，96-97
- 常见输入错误，101-105
- 错误消息，105-111
- 完整 PATH 名称，100-101
- 来自 man 页的帮助，89-91
- 来自 man 页的帮助，93-95
- 来自重排索引（permuted index）的帮助，95-96
- 将输出/错误保存到文件，112-113, 117
- 主页中的系统子程序，92-93
- shell 提示符，29
- 关机，300-302
- 排序，202, 235-236, 245-246
- ASCII 字符值，202-204




由于提供的原始文本包含大量的 HTML 实体字符（`&#124;` 代表 `|`）和重复的图片占位符，根据高级文档工程师的规范，我已去除冗余的格式符号，提取了核心的描述性信息，并对其进行了标准的 Markdown 列表排版。

# 功能描述与操作说明

- 基于行内字段，209-210
- 基于主/次排序键，210-214
- 通过文件大小比较文件，260
- 忽略开头的空白空格，204
- 忽略标点符号，208-209
- 忽略大小写，207
- 按数量级相乘，204-206
- 逆序排序，207-208
- 将结果保存到原始文件，206-207
- 分割，226-227
- 字符串，166-167
- stty，63-64, 111, 325-326
- su，278-279
- 第 831 页
- 替换。另参见反引号（`）
- 使用 ` `（反引号），245-247
- 正则表达式中的 shell，392-393
- 求和
- 比较不同名称下的相同文件，269
- 比较不同系统上的文件，267-269
- 系统函数，112
- tail，216-217, 235
- tar，88, 339-340, 376
- 备份目录，341-343
- 块大小，354-355
- 复制子树，191
- 局限性，355
- 列出归包，343-344
- 恢复文件/目录，344-353
- 备份设备表，354
- 测试
- 检查变量内容，652-654
- 检查文件系统对象属性，648, 651-652
- tr，235
- 关闭第 8 位，443
- 更改大小写，441-442





| 选择性删除字符, 443 |
| | |
| |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 替换/删除字符, 440-441 |
| | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 将控制字符翻译为一个错误字符, 444 |
| | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 版本, 441 |
| | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| tty, 61 |
| | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 类型, 100-101 |
| | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| umask, 290-291 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| uname, 73-74 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 解压缩, 221 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 卸载, 371-372 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 运行时间, 66-67 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 解码, 221-223 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 编码, 221-223 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| vi 编辑器, 498 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set, 490 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set autoindent, 488 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set ignorecase, 490 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set number, 489 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set showmode, 487-488 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: set wrapmargin, 488 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: f, 460 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: q!, 455 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: w, 458 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: wq, 455 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| (: G/G, 460 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| A, 458 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 修改文本, 469-470 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| Ctrl+L, 457 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| Ctrl+R, 457 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| Ctrl+V, 476, 479 |
| | | |
| | |
|3a4f3a8aef38b56941e55505c60e4](./](content/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| 光标移动, 465 |
| | |
| cW, 459-460 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| dd, 454-455 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| h, 452-453 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| i, 454 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| j, 452-455 |
| | | |
| | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| J, 误用, 479-480 |
| | | |
| | | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | |





| `k`, 452-453 |
| :--- |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `l`, 452-453 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `motion`, 475-479 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `n`, 474-475 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `period (.)`, 472-475 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `r`, 459 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `replacing text`, 470 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `text deletion`, 468 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `u`, 457-460 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `view`, 464 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `x`, 454 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `w`, 66 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `whence`, 101 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `which`, 101 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `who`, 64-66 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `who am I`, 61 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `whoami`, 60 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `write`, 68 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `xargs`, 247-249 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `yppwd`, 277 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `comments` |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `adding to commands`, 86 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `awk scripts`, 682 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `# (pound sign)`, 723 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| common desktop env. See `CDE` (common desktop environment) |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `comparing` files |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `by date accessed`, 254-259 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `by date modified`, 252-259 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `by size`, 259-262 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `by type of contents`, 267 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `common/unique text lines`, 266-267 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `identical, but under different names`, 269 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `on systems`, 267-269 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `text differences`, 262-263 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `text differences side by side`, 263-264 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| `text differences, three files`, 264-266 |



- 名称新于给定名称，255-257
- 比较运算符，`awk` 脚本，678
- 比较关系运算符，`Perl`，731
- 编译器，`C`
- 编译器套件，621
- GNU，621
- 复合模式运算符，`awk` 脚本，678-679
- compress 命令，219-221, 375-376
- 第 832 页
- 压缩文件，219-221, 616
- 合并文件，223
- 字符串连接运算符，`awk`，688
- 条件结构，`Perl`，729-730
- 条件流 (awk)，696-697
- 条件运算符，`awk`，697-698
- 配置文件，`cu program`，549-552
- 配置
- 调制解调器，599-601
- `PPP (点对点协议)`, 558-560
- 串口设备
- 访问控制，543
- 拨入，543-545
- 拨出，545-547
- Windows，590-592
- 确认请求，188
- 连接到网络。见网络
- Console CDE 应用程序，133-134
- 包含单词，`vi` 编辑器，465
- continue 语句，`awk`，698-699
- 控制字符，165-167
- 控制结构，`Perl`，729-730
- 将二进制文件转换为简单文本，221-223
- `CONVFMT` 预定义变量 (`awk`)，684-685
- 复制入/出。见 `cpio` 命令
- 复制
- 目录子树，189-191




# 文件

- 确定目标路径，185-187
- 在当前目录下，182-184
- 在不同目录下，184-185
- 列出到目录，187
- 覆盖权限，188
- 文件/目录，CDE 文件管理器，140-142
- 文本
- 文件之间，485-487
- 在 emacs 中，512-514
- 在同一文件中，485
- 基础文件名 (basename)，删除，158
- `cos()` awk 数值函数，695
- `cp` 命令，235

# 目录

- 当前，182-184
- 确定目标路径，185-187
- 不同的，184-185
- 文件列表，187

# cpio

- `cpio` 命令，339-340, 355
- 选择性备份目录或文件，358-359
- 备份目录子树，356-358
- 块大小，368
- 目录，复制子树，189-191
- 列出存档目录 (TOC)，360-361
- 恢复文件/目录，361, 365-368

# CPU（中央处理单元），12

# cron

- 任务，308
- 添加/删除/编辑，310-312
- `crontab` 命令，308-312
- (星号) 通配符，312
- 每日备份，313
- 启用/禁用用户权限，316
- crontabs (时间表) 文件，308-312

# crypt

- `crypt` 命令，217-219, 493-494

# csplit

- `csplit` 命令，227-229





- **cu 程序**, 547-548
- **配置**, 549-552
- **传输文件**, 552-553
- **右大括号 (}), Perl 脚本代码块终止符**, 720
- **当前目录**
  - **访问**, 47
  - **添加到 PATH 变量**, 99-100
- **文件**
  - **访问**, 49-51
  - **复制**, 182-184
  - **删除**, 191-192
  - **移动**, 182-184
  - **重命名**, 182-184
  - **全路径**, 43
  - **子目录**, 45-46
  - **查看内容**, 42-43
- **vi 编辑器光标移动**, 452-453, 465-466
- **文件开头/结尾**, 460
- **字符**, 467
- **闭合符号**, 467
- **字符串**, 466-467
- **设置标记**, 467-468
- **重复计数**, 454
- **cut 命令**, 437-438
- **在 emacs 中剪切文本**, 512-514
- **剪粘贴文本**, 833
- **cw (vi 编辑器) 命令**, 459-460
- **d 目录类型字母**, 149
- **Data General (DG) UNIX 操作系统, DG-UX**, 19
- **date 命令**, 72-73, 84
- **日期，格式**, 72-73
- **dd (vi 编辑器) 命令**, 454-455
- **Debian GNU/Linux 操作系统 (Debian)**, 20
- **调试脚本**
- **Bourne shell 脚本**, 663-665





- Perl, 748-749
- `breakpoints`, 751-754
- `执行代码行 (n)`, 750
- `列出代码 (l)`, 749-750
- `打印变量值`, 750-751
- 十进制点表示法 (Decimal Dot Notation), 567
- 二进制 IP 地址 (Listing 22.2), 567
- 变量值递减, (N), Perl, 745
- 解密文件, 219
- 默认目录。`查看`当前目录
- 推延任务。`查看`一次性调度
- 删除键 (Delete key), 111
- 修正错误, 103
- 删除字符
- `按列位置`, 437-438
- `在文件/管道中`, 439-441
- 选择性地, 443
- `vi 文本编辑器`, 454
- `cron` 任务, 310-312
- 目录, 52
- 以及文件和子目录, 53-54
- `子树`, 192
- 文件
- `core`, 158
- `从当前目录`, 191-192
- `从不同目录`, 192
- 硬链接, 197
- 列出目录, 192
- `以...开头`, 233-234
- 行
- 包含模式的, 445
- 匹配上一行, 445
- `vi 文本编辑器`, 454-455
- 字符串, 417
- `基于字段`, 429




- `matching shortest span, 426-427`
- `selectively, 417-418, 429`
- `using Perl, 425-426`
- `using spaces for readability, 427`
- `text, vi text editor commands, 468`
- `destination directories, 184-187`
- `destination files, 184-187`
- `device files, 329-330`
- `disk drives`
- `floppy, 336`
- `tape, 332-333`
- `names, 330-332`
- `floppy drives, 336-339`
- `tape drives, 333-336`
- `node files, 148-150`
- `devices configuration file (cu program), 549-550`
- `df (disk free blocks), adding to profile, 308`
- `df command, 74-77, 181, 373`
- `DG-UX operating systems (Data, DG), 19`
- `diagnosing problems, booting system, 297`
- `dial in configuration, 543-545`
- `dial out configuration, 545-547`
- `dial-in devices, 542`
- `dial-out devices, 542`
- `Dial-up Networking, 602`
- `dialers file (cu program), 550`
- `diff command, comparing text, 262-263`
- `diff command, comparing text differences, 264-266`
- `Digital Equipment Corp (DEC), UNIX systems`
- `Digital UNIX, 20`
- `ULTRIX, 20`
- `direct printing, 169-171`
- `directories, 36. See also absolute directory; current directory; destination directories; home directory`
- `/dev, 329`
- `/etc`
[/content]

[content]
- `匹配最短跨度, 426-427`
- `选择性地, 417-418, 429`
- `使用 Perl, 425-426`
- `使用空格提高可读性, 427`
- `文本, vi 文本编辑器命令, 468`
- `目标目录, 184-187`
- `目标文件, 184-187`
- `设备文件, 329-330`
- `磁盘驱动器`
- `软盘, 336`
- `磁带, 332-333`
- `名称, 330-332`
- `软磁盘驱动器, 336-339`
- `磁带驱动器, 333-336`
- `节点文件, 148-150`
- `设备配置文件 (cu 程序), 549-550`
- `df (磁盘空闲块), 添加到配置文件, 308`
- `df 命令, 74-77, 181, 373`
- `DG-UX 操作系统 (Data, DG), 19`
- `诊断问题, 系统启动, 297`
- `拨号入配置, 543-545`
- `拨号出配置, 545-547`
- `拨入设备, 542`
- `拨号出设备, 542`
- `拨号网络, 602`
- `拨号器文件 (cu 程序), 550`
- `diff 命令, 比较文本, 262-263`
- `diff 命令, 比较文本差异, 264-266`
- `数字设备公司 (DEC), UNIX 系统`
- `Digital UNIX, 20`
- `ULTRIX, 20`
- `直接打印, 169-171`
- `目录, 36. 另另：绝对目录; 当前目录; 目标目录; 目录`
- `/dev, 329`
- `/etc`




由于原始文本包含大量 HTML 占位符和冗余表格结构，根据高级文档工程师的规范，我已提取其核心内容，并对其进行了结构化的 Markdown 重新排版。

# 文件与变量操作概览

- **组文件 (group file)**，71
- **密码文件 (passwd file)**，70
- 访问 (Accessing)
- **CDPATH 变量**，54-56
- **常用 (often used)**，56-57

## 常用操作说明

- **属性 (attributes)**，648-652
- **备份 (backing up)**
- **cpio 命令**，356-359
- **tar 命令**，341-343
- **文件名与目录名 (basenames and dirnames)**，43
- **切换至 (changing to)**，46-47
- **复制 (copying)**

## CDE 文件管理器 (140-142)

### 核心功能
- **子树 (subtrees)**，189-191
- **创建 (creating)**，51, 180-181
- **删除 (deleting)**，52
- **加上文件和子目录 (plus files and subdirectories)**，53-54
- **子树 (subtrees)**，192

### 目录结构
- **目录/文件结构 (directory/file structure)**，74-77
- **点 (.)**，47
- **点点 (..)**，47-49
- **文件 (files)**，37-38, 148-150

### 文件列表管理
- **复制文件列表 (copying list of files)**，187
- **复制到不同目录 (copying to different directories)**，184-185
- **从目录中删除 (deleting from directories)**，191-192
- **删除硬链接 (deleting hard links)**，197
- **删除文件列表 (deleting list of files)**，192
- **确定目标 (determining destination)**，185-187
- **查找 (finding)**，153-159
- **查找硬链接 (finding hard links)**，195-197
- **列出 (listing)**，151-153
- **移动文件列表 (moving list of files)**，187
- **移动到不同目录 (moving to different directory)**，184-185
- **多重名称 (multiple names)**，193-199
- **重命名到不同目录 (renaming to different directory)**，184-185
- **inode 节点 (indoe numbers)**，148





- `lost+found`, 375
- `moving`, 188-189
- `CDE 文件管理器`, 140-142
- `Solaris 新特性`, 41
- `parent`, 48-49
- `路径`, 38-39
- `权限`, 280-283
- `更改`, 285-286
- `执行`, 285
- `覆盖`, 188
- `读取`, 285
- `数字模式设置`, 287
- `符号模式设置`, 289
- `写入`, 181
- `处理所有文件`, 666-667
- `rc0.d`, 305-306
- `rc2.d`, 302, 305
- `重命名`, 188-189
- `恢复`
- `cp 命令`, 361, 367-368
- `destination`, 348-350, 362-265
- `tar 命令`, 344-350, 353
- `返回上一个`, 49
- `root`, 74
- `SGID 权限`, 284
- `标准名称`, 40-41
- `stick bits`, 283-284
- `子目录`, 370
- `通配符搜索`, 237
- `文件列表`, 239
- `/dev 目录`, 40, 329
- `目录树`
- `结构`, 37-38
- `路径`, 38-39, 148
- `子树`
- `复制`, 189-191
- `删除`, 192





- `dirnames`, 43
- 磁盘驱动器，容量和文件名, 36
- 磁盘空闲，检查
- `cpio` 命令, 361-362
- `tar` 命令, 345-346
- 显示
- 文件
- 包含控制字符的, 165-167
- DOS, 167-168
- 结束行, 216-217
- 第一行, 215-216
- 行号, 165
- 手册页 (man pages), 168-169
- 小的, 160
- 横幅字母中的文本, 167
- 通过分页器程序, 160-164
- 信息
- 系统, 60-64
- UNIX 密码文件, 69-71
- 用户, 64-68
- 字符串
- 基于所选字段, 431
- 将字段格式化为列, 433-436
- `dmesg` 命令, 566
- ` (Domain Name System), 575-577
- `awk` 语句, 698
- 美元符号 `$` 正则表达式, 390-391
- 域名系统 (Domain Name System)。见 `Domain Name System`
- DOS 与 UNIX, 167-168
- 点 `.` 目录, 47, 746
- 双点 `..` 目录, 47
- 点文件生成器 (Dotfile Generator), 534
- 双重过滤器, 387-388
- 双引号 `()`
- 查找/替换字符串, 419
- 命令中的误用, 104-105





- `downcase-word` 函数 (emacs), 535
- 第 835 页
- 从互联网下载软件, 615
- `free`, 626-627
- `Lynx`, 615, 620
- `patch clusters`, 627-628
- `Security Bulletins`, 628
- `2000 年问题`, 628-629
- `drivers`, 329
- `du` 命令, 373
- `E`
- `each` 函数 (Perl), 741
- `echo` 命令, 246, 643-645
- 编辑命令, 498
- `Korn shell 历史`, 498-500
- 使用 `With vi` 命令行编辑器, 502-506
- `cron` 任务, 310-312
- 参见（See） 文本编辑器
- `edquota` 命令, 375
- `egrep` 命令
- 查找行
- 可用的正则表达式通配符, 402
- 指定 0 次或多次出现, 403
- 指定 1 次或多次出现, 403
- `elif` 语句, 648-650
- `elisp-manual`, 534
- `else` 语句, 648-650
- `emacs` 命令, 498
- `.emacs` 文件, 517-518
- `emacs Lisp 语言`, 517
- `emacs-lisp-introduction`, 534
- 电子邮件
- 文件, 编码为纯文本, 221-223
- 读取/发送, `CDE Mailer`, 142-144
- 向厂商报告技术问题, 625




-   通过 Netscape Communicator 与 UNIX 交互, 608
-   emacs 文本编辑器, 508-509
-   退出, 512
-   文件
-   自动备份, 514-515
-   绑定键, 515-518
-   打开/保存, 512
-   函数，编写, 534-535
-   启动, 510-511
-   宏
-   录制, 518-519
-   重复, 519-520
-   保存, 519
-   主/次要模式, 530-531
-   在线帮助, 531-533
-   文本
-   复制/剪切/粘贴, 512-514
-   搜索/替换, 520-526
-   拼写检查, 526-528
-   撤销更改, 512
-   帮助网站, 533-534
-   包围符号，查找, vi 文本编辑器, 467
-   将文件编码为纯文本, 221-223
-   加密/解密文件, 217-219
-   vi 文本编辑器, 493-494
-   END 块, 675-676
-   End 键，错误, 103
-   行尾符, 167-168
-   行结束函数 (emacs), 535
-   ENVIRON 预定义变量 (awk), 684-685
-   环境变量
-   `$TERM`, 62-63
-   `PATH`, 642
-   等号关系运算符, Perl, 731
-   Erase 键。参见 Delete 键
-   删除。参见 deleting




| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | |
| | | ERRNO 预定义变量 (awk), 684-686 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 错误信息 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 检查 intr 和 erase 键, 111 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 命令 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 保存到文件, 112 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 无法 stat 文件, 108 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 命令输入 |
| | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 大小敏感性, 101-102 |
| | | | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 未找到命令, 96-97 |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 修正退格键, 103-104 |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 间距不正确, 102 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 特殊键的误用, 103 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 引号, 104-105 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 在无提示的情况下跳转到下一行, 107-108 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 文件名生成 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 参数列表过长, 244-245, 249 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 无空格, 247 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 权限拒绝, 181, 188 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 终止模式, 108-111 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 用法, 105, 661-662 |
| | | | |
| | | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 写权限, 459 |
| | | | |
| | | | |
| | | 提权调用, 625 |
| | | | |
| | | | |
| | | 第 836 页 |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc 目录 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 组, 71 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | passwd, 70 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/default/tar 文件, 354 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/filesystem, 370-371 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/hosts 文件, 571-573 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/inittab 文件, 543-546 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/passwd 文件, 278 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/profile 文件, 307-308 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/resolv.conf 文件, 576 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | /etc/shadow 文件, 70 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 以太网网络, 565 |
| | | | |
| | | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | | |
| | | 正在搜索卡, 566 |
| | | | |
| | | | |





- -exec 执行命令, 157-158
- 执行权限, 285
- exit 命令, 84, 661
- 退出
- emacs, 512
- 文件, vi 文本编辑器, 455
- exp() awk 数值函数, 695
- Expr 程序, 数学计算, 656-657
- 表达式, 676
- 运算符
- 复合模式, 678-679
- 范围模式, 679-680
- 扩展正则表达式, 402
- 从输出中提取字段, 439
- F
- (:f (vi 文本编辑器) 命令, 460
- FAQs (常见问题解答), 626
- fc 命令, 498-500
- FD 网络, 565
- fg 命令, 323-325
- 字段
- 从输出中提取, 439
- 排序文件, 210-214
- FIELDWIDTHS 定义变量 (awk), 684-686
- file 命令, 内容类型, 150-151, 165
- 文件压缩, 616
- 文件转储, 十八进制, 165-166
- 文件列表
- 检查页面是否接受, 234-236
- 目录, 通配符搜索
- 使用 (), 245
- 使用 xargs 命令, 247-249
- 隐藏文件, 238
- 使用多个模式, 237-238
- File Manager CDE 应用程序, 132-134
- 复制/移动





# 文件/目录 (140-142)

## 文件系统 (74)

## 可用空间 (373-374)

## 目录，子目录 (370)

## 用户空间 (374-375)

## lost+found 目录 (375)

## 空间管理，命令 (375-376)

## 挂载 (370-371)

## 对象，属性 (648-652)

## 尺寸 (74-77)

## 卸载 (371-372)

## 文件传输协议 (file transfer protocol)

## 文件/目录结构 (74-77)

## 文件句柄, Perl (724-725)

## 关闭 (739-740)

## 打开 (740)

##文件名生成

## 反引号 (245-247)

## 禁止使用的字符 `..` (方括号) (243-244)

## 通配符 `*` (星号) (232-233)

## 检查 man pages (234-236)

## 忽略目录 (237)

## 列出其他目录下的文件 (239)

## 列出隐藏文件 (238)

## 多个模式的一次列出 (237-238)

## 减少长名称的输入 (236)

## 通配符 (151-153, 232)

## 参数过长 (244-245)

## 正则表达式序列 (250)

## 通配符 `?` (问号) (239-241)

## 通配符[...]` (方括号) (241-243)

## xargs 命令 (247-249)

## 文件名生成通配符 (154, 173, 388, 395)

## FILENAME 预定义变量 (awk) (684-686)

## 文件 (36)，*另请*文件名生成；文件





| 主题 | 页码 |
| :--- | :--- |
| 基准名 (basenames) 和目录名 (dirnames) | 43 |
| 匹配模式的文件行 | 386-387 |
| 多个 | 193-194 |
| 删除硬链接 | 197 |
| 查找硬链接 | 195-197 |
| 使用硬链接 | 194-195 |
| 使用软链接/符号链接 | 197-199 |
| 引用当前目录 | 42-43 |
| 以 # (井号) 开 | 86 |
| 无法 stat (获取状态) | 108 |
| vi 文本编辑器 | 460 |
| 文件, 36-38。另请参设备文件；文件名 | |
| 属性 | 648-652 |
| 备份 | 328-329 |
| 使用 `cpio` 命令进行选择性备份 | 358-359 |
| 使用 `tar` 命令进行选择性备份 | 343 |
| 关闭，Perl | 739-740 |
| 比较 | |
| 按访问日期 | 254-259 |
| 按最后修改日期 | 252-254, 257-259 |
| 按大小 | 259-262 |
| 按内容类型 | 267 |
| 共同/唯一行 | 266-267 |
| 相同但名称不同的文件 | 269 |
| 在不同系统上 | 267-269 |
| 文本差异 | 262-263 |
| 并排比较文本差异 | 263-264 |
| 三个文件的文本差异 | 264-266 |
| 名称较于给定名称的文件 | 255-257 |
| 压缩 | 219-221 |
| 拼接 | 223 |
| 配置，cu 程序 | 549-522 |
| 复制 | |
| CDE 文件管理器 | 140-142 |
| 在当前目录中 | 182-184 |




- 在不同目录中，184-185
- 列表到目录，187
- 统计章节中的行数、字符、单词数，495
- 创建，180-181
- crontabs（时间任务表），308-312
- 解密，219
- 删除
- 核心文件名 (basename)，158
- 从当前目录，191-192
- 从不同目录，192
- 列出目录，192
- 以模式开头的，233-234
- 删除字符
- 按列位置，437-439
- tr 命令，441
- 目的，184-187
- 确定目的，185, 187
- 内容类型，150-151
-  own，148-150
- 设备节点，148-150
- 目录，148-150
- 目录 (home)，44
- SGID 位，284
- 显示控制字符，165-167
- DOS，167-168
- 结束行，216-217
- 首行，215-216
- 行号，165
- man 手页，168-169
- 较小的，160
- 横幅幅字母中的文本，167
- 通过分页器工具，160-164
- 编辑多个，495
- .emacs，517-518




| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 编码为简单文本, 221-223 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 加密/解密, 217-219, 493-494 |

### 系统配置文件
-- `/etc/default/tar`, 354
- `/etc/filesystem`, 370-371
- `/etc/hosts`, 571-573
- `/etc/inittab`, 543-546
- `/etc/passwd`, 278
- `/etc/profile`, 307-308
- `/etc/resolv.conf`, 576
- `/etc/shadow`, 70

### 文件编辑与操作
- `.exrc`, 保存 `vi` 编辑器 (`:`) 选项, 490
- **查找**:
    - 选项与操作, 157-158
    - 通过文件名, 153-157
    - 通过逻辑运算符 `AND`、`OR` 和 `NOT`, 159
    - 通过内容中的特定单词, 158-159
- 配合 `tail` 命令使用, 217
- 段落格式化, 139-140
- 组，更改, 290
- `$HOME/.sh_history`, 499
- 节点号, 36, 148, 193-197
- 列出, 31, 151-153
- 基于连接字段的合并, 224-226
- 移动

### CDE 文件管理器
- `CDE File Manager`, 140-142
- 在当前目录, 182-184
- 在不同目录, 184-185
- 列出到目录, 187
- 导航, 137-138

### 第 838 页
- 非冲突临时, 659-660
- 打开
- `CDE Text Editor`, 136-137
- `Perl`, 724, 740
- 所有权, 279-280, 290
- 并排粘贴, 223





| 路径, 38-39 | |
| :--- | :--- |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 权限, 279-283 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 更改, 285-286 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 默认, 290-291 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 覆盖, 188 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 数字模式设置, 287 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 符号模式, 289 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| SUID/SGID, 291-293 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 写入, 181 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 打印 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 取消/删除作业, 174 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 检查队列, 173-174 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 格式化输出, 175-177 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 列出打印机名称, 171-173 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 移动作业, 174-175 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 打印打印/队列系统, 169-171 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 处理所有 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 目录树, 666-667 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 在一个目录中, 666 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 正则表达式, 148 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 相对路径, 49-51 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 重命名 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 在当前目录中, 182-184 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 在不同的目录中, 184-185 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 替换字符命令, 441 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 恢复 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| cio 命令, 361 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 目标, 348-350, 362-365 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| tar 命令, 344-350 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 恢复选定的 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| cio 命令, 367 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| tar 命令, 352 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 恢复到不同的目录 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| 恢复到原始目录 | |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | |
| cio 命令, 365-366 | |





![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `tar` 命令, 351-352

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 保存

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 命令输出/错误, 112-113, 117

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 输出, grep, 382-383

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 串口设备, 541-542

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 列出, 542-543

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 串口设备配置

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 访问控制, 543

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 拨入, 543-545

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 拨出, 545-547

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 排序, 202

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | ASCII 值, 202-204

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于行, 209-210

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于主键/次键, 210-214

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 忽略前导空格, 204

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 忽略标点符号, 208-209

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 大小写忽略, 207

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 多个, 223

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 数字数字, 204-206

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 逆序, 207-208

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 保存到原始文件, 206-207

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | vi 编辑器, 492

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 源, 184-187

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 拼写检查, 138-139

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 分割

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于部分关键词, 227-228

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于唯一关键词, 228-229

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 分成等长度部分, 226-227

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 符号链接, 148-150

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 传输, 180

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 取消 ucp 请求, 577

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | cu 程序, 552-553

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | ftp (文件传输协议), 582-584

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | rcp 程序, 585-586

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 到/来自 UNIX, 596, 607





- `uucp` 程序, 554-557
- 解压缩, 221
- UNIX 内核，加载到内存, 297
- `vi` 编辑器，大小, 460
- 过滤器, 31
- `egrep` 命令
- 可用的正则表达式通配符, 402
- 指定 0 次或多次出现, 403
- 指定 1 次或多次出现, 403
- `grep` 命令, 31, 158-159, 247, 321-322, 381
- `awk`, 713
- 选择模式, 384-385
- 显示模式的文件名, 386-387
- 查找行, 380-402
- `sort` 命令, 管道, 202
- `find -exec` 命令, 157-158
- `find -print` 命令, 157-158

### 第 839 页
- `find` 命令, 88, 373-374
- `awk`, 712-713
- 比较文件, 255-257
- 按日期, 257-259
- 按大小, 260-262
- 通过文件名, 153-157
- 使用逻辑 `AND`、`OR` 和 `NOT`, 159
- 内容中的单词, 158-159
- 查找
- 字符，`vi` 编辑器, 467
- 边界符号，`vi` 编辑器, 467
- 文件
- 动作, 157-158
- 按访问日期, 252-259
- 按大小, 259-262
- 按内容类型, 267
- 硬链接, 195-197
- 相同但名称不同, 269





| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用文件名，153-157 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用逻辑与 AND、OR 和 NOT，159 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用比给定名称新的名称，255-257 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 内容中包含特定单词，158-159 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `awk`，407-409 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 允许正则表达式的命令，394 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 包含模式，380-381, 384-391 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 忽略大小写，382 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 行号，385 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 匹配字符，395-396, 403 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 不包含模式，385 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 正则表达式通配符，394-395, 402-404 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用 `egrep` 命令指定 0 次或多次出现，403 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 在模式位置指定不允许的字符，397 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 指定正则表达式元素的出现次数，399 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用 `egrep` 命令指定一次或多次出现，402 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 以模式开头和结尾，391-392 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 无界正则表达式通配符，401 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 在正则表达式中使用 shell 替换，392 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 在正则表达式中使用 shell 变量，392 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 在正则表达式周围使用单引号 `()`，393 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `Perl` 中更长的单词，405 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `vi` 编辑器，466-467 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `finger` 命令，67-68 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 火火墙，614, 622 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 软盘驱动器，13, 336 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 备份，328 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 名称，336-339 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 系统前移除磁盘，296 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `fmt` 命令，461-462 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | ENR 变量 `(awk)`，684-687 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `for` 命令，`Perl`，733-734 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | for 循环，662-665, 733-734 |





- `for` 语句, `awk`, 699-700
- `foreach` 命令, `Perl`, 734
- `foreach` 循环, `Perl`, 734
- `前台作业`, 暂停/恢复, 323-325
- `格式`,日期, 72-73
- `段落格式化`
- `CDE 编辑器`, 139-140
- `vi` 编辑器, 461-463
- `FORTRAN` 编程语言, 13, 17
- `Free BSD (自由软件发行)` 操作系统, 20
- `自由软件，从 Internet 下载`, 626-627
- `patch 簇`, 627-628
- `安全公告`, 628
- `2000 年问题`, 628-629
- `自由软件基金会 (Free Software Foundation)`
- `UNIX` 操作系统, `GNU/Linux`, 20-21
- `网站`, 621
- `常见问题解答. FAQs`
- `FS` 预定义变量 (`awk`), 684-686
- `fsck` 实用, 297-298, 375
- `ftp` (文件传输协议)
- `匿名`, 615
- `Windows 版本`, 328, 596
- `全路径`, 45. 另见 `绝对路径`, `路径`, `相对路径`
- `函数`. 另见 `命令`
- `awk`
- `数组`, 693-694
- `数值型`, 695

### 第 840 页
- `字符串`, 689-691
- `system`, 713-714
- `用户定义`, 707-710
- `emacs`
- `帮助`, 531-532
- `列表匹配行`, 524-526
- `写入`, 534-535





- `Perl`, 735-736
- `chomp`, 747
- `each`, 741
- `join`, 747
- `keys`, 742
- `localtime`, 743-744
- `pop`, 736
- `push`, 736
- `shift`, 737-738
- `splice`, 739
- `split`, 746-747
- `time`, 742
- `unshift`, 737-738
- `values`, 742
- `gawk (GNU awk)` 编程语言, 672, 675
- `getline` 语句, `awk`, 701-702
- `Getty` 程序, 543-545
- `gigabytes (GB)`, 36
- `GNU awk (gawk)` 编程语言, 672
- `autoconfig`set, 621-622
- `C` 编译器, 621
- `软件站点`, 621
- `工具`
- `gzip`, 618
- `make`, 621-622
- `GNU/Linux 操作系统 (自由软件基金)`, 20-21
- `goto-line` 函数 (emacs), 535
- `图形用户界面`。参见 `GUI`
- `反引号`。参见 `backquotes()`
- `大于或等于` 运算符, `Perl`, 730
- `大于` 运算符, `Perl`, 730
- `grep` 命令, 31, 158-159, 247, 321-322
- `awk`, 713
- `选择模式`, 384-385
- `显示匹配模式的文件名`, 386-387





# 查找行，380-402, 445

- 起源, 391
- 输出
- 管道至其他命令, 383-384
- 保存, 382-383
- 正则表达式中的 shell 命令替换, 392-393
- 正则表达式中的 shell 变量, 392
- 正则表达式周围的单引号 (),393-394
- 组文件，71
- 组信息，SGID, 283
- 组, 32
- 文件，修改, 290
- 文件所有权, 279-280
- 权限
- 覆盖, 188
- 写入, 181
- 主要与关联, 71
- groups 命令, 280
- `gsub()` 函数, 689
- GUI (图形界面)
- CDE (通用桌面环境)
- 支持的应用, 132-134
- 复制/移动文件/目录, 140-142
- 编辑文本文件, 136-134
- 帮助, 134
- Motif 窗口, 129-132
- 收/发送电子邮件, 142-144
- 运行命令, 135
- Solaris, 122
- CDE (通用桌面环境), 129
- OpenWindows, 122, 125
- 系统控制台, 121-122
- Windows Manager, 121
- X 终端, 121
- X 窗口, 120
- gunzip 命令, 221





- `gzip` 命令, 219-221
- `gzip` 实用程序 GNU, 618
- `H`
- `h` (vi 文本编辑器) 命令, 452-453
- 硬盘
- 容量, 12
- 命令, 375-376
- 文件系统
- *可用空间*, 373-374
- *限制用户空间*, 374-375
- *lost+found 目录*, 375
- *挂载*, 370-371
- *卸载*, 371-372
- *管理*, 370
- 子系统层级结构, 370
- 第 841 页
- 硬链接, 193-195
- 删除, 197
- 查找, 195-197
- 硬件, 12-13
- 串口设备, 541-542
- 访问控制, 543
- 拨入, 543-545
- 拨出, 545-547
- 列出, 542-543
- 哈希数组 (l), 741
- 每一个函数, 741
- 键函数, 742
- 值函数, 742
- `head` 命令, 215-216, 235
- Bourne 脚本中的标题, 643-645
- 帮助
- CDE 应用程序帮助, 132-134
- 手页, 89-91
- *斜杠 (/) 命令*, 93
- *系统子程序*, 92-93
- *带有命令描述*, 94-95
- 在线, emacs, 531-533





- 排序索引，95-96
- vi 文本编辑器，456-457
- here-iss, Perl, 725
- 惠尔惠公司 (HP)
- UNIX 操作系统
- HP-UX, 19
- HP-UX，带有 CDE GUI, 126
- 网站, 624
- 隐藏文件，238-239
- 分级文件系统， 74-77
- UNIX 历史，15-18
- 家目录, 41, 44, 180-181
- Home 键，命令错误，103
- 主机名
- DNS（域名系统），575-577
- UNIX, 571-573
- hotJava (Sun 公司), 612
- HP-UX 操作系统 (惠尔惠公司, HP), 19, 126
- 挂起端口，108
- Hyper 程序，604
- 超文本链接，帮助, 134
- I
- i (vi 文本编辑器) 命令，454
- I/O 选项，终端，63-64
- IBM UNIX 操作系统
- AIX, 20
- 带有 CDE GUI 的 AIX，126
- 网站, 624
- ic (vi 文本编辑器) 命令
- ignore (vi 文本编辑器) 命令
- Icon CDE 应用，133-134
- id 命令，61
- if 命令, Perl, 732
- if 语句，647-650
- if 语句, awk, 696-697
- if-else 语句, Perl, 732-733
- ifconfig 程序，567-571
- ignorecase (vi 文本编辑器) 命令，490





- `IGNORECASE` 定义变量 (awk), 684-686
- Image Viewer CDE 应用程序, 133-134
- 增量搜索, 521-522
- 变量自增 (`++`), Perl, 745
- 行缩进，自动缩进模式, 488
- 打印机输出, 175-177
- `index()` 字符串函数 (awk), 689
- 索引，排列过的, 95-96
- info (emacs), 532-533
- init 级别。参见 `run` 级别，System V (SCO)
- `init` 程序, 543-545
- 变量初始化, awk, 683
-文件的 inode 变化, 255
- inode 节点, 36, 148, 193-197
- awk 脚本中的输入，处理, 680-681
- 插入键 (Insert key), 命令错误, 103
- 插入模式
- 终止, 108-111
- vi 编辑, 454
- 安装
- 调制解器, 599-601
- Windows, 590-592
- `int()` awk 数值型, 695
- 整数运算符，test 命令, 653-654
- 交互式控制结构 (Perl), 729-730
- 交互式 UNIX 系统 (Sun Microsystems/SunSoft), 19
- 第 842 页
- 互联网 浏览, 612-614, 622-623
- 下载软件, 615
- 免费, 626-627
- `Lynx`, 615, 620
- 网络连接通性, 577-578
- 搜索引擎, 613-614
- UNIX 的技术支持, 624-626
- 补丁集群, 627-628





- 安全公告，628
- 2000 年问题，628-629
- UNIX，18-19
- USENET 新闻组，629-631
- 访问，631
- UNIX 倾斜的，632-633
- Windows 网络连接
- 访问 UNIX 主机，598-602
- 使用 Hyper Terminal 访问 UNIX 主机，603-604
- 通过 Netscape Communicator 发送邮件，607-608
- 向/从 UNIX 主机传输文件，604, 607
- Intr 键，111
- IP（互联网协议）地址，569-570
- 数据包，使用 `PPP`（点对点协议）传输，558
- IRIX 操作系统（SiliconGraphics, SGI），20
- ISP（互联网服务提供商），通过互联网访问主机，598-602
- J 命令（vi 编辑器），452-455
  - 意外使用，479-480
- Java 编程语言，13
- 任务
  - 后台
  - 杀死，320, 322, 325
  - 注销时不杀死，320
  - 开始，319
  - 挂起输出，325-326
  - 控制，列出后台任务，323
- 调度
  - 根据系统选择运行，315-316
  - 在平日运行，313
  - 运行一次，313-315
  - 定期运行，308-312
- 开始
  - 更改优先级，318-319
  - 低优先级运行，317-318





# 索引与指南

- **暂停/恢复**: 323-325
- **查看与优先级**: 317
- **jobs 命令**: 323
- **join 命令**: 224-226
- **join 字段**: 224-226
- **join 函数 (Perl)**: 747
- **合并行，vi 编辑器**: 455
- **误删的行**: 479-480

## K
- **k (vi 编辑器) 命令**: 452-453

## Kerm
- **it 程序**: 607
- **内核**: 27
- **文件，加载到内存**: 297

## 键盘
- **键绑定**: 515-518
- **命令错误**
- **使用 Backspace 键纠正**: 103-104
- **误用按键**: 103
- **排序键**: *参见* 排序键，主键和次键
- **keys 函数 (Perl)**: 742
- **关键字**
- **文件，分割**: 227-229
- **man 手**: 331-332
- **kill 命令**: 320-322, 325
- **kill-buffer 函数 (emacs)**: 535
- **kill-line 函数 (emacs)**: 535

## 杀死
- **后台作业**: 320, 322, 325
- **会话**: 108-111
- **千字节，大小**: 74-77
- **shell**: 28-83
- **后台作业**
- **杀死**: 325
- **列出**: 323
- **输出前暂停**: 325-326
- **命令行编辑**: 498





# 索引摘要

- `commands`, `history`, 498-500
- `foreground jobs`, 暂停/恢复, 323-325
- `login id`, `aliases`, 184
- `scripts`, `CDPATH` 变量, 54

## 第 843 页

## L.

- `l` (vi 编辑器) 命令, 452-453
- `l` 符号链接文件类型字母, 149
- `languages`. 参见编程语言
- `launching`. 参见启动
- `leading spaces`. 参见行缩进
- `length()` (awk), 689-690
- `less` 命令, 160-164
- `less than or equal to relational operator`, Perl, 731
- `less than relational operator`, Perl, 731
- `less than signs (<<)`, 此处引用 here-iss, Perl, 725
- `lines in files`
- `finding`
- `awk`, 407-408
- `commands allowing regular expressions`, 394
- `containing patterns`, 380-91
- `deleting repeated lines`, 445
- `ignoring case`, 382
- `line numbers`, 385-386
- `matching any character`, 395-396
- `matching characters in pattern positions`, 396-397
- `not containing patterns`, 385
- `regular wildcards`, 395, 402, 404-405
- `shell command in regular expressions`, 392-393
- `shell variables in regular expressions`, 392
- `single quotes () around regular`, 393-394
- `specifying disallowed characters in pattern positions`, 397-398
- `starting and ending with patterns`, 389-392
- `unbounded regular expression wildcards`, 402
- `words not part of larger words with Perl`, 405
- `displaying line number`, 489





| 缩进，自动缩进模式，488
| 由 grep 命令输出
| 管道传输至其他命令，383-384
| 保存，382-383
| 终止，Perl 脚本，720
| 使用模式。另见模式；字符串
| 删除，445
| 替换，444-445
| 计数，196-197
| 链接到文件
| 硬链接，193-195
| 删除，197
| 查找，195-197
| 软链接/符号链接，197-200
| Linus Torvalds，UNIX 操作系统，Linux 内核，20
| Linux 内核操作系统 (Linus Torvalds)，20
| 设备名称，331
| 软盘驱动器，339
| 磁带驱动器，333-336
| 列表匹配行 (emacs)，524-526
| 列出
| 后台作业，323
| 文件，31, 151-153
| 按最后访问日期，254-259
| 按最后修改日期，252-254, 257-259
| 大小，260
| 使用较于指定名称的文件，255-257
| 串行设备，542-543
| 列出列表
| 使用 ftp 访问远程主机，582
| 检查 ftp 服务器，596
| 字符串拼接示例，688
| 定义和调用函数，708
| `/etc/hosts` 文件，572-573
| `/etc/resolv.conf` 文件，576





# 索引

- `ifconfig` 程序配置详情, 568
- 使用 `fpp`（文件传输协议）列出文件, 583
- 子掩码值, 569
- 传递参数, 708-709
- `ping` 程序, 574-575
- 打印格式说明和修饰符, 705
- 范围模式示例, 679
- 使用十进制点符号表示 IP 地址, 567
- 返回值, 709
- `/etc/inet` 示例, 544
- 查找以太网卡, 566
- `awk` 的最用法, 674
- `talnet` 连接, 579
- 使用 `fpp`（文件传输协议）传输多个文件, 584-585
- 字面量 (Perl), 721
- `ln` 命令, 第 844 页
- 目录，多个文件名, 193
- 文件，多个名称, 194-199
- 本地标识，Perl 变量, 722
- `localtime` (Perl), 743-744
- `log()` `awk` 数值函数, 695
- 逻辑与 (`&&`), 159, 408, 731
- 逻辑或运算符 (Perl), 159, 731
- 将 `logins` 登录单用户模式, 298
- `rlogin`, 579-581
- 脚本, 307-308
- 用于 Lynx 的 `Bourne/Korn Shell`, 623
- 用于 Lynx 的 `C Shell`, 622
- 使用 `cu` 程序的串口设备, 547-548
- 名字, 274
- 程序, 543-545
- `telnet`, 578-579
- 使用 Windows `telnet` 程序的 UNIX 主机, 597





- `logout` 命令, 84
- 循环, 698
- `awk`, 698
- `break` 语句, 698-699
- `continue` 语句, 698-699
- `do` 语句, 698
- `while` 语句, 700
- `awk for` 语句, 699-700
- `for`, 662-665
- Perl
- `for`, 733-734
- `foreach`, 734
- 丢失的目录, 41, 375
- 小写
- 使用 `tr` 命令更改, 442-443
- 忽略、替换字符串, 490
- 忽略
- `grep` 搜索, 382
- `Perl`, 429
- 文件排序, 207
- `lp` 命令, 89, 169, 171-173, 237-238, 245-246
- `lmove` 命令, 174-175
- `lpr` 命令, 169-173
- `lprm` 命令, 174
- `lpstat` 命令
- 检查打印队列, 173-174
- 打印机名称, 171-172
- `ls -1 /dev/cua?` 命令, 542
- `ls -1 /dev/ttyS?` 命令, 542
- `ls` 命令, 31, 42-43, 46, 87, 90, 238, 279-283
- 比较文件
- 按访问日期, 254-255
- 按修改日期, 252, 254
- 按大小, 259
- 确定文件类型, 148-153
- 查找文件的硬链接, 195-197
- `lycos`, 614




- Lynx, 612
- 命令, 623
- 使用 make 实用编译, 621-622
- 从 Internet 下载, 615, 620
- Internet 浏览, 622-623
- M
- M+x (Meta-x), 509
- 宏
- 录制, 518-519
- 重复, 519-520
- 保存, 519
- 魔法数字, 151
- Mailer CDE 应用, 132-134
- 读取/发送邮件, 142-144
- 维护模式, 298
- 主模式 (emacs), 加载, 531
- 文件上的主编号, 330
- make 实用-配套的 C 套件, 621-622
- GNC, 621-622
- man 命令, 92, 234
- man 页面, 168-169
- 检查允许的文件列表和通配符, 234-236
- 设备文件名, 331
- 帮助, 89, 91
- `/` 命令, 93
- 系统子程序, 92-93
- 带有描述, 94-95
- k 选项 (关键字), 331
- PAGER, 92
- 边距。参见行的缩进
- 标记,设置, vi 编辑器, 467-468
- `match()` 字符串函数 (awk), 689-690
- 数学运算, `expr` 程序, 656-657
- 内存, 12
- 第 845 页
- 菜单,选择项目, 668-670




- 根据连接字段合并排序后的文件，224-226
- `mesg` 命令，68
- 微软 (Microsoft)
- UNIX 操作系统，XENIX，20
- 网络客户端，590-592
- 辅助模式 (emacs)，加载，530
- 设备文件上的次设备号，330
- `mkdir` 命令，51
- 调制解调器通信，540-541
- 调制解调器，安装/配置，598-599
- 串口设备，541-542
- 访问控制，543
- 取消 `uuc` 程序的请求，557
- 配置 `cu` 程序，549-552
- 拨入 (dial ins)，543-545
- 拨出 (dial outs)，545-547
- 列出，542-543
- 在 `cu` 程序中登录，547-548
- 网络 `PPP` (点对点)协议协议，558-560
- 在本地系统上运行命令，553-554
- 使用 `uux` 在远程主机上运行命令，556
- 停止网络 `PPP` (点对点)，560
- 停止连接，560
- 使用 `cu` 程序传输文件，552-553
- 使用 `uuc` 程序传输文件，554-557
- 主/次设备号 (emacs)，530-531
- 多用户，299
- 单用户，298
- `vi` 文本编辑器，487-488
- 自动缩进行，488
- 自动换行行，488
- 显示行号，489
- 忽略大小写，490
- 在 `.exrc` 文件中保存 (:) 设置选项，490





由于您提供的文本包含大量的 HTML 实体字符（如 `&#124;`）、重复的图片链接以及碎片化的表格数据，根据高级文档工程师的规范，我已提取了其中的核心内容信息，并按照 Markdown 格式进行了排版优化：

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

- more 命令，152, 160-164
- Mosaic（国家超导应用中心），612
- Motif 窗口管理器（开放软件基金会），121
- CDE（通用桌面环境），126
- 窗口
- 可用控件，129-131
- 在之间移动文本，131-132
- 移动命令（vi 编辑器），475, 476, 479
- `mount` 命令，293, 370-371
- 已挂载的文件系统，293
- 移动传输
- MS-DOS 对比 UNIX，22-24
- 多用户模式，299
- 多维数组，`awk`，694
- `mv` 命令，目录
- 当前，182-184
- 确定，185-187
- 不同的，184-185
- 文件列表，187
- 移动/重命名，188-189
- 覆盖权限，188
- 我的标识，Perl 变量，722
- N
- `n`（vi 编辑器）命令，474-475
- 设备文件，330, 332
- 软驱器，336-339
- 磁带驱动器，333-336
- 文件/管道中的名称，查找包含模式的行，385
- 脚本命名，`awk`，675
- 导航文件，CDE 编辑器，137-138
- Navigator/Communicator（网景），612
- 自动代理服务器，614
- `nawk` 编程语言，672, 675
- NCR UNIX 操作系统（NCR），20
- 子网掩码值，568-569





* Netscape Communicator, 608
* 网络连接性, 564-565
* DNS (域名系统), 575-577
* 在另一个系统上执行命令, 587
* 登录
* `rlogin`, 579-581
* `telnet`, 578-579
* NICs (网络接口卡, 565-567)
* `TCP/IP` 地址, 567, 571
* 第 846 页
* 协议 `ftp` (文件传输协议), 582-584
* 使用 `ping` 程序进行测试, 573-575
* 到 Internet, 577-578
* 传输文件
* 使用 `ftp` (文件传输协议), 582-584
* 使用 `rcp` 程序, 585-586
* UNIX 主机名, 571-573
* 网络接口卡。参见 `NICs` (网络接口卡）
* 新闻传输协议。参见 `NNTPSERVER` (新闻传输服务器）
* 新闻。参见 `USENET` 新闻组
* 网络
* 调制解器通信
* `PPP` (点对点协议), 558-560
* 停止 `PPP` (点对点协议), 560
* 打印作业的溢打印/队列, 172
* Windows, 590-592
* 通过 Internet 访问 UNIX 主机, 598-602
* 使用 `Hyper` 程序访问 UNIX 主机, 603-604
* 通过 Netscape Communicator 发送邮件, 608
* 使用 `telnet` 程序登录 UNIX 主机, 597
* 使用 `ping` 程序测试连接, 593
* 使用 `ftp` 程序传输文件, 596
* 使用 `kermit` 程序传输文件, 607
* 使用 `wincfg.exe` 程序查看配置, 594
* `newgrp` 命令, 284





- 换行符，167-168
- 新闻服务器，631
- 新闻组 (newgroups)
- FAQ（常见问题），626
- USENET，629-631
- 访问，631
- UNIX 倾斜体，632-633
- NF 预定义变量 (awk)，684
- `nice` 命令，317-319
- nice 值。参见任务优先级 (priorities of jobs)
- NICs（网适配器），565-567, 590-592
- TCP/IP 地址，567, 571
- `nispasswd` 命令，277
- `nl` 命令，165
- NNTPSERVER（网络新闻传输服务器），631
- `nohup` 命令，320
- 非单词 (non-words)，vi 文本编辑器，465
- 正常 Shell 参数 (Normal Shell Argument)。参见通配符字符 (wildcard characters)
- 不等于关系运算符 (Perl)，731
- NOT 逻辑，159
- 新型 UNIX 系统，UnixWare，19, 26
- NR 预定义变量 (awk)，684-687
- `nu` (vi 文本编辑器) 命令。参见数字 (vi 文本编辑器) 命令
- 空语句 (:) statements)，awk，697
- 数字 (number) 命令 (vi 文本编辑器)，489
- 数字 (numbers)
- Perl 运算符，730-731
- 设备文件，主设备/次设备号，330
- 数值函数，awk，695
- 数值模式，权限，287
- O
- 八进制导出 (octal dumps)，165-166
- `od` 命令，165-166
- OFMT 预定义变量 (awk)，685-687
- OFS 预定义变量 (awk)，685-687
- 在线帮助手册。参见 `man` 命令；手册页 (man pages)




- 在线帮助，emacs, 531-532
- info 页面， 532-533
- open 命令, Perl, 740
- Open Look 管理器, Open Windows, 122
- Open 软件基金会 (OSF), Motif 管理器, 121
- 打开
- emacs 文件, 512
- 文件
- `CDE` 编辑器, 136-137
- `Perl`, 724, 740
- 第 847 页
- 开放操作系统 (Santa Cruz, SCO), 19, 26
- OpenWindows GUI, 122, 125
- 操作系统, 14-17
- 在 Perl 中使用反引号（`` ``）调用, 744-745
- 配置文件 (cu 程序), 551
- 控制台, 121-122
- 信息
- 命令, 60-64
- 日期, 72-73
- 官方名称, 73-74
- 批处理命令, 315-316
- 关机, 300-301
- `BSD` (AIX), 302
- 脚本, 305-306
- `System V` (SCO), 301
- 启动, 296
- 使用 `fsck` 检查根文件系统, 297-298
- 加载 UNIX 内核文件, 297
- 多用户模式, 299
- 先开启辅助系统, 296-297
- 开启诊断, 297
- 移除启动媒体, 296
- 脚本, 302-307
- `System V` (SCO) 运行级别, 299
- 子程序, man 页面, 92-93




# UNIX，各公司的营销版本，19-20

## 运算符
* `arithmetic`, 695-696
* `awk`
* `conditionial`, 697-698
* `comparison`, 678
* `compound pattern`, 678-679
* `range pattern`, 679-680
* `integer, test command`, 653-654

## Perl
* `angle`, 729
* `logical AND`, 731
* `logical OR`, 731
* `relational`, 730-731
* `string`

## awk
* `options`, 688
* `test command`, 652-653
* `adding arguments`, 88-89
* `adding to commands`, 86-88
* `separating from arguments and commands with white spaces`, 86
* `OR logical`, 159
* `ordinary search/replace processes`, 522-523
* `predefined variable (awk)`, 685-687
* `output`
* `fields, extracting`, 439
* `grep command`
* `piping to other commands`, 383-384
* `saving`, 382-383
* `saving`
* `replaced strings`, 415
* `to files`, 112
* `to screens (tee)`, 117
## 覆盖权限, 188
* ownership, changing files, 290

## P
* page headings, printer output, 175-177




- 页面长度，打印机输出，175-177
- 向上/向下翻键，命令错误，103
- PAGER 分页工具，92, 160-164
- 段落格式
- CDE 文本编辑器，139-140
- vi 文本编辑器，461-463
- 参数.*另参见*参数
- Perl，使用 `@argv` 数组捕获，728-729
- 用户定义函数，708-709
- 父目录，48-49
- `passwd` 命令，71, 277
- `passwd` 文件，70
- 密码，274
- 对他人的访问权限，277-278
- 修改，276-277
- 进入单用户模式，298
- 最小有效时间，275-276
- 次要，274-275
- 替换用户，278-279
- `passwd` 命令，223
- 粘贴
- 文件并排显示，223
- 文本
- 在 emacs 中，512-514
- 在 Motif 窗口中，132
- 集群，627-628
- diag 诊断工具，627
- `PATH` 变量，97-98, 642
- 添加当前目录，99-100
- 添加新软件，100
- 全命令路径名，100-101
- 路径名，38-39.*另参见*绝对路径名、全路径名、`PATH` 变量、相对路径名
- 当前目录，43
- 目录，148-149
- `CDPATH` 变量，54-56
- 常用，56-57




# 索引

- 当前目录的子目录, 45-46
- 第 848 页
- 模式
- awk 脚本, 675-676
- 运算符, 678-680
- 正则表达式, 676-677
- 查看帮助页 (man pages), 234-236
- 删除行
- grep 命令, 445
- uniq 命令, 445-446
- vi 编辑器, 493
- 查找行, 380-382, 389
- awk, 407-408
- 行号, 385-386
- 位置上的字符, 396-397
- 选择模式, 384-385
- 允许正则表达式的命令, 394
- 包含两个模式, 387-388
- 位置上不允许的字符, 397-398
- 仅显示文件名, 386-387
- 忽略大小写, 382
- 不包含模式, 385
- 正则表达式通配符, 389-396, 402, 404-405
- 保存输出, 382-383
- 正表达式中的 shell 命令替换, 392-393
- 正表达式中的 shell 变量, 392
- 无界表达式通配符, 402
- 生成文件名
- 来自目录, 239
- 隐藏文件, 238
- 使用通配符, 232-233, 239-245, 250
- grep 输出，管道到其他命令, 383-384
- 忽略目录, 237
- 多个模式的单一列表, 237-238
- 减少输入量, 236
- 使用 sed 命令替换行, 444-445




- 替换字符串。另见文件中的行，字符串
- 条件性地，482-484
- 全局地，480-481
- 在章节中，481-482
- PC PKZIP 工具，616
- 百分号 (%) 分隔符，sed 命令，416-417
- Performance Meter CDE 应用，133-134
- 句号 (.)
- 正则表达式，395-396
- vi 编辑器，472-475
- Perl 语言，718
- 删除字符串，425-426
- 基于字段，429-431
- 匹配最短跨度，426-427
- 选择性地，429
- 使用空格提高可读性，427
- 可用的正则表达式通配符，404-405
- 替换字符串，425-426
- 忽略大小写，428
- 匹配最短跨度，426-427
- 选择性地，429
- 空格提高可读性，427
- 与其他字符串，427-428
- 不在较大单词中的单词，427
- Perl 脚本，718-719
- 数组，哈希表，741
- 使用反引号 (``) 调用系统，744-745
- 代码引用，723-724
- 命令，732-745
- 使用点号 (.) 拼接字符串，746
- 控制结构，729-730
- 调试，748-749
- 断点点，751, 753-754
- 执行代码行 (n)，750
- 列出代码 (l)，749-750




- 打印变量值，750-751
- 文件句柄，724-725
- 文件
- 关闭，739-740
- 打开，740
- 函数，735-736
- chomp，747
- each，741
- join，747
- keys，742
- localtime，743-744
- pop，736
- push，736
- shift，737-738
- splice，739
- split，746-747
- time，742
- unshift，737-738
- values，742
- here-iss，725
- 输入
- 作为参数，728-729
- 在命令行上，729
- 字面量，721
- 语句-else，732-733 
- 终止符，720
- 真值，730-731
- 变量，721-722
- 自增与自减 (++ and --)，745
- 特殊，725-728
- 权限，279-283
- 配置文件 (cu 程序)，551-552
- 目录
- 更改，285-286
- 使用数字模式设置，287
- 使用符号模式设置，289





- 错误，权限拒绝错误，181-188
- 执行，285
- 文件
- 更改，285-286
- 默认值，290-291
- 数值模式设置，287
- 符号链接模式设置，289
- SUID/SGID，291-293
- 覆盖，188
- 读取，281, 285
- 写入，181, 283-284
- 置换索引，95-96
- `pg` 命令，31, 152, 160-164
- PID 号
- 使用 `ps` 命令查找，321-322
- 杀死作业，320-321
- `ping` 程序，573-593
- 检查互联网访问，577
- 管道符号 (`|`)，107
- 管道线，107
- 压缩，219-221
- 解密，219
- 删除字符
- 按列位置，437-439
- `tr` 命令，441
- 显示
- 末尾行，216-217
- 前几行，215-216
- 加密，217-219
- 文件到分页器工具，160-164
- 数字到分页器工具，165
- 查找行，380-382
- `awk`，407-408
- 行号，385-386
- 选择模式，384-385
- 允许正则表达式的命令，394





![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 包含两种模式，387-388
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 仅显示文件名，386-387
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 忽略大小写，382
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 不包含模式，385
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 特定位置的字符，396-397
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 特定位置的不允许字符，397-398
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 正正则表达式通配符，389-396, 402-405
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 保存输出，382-383
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 正表达式中的 shell 替换，392-393
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 正表达式中的 shell 变量，392
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 无界表达式通配符，402
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 输出，31, 383
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 打印，172-173
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 替换字符，`tr` 命令，441
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 保存输出，`grep` 命令，382-383
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 排序，202
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) ASCII 值，202-204
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 行内的字段，209-210
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 基于主/次键的，210-214
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 忽略前空格，204
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 忽略标点符号，208-209
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 忽略大小写，207
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 按数值排序的数字，204-206
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 逆序，207-208
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 将结果保存到原始文件，206-207
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 解压缩，221
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 纯文本文件，280
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 点对点协议。参见 `PPP`（点对点协议）
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 点，509
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) `pop` 函数 (perl)，736
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 端口，串口，541-542
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) POSIX `awk` 编程语言，672, 675
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) POSIX UNIX 标准 (IEEE),24
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 向新闻组发布消息，630





# 索引与列表

- UNIX shell, 86-87
- Perl, 723
- PPP (点对点协议), 558
- 配置, 558-560
- 停止连接, 560
- `pr` 命令, 175-177
- 预定义变量, `awk`, 684-687
- 当前目录。*参见* current directory
- 主要排序键, 210
- `-print` 命令, `find`, 157-158
- 格式指定符 (`awk`), 704
- Print Manager CDE 应用, 132-134
- 第 850 页
- `printf` 函数, 433-436
- `printf` 语句, `awk`, 703-706
- `printf()` 字符串函数 (`awk`), 689
- 打印文件, 172-173
- 取消/删除作业, 174
- 检查打印队列, 173-174
- 格式化输出, 175-177
- 列出打印机名称, 171-172
- 移动打印作业, 174-175
- 打印缓冲/队列系统, 169-171
- 作业优先级
- 更改, 318-319
- 低, 317-318
- 查看, 317
- 进程, 77-79
- `.profile` 文件, 脚本, 登录, 307-308
- 编程语言, 13-14
- `awk`, 672
- 删除/替换字符串, 429-435
- 特性, 673
- 查找行, 407-409
- 用性, 673
- 版本, 672, 675





- emacs Lisp, 517
- Perl, 718. *另参见* Perl 脚本
- 删除字符串, 425-426
- 删除/替换字符串, 427-429
- 查找不是较大单词部分的单词, 405
- 可用的正则表达式通配符, 404-405
- 替换字符串, 425-426
- 程序, 13-15. *另参见* 命令，实用程序
- 添加到 `PATH`, 100
- `chmod` (更改模式), 285-289
- `cu`, 547-548
- 配置, 549-552
- 在本地系统上运行命令, 553-554
- 传输文件, 552-553
- 从 Internet 下载, 615
- 免费, 626-627
- Lynx, 615, 620
- 补丁簇, 627-628
- 安全公告 (Security Bulletins), 628
- 2000 年问题, 628-629
- expr, 数学计算, 656-657
- ftp, 582-584
- Windows 版本, 328, 596
- getty, 543, 545
- GNU 站点, 621
- Terminal, 604
- `ifconfig`, 567-571
- init, 543, 545
- kermit, 607
- , 543-545
- Netscape Communicator, 608
- ping, 573-575, 593
- 检查 Internet 访问, 577
- rcp, 585-586
- rlogin, 579-581
- rsh, 587





# 主题索引

- **SGID (Set Group ID)**, 283
- `shell`, 543-545
- **SUID (Set User ID)**, 283
- **SymbEL (Virtual Adrian) 软件**, 626
- `telnet`, 328, 578-579, 597
- `uucp`
- *取消请求*, 557
- *传输文件*, 554-557
- `uugetty`, 545-547
- `uustat`, `uucp` 传输状态, 556-557
- `uux`, 远程主机上的命令, 556
- `winipcfg.exe`, 594
- `X11`, 120
- `prompts`
- `Bourne shell scripts`, 643-645
- `shell (UNIX)`, 82
- *为命令添加参数*, 84-86
- *为选项添加参数*, 88-89
- *为命令添加注释*, 86
- *将当前目录添加到 PATH*, 99-100
- *将新软件添加到 PATH*, 100
- *为命令添加选项*, 86-88
- *为命令添加 PATH 变量*, 97-98
- *Command not found 错误*, 96-97
- *常见输入错误*, 101-105
- *错误消息*, 105-111
- *完整路径名*, 100-101
- *来自 man pages 的帮助*, 89-91, 93-95
- *来自重排索引索引 (permuted index) 的帮助*, 95-96
- *将命令输出/错误保存到文件*, 112-113, 117
- *来自 man pages 的系统子程序*, 92-93

- **专有系统**, 16-18
- **协议**
- `ftp (file transfer protocol)`, 582-584
- **网页浏览**, 612-613





# PPP (点对点协议), 558

- 配置, 558-560
- 停止连接, 560
- rcp 程序, 585-586
- TCP/IP, 18, 590-592
- 地址, 567, 571
- 拨号上网网络配置, 601
- 使用 telnet 程序登录 UNIX 主机, 597-598
- 使用 `ping` 程序测试连通性, 573-575
- UNIX 主名, 571-573
- 使用 `winipcfg.exe` 程序查看设置, 594-596
- 代理服务器, 614, 622
- 代理服务，访问 Internet, 577-578
- `ps-ef` 命令, 78-79
- `ps` 命令, 317, 321-322
- PS2 提示错误消息, 107
- 伪终端, 61
- 标点符号，忽略排序文件, 208-209
- `push` (Perl), 736
- `pwd` 命令, 43-44
- Q
- `(:q!` (vi 编辑器) 命令, 455
- `qcan` 命令, 174
- 四分之一英寸卡带 (QIC) 磁带磁盘驱动器, 332
- 问号 (`?`) 文件生成通配符, 232, 239-241
- 问号 (`?`) 通配符, Perl, 426-427
- 任务队列/打印池作业, 169-171
- 取消/删除, 174
- 移动, 174-175
- 网络, 172
- 状态, 173-174
- 快速保存， vi 编辑器, 458
- `quota` 命令, 374
- 引号, 命令错误, 104-105
- R
- `r` (vi 编辑器) 命令, 459





- `rand()` `awk` 数值函数, 695
- 范围模式运算符，`awk` 脚本, 679-680
- `rc` 脚本, 302, 305-307
- `rc0.d` 目录, 305-306
- `rc2.d` 目录, 302, 305
- `rcp` 程序，传输文件, 585-586
- `read` 命令, 645-646
- `read` 权限, 281, 285
- `read-only` 模式，`vi` 编辑器, 464
- `reading` 邮件，`CDE Mailer`, 142-144
- `rebinding` 键盘绑定, 517
- `recording` 宏, 518-519
- 在 `vi` 编辑器中 `recovering text`
- `deleted text` 删除的文本, 469
- `lost changes` 丢失的更改, 463-464
- `recursively copying directory subtrees` 递归复制目录子树, 189-191
- `RedHat Software`, UNIX 操作系统，`RedHat Linux`, 20
- `redirecting` 重定向
- `grep` 命令的 `output`, 382-383
- 使用 `*` (星号) 将标准输出到文件, 235
- `reel to reel drives` 卷带驱动器。见 9 轨半英寸磁带驱动器
- `regular aliases` 普通别, 506
- `regular expression patterns` 正则表达式模式, 676
- `metacharacters` 元字符, 676-677
- `operators` 运算符
- `comparison` 比较, 678
- `compound pattern` 复合模式, 678-679
- `range pattern` 范围模式, 679-680
- `regular expression wildcards` 正则表达式通配符, 158, 388
- `available with egrep command` 可用, 402
- `available with Perl` 可, 404-405
- `circumflex` (`^`), 389-390
- `circumflex and dollar sign` (`^$`), 391-392
- `deleting strings` 删除字符串, 417
- `based on fields` 基于字段, 429
- `selectively` 选择性地, 417-418, 429





| 主题 | 页面引用 |
| :--- | :--- |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 美元符号 ($), 390-391 |
| 句号 (.), 395-396 |
| 替换字符串, 412-415 |
| 基于字段, 429 |
| 匹配字符, 421-423 |
| 忽略大小写 (Perl), 429 |
| 匹配最长跨度, 424-425 |
| 第 852 页 |
| 每行一次, 416 |
| 选择性, 417-418, 429 |
| 方括号 ([..]), 396-397 |
| 方括号 ([^..]), 397-398 |
| 关闭, 406 |
| 无边界, 402 |
| 正则表达式, 388 |
| 更改行缩进, 484 |
| 允许使用, 394 |
| 扩展, 402 |
| Shell 替换, 392-393 |
| Shell 变量, 392 |
| 字符串 |
| 条件替换, 482, 484 |
| 全局替换, 480-481 |
| 分区域替换, 481-482 |
| 普通文件, 148-187 |
| 常规搜索/替换, 523-524 |
| 关系运算符, Perl, 730-731 |
| 相对路径, 45, 149, 180 |
| 文件，访问, 49-51 |
| 与路径的对比 |
| 使用 cpio 命令检查, 362 |
| 使用 tar 命令检查, 346-348 |
| 依赖操作系统 (Siemens Nixdorf, SNI), 20 |
| 备注。参见注释 |
| 远程主机 |
| 取消 uucp 程序请求, 557 |




- 登录, 579-581
- 接收文件, 552-553
- 运行命令
- 在本地系统上, 553-554
- 使用 uux 程序, 556
- 使用 uucp 程序传输文件, 554-557
- 删除。见删除 (deleting)
- 重命名
- 目录, 188-189
- 文件
- 确定目标, 185-187
- 在当前目录, 182-184
- 在不同目录, 184-185
- 覆盖权限, 188
- renice 命令, 318-319
- 重绘屏幕，vi 编辑器, 457
- 重复宏, 519-520
- 替换文本。见搜索/替换 (searching/replacing)
- 报告, awk
- 复杂的, 710-711
- 数据提取, 711
- repquota 命令, 374-375
- 恢复文件/目录
- cpio 命令, 361
- 目标, 348-350, 362-365
- 选的文件/目录
- cpio 命令, 367-368
- tar 命令, 353
- tar 命令, 344-350
- 不同目录
- cpio 命令, 367
- tar 命令, 352-353
- 原始目录
- cpio 命令, 365-366
- tar 命令, 351-352
- 恢复行，vi 编辑器, 460




- `return statement`, `awk`, `用户定义函数`, 709-710
- `反向过滤器 grep 命令`, 385
- `RLENTH` 预定义变量 (`awk`), 685-687
- `rlogin` 程序, 579-581
- `rm` 命令, 53-54, 84-86, 233-234, 237-245
- `目录`
- `删除文件`, 191-192
- `删除文件硬链接`, 197
- `删除子树`, 192
- `覆盖权限`, 188
- `rmdir` 命令, 52
- `robots`, 613
- `根目录`, 48, 74
- `更改`, 44-45
- `使用 fsck 检查`, 297-298
- `目录`
- `文件`, 37-38
- `路径名`, 38-39
- `路径名`, 46
- `RS` 预定义变量 (`awk`), 685-687
- `rsh` 程序, 587
- `RSTART` 预定义变量 (`awk`), 685-687
- `运行级别`, System V (SC0), 299
- `set` (`vi` 编辑器)
- `autoindent`, 488
- `ignore`, 490
- `number`, 489
- 第 853 页
- `.rc` 文件中的 `options`, 490
- `showmode`, 487-488
- `Santa Cruz (SCO)` 操作系统
- `OpenServer`, 19, 26
- `UnixWare`, 19, 26
- `UnixWare 7`, 26
- `UnixWare 7 CDE GUI`, 126





- XENIX, 19
- 保存
- 在 `.exrc` 文件中使用 `(:set options (vi text editor)`, 490
- 将命令输出/错误写入文件, 112
- 经常使用的目录路径, 56-57
- emacs 文件, 512
- 宏, 519
- 输出
- `grep` 命令的输出, 382
- 替换的字符串, 415
- 标准输出到屏幕, 117
- Motif 窗口中的文本, 132
- `vi` 编辑器
- 更改, 455
- 更改（快速保存）, 458
- 更改（快速保存到不同文件）, 458
- 文件, 458
- `/sbin` 目录, 41
- 任务调度
- 根据系统选择运行, 315-316
- 在工作日运行, 313
- 运行一次, 313-315
- 定期运行, 308-312
- UNIX
- OpenServer 设备名称, 331
- 软磁盘驱动器, 338
- 磁带驱动器, 333-336
- 运行级别, 299
- 系统关机, 301, 305-306
- 系统启动, 302, 305
- 临时文件, 180
- 使用 `vi` 编辑器创建, 451-452
- 脚本。*参见* `awk` 脚本；Bourne shell 脚本；Perl 脚本





# 功能列表与页码

- `login`, 307-308
- `shutdown`
- `BSD (AIX)`, 305-306
- `System V (SCO)`, 305-306
- `startup`
- `BSD (AIX)`, 306-307
- `System V (SCO)`, 302, 305
- `SCSI 磁带`, 332-333
- `sdiff 命令`, 235-236
- `并排比较文本差异`, 263-264
- `互联网搜索引擎`, 613-614
- `搜索/替换`
- `emacs 编辑器`, 520-521
- `字符情况`, 525-526
- `增量搜索`, 521-522
- `列出匹配项`, 524-526
- `普通搜索`, 522
- `普通搜索/替换`, 522-523
- `正则搜索/替换`, 523-524
- `包含模式的行`, 444-445
- `strings`, 412-414
- `基于字段值`, 432
- `基于字段`, 429-431
- `正则表达式通配符匹配的字符`, 421-423
- `条件地`, 482-484
- `删除除模式以外的所有内容`, 423-424
- `全局地`, 480-481
- `忽略大小写`, 428
- `在章节内`, 481-482
- `匹配最长跨度`, 424-425
- `匹配最短跨度`, 426-427
- `不替换 0 次或多次出现`, 421
- `每行一次`, 415-416
- `Perl`, 425-426
- `正则表达式通配符`, 414-415




- 保存输出, 415
- sed 命令分隔符, 416-417
- 选择性地, 417-418, 429
- shell 变量, 420
- 为了可读性使用空格, 427
- 特殊字符, 419
- 另一个字符串, 427-428
- 不包含在较大单词中的单词
- 字符, 459
- 命令, 470
- 单词, 459-460
- 次级密码, 274-275
- 排序键, 210-214
- 安全
- 公告, 628
- 登录名, 274
- 密码, 274
- 他人的访问权限, 277-278
- 修改, 276-277
- 进入用户模式, 298
- 有效时间, 275-276
- 次级, 274-275
- 替换用户, 278-279
- 问题，将当前目录添加到 `PATH` 变量, 100
- sed 命令, 215-216
- 修改缩进, 484
- 删除字符串, 417-418
- 替换
- 分隔符, 416-417
- 行, 444-445
- 替换字符串, 412-414
- 正则表达式通配符匹配的字符, 421-423
- 有条件地, 482-484
- 删除除搜索模式以外的所有内容, 423-424
- 全局地, 480-481
- 匹配最长跨度, 424-425



- `在章节中`, `481-482`
- `不替换 0 次或更多次`, `421`
- `每行一次`, `415-416`
- `正则表达式通配符`, `414-415`
- `保存输出`, `415`
- `选择性地`, `417-418`
- `shell 变量`, `420`
- `特殊字符`, `419`
- `分号 (:), Perl 行终止符`, `720`
- `发送邮件, CDE Mailer`, `142-144`
- `vi 编辑器中分隔的单词`, `465`
- `顺序访问`, `330`
- `串行设备`, `541-542`
- `配置`
- `访问控制`, `543`
- `拨号入`, `543-545`
- `拨号出`, `545-547`
- `cu` 程序, `549-552`
- `在本地系统上运行命令`, `553-554`
- `传输文件`, `552-553`
- `列出`, `542-543`
- `使用 cu 程序登录`, `547-548`
- `网络`
- `PPP (点对点协议)`, `558,560`
- `停止 PPP (点对点协议) 连接`, `560`
- `up` 程序
- `取消请求`, `557`
- `传输文件`, `554-557`
- `ux` 程序, `556`
- `服务器`
- `新闻`, `631`
- `代理`, `614,622`
- `第七版 UNIX`, `25`
- `SGID (Set Group ID) 程序`, `283-284`
- `SUID 文件`, `291-293`
- `shadow 密码`, `278`




# Shell (UNIX)

- **Shell (UNIX) 提示符**，27, 543-545。另见 Bourne Shell（Bourne shells）、K Shell（Korn shells）。
- **命令**，29, 82-84。
- **添加参数**，84-86。
- **为选项添加参数**，88-89。
- **添加注释**，86。
- **将当前目录添加到 PATH**，99-100。
- **将新软件添加到 PATH**，100。
- **添加选项**，86-88。
- **添加 PATH 变量**，97-98。
- **未找到命令错误**，96-97。
- **常见输入错误**，101-105。
- **错误信息**，105-111。
- **完整路径名**，100-101。
- **来自帮助页（man pages）的帮助**，89-91, 93-95。
- **来自置换索引（permuted index）的帮助**，95-96。
- **在 CDE 中运行**，135。
- **将输出保存到文件**，112-113, 117。
- **正则表达式中的替换**，392-393。
- **来自帮助页（man pages）的系统子程序**，92-93。
- **变量**，30。
- **在正则表达式中**，392。
- **替换字符串**，420。
- **异常输出的排除**，33。

## Shell 模式元字符

- 见通配符字符。
- **Shell**。另见 Bourne Shell（Bourne shells）、K Shell（Korn shells）。
- **列出作业**，323。
- **将作业挂起到后台**，323-325。
- **shift (Perl)**，737-738。
- **字符串快捷方式、别名命令（alias command）**，506。
- **showmode (vi 编辑器) 命令**，487-488。
- **关闭命令（shutdown command）**，300-302。
- **关闭系统**，300-301。
- **BSD (AIX)**，302。
- **System V (SCO)**，301。





# 索引

- Silicon Graphics (IRIX), 20, 624
- 西门子 Nixdorf (SNI) UNIX 操作系统, 20
- `sin()` awk 数值函数, 695
- 单引号 ()
- 字符串搜索/替换, 419
- 在命令中的误用, 104-105
- 第 855 页
- 单用户模式, 298
- 第六版 UNIX, 25
- `/` 命令, 93
- `/` 分隔符，`sed` 命令, 416-417
- 连接槽, 565
- Snapshot CDE, 133-134
- 软链接/符号链接, 197-200
- 软件。见“程序”
- Solaris
- 设备文件名, 331
- 软磁盘驱动器, 337
- 磁带驱动器, 334-335
- 新目录名称, 41
- Solaris/SunOS 操作系统 (Sun Microsystems/SunSoft), 19, 122
- 图形用户界面 (GUI), 122, 125, 129
- `sort` 命令, 202, 235-236, 245-246, 445
- ASCII 字符值, 202, 204
- 基于行内字段, 209-210
- 主要/次要排序键, 210-214
- 按大小比较文件, 260
- 忽略
  - 行首空白空格, 204
  - 标点符号, 208-209
  - 大写/小写, 207
  - 多文件, 223
  - 按大小排序数字, 204-206
  - 倒序, 207-208
  - 将结果保存到原始文件, 206-207





# 排序

- 按最后访问日期排序，254-259
- 按最后修改日期排序，252-254, 257-259
- 按大小排序，260
- 多重排序，223
- vi 文本编辑器，492
- 按比给定名称更新的名称，255-257

# 文件

- 管道线 (pipelines)，202
- ASCII 值，202-204
- 基于行排序，209-210
- 基于主键/次主键排序，210-214
- 忽略前导，204
- 忽略标点符号，208-209
- 忽略大小写，207
- 按数字数值大小排序，204-206
- 倒序排序，207-208
- 保存到原始文件，206-207
- 代码，Lynx，615, 619-621
- 目录，184-187
- 目录名，186
- 编辑器
    - emacs，498
    - vi，498
- 源文件，184-187
- 命令中的空格，102
- UNIX 标准，24
- 通配符
- 特殊变量，Perl，725-728
- 文本拼写检查
- CDE 文本编辑器，138-139
    - emacs，526-528
    - vi 文本编辑器，461
- 爬虫程序 (spiders)，613
- splice 函数 (Perl)，739





# split 命令, 226-227

## split 函数 (Perl), 746-747
## `split()` 字符串函数 (awk), 689-691

## 分割文件
- 根据节关键字, 227-228
- 根据唯一关键字, 228-229
- 分成等长度的分段, 226-227

## 打印任务的缓冲/队列, 169-171
- 取消/删除, 174
- 移动, 174
- 移动, 175
- 网络, 172
- 状态, 173-174

## `sprintf()` 函数 (awk), 689-691
## `sqrt()` 数值函数, 695

## 方括号 `[..]`
- 文件生成, 232

## 不允许的通配符
- 字符, 243-244

## 通配符字符, 241-243
- 正则表达式, 396-398

## `srand()` awk 数值函数, 695
- 目录, 41

## 标准错误 (stderr), 30, 655
- 第 856 页
- 标准输入, 112
- 标准输出, 30, 655

## 使用 `*` 重定向到文件, 235
- 保存
- 替换字符串, 415
- 重定向到文件和屏幕 (`tee`), 117

## 排序后的文件, 206-207
- 开始

## emacs, 510-511
- 任务
- 更改优先级, 318-319
- 低优先级, 317-318





- 文本编辑器，`vi`, 450-451
- `stat` 子程序，108
- 语句
- `awk`
- `break`, 698-699
- `continue`, 698-699
- `do`, 698
- `for`, 699-700
- `getline`, 701-702
- `if`, 696-697
- `null ()`, 697
- `printf`, 703-706
- `return`, 709-710
- `while`, 700
- `case`, 668-670
- `elif`, 648-650
- `else`, 648-650
- `if`, 647-650
- `Perl, if-else`, 732-733
- `uuc 文件传输状态`，556-557
- `stderr`（标准错误），30
- `stdin`（标准输入），30
- `stdout`（标准输出），30
- 粘滞位（stick bits），283-284
- `strftime()` 字符串函数 (`awk`)，689-691
- `tail` 命令，216-217, 235
- 带归档工具。参见 `tar` 命令
- 磁带驱动器，13, 332-333
- 备份，328
- 设备名称，333-336
- 启动系统前移除磁带，296
- `tar` 命令，88, 339-340, 376
- 选择性备份目录或文件，343
- 备份目录子树，341-342
- 块大小，354-355
- 目录，复制子树，191





- 局限性，355
- 列表目录 (TOC), 343-344
- 恢复文件/目录，344-350, 353
- 恢复到不同的目录，352-353
- 恢复到原始目录，351-352
- 备份设备表，354
- TCP/IP 协议，18, 590-592
  - 地址，567, 571
  - 使用 `ping` 测试连通性, 573-575
  - UNIX 主机名, 571-573
- 配置拨号上网网络, 601
- 使用 `telnet` 登录 UNIX 主机, 597-598
- 使用 `winipcfg.exe` 查看设置, 594-596
- `tcsh` (Linux) 壳， 28, 83
- UNIX 技术支持
- 互联网，624-626
- 补丁集群，627-628
- 安全公告 (Security Bulletin)，628
- 2000 年问题，628-629
- 仅限软件，624-625
- `telnet`，328, 578-579, 597
- 临时文件，180
- 太字节 (TB)，36
- Terminal CDE 应用，132-135
- 另见终端 (terminals)
- 连接，61
- 使用 Hyper 访问 UNIX 主机，604, 607
- I/O 设置，63-64
- 类型，62-63
- 终止作业，320-322
  - 在注销时防止，320
  - 在 Korn shell 下，325
- 终止符，在脚本中，720
- test 命令
- 检查





## 变量内容， 652-654

## 文件系统对象属性, 648-652
- 文件系统对象属性， 650
- 文本
- 复制
- 文件之间，485-487
- 在同一文件内，485
- 删除，vi 编辑器命令，468
- 编辑器。参见文本编辑器

## 第 857 页
- 文件
- 比较/唯一行，266-267
- 比较差异，262-266
- 从二进制转换，221-223
- DOS，167-168
- 帮助页 (man pages)，168-169
- 段落格式化，139-140
- Motif 窗口
- 在...窗口之间移动，131-132
- 粘贴，132
- 保存，132
- 移动
- 文件之间，485-487
- 在同一文件内，485
- 替换，vi 编辑器命令，470
- 拼写检查，138-139
- Text Editor C 应用，132-134
- 文件
- 段落格式化，139-140
- 导航，137-138
- 打开，136-137
- 拼写检查，138-139
- 帮助，134
- 编辑器
- emacs，508-509
- 自动备份文件，514-515
- 键位绑定，515-518





# 编辑器功能与操作指南

### 复制/剪切/粘贴文本，512-514
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 退出，512
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 启动，510-511
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 主模式/次模式，530-531
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在线帮助，531-533
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 打开/保存文件，512
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 录制宏，518-519
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 重复宏，519-520
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 保存宏，519
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 搜索/替换文本，520-526
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 文本拼写检查，526-528
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 撤销更改，512
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### Web 帮助站点，533-534
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 编辑函数，534-535
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 打开 Windows，125
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### Text Editor CDE 应用，450
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 字符串缩写，489
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 放弃更改并退出，455
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 在行末追加文本，458
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 自动缩进行，488
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 自动自动换行，488
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 错误蜂鸣，453
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 更改行缩进，484
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 其他 UNIX 命令，491
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 检查拼写，461
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 复制文本，485-487
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 统计区域的行数/单词，495
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 创建临时文件，451-452
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 光标移动，452-453, 460, 465-468
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 删除字符，454
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 删除行，454-455
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示输入模式，487-488
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 显示行号，489
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 编辑多个文件，495
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)

### 加密/解密文件，493-494
![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif)





| `文件名、大小和当前位置, 460` |
| | |
| | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `查找和重复编辑, 474-475` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `段落格式化, 461-463` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `帮助功能, 456-457` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `插入模式, 454` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `插入横幅标题, 494` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `插入其他 UNIX 命令输出, 491-492` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `合并行, 455` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `意外合并行, 479-480` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `将按键映射到命令序列, 475-476, 479` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `在文件间移动文本, 485-487` |
| | |
| | | |
| | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `在同一文件中移动文本, 485` |
| | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `非单词, 465` |
| | |
| | | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `快速保存, 458` |
| | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `只读模式, 464` |
| | |
| | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `恢复删除的文本, 469` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `恢复丢失的更改, 463-464` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `重绘屏幕, 457` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `光标移动计数, 454` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `重复编辑, 472-473` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `替换单个字符, 459` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `替换字符串, 480-484, 490` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `替换单词, 459-460` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `恢复行, 460` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `在文件中保存选项, 490` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `保存更改并退出, 455` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `保存不同的文件, 458` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `分离单词, 465` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `排序文件, 492` |
| | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `开始/结束, 450-451` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `文本更改, 469-470` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `文本删除命令, 468` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `文本插入命令, 464-465` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `文本替换命令, 470` |
| | |
| | | |
| | | | ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) |
| | |
| | `撤销更改, 457-458` |
| | |





- 写入权限错误, 459
- 文本插入命令, vi 编辑器, 464-465
- 新闻组帖子线程化, 631
- 时间函数 (Perl), 742
- 分时制, 16
- 标题, Bourne shell 脚本, 643-645
- /tmp 目录, 40
- 令牌环网络, 565
- `tolower()` 字符串函数 (awk), 690-691
- `toupper()` 函数 (awk), 690-691
- `tr`, 235
- 字符
- 关闭第 8 位, 443
- 转换大小写, 441-442
- 选择性删除, 443
- 替换/删除, 440-441
- 将控制字符转换为一个错误信息, 444
- 版本, 441
- 别名, 506
- 传输, 131
- 目录, 188-189
- 文件
- 取消 uucp 请求, 557
- 确定目标地, 185-187
- ftp (文件传输协议), 582-584
- 在当前目录下, 182-184
- 在不同目录下, 184-185
- 将列表转换为目录, 187
- rcp 程序, 585-586
- 使用 cu 程序, 552-553
- 使用 uucp 程序, 554-557
- 写入权限, 188
- 到/从 UNIX 文件
- 使用 Windows ftp 程序, 596
- 使用 Windows kermit 程序, 607





# 文件/目录, CDE 文件管理器, 140-142

- `在文件之间`, 485-487
- `在 Motif 窗口之间`, 131-132
- `在同一文件中`, 485
- `字符转换`, 441
- `控制进入错误`, 444
- `CDE 垃圾箱`, 129
- `树形结构`。参见目录
- `trn 实用程序`, 631
- `排除 Windows 连接故障，ping 程序`, 593-594。另请参见调试脚本
- `真值, Perl`, 730-731
- `tty 命令`, 61
- `双指编辑`, 474-475
- `TX 段落 (emacs)`, 535
- `type 命令`, 100-101
- `U`
- `u (vi 编辑器) 命令`, 457-460
- `加州大学伯克利大学操作系统，BSD 软件`, 20-21
- `ULTRIX 操作系统 (数字设备公司，DEC)`, 20
- `umask 命令`, 290-291
- `uname 命令`, 73-74
- `uncompress 命令`, 221
- `解压文件`, 221
- `撤销更改`
- `emacs`, 512
- `vi 编辑器`, 457-458
- `uniq 命令，删除重复行`, 445-446
- `UNIX`
- `公司营销系统`, 19-20
- `历史`, 15-18
- `主机`, 571-573
- `Internet`, 18-19
- `用户感兴趣的新闻组`, 632-633
- `购买/免费获取`, 32-33
- `修订`, 24-26





# 脚本。参见 Shell (UNIX) 提示符

- 标准，24-26
- 来自互联网的术支持，624-626
- 补丁集群，627-628
- 安全公告，628
- 2000 年问题，628-629
- 供应商，网站，623-624
- 与 Windows 和 MS-DOS 的对比，22-24

## 第 859 页

### Windows 网络
- 通过互联网访问主机，598-599, 601-602
- 使用 Hyper Terminal 访问 UNIX 主机，603-604
- 使用 Netscape Communicator 收发电子邮件，608
- 使用 ftp 程序传输文件，596-597
- 使用 kermit 程序传输文件，607
- 使用 telnet 程序登录 UNIX 主机，597

### TCP/IP 协议，590-592
- 使用 ping 程序测试连接，593-594
- 使用 winipcfg.exe 查看配置，594-596
- 加密软件，219

### UNIX GUI
- CDE (通用桌面环境)，124
- 支持的应用程序，132-134
- 复制/移动文件/目录，140-142
- 编辑文本文件，136-140
- 帮助，134
- Motif 窗口，129-132
- 读取/发送电子邮件，142-144
- 运行 shell 命令，135
- Solaris，122
- CDE (通用桌面环境)，129
- OpenWindows，122-125
- 系统控制台，121-122
- Windows Manager，121
- X 终端，121
- X 窗口，120





由于提供的原始文本包含大量的表格占位符（`&#124;`）和重复的图片链接，根据高级文档工程师的规范，我已过滤掉冗余的格式符号，提取了核心内容并对其进行了结构化排版：

- UNIX SVR3 和 SVR4 操作系统 (AT&T), 19, 26
- UNIX-to-UNIX-copy-program。参见 `uucp` 程序，传输文件
- UnixWare
- 7 种操作系统 (Santa Cruz Operation, SCO), 26, 126
- Novell, 19, 26
- Santa Cruz Operation, SCO, 19, 26
- `unmount` 命令, 371-372
- `unshift` 函数 (Perl), 737-738
- unzip 工具, 615, 618
- 读取/写入 PKZIP 文件. 616
- `upcase-word` 函数 (emacs), 535
- 使用 `tr` 命令进行大写写转换, 442-443
- 忽略，替换字符串, 490
- 忽略
- `grep` 搜索, 382
- `Perl`, 429
- 排序排序, 207
- USP (不间断电源), 298
- 适当系统关机设置, 302
- `uptime` 命令, 66-67
- URLs (统一资源定位符) 标识符, 612-613
- USENET 新闻组, 629-631
- 访问, 631
- UNIX 斜体, 632-633
- 用户账户, 32
- 文件所有权, 279-280
- 权限
- 覆盖, 188
- 写入, 181
- PPP (点对点)协议连接, 558-560
- 启用/禁用 `crontab/at` 命令, 316
- 替换, 278-279
- 用户信息
- 命令





- 当前用户, 60-64
- 其他用户, 64
- SUID 程序, 283
- 用户信息字段, 编辑, 70
- 用户输入, Bourne shell 脚本, 645-647
- 用户输出, Bourne shell 脚本, 643-645
- 用户定义函数, awk, 707
- 定义, 707-708
- 参数, 708-709
- 返回值, 709-710
- `/usr` 目录, 41
- `/usr/bin` 目录, 41
- `/usr/lib` 目录, 41
- `/usr/sbin` 目录, 41
- `/usr/spool` 目录, 41
- `/usr/tmp` 目录, 40
- 工具, 15, 27. 另参见命令，程序
- autoconfig, GNU, 621-622
- fsck, 297-298
- lost+found 目录, 375
- gzip, GNU, 618
- make, 860
- 配套的 C 工具集, 621-622
- NC, 621-622
- 分页器, 160-164
- patchdiag, 627
- PC PKZIP, 616
- trn, 631
- unzip, 615, 618
- 读取/写入 ZIP 文件, 616
- uucp 程序, 传输文件, 554-555
- 状态, 556-557
- undecode 命令, 221-223
- uuget 程序, 545-547
- uustat 程序, 检查 uucp 文件传输状态, 556-557
- uux 程序, 在远程主机上运行命令, 556
- V




- `values function` (Perl), 742
- `/var` 目录, 41
- `variables`
- `awk scripts`, 682-683
- `predefined`, 684-687
- `strings`, 687-688
- `Bourne shell scripts`
- `检查内容`, 652-654
- `检查指定的命令行参数数量`, 658
- `检查上一个命令的状态`, 658-659
- `创建/使用`, 639-641
- `列出参数`, 660
- `遍历命令行参数`, 662-663
- `获取用户输入`, 645-646
- `使用反引号设置`, 641-642
- `使用不冲突的临时文件`, 659-660
- `CDPATH`, 54-56
- `PATH`, 97-98
- `添加当前目录`, 99-100
- `命令全名`, 100-101
- `Perl`, 721-722
- `值的递增与减少` (`++` 和 `--`), 745
- `打印值`, 750-751
- `special`, 725-728
- `shell`, 30
- `在正则表达式中`, 392. 另另 `environment variables`
- `vendors`
- `UNIX 技术支持`, 624-626
- `补丁集群`, 627-628
- `安全公告`, 628
- `2000 年问题`, 628-629
- `UNIX 网站`, 623-624
- `竖线` (`|`) 管道, 31
- `vi 命令`, 498
- `vi 命令行编辑器命令`, 502-506




![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) vi 编辑器, 450

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 取消更改并退出, 455

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 在行末附加文本, 458

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 错误警报, 453

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 更改行缩进, 484

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查其他 UNIX 命令, 491

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 检查拼写, 461

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 包含的单词, 465

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 创建临时文件, 451-452

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 光标移动, 452-453, 465-466

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 到文件开头/结尾, 460

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 光标移动, 466-468

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 删除

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 字符, 454

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 行, 454-455

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 显示输入模式, 487-488

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 编辑

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 查找与重复, 474-475

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 重复, 472-473

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 文件名和当前位置, 460

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 文件

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 统计章节中的行/单词, 495

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 多次编辑, 495

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 加密/解密, 493-494

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 插入标题, 494

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 排序, 492

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 段落格式化, 461-463

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 帮助功能, 456-457

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 插入模式, 454

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 插入其他 UNIX 输出, 491-492

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 合并行, 455

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 意外, 479-480

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 行

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 自动缩进, 488

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 自动换行, 488

![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) 显示数字, 489





- 将键映射到命令序列，475-476, 479
- 非单词，465
- 快速保存，458
- 只读模式，464
- 第 861 页
- 恢复
- 已删除的文本，469
- 丢失的更改，463-464
- 重绘屏幕，457
- 移动计数，454
- 替换
- 逐个字符，459
- 单词，459-460
- 恢复行，460
- 保存
- (:) 在 `.exrc` 文件中设置选项，490
- 更改并退出，455
- 更改到不同的文件，458
- 分隔单词，465
- 开始/结束，450-451
- 字符串
- 缩写，489
- 忽略大小写并替换，490
- 条件替换，482-484
- 全局替换，480-481
- 区域替换，481-482
- 文本
- 更改命令，469-470
- 文件间复制，485-487
- 同一文件内复制，485
- 删除命令，468
- 插入命令，464-465
- 文件间移动，485-487
- 同一文件内移动，485
- 替换命令，470
- 撤销更改，457-458
- 写入权限错误，459





# 命令与工具参考

- `vi` (文本编辑器) 命令，464
- 查看作业和优先级，317
- 虚拟机，77
- visual BASIC 编程语言，13
- 可视模式，`vi` 文本编辑器，476, 479

## W

- `w` 命令，66
- `(:)w` (`vi` 文本编辑器) 命令，458
- Web 浏览器 CDE 应用程序，133-134
- 网站
- emacs
- `Dotfile` 生成器，534
- `functions`，534
- `manuals`，534
- `references` 卡，533
- 自由软件基金会，GNU 软件，621
- FreeBSD，21
- GNU/Linux，21
- SCO UNIX 许可证，32
- Sun HotJava，612
- UNIX 软件，压缩文件，221
- UNIX 供应商，623-624
- `whence` 命令，101
- `which` 命令，101
- `while` 语句，`awk`，700
- 空格，86
- `who` 命令，64-66
- `whoami` 命令，60-61
- 通配符字符
- `awk` 脚本，676-677
- `filename`，150-154, 388
- `filenames`，232
- `arg list too long` 错误，244-245
- 等价正则表达式序列，250
- 使用 `*` (星号) 生成文件名，232-233
- 检查 man pages 用于，234-236





| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 忽略目录, 237 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 列出其他目录下的文件, 239 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 列出隐藏文件, 238 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 多个模式的单次列出, 237-238 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 减少长名称的输入, 236 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用 `?` (问号)生成文件名, 239-240 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 固定长度名称, 240-241 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用不允许的 `[! . . .]` (方括号)生成文件名, 243-244 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用 `[. .]` (方括号)生成文件名, 241-243 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | Perl, 427, 721 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | `?` (问号), 426-427 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 正则表达式, 158, 388 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 使用 `egrep` 命令可用, 402 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 在 Perl 中可用, 404-405 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 脱字符符号 (`^`), 389-390 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 脱字符与美元符号 (`^`), 391-392 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 替换字符串, 417-418, 429-431 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 美元符号 (`$`), 390-391 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 句号 (`.`), 395-396 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 替换字符串, 414-415 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 替换字符串并忽略大小写 (Perl), 429 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于字段替换字符串, 429-431 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 替换最长跨度字符串, 424-425 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 每行替换字符串, 416 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 选择性替换字符串, 417-418, 429 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 用字符替换字符串, 421-423 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 方括号 (`[]`), 396-398 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 关闭, 406 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 无限制, 402 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 窗口管理器, 121 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | Windows |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 基于 X Window |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 系统 (X Consortium).*参见* X 窗口 |
| ![fc4f3a8aef38b56941e55505c60e4caf.gif](img/fc4f3a8aef38b56941e55505c60e4caf.gif) | 电子邮件, 支持 uuencode/uudecode, 223 |





- 安装/配置, 590-592
- Motif
- 可用控制, 129-131
-在...之间移动文本, 131-132
- 网络连接
-通过 Internet 访问 UNIX 主机, 598-602
- 使用 Hyper Terminal 程序访问 UNIX 主机, 602, 604
-通过 Netscape Communicator 发送邮件, 608
- 使用 ftp 程序传输文件, 596
- 使用 kermit 程序传输文件， 604, 607
- 使用 telnet 程序登录 UNIX 主机, 597
- 使用 ping 程序进行测试, 593
- 使用 `winipcfg.exe` 程序查看配置, 594
- 相比于，UNIX, 22-24
- `winipcfg.exe` 程序, 594
- `vi` (`vi` 编辑器)。参见 `wrapmargin` (`vi` 编辑器) 命令
- 工作目录。参见当前目录
- 维维网 (World Wide Web)。参见 Internet
- `:wq` (`vi` 编辑器)命令, 455
- `wrapmargin` (`vi` 编辑器)命令, 488
- `write` 命令, 68
- `write` 权限, 181, 283-284
- 覆盖, 188
- `vi` 编辑器, 459
- 媒体写保护, 329
- 写入
- `awk` 脚本, 673-674
- `predefined variables`, 684-687
- `action variables`, 682-683
- `actions`, 675-676, 682
- `arithmetic operators`, 695-696
- `array functions`, 693-694
- `arrays`, 692-693
- `break statement`, 698-699
- `built-in functions, system`, 713-714





- `coding`, 681-682
- `comparison operators`, 678
- `complex reports`, 710-711
- `compound pattern operators`, 678-679
- `conditional operators`, 697-698
- `continue statement`, 698-699
- `data extraction for reports`, 711
- `do statement`, 698
- `find command`, 712-713
- `for statement`, 699-700
- `from line`, 674-675
- `getline statement`, 701-702
- `grep command`, 713
- `handling input`, 680-681
- `if statements`, 696-697
- `input`, 701
- `input from commands`, 702
- `input from commands, ending`, 702-703
- `input from files`, 702
- `input from files, ending`, 702-703
- `loops`, 698
- `multidimension arrays`, 694
- `null (:) statements`, 697
- `null`, 697
- `numeric functions`, 695
- `output`, 703
- `output to commands`, 706
- `output to files`, 706
- `output to files, ending`, 706-707
- `output to pipes, ending`, 706-707
- `patterns`, 675-676
- `printf statement`, 703-704, 706
- `range pattern operators`, 679-680
- `regular expression patters`, 676-677
- `special string constants`, 692
- `string functions`, 689-691





- 字符串操作符，688
- 字符串，687-688
- 用户定义函数定义，707-708
- 用户定义函数参数，708-709
- 用户定义函数返回值，709-710
- 用户定义函数，707
- while 语句，700
- Bourne shell 脚本，638-639
- CDPATH 变量，54
- 检查结果，654-656
- 变量内容，652-654
- 检查文件/目录属性，648-652
- 检查给定的命令行数量，658
- 检查上一个命令的状态，658-659
- 命令行参数，646-647
- 命令行替换，641-642
- 创建/使用变量，639-641
- 调试，663-665
- exit 命令，661
- if 语句，647-648
- 列出参数，660
- 循环遍历命令行参数，662-663
- 循环遍历项目列表，665
- 使用 expr 程序进行数学计算，656-657
- 处理所有文件，666
- 处理树中的所有目录文件，666-667
- 返回用法说明，661-662
- 从菜单选择，668-770
- 用户输入，645-646
- 用户输出，643, 645
- 使用不冲突的临时文件，659-660
- Korn shell 脚本，CDPATH 变量，54
- Perl 脚本，718-719
- 使用反引号（``)调用系统，744-745





- `chomp function`, 747
- `close command`, 739-740
- `closing files`, 739-740
- `code references`, 723-724
- `concatenating strings with dot (.)`, 746
- `control structures`, 729-730
- `debugging`, 748-754
- `each function`, 741
- `filehandles`, 724-725
- `for command`, 733-734
- `foreach command`, 734
- `functions`, 735-736
- `hash arrays`, 741
- `here-iss`, 725
- `if command`, 732
- `if-else statement`, 732-733
- `incrementing and decrementing (++ and --) of variables`, 745
- `input as parameters`, 728-729
- `input on line`, 729
- `join function`, 747
- `keys function`, 742
- `literals`, 721
- `localtime function`, 743-744
- `open command`, 740
- `opening files`, 740
- `pop function`, 736
- `push function`, 736
- `shift function`, 737-738
- `special variables`, 725-728
- `splice function`, 739
- `split function`, 746-747
- `system command`, 744-745
- `terminators`, 720
- `time function`, 742
- `truth`, 730-731
- `unshift function`, 737-738





- `values` 函数， 742
- `variables`, 721-722
- UNIX shell 脚本。参见 Shell (UNIX) 提示
- X-Z
- `x` (vi 编辑器) 命令， 454
- X 终端， 121
- X Window System (X Consortium), 120
- X Windows, 120
- X-Windows 终端， 62-63
- X/Open Company Ltd., 26
- X/Open 标准, 24
- X11 软件, 120
- `xargs` 命令，生成文件名， 247-249
- XENIX 操作系统
- Microsoft, 20
- Santa Cruz Operation (SCO), 19
- XINU 编程语言, 672
- XPG3 和 XPG4 UNIX 标准, 24
- Yahoo!, 614
- 2000 年问题，628-629
- `yppasswd` 命令， 277
