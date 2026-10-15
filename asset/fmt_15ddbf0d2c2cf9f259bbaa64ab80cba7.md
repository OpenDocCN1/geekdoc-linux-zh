
# Example Script

```tcl
proc upper_level {} {

  set this_does_not_yet_exist

  proc twoargs {a b} {

    puts $a$b

  }

  expr 5+"a"

  expr (5+"a")

  proc foo {a} {

    upvar sa x

    set x 5

  }

  foo

  foo bar of this and that

  proc foo {a} {

    catch {unset x}

    list [twoargs 1 2 3 4]

  }

  catch {lappend}

}
```

## tcl lint Output

In proc `"foo"`:

file `"has_bugs_1.tcl"` line 33.

At or near: `"catch {unset x}"`

--- ERROR ---: unset or undeclared Variable `"x"`.

file `"has_bugs_1.tcl"` line 33.

At or near: `"unset x"`

--- ERROR ---: Illegal # args to proc `"twoargs"` = 4.

Usage : `"twoargs arg arg "`

file `"has_bugs_1.tcl"` line 34.

At or near: `[list [twoargs 1 2 3 4]]`

In proc `"upper_level"`:

--- ERROR --- unset or undeclared Variable

`"this_does_not_yet_exist"`--

WARNING ---: User should check to ensure
`"this_does_not_yet_exist"` exists at
this point.
file `"has_bugs_1.tcl"` line 16.
At or near: `"set this_does_not_yet_exist"`

--- ERROR ---: Illegal # args to proc `"lappend"` = 0.

Usage : `"lappend varName ?value ...?"`

编译完成！

## 14.2.3 tclparse

| 语言 | C++ |
| :--- | :--- |
| 主站 | http://www.informatik.uni-stuttgart.de/ipvr/swlab/sopra/tclsyntax/tclparse-HomeEngl.html |
| 联系方式 | 07031760536-002@t-online.de |
| 支持的 Tcl 版本 | Tcl: 7.3-8.1 Tk: 3.6-8.1 |
| 支持平台 | Unix |

`Tclparse` 检查大量的编程错误，包括参数数量错误、缺少引号和括号、变量名错误、命令名错误以及变量名前缺少美元符号。

`Tclparse` 以 C++ 源码的形式发行，并带有一个 `Makefile`。它可以使用 `gcc` 干净编译，但不能用 `VC++ 4.0` 编译。

## 14.2 代码检查器

`tclparse` 程序根据示例 14.2.2-1 中的脚本生成以下输出：

### 示例 14.2.3-1

```
1 proc upper_level () {
2   set_this_does_not_yet_exist
3   proc twoargs {a b} {
4
5   puts $a$b
6   }
7
8   expr 5+"a"
```

ERROR ( line 9 ) - wrong # args: should be 'proc name args body'

```
6
7   expr 5+"a"
8   expr (5+"a") {
9   proc foo {a} {
10    upvar $a x
11    set x 5
12  }
```

ERROR ( line 13 ) - unknown command 'foo'

```
10   upvar $a x
11   set x 5
12  }
13  foo
14  foo bar of this and that
15
16  proc foo {a} {
```

```
ERROR ( line 17 ) - unknown variable 'x'
```

```
14 foo bar of this and that
15
16 proc foo {a} {
17 catch {unset x}
18 list [twoargs 1 2 3 4]
19 }
20
```

```
ERROR ( line 18 ) - called '3'
```
15
16 proc foo {a} {
17 catch {unset x}
18 list [twoargs 1 2 3 4]
19 }
20
```

# 第 14 章 编程工具

## 14.3.2 图形调试器

Tcl 提供了多种面向 GUI 的调试器，范围从 Scriptics 提供的商业调试器到免费软件不等。

### 14.3.2.1 Tuba

- 语言：Tcl/C++
- 主页地址：http://www.doitnow.com/~iliad/Tcl/tuba/
- 联系人：iliad@doitnow.com
- 支持的 Tcl 版本：Tcl: 8.0-8.1 Tk: 8.0-8.1
- 支持的平台：Unix, Windows NT, Windows 95

该软件包使用多个窗口来显示正在调试的代码；允许用户显示和修改变量内容；进入或逐过程过程；以及按行、过程或在变量赋值时设置断点。该 GUI 非常友好，并包含了用于描述工具按钮的气泡浮窗。

`Tuba` 包含一个扩展的 `update` 命令和一些解析代码，使其能够控制正在调试的代码。这些函数分别用 C++ 和 Tcl 编写。Tcl 代码和 C++ 库具有相同的功能，但编译后的代码运行速度快。如果你无法编译 C++ 库，Tcl 库的运行也是可以接受的。

接下来的幅图像显示了主窗口和文件选择窗口。第二幅图像显示了源代码窗口，上方显示了一个变量监控窗口。

### 14.3.2.2 TdChoose/TdDebug

- 语言：Tcl
- 主页地址：http://www.neosoft.com
- 联系人：david.dougherty@amd.com

14.3 调试

![](img/fdcc2919568b5c9f5301d5a1e8d7_590_0.png) `Tuba v2.1`

![](img/fdcc2919568b5c9f5301d5a1e8d7_590_1.png) 在 `/usr/src/Tcl/dummy/test.tcl` 上命中断点

第 14 章 编程工具

支持的 Tcl 版本：Tcl: 7.3-8.0 Tk: 3.6-8.0

支持的平台：Unix

`TdDebug` 软件包（最初由 Gregor Schmid 开发）的独特之处在于，它可以附加到已经运行的 `wish` 程序中。当你有一个程序运行了几天，突然进入奇怪状态并需要检查时，这种方法非常有用。通过 `TdChoose`，你可以选择想要调试的 `wish` 解释器，然后选择你想要观察的过程。Tcl 命令会被添加到你的代码中，一旦进入所选过程，就会调用调试窗口。搜索字段使得在大型程序中选择过程变得轻而许多。

当调试器控制你的应用程序时，你可以逐过程执行、插入断点，或带有用户指定的延迟后继续执行。调试器会在每行代码被评估时更新变量窗口并显示结果。你也可以输入一行 Tcl 代码在程序的当前作用域内进行求值。这行代码可以修改变量、改变程序流等。

`TdDebug` 支持详尽的配置文件，允许你定义颜色并为调试窗口信息的显示和细节设置各种实用的控制项。如果 `wish` 解释器包含 `Tix` 或 `BL` 扩展，则可以使用额外功能。

以下图像显示了一个用于计算一组数字列表平均值的 GUI 的调试会话部分。

示例 14.3.2-1 脚本

```tcl
proc addList {lst} {
    set total 0
    foreach num $lst {
        set total [expr $total + $num]
    }
    return total
}
```

```tcl
proc mean {lst} {
  set sum [addList $lst]
  set count [length $lst]
  set mean [expr $sum / $count]
  return $mean
}
```
