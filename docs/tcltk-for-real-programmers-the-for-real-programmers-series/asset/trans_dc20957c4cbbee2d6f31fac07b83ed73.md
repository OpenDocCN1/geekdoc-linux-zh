

## 6.6 创建一个 Tcl 对象

```t
####################################################################
# proc addDirToTree
#   将目录添加到节点中。
#   为每个目录条目创建子节点，并设置每个子节点
#   的名称和类型。
# 参数:
#   parent 该目录的父节点。
#   directory 要添加到树中的目录。
# 结果:
#   树（Tree）的长度将根据目录中条目的数量增加。

proc addDirToTree {parent newDir} {
#
  # 如果这不是一个目录，它将没有下属。

if {[file type $newDir] != "directory"} {
    error "$newDir is not a directory. Can't add to tree."
}
#
  # 如果父目录还没有更新名称和
#   类型，现在进行更新。

if {[catch ($parent get name)]} {
    $parent set name $newDir
    $parent set type directory
}
#
  # 空或不可读的目录将使 glob 命令
#   返回失败。
#   如果目录可以读取，则名称列表将位于
#   fileList 中。

  set fail [catch (glob $newDir/**) fileList]
if {$fail} {
    return;
}
# 遍历 fileList 中的名称
#
foreach name $fileList {
    set node [$parent add]
    $node set name $name
    $node set type [file type $name]
}
```

## 第 6 章 过程技术

### 示例脚本

```tcl
# 创建一个树结构
#
set base [newTreeObject]
#
# 将初始目录及其目录条目添加到
# 树结构中
#
addDirToTree $base [file filename C:/]
#
# 如果任何子节点是目录，则将它们的条目作为子节点
# 添加树中。
#
foreach entry [$base childList] {
    if [[$entry get type] == "directory"] {
        addDirToTree $entry [$entry get name]
    }
}

# 以以下形式打印树：
# Dir1
# Dir1/Entry1
# Dir1/Entry2
# Dir2
# Dir2/Entry3
# Dir2/Entry4
```

```tcl
foreach entry [$base childList] {
    puts "[$entry get name]"
    if [[$entry get type] == "directory"] {
        foreach sub [$entry childList] {
            puts "[$sub get name]"
        }
    }
}
```

脚本输出

- C:/IO.DOS
- C:/MSDOS.DOS
- C:/COMMAND.DOS
- C:/COMMAND.COM
- C:/BOOTLOG.PRV
- C:/CONFIG.SYS
- C:/NETLOG.TXT
- C:/DRVSPACE.BIN
- C:/AUTOEXEC.BAT
- C:/CONFIG.WIN
- C:/Program Files
    - C:/Program Files/Common Files
    - C:/Program Files/PLUS!
    - C:/Program Files/The Microsoft Network
    - C:/Program Files/Microsoft Exchange
    - C:/Program Files/Accessories
    - C:/Program Files/Tcl
    - C:/Program Files/Seagate
    - C:/Program Files/WinZip
- C:/tcltutor
    - C:/tcltutor/nopty.tcl
    - C:/tcltutor/icon
    - C:/tcltutor/TclTutor.bat
- C:/WINDOWS
    - C:/WINDOWS/INF
    - C:/WINDOWS/COMMAND
    - C:/WINDOWS/SYSTEM

前面的示例与第 5 章中的示例非常相似，因为大部分代码都在处理文件系统，而不是树。然而，使用较短的子命令名称而不是长长的树过程，跟起来更容易理解。

这个树对象有两个问题：

- 1. 关联数组 `Tree_InternalArray` 位于全局作用域，任何代码都可以轻松访问它。
- 2. 想要使用 treeObject 的脚本需要知道 `treeObj.tcl` 存储的目录，且 `treeObj.tcl` 需要能够找到 `treeObj.tcl`。

第 7 章将讨论命名空间（namespace）和包（package）命令。示例展示了如何使用 `namespace` 命令在私有命名空间中隐藏 `Tree_InternalArray`，如何使用 `package` 命令创建一个包，而脚本无需知道其加载的文件的位置即可使用该包。

## 6.7 总结

- 通过将 `args` 参数放在参数列表的最后，可以将一个过程定义为接受任意数量的参数。
- 具有默认值的过程参数通过将该参数声明为列表来定义。列表的第二个元素是默认值。
- 当评估 Tcl 过程时，它会为变量创建一个局部作用域。该局部作用域堆在调用该过程的代码的作用域之下。

