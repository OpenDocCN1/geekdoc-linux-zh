
```c
case 2:
    glLookAt(0.0, 0.5, -3.3, 1.0, 0.0, 0.0, -0.7, 0.2, 0.4);
    break;
}
if (shade_flag == 0)
    glShadeModel(GL_SMOOTH);
else
    glShadeModel(GL_FLAT);

void key_press_callback(unsigned char key, int x, int y) {
    switch (key)
    {
        case 27: /* escape character */
        case 'q':
        case 'Q':
            exit(0);
        default:
            cycle_view();
            break;
    }
}
```

```c
int main(int argc, char *argv[]) {
    glInit(&argc, argv);
    glutDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
    glutWindowSize(500, 500);
    glutWindowPosition(100, 100);
    CreateWindow(argv[0]);
    init();
    glutGetKeyFunc(key_press_callback);
    glutDisplayFunc(display);
    glutReshapeFunc(reshape);
    glutMainLoop();
    return 0;
}
```

这个简单的示例程序演示了如何对几何对象制作动画。该程序可以作为编写简单3D游戏的基础，这些游戏仅使用`OpenGL`工具库中定义的“内置”3D形状（如球体、立方体、锥体等）。关于`OpenGL`的更多信息可以访问 `http://www.opengl.org/`。

`opengl.org`上的更多信息可以在：

`http://www.opengl.org/Documentation/Implementations/Mesa.html`

## 特殊编程技术

## 第五部分

## 本部分内容

- 使用 `GNU bash` 进行 `Shell` 编程 609
- 安全编程 639
- 调试：`GNU gdb` 687

# `Shell`

使用 `GNU bash` 进行编程

作者：Kurt Wall

## 本章内容

- 为什么选择 `bash`？ 610
- `bash` 基础 610
- 使用 `bash` 变量 613
- 使用 `bash` 运算符 615
- 流程控制 619
- `Shell` 函数 628
- 输入与输出 629
- 命令行处理 633
- 进程与作业控制 635

在1993年成为`Linux`用户后的头两天内，我写了我的第一个`bash`脚本，那是一个为了自动化备份而非常笨拙的尝试。这个逸事说明了`shell`脚本在`Linux`中是多么的普遍。在本章中，我将为你提供`bash shell`编程基础的坚实基础。

## 为什么选择 `bash`？

`GNU`的`bash`（`Bourne Again Shell`，名字是以双关语的方式向`Bourne`及其作者`Stephen Bourne`致敬并命名的）是`Linux`的默认`shell`。`bash`由`Brian Fox`编写并由`Chet Ramey`维护，它最受欢迎的功能是它的命令行编辑功能和作业控制能力。从程序员的角度来看，`bash`的主要优势是它的可定制性和它提供的完整编程环境，包括函数定义、整数数学以及一个出奇地完整的`I/O`接口。正如你对一个`Linux`工具所预期的那样，`bash`包含了所有流行的`shell`——`Bourne`, `Korn`和`C shell`的元素，以及它自己的一些创新。在本书时，`bash`的当前发布版本是`2.0.3`。然而，大多数`Linux`发行版使用的是经过测试的`1.14`版本。尽管如此，我将涵盖`bash`版本`2`，并在其出现时指出早期版本中不可用的功能，版本`2`比版本`1`更符合`POSIX`标准。

## `bash` 基础

在本章中，我假设你已经熟练使用`bash`，因此我的讨论侧重于从`shell`程序员的角度来看`bash`的功能。然而，通过回顾，我将刷新你对`bash`通配符及其特殊字符的记忆。

### 通配符

`bash`通配符运算符为`` `*` ``、`` `?` ``以及集合`` `[SET]` ``和`` `![SET]` ``。`` `*` ``匹配任何字符字符串，`` `?` ``匹配任何字符。假设你有一个包含以下文件的目录：

```
$ ls
zeistopnm zic2xpm zipgrep zipsplit znew
zcmp zforce zip zipinfo zless
zdiff grep zipcloak zpinote zmore
```

命令 `` `ls*` `` 匹配`zic2xpm`、`zip`、`zipcloak`、`zipgrep`、`zipinfo`和`zipsplit`，但 `` `ls ?` `` 仅匹配`zip`。

## 使用 `GNU bash` 进行 `Shell` 编程

第34章

集合运算符允许你使用字符范围或不相交字符集作为通配符。要指定一个包含边界的字符范围，请在字符之间使用连字符。例如，集合`` `[a-o]` ``包含所有从“a”到“o”的小写字母。使用逗号来表示不相交的集合，例如“a”到“h”之间以及“w”到“z”之间的字符范围。在`bash`的表示法中，为`` `[a-h-w-z]` ``。如果你只想用于几个单独字符（如英语元音），符号`` `[aeiou]` ``就足够了。集合前缀“~”意味着包含不在集合中的所有内容。因此，查找所有辅音的一种简单方法是写`` `[^aeiou]` ``。

### 特殊字符

特殊字符——对`bash`有特定含义。表34.1列出了所有它们。

| 字符 | 描述 |
| --- | --- |
| `<` | 重定向输入 |
| `>` | 重定向输出 |
| `(` | 开始子`shell` |
| `)` | 结束子`shell` |
| `|` | 管道 |
| `&` | 后台执行命令 |
| `{` | 开始块 |
| `}` | 结束块 |
| `~` | 家目录 |
| `;` | 命令分隔符 |
| `#` | 注释 |
| `'` | 强引用 |
| `$` | 变量表达式 |
| `*` | 字符串通配符 |
| `?` | 单字符 |

### 使用变量

正如你所预期的，`bash`有变量。通常它们是字符字符串，但`bash`也有处理数值（整数）值的特殊设施。要给变量赋值，使用以下语法：

```
varname=value
```

要获取变量的值，你可以使用以下两种格式之一：

```
$varname
${varname}
```

第二种格式，`$varname`是更通用也更难输入的。然而，你必须使用它来区分变量与末尾的字母、数字或下划线。例如，假设你有一个变量`MYNAME`并想显示它的值后面跟着下划线。你可能会尝试以下命令：

```
$ echo $MYNAME_
```

但这种尝试会失败，因为`bash`会尝试打印变量`MYNAME_`而不是`MYNAME`。在这种情况下，你必须使用第二种语法，如下所示：

```
$ echo ${MYNAME}_
```

列表34.1说明了这种微妙之处。
