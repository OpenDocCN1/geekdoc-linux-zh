
**答案：** 这段代码实际上包含两个问题。第二个 if 语句永远不会执行，因为该条件要求 `$name` 不能是 Tom——然而，这个 `if` 语句嵌套在另一个仅在 `$name` 是 Tom 时才执行的 `if` 语句内部。第二个 `if` 语句缺少 `fi` 关键字。

4. 以下代码有什么问题？（你注意到这一组练习题的问题规律了吗？）

```
#!/bin/bash
clear
case $city in
	"q")
		echo "Search by name"
		;;
	"b")
		echo "Search by telephone number"
		;;
	"c")
		echo "Search by employee number"
		;;
	"q")
		declare flag="Q"
		;;
	*)
		echo "Incorrect menu selection."
		;
	esac
```

**答案：** 你没有给 `$city` 赋值。而且 `case` 语句需要 `esac` 关键字，但程序的最后一行缺少了这个关键字。

5. 以下代码有什么问题？

```
#!/bin/bash
clear
for friend in Bob Smith Mary Jones Joan Adams
do
	echo "Hi, $friend"
done
```

**答案：** 你需要用引号将 Bob Smith、Mary Jones 和 Joan Adams 这些名字括起来：

```
for friend in "Bob Smith" "Mary Jones" "Joan Adams"
```

## 附录 E
## 浏览示例代码

*如果你和我一样讨厌打字，那么你会很高兴知道，我将本书中较大的代码片段放到了网上供你下载，这样你就不用敲坏手指了。*

你可以从以下网址在网络上获取代码：

```
www.idgbooks.com/extras/dummies/11muxprog.html
```

只需点击页面上方便的**点击此处下载示例代码**按钮即可下载。下载的文件是一个 zip 文件，其中包含以各章节名称命名的文本文件。如果你在书中看到某段代码不想输入，请遵循以下步骤：

- 1. 导航到你将解压的文本文件放在目录（或任何位置）的计算机上。
- 2. 找到并打开与你在书中找到想要代码的章节号相对应的文本文件。
- 3. 找到你想要的代码，然后将代码从文本文件复制并粘贴到你想要使用该代码的编译器（或其他程序）中。

我并没有将这些文本文件中的书中每一个小代码片段都包含进去——只是较大的部分。因此，如果你在对应的文本文件中找不到你要找的代码（如果有的话——有些章节没有可发布的代码），那可能只是我认为你自己打字会更快的一两行。

![](img/05279073f26be7df99b3c487360dec6a_350_0.png)

如果你在示例代码方面遇到困难并需要协助，请致电 IDG Books Worldwide 客户服务电话：800-762-2974（或美国以外地区：317-572-3342）。

![](img/05279073f26be7df99b3c487360dec6a_350_1.png)

# 索引

### 数字与符号

- ! (非运算符), 79-80
- # (数字符号), 注释
- and, 191
- $ (美元符号), 161
- variables, 在其中, 61
- $* 变量, 166-167
- $# (除法余数运算符), 76, 78-79
- && (与运算符), 79-80
- ) (右括号), 100, 106
- * (星号保留字), 101-102
- * (乘法运算符), 76-78
- + (加法运算符), 76-77
- -eq (等于运算符), 81-82, 91
- values, 检查, 90
- -ge (大于或等于运算符), 81, 83-84, 91
- -gt (大于运算符), 81, 83, 91
- -le (小于或等于运算符), 81, 85, 91
- -lt (小于运算符), 81, 84, 91
- -ne (不等于运算符), 81-83, 91
- values, 检查, 90
- -o, 202
- / (除法运算符), 76, 78
- / (正斜杠), 282
- \ (反斜杠), 275
- || (或运算符), 79-81
- ~ (波浪号), 46, 287
- > (大于符号), 72
- > (重定向) 运算符, 172
- - (减法运算符), 76-77

- addition operator (+), 76-77
- addresses
  - destination (e-mail), 219
  - e-mail, 217
  - e-mail, copy addresses, 224-225
  - e-mail, multiple, 224
- administrator, 282
- American National Standards Institute. 参见 ANSI
- and operator (&&), 79-80
- anonymous FTP, 275
- ANSI (American National Standards Institute), 82
  - character codes, 82
- appending to files, 172
- applications, 275
- archive files, 270-271
- arguments, 275
  - $* variable, 166-167
  - accepting, 162-164
  - defined, 159
  - functions, passing to, 138-140
  - multiple, e-mail programs, 234-237
  - passing, 159-162
  - passing, command line and, 229
  - passing, troubleshooting, 165-166
  - passing e-mail addresses, 231-232
  - passing e-mail blind copies, 233
  - passing e-mail messages, 229-231
  - passing e-mail subject, 234
  - passing multiple, 164
  - passing to e-mail programs, 229-234
  - passing to programs, 230-231
  - reasons to use, 159-161
  - switches and, 240-243
  - verifying passing to function, 139-140
- arithmetical operators, 76-79
- ascending sort order, 250
- assembly language, 14-15
- assigning
  - strings to variables, 61-62
  - values to variables, 60-61
  - variables to variables, 62
- asterisk (*) multiplication operator, 76
- asterisk (*) reserved word, 101-102

### B

- background operation, 275
- background processing, 20
- backslash character, 263-264
- backslash (\), 275
- backups, 275
- bash shell, 34, 42, 45, 276
  - converting commands to C shell, 303-305
  - starting, 66
- binary code, 14
- binary numbers, 82
  - mathematical calculations, 82
- bit, 276
- blind copies, e-mail passing, 233
- Bourne Again shell, 42. 另见 bash shell
- Bourne shell, 42, 276
- break statement, while loops, 130-131
- BSD Unix, 276
- buffers, 252, 276
- bugs, 36, 197. 另见 debugging
  - comments and, 194-195
  - sources of, 198
- bytes, 276

### C

- C For Dummies, 43
- C programming language, 43
- C shell, 42, 276
  - converting bash shell commands, 303, 305
- C++ For Dummies, 43
- C++ programming languages, 43
- calling functions, 137-138
- calling subprograms, 154
- case sensitivity, user IDs, 215
- case statement, 100, 130
  - * (asterisk reserved word), 101-102
  - default actions, 101
  - if statement, replacing, 100
  - nesting, 106
  - user interface, 102-103
- c utility, 185
- central processing unit (CPU), 276
- CGI (Common Gateway Interface), 44
- character blocks, 13
- character codes (ANSI), 82
- character-based systems, 13
  - characters, displaying, 13
- chmod command, 267
  - subprograms and, 153
- chmod utility, 228
- executable files, creating, 17-18
- clearing screen, 66
- close parenthesis, 100, 106
- clusters, 260
- cmp utility, 252
- code, 14. 另见 pseudo code, 34
  - programming languages: scripting languages
    - defined, 33
    - development cycle
      - considerations, 14
      - reviewing, debugging, 202
      - translating from outline, 39-40
- college computer labs, 261
- college courses, 257-258
- column matching, *awk* utility, 179
- columns (databases), 175
- combining variables, 58
- command line
  - arguments, passing, 229
  - options, 280
  - passing arguments and, 161-162
- command mode, text editors, 277
- command mode, *vi*, 46, 287
  - command mode (*vi*), 288
- commands, 277
  - convd, 267
  - converting shell commands, 303-305
  - defined, 33
  - echo, 184, 202
  - exit(*vi*), 300-301
  - if *for* command, 141
  - external, 278
  - find, 268
  - function, calling, 137
  - functions and, 135
  - jobs, 264
  - *kill*, 264-265, 279
  - pipes, 281
  - *mkdir*, 269-270
  - *myprogram*, 205-206
  - *q*, 271
  - text searching (*vi*), 296
  - tr, 270
  - *vi*, 47
  - *vi*, editing in, 298-299
  - *vi*, saving files in, 300
  - *vi* input mode, 297
  - *vi* last line mode, 299, 301
  - *x*, 271
- comments, 191
  - # (number sign), 191
  - $ debugging, 194-195
  - hard return, 194
  - printing, 187
  - readability, 193-194
  - usefulness, 192-193
- companion Web site, sample code, 327
- comparing files, cmp utility, 252
- comparison operators, 81, 83-85
- compilers, 266
- computer clubs, 260
- computer labs, colleges, 261
- computer science. 参见 code; programming languages: scripting languages
- computers, programming languages, 14-15
- concatenation, 173
- conditions, 88-96, 111
  - endless loops, 129
  - expressions, 90-96
  - operators, 91
  - variables, 90
- conferences, 258
- *continue* statement, loops, 131-132
- copy addresses, e-mail, 224-225
- copying
  - files between Windows and Linux, 267-268
  - variables, 62
- counters, for in loops and, 121
- CPU (central processing unit), 276
- cursors, 13, 277
- cut utility, 256
- daemon programs, 264
- daemons, 20, 277
- data, 277
  - defined, 171
- data types, 62-63
- database management system, 174
- databases
  - columns, 175
  - creating, 174-176
  - detecting information, 180-181
  - extracting information to, 180
  - fields, deleting, 256
  - file comparison, 173-174
  - *gawk*, 177-181
  - printing, 185-187
  - rows, 175
  - saving to, 175
  - searches, 177-181
- debugging, 36, 197-198
  - comments and, 194-195
  - *flags*, 203-204
  - hidden values, displaying, 204-205
  - proofreading code, 199-201
  - reviewing code, 202
  - spell check and, 208
  - subprograms and, 198
  - techniques, 199-202
  - turning program parts on/off, 206-207
- declaring variables, 58
  - local, 57
- default actions, case statement, 101-102

