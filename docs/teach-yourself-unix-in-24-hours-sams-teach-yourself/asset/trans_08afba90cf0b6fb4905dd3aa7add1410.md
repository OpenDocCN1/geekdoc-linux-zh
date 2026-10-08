
./OWL/WordMap
./.elm
./Archives
./InfolderId
./InfolderId/PIMS
./Mail
./News
./bin
./src
./temp
%

# 表 19.2. 有用的 find -type 文件类型。

| 字母 | 含义 |
|---|---|
| d | 目录 |
| f | 文件 |
| l | 链接 |

为了查找这些目录中的每一个信息，可以使用 find 的 `-exec` 选项。遗憾的是，我不能直接输入命令：`-exec` 选项必须配合 `{}` 使用（`{} 会被匹配到的文件名替换），并在命令末尾使用 `\;`。（如果漏掉 `\`，shell 会把 `;` 解释为命令的结束）。你必须确保 `{}` 和 `\;` 之间有一个空格。

```
% find -type d -exec ls -ld {} {}
drwxr-xr 1024 Dec 10 14:13
drwxr-xr 532 Dec 6 18:31 /OWL
drwxr-xr 512 Dec 2 21:18 /Doc
drwxr-xr 512 Nov 7 11:52 /OWL/WordMap
drwxr-xr 512 Dec 10 13:30 /.elm
drwxr-xr 512 Dec 21 10:30 /Archives
drwxr-xr 512 Dec 3 02:03 /InfoWorld
drwxr-xr 512 Sep 30 10:38 /InfoWorld/PIMS
drwxr-xr 1024 Dec 9 11:42 /Mail
drwxr-xr 512 Oct 6 09:38 /News
drwxr-xr 512 Dec 10 13:58 /bin
drwxr-xr 512 Oct 13 10:45 /src
drwxr-xr 512 Nov 8 22:20 /temp
```

7. `find` 命令通常用于删除超过几天的核心文件（core files）。正如你记得的，这些核心文件是程序意外崩溃时运行程序内存镜像的副本。它们可能非常巨大，偶尔修剪一下是明智的：

```
% find -name core -ctime -4 -exec /bin/rm -f {} \;
```

这条命令没有输出，因为我没有在命令末尾使用 `-print`。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_409_0.png)

# 搜索信息和文件

`find` 命令是 UNIX 中强大的命令。它可以帮助你根据所有者、文件名和其他属性查找文件。该命令最笨拙的部分是 `-exec` 选项所需的元素元素，而这正是 `xargs` 命令非常有帮助的地方。

# 任务 19.2：结合 xargs 使用 find

你可以使用 `find` 搜索文件，使用 `grep` 在文件内部进行搜索，但如果你想组合使用呢？这就是 `xargs` 大显身手的地方。

- 几天前

输出很有趣，但它没有包含任何文件名！

2. 第二种更聪明的策略是使用 `-l` 标志，让 `grep` 只指定匹配到的文件名：

```
% find -type f -exec grep -l i mapping {} \; \
./OWL/WordMap/msw-to-txt.c
./elm/aliases.text
./Mail/mark
./News/usetnam.alt
./bin/my_new_cmd: Permission denied
./src/fixit.c
./temp/attach.msg
```

3. 这是朝着正确方向的一步，但这种方法的问题是，每匹配到一个文件就会调用一次 `grep`，这是一种非常消耗资源的策略。相反，你使用 `xargs` 读取 `find` 的输出并构建 `grep` 调用（记住，每看到一个文件，`grep` 程序都会检查它），一次性指定大量文件。这样一来，即使检查了 200 或 300 个文件，`grep` 也只会被调用四五次。默认情况下，`xargs` 总是跟踪文件名列表直到指定命令的末尾，因此使用它非常简单：

```
% find -type f -print | xargs grep -l i mapping
./OWL/WordMap/msw-to-txt.c
./elm/aliases.text
./Mail/mark
./News/usetnam.alt
./bin/my_new_cmd: Permission denied
./src/fixit.c
./temp/attach.msg
```

这得到了相同的输出，但速度快得多。

4. 这种方法的妙处在于，由于 `grep` 接收了多个文件，当 `grep` 显示匹配行时，它会自动包含包含任何匹配项的文件名。移除 `-l` 标志的结果正是我想要的：

```
% find -type f -print | xargs grep -i m mapping
./OWL/WordMap/msw-to-txt.c:typedef struct mappings {
./OWL/WordMap/msw-to-txt.c:int entry character-mapping[] = {
long-mappings = FALSE;
./OWL/WordMap/msw-to-txt.c:int c
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_411_0.png)
