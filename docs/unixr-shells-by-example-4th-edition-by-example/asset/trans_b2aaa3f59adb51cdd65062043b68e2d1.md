

## nice——以低优先级运行命令

```
nice [ -increment ] command [ arguments ]
```

/usr/bin/nice 以较低的 CPU 调度优先级执行命令。调用进程（通常是用户的 shell）必须处于分时调度类中。该命令在分时类中执行。默认增量为 10。除非您是超级用户，否则增量值必须在 1 到 19 之间。这也是 csh 的内置命令。

## nohup——使命令免受挂断和退出的影响

```
/usr/bin/nohup command [ arguments ]
```

nohup 有三个不同的版本。nohup 内置于 C shell 中，当使用 Bourne shell 时，它也是一个可执行程序，位于 /usr/bin/nohup。Bourne shell 版本的 nohup 执行命令时，使其不受 HUP（挂断）和 TERM（终止）信号的影响。如果标准输出是终端，则将其重定向到文件 nohup.out。标准错误会被重定向以跟随标准输出。优先级会增加五。应从 shell 中配合 `&` 调用 nohup，以防止它响应中断或来自下一个用户的输入。

### 示例 A.39

```
nohup look up &
```

### 说明

look up 程序将在后台运行，并持续运行直到完成，即使用户注销也是如此。生成的任何输出都会写入当前目录中名为 nohup.out 的文件。

## od——八进制转储

```
od [ -bcCdDfFosSvXx ] [ filename ] [ [ + ] offset [ . ] [ b ] ]
```

od 以第一个参数选择的一种或多种格式显示文件。如果缺少第一个参数，则默认使用 -o（例如，文件可以按字节八进制、ASCII、十进制、十六进制等格式显示）。

## pack, pcat, unpack——压缩和展开文件

pcat 对打包文件所起的作用与 cat 对普通文件所起的作用相同，但 pcat 不能用作过滤器。指定的文件会被解包并写入标准输出。因此，要查看名为 name.z 的打包文件，请使用 `pcat name.z` 或直接使用 `pcat name`。unpack 用于展开由 pack 创建的文件。

## passwd——更改登录密码和密码属性

```
passwd [ name ]
passwd [ -d | -l ] [ -f ] [ -n min ] [ -w warn ] [ -x max ] name
passwd -s [ -a ]
passwd -S name
```

passwd 命令用于更改密码或列出与用户登录名关联的密码属性。此外，特权用户可以使用 passwd 来安装或更改与任何登录名关联的密码和属性。

## paste——合并多个文件的相同行或单个文件的后续行

```
paste filename1 filename2...
paste -d list filename1 filename2...
paste -s [ -d list ] filename1 filename2...
```

paste 将给定输入文件 filename1、filename2 等的对应行连接起来。它将每个文件视为表格的一列或多列，并将它们水平粘贴在一起（参见 cut）。

### 示例 A.40

- 1. ls | paste - - -
- 2. paste -s -d"\t\n" testfile1 testfile2
- 3. paste file1 file2

### 说明

- 1. 文件以三列形式列出，并用制表符粘合在一起。
- 2. 使用制表符和换行符作为分隔符将一对行合并为一行（即，第一对行用制表符粘合；下一对行用换行符粘合，再下一对用制表符，依此类推）。-s 选项使 testfile1 的后续行先被粘贴，然后是 testfile2 的后续行。
- 3. file1 中的一行与 file2 中的一行粘贴在一起，用制表符粘合，使文件行显示为两列。

## pcat——（参见 pack）

## pine——一个用于互联网新闻和电子邮件的程序

```
pine [ options ] [ address, address ]
pinef [ options ] [ address, address ]
```

pine 是一个面向屏幕的消息处理工具。在默认配置中，pine 有意提供一组有限的功能，面向新手用户，但它也有越来越多的选项以及“高级用户”和个人偏好功能。pinef 是 pine 的一个变体，使用功能键而不是助记单字母命令。pine 的基本功能集包括：查看、保存、导出、删除、打印、回复和转发消息。

## pg——逐页显示文件

```
pg [ -number ] [ -p string ] [ -c e f n r s ] [ +linenumber ]
[ +/pattern/ ] [ filename ... ]
```

pg 命令是一个过滤器，允许您在终端上一次一屏地浏览文件。如果未指定文件名，或者遇到文件名 `-`，pg 将从标准输入读取。每屏后都有一个提示符。如果用户按下回车键，则显示下一页。它允许您回退并查看已经过去的内容。（参见 more。）

## pr——打印文件

```
pr [[-columns] [-width] [-a] [-eck] [-ick] [-drtfp]
[+page] [-nck] [-offset] [-l length] [-sseparator]
[- header] [-f] [filename ...]
pr [[-m] [-width]] [-eck] [-ick] [-drtfp] [+page] [-nck]
[-offset] [-l length] [-sseparator] [-h header] [-f]
[filename1 filename2 ...]
```

pr 命令根据不同的格式选项格式化并打印文件内容。默认情况下，列表发送到标准输出，并分成页，每页带有页码、文件上次修改的日期和时间以及文件名。如果未指定选项，默认文件格式为 66 行，带有五行页眉和五行页脚。

### 示例 A.41

```
pr -2dh "TITLE" file1 file2
```

### 说明

以双列双面形式打印 file1 和 file2，并带有页眉“TITLE”。

## ping——报告远程系统是否可达并处于活动状态

```
ping [-dfgnqrVR] [-c count] [-i wait] [-l preload] [-p pattern]
[-s packetsize]
```

ping 向主机发送 ICMP ECHO_REQUEST 数据包，并等待响应，以告诉您主机或网关是否可达并处于活动状态。它用于排查网络连接问题。如果 ping 根本没有收到任何回复数据包，它将退出并返回代码

