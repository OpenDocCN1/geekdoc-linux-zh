

## 5.5 Tree 包实现

### 示例

```cl
TreeGetNameParts tree1.2 treeName nodeID
puts "Tree Name is: $treeName. Node ID is: $nodeID"
```

# 输出
Tree Name is: tree1. Node ID is: 2

### 5.5.2 创建新树

此包中创建新树的命令是 `treeCreate`。它会增加 `Tree_InternalArray(base)` 中的计数器，创建新的树名，并将 `Tree_InternalArray(treeName.base)` 计数器设置为 0（这是节点 ID 数字的起始值）。操作完成后，会创建一个新节点作为该树的顶级节点，并返回新节点的句柄。

### 示例 5.5.2-1

```cl
TreeGetNameParts
proc treeCreate {} {
    global Tree_InternalArray

    # 为此树创建唯一名称。

    set primaryName "tree$Tree_InternalArray(base)"
    incr Tree_InternalArray(base)

    # 不能有两个同名的树。
    # 这种情况永远不应该发生，但以防万一...

    if {[array name Tree_InternalArray $primaryName.base] != ""} {
        error "$primaryName already exists"
    }

    # 设置此树中节点的初始唯一 ID。
    #
    set Tree_InternalArray($primaryName.base) 0
    #
    # 创建根节点
    set rootNode [TreeCreateNode $primaryName.base]

    #
    # 看起来不错，发布吧！
    #
    return $rootNode
}
```

```cl
set tree [treeCreate ]
puts "The root node for this tree is: $tree"
```

# 输出
The root node for this tree is: tree0.1

### 5.5.3 创建新子节点

创建新节点的过程是 `treeCreateChild`。该过程创建一个节点，将它的句柄添加到父节点的子节点列表中，并将父节点的句柄放入新节点的父节点索引中。`treeCreateNode` 过程调用了两个内部过程：一个用于创建节点（TreeCreateNode），另一个用于将节点与父节点链接（TreeAddChild）。

`TreeCreateNode` 创建一个孤立节点，没有父节点也没有子节点。

**语法：** `TreeCreateNode treeID`

**TreeCreateNode**
创建一个新节点。确认树存在，并增加唯一 ID。

**treeName**
树的名称，可以是 `trename.base` 或节点名称。

**语法：** `TreeAddChild parent child`

**TreeAddChild**
确认子节点存在。将子节点的句柄添加到父节点的子节点列表中，并设置子节点的父节点索引。

## 5.5 Tree 包实现

**parent**: 接收此子节点的父节点。

**child**: 要添加到父节点中的新子节点。

以下示例展示了用于创建新子节点的三个过程：一个公共入口和两个内部过程。在本示例中，通过调用内部过程来展示创建子节点的步骤。

由于程序员与 Tree 包之间的所有交互都是通过 Tree 包返回的句柄完成的，应用程序程序员永远不需要知道 Tree 包的内部命名规范。在本示例中，显示了数组索引以展示该包的工作原理。

### 示例 5.5.3-1

```cl
############################################################
# proc treeCreateChild (parent)
# 为给定的父节点创建子节点
#
# 参数:
#    parent: 包含此新节点的父节点
# 结果:
#    创建一个新节点。
#    将子节点添加到父节点。
#    返回新节点的句柄
#
proc treeCreateChild (parent) {
    global Tree_InternalArray

    TreeGetNameParts $parent primary idNum

    set child [TreeCreateNode $primary.base]

    TreeAddChild $parent $child
    return $child
}
```

```cl
################################################************
# proc treeCreateNode (rootname) --
# 在此树中创建一个新节点（未挂载的）
# 参数:
#   rootname: 树中节点的名称
#
# 结果:
# 创建一个新节点。
# 返回一个用于标识此节点的句柄。
#
proc TreeCreateNode(rootname) {
    global Tree_InternalArray

    TreeGetNameParts $rootname primary idNum

    set val [incr Tree_InternalArray($primary.base)]
    set childname "$primary,$val"
    Tree_InternalArray($childname) OK
    return $childname
}

#################################################
# proc TreeAddChild(parent child) --
# 将节点添加到父节点的子节点列表中，并设置
# 子节点的父指针以反映父节点。
#
# 参数:
#   parent: 父节点
#   child: 正在添加到父节点中的新子节点。
#
# 结果:
#   添加子节点并更新列表与指针
#   无有效返回值。
#
proc TreeAddChild(parent child) {
    global Tree_InternalArray

    if {[array name Tree_InternalArray $parent] == ""} {
        error "TreeAddChild: Parent $parent does not exist"
    }

    if {[array name Tree_InternalArray $child] == ""} {
        error "TreeAddChild: Child $child does not exist"
    }
}
```

