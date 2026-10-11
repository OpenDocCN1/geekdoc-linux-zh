
```
$ find /usr/share/doc -type f -exec grep -i -H -1 '3d modeling' "{}" \; | cut -c -100
/usr/share/doc/openscad/README.md:-application Blender), OpenSCAD focuses on the CAD aspects
rather t
/usr/share/doc/openscad/README.md:artistic aspects of 3D modeling. Thus this might be the applicatio
/usr/share/doc/openscad/README.md:-looking for when you are planning to create 3D models of
machine p
/usr/share/doc/openscad/doc/publications.html-3D graphics library for Constructive Solid
Geometry (CS
/usr/share/doc/openscad/doc/publications.html-This major approach of 3D modeling has not been
support
/usr/share/doc/openscad/doc/publications.html-by real-time computer graphics until recently.
```

选项 `-1` 指示 `grep` 在找到匹配行时，包含前一和后一各一行。这些额外的行被称为*上下文行*，在输出中通过文件名后的减号进行标识。使用 `-C 1` 或 `--context=1` 也可以获得相同的结果，并且可以指定其他数量的上下文行。

`grep` 有两个互补程序：`egrep` 和 `fgrep`。`egrep` 程序等同于命令 `grep -E`，除了基本正则表达式外，它还包含额外的功能。例如，使用 `egrep` 可以利用扩展正则表达式功能，如分支：

```
$ find /usr/share/doc -type f -exec egrep -i -H -1 '3d (modeling|printing)' '{ }' \; | cut -c -100
/usr/share/doc/openscad/README.md-application Blender), OpenSCAD focuses on the CAD aspects
rather t
/usr/share/doc/openscad/README.md-artistic aspects of 3D modeling. Thus this might be the
applicatio
/usr/share/doc/openscad/README.md-looking for when you are planning to create 3D models of
machine p
/usr/share/doc/openscad/RELEASE_NOTES.md-* Support for using 3D-Mouse / Joystick / Gamepad
input dev
/usr/share/doc/openscad/RELEASE_NOTES.md:* 3D Printing support: Purchase from a print
service partne
/usr/share/doc/openscad/RELEASE_NOTES.md-* New export file formats: SVG, 3MF, AMF
/usr/share/doc/openscad/doc/publications.html-3D graphics library for Constructive Solid
Geometry (CS
/usr/share/doc/openscad/doc/publications.html-This major approach of 3D modeling has not been
support
/usr/share/doc/openscad/doc/publications.html-by real-time computer graphics until recently.
```

在此示例中，“3D modeling”或“3D printing”都会匹配该表达式，且不区分大小写。要仅显示文本流中与 `egrep` 使用的表达式匹配的部分，请使用 `-o` 选项。

`fgrep` 程序等同于 `grep -F`，即它不解析正则表达式。它在目标为匹配字面表达式的简单搜索中非常有用。因此，像美元符号和点号这样的特殊字符将被按字面意思处理，而不是按其在正则表达式中的含义处理。

### 流编辑器：sed

`sed` 程序的目的是以非交互方式修改基于文本的数据。这意味着所有的编辑都是通过预定义的指令完成的，而不是直接在屏幕上显示的文本上随意输入。用现代术语来说，`sed` 可以被理解为一种模板解析器：给定文本作为输入，它会在预定义的位置放置自定义内容，或者在找到正则表达式的匹配项时进行替换。

正如名称所暗示的那样，`sed` 非常适合通过管道流传输的文本。其基本语法是 `sed -f SCRIPT`（当编辑指令存储*在文件 SCRIPT* 中时）或 `sed -e COMMANDS`（直接从命令行执行*命令*）。如果既没有 `-f` 也没有 `-e`，*sed* 会使用第一个非选项参数作为脚本文件。也可以通过将路径作为参数传递给 *sed* 来使用文件作为输入。

`sed` 指令由单个字符组成，前面可能带有地址，后面可能带有一个或多个选项，并逐行应用于每一行。地址可以是单个行号、正则表达式或行范围。例如，可以使用 `1d` 删除文本流的第一行，其中 `1` 指定应用 `delete` 命令 `d` 的行。为了澄清 *sed* 的用法，查看命令 `factor $(seq 12)` 的输出，它返回 1 到 12 的数字的质因数：

```
$ factor $(seq 12)
1:
2: 2
3: 3
4: 2 2
5: 5
6: 2 3
7: 7
8: 2 2 2
9: 3 3
10: 2 5
11: 11
12: 2 2 3
```

使用 `1d` 删除第一行：

```
$ factor $(seq 12) | sed 1d
2: 2
3: 3
4: 2 2
5: 5
6: 2 3
7: 7
8: 2 2 2
9: 3 3
10: 2 5
11: 11
12: 2 2 3
```

可以使用逗号分隔符指定行范围：

```
$ factor $(seq 12) | sed 1,7d
8: 2 2 2
9: 3 3
10: 2 5
11: 11
12: 2 2 3
```

可以在同一次执行中使用多个指令，以分号分隔。在这种情况下，重要的是用括号将它们括起来，以便分号不被 shell 解释：

```
$ factor $(seq 12) | sed "1,7d;11d"
8: 2 2 2
9: 3 3
10: 2 5
12: 2 2 3
```

在此示例中，执行了两个删除指令，首先针对第 1 到 7 行，然后针对第 11 行。地址也可以是正则表达式，因此只有包含匹配项的行才会受指令影响：

```
$ factor $(seq 12) | sed "1d;/:.*2.*/d"
3: 3
5: 5
7: 7
9: 3 3
11: 11
```

正则表达式 `:.*2.*` 匹配冒号后任意位置出现的数字 2，导致删除那些以 2 为因数的数字对应的行。在 `sed` 中，斜杠（`//`）之间的任何内容都被视为正则表达式，默认支持所有基本正则表达式（RE）。例如，`sed -e "/^#/d" /etc/services` 会显示文件 `/etc/services` 的内容，但不包括以 `#` 开头的行（即注释行）。

删除指令 `d` 只是 `sed` 提供的众多编辑指令之一。除了删除某一行，sed 还可以用指定的文本替换该行：

```bash
$ factor $(seq 12) | sed "1d;/:.*2.*/c REMOVED"
REMOVED
3: 3
REMOVED
5: 5
REMOVED
7: 7
REMOVED
9: 3 3
REMOVED
11: 11
REMOVED
```

指令 `c REMOVED` 简单地用文本 REMOVED 替换该行。在示例的情况下，所有包含匹配正则表达式 `:.*2.*` 子串的行之内容都会受到指令 `c REMOVED` 的影响。指令 `a TEXT` 将 TEXT 指示的文本复制到匹配行之后的一个新行中。指令 `r FILE` 执行相同的操作，但复制的是由 FILE 指示的文件内容。指令 `w` 执行与 `r` 相反的操作，即将该行追加到指定的文件中。
