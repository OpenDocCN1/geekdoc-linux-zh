

# 第 11 章 Tk 巨组件 (Megawidgets)

语法：scrolledListBoxName delete first ?last?

scrolledListBoxName delete

从列表框中删除一个或多个项。

first 要删除的第一个项的索引。listbox 项从 0 开始编号。

?last? 要删除范围内的最后一个项的索引。如果不存在此参数，则仅删除由 first 指定的项。

selection 子命令返回 listbox 中被选中条目的内容。注意，listbox 的 cursor 子命令返回的是被选中项索引的索引列表，而此 selection 命令返回的是内容的列表。

语法：scrolledListBoxName selection

scrolledListBoxName selection

返回 listbox 中选中的项或多个项的文本。

subwidget 子命令返回 scrolledListBox 子组件的完整路径名。

语法：scrolledListBoxName subwidget

scrolledListBoxName subwidget

返回此 scrolledListBox 子组件的完整名称。

subwidget 要返回的子组件名称。可以是以下内容之一：

- listbox 列表框组件的完整名称。
- scrollbar 滚动条组件的完整名称。

## 11.4.2 使用 scrolledListBox

以下是如何使用 scrolledListBox 的简单示例。该组件的创建命令与标准的 Tk 组件相似。

## 11.4 滚动列表框巨组件

### 示例 11.4.2-1

#### 示例脚本

```tk
# 设置 auto_path 并声明我们需要使用
# scrolledListBox 软件包。
# 组件的 pkgIndex.tcl 文件位于当前目录

lappend auto_path .
package require widgets 1.0

# 创建 scrolledListBox，高三行，背景为白色
# 注意，同时为 listbox 和滚动条设置了背景颜色
set sll1 [scrolledListBox -height 3 -background white ]

# 向 listbox 插入这些项。
foreach musketeer [list Athos Porthos Aramis d'Artagnan] {
    $sll1 insert end $musketeer
}

# 创建一个按钮来显示结果。
button .report -text "Which Musketeer is selected" \
-command (puts "{$sll1 selection} is selected")

# 显示组件
pack $sll1 -side top
pack .report -side top
```

#### 脚本输出

Aramis is selected      # 点击按钮时打印

#### 脚本结果

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_434_0.png)

# 第 11 章 Tk 巨组件 (Megawidgets)

## 11.4.3 实现滚动ListBox

scrolledListBox 组件使用了第 7 章中描述 Tree 对象时相同的代码模式。在通用命名空间中将有一个通用过程库，在私有命名空间中有一用于 scrolledListBox 的支持过程，并在全局作用域中有一个创建组件的过程。

实现 scrolledListBox 巨组件的代码由一个状态变量和三个过程组成。

状态变量 `scInfo` 存在于 scrolledLB 信息中，这些信息在程序包的脚本评估之间需要维护。对于 scrolledListBox 软件包，这些信息包含在创建命令行中未提供名称时，用于为 scrolledListBox 组件创建唯一名称的数字。

scrolledListBox 巨组件由两对过程组成。在每对中，一个过程存在于全局作用域并供脚本编写者使用。另一个过程存在于 scrolledLB 命名空间中，用于与巨组件的组件交互。这与第 7 章描述的创建树对象并实现其方法的模式相同。

这些过程对中的第一对创建一个 scrolledListBox 巨组件。

脚本编写者将调用 `scrolledListBox` 来创建一个带滚动条的列表框。`scrolledListBox`过程调用 `MakeScrolledListBox` 来创建组件并返回它创建的巨组件的名称，该名称也将是与此新巨组件交互的过程名称。

| 全局作用域 | scrolledLB 命名空间 |
| :--- | :--- |
| listBox | MakeScrolledListBox |
| 创建一个新的 scrolledListBox | 创建一个具有巨组件名称 (scrolledListBox-Name) 的帧 (frame)。 |
| | 调用 MakeScrolledListBox 构建帧和子组件。 |
| | 在帧中填充相应的子组件。 |
| | 创建一个新的过程 scrolledlistListBoxName，用于与巨组件交互。 |

在 `MakeScrolledListBox` 创建了用于存放子组件的帧后，它会在全局作用域中创建一个与该帧同名的过程。这个新过程是第二对过程的全局部分。脚本编写者在需要与巨组件交互时将使用此过程。此过程将调用 scrolledLB 命名空间中的 `ScrolledListProc` 来实际实现组件命令。

| 全局作用域 | scrolledLB 命名空间 |
| :--- | :--- |
| scrolledListListBoxName 接受 scrolledListBox 组件子命令。 | scrolledListBoxProc 执行由子命令请求的组件交互。 |

`MakeScrolledListBox`过程需要创建一个帧来包含构成此巨组件的子组件。该帧的名称应该与巨组件的名称相同。这允许我们作为父巨组件的子项访问子组件。

然而，存在名称冲突：如果你为巨组件和帧使用相同的名称，就会发生冲突。解决方案是重命名帧过程。

