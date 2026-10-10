
在更新 `make_dir` 函数（用于创建目录的规则）时增加对 `set_insert` 函数的调用，意味着变量 `MADE_DIRS` 将跟踪已创建的目录集合。

在 Makefile 中，可能会构建许多目录，使用集合是发现任何时候哪些目录已经构建的简便方法。

请注意，由于集合是实现为 GNU make 列表的，因此您无法插入包含空格的项。

## set_create

您通过 `set_create` 函数创建一个集合：

### set_create

- 参数: 1: 集合元素列表
返回: 新创建的集合

它接收一个元素列表并将它们添加到集合中。返回集合本身。注意，集合元素可能不包含空格。

## set_insert

一旦使用 `set_create` 创建了集合，您可以使用 `set_insert` 向其添加元素：

### set_insert

- 参数: 1: 要添加到集合的单个元素
2: 一个集合
返回: 添加了该元素后的集合

## set_remove

要从集合中删除一个元素，请调用 `set_remove`：

### set_remove

- 参数: 1: 要从集合中删除的单个元素
2: 一个集合

返回: 删除了元素后的集合

从集合中删除一个不存在的元素并不是错误。

## set_is_member

要测试一个元素是否为集合的成员，请调用 `set_is_member`。它返回一个布尔值，指示元素是否存在：

### set_is_member

- 参数: 1: 单个元素
2: 一个集合

返回: 如果元素在集合中，则返回 `$(true)`

## set_union

通过对两个集合调用 `set_union` 函数将其合并。返回合并后的集合：

### set_union

- 参数: 1: 一个集合
2: 另一个集合

返回: 两个集合的并集

## set_intersection

要确定两个集合的共同元素，使用 `set_intersection`。它返回作为参数的两个集合都存在的元素集合：

### set_intersection

- 参数: 1: 一个集合
2: 另一个集合

返回: 两个集合的交集

## set_is_subset

通过调用 `set_is_subset` 了解一个集合是否是另一个集合的子集是有用的：

### set_is_subset

- 参数: 1: 一个集合
2: 另一个集合
返回: 如果元素是子集，则返回 `$(true)`

## set_equal

要确定两个集合是否相等，请调用 `set_equal`：

### set_equal

- 参数: 1: 一个集合
2: 另一个集合
返回: 如果集合相等，则返回 `$(true)`

## 关联数组

关联数组有时被称为映射（maps）。栈是有序的字符串列表（不包含空格）。在 GMSL 中，栈在内部存储，并且拥有名称，就像关联数组一样。例如：

```
traverse-tree = $(foreach d,$(patsub %/.,%,$(wildcard $1/*)), \
$(call push,dirs,$d)$(call traverse-tree,$d)
```

```
$(dump-tree = $(if $(call sne,$(call depth,dirs),0),$call pop,dirs) \
$(call dump-tree))
```

```
$(info $(call dump-tree))
```

这个小型 Makefile 使用栈跟踪目录树。

### traverse-tree

`traverse-tree` 函数使用 `$(wildcard)` 函数查找参数（存储在 `$1` 中）的所有子目录，查找目录中始终存在的 `.` 文件。它使用 `$(patsub)` 函数去掉 `$(wildcard)` 返回的每个值末尾的 `/`，以获取完整的目录名称。

在遍历该目录之前，它将找到的目录推名为 `dirs` 的栈中。

### dump-tree

`dump-tree` 函数从 `dirs` 树中弹出项，直到没有为止（直到深度变为 0）。

列表 6-1 显示了一个目录结构。

```
$ ls -R sources

sources:

bar foo
```

```
sources/bar:

barsub
```

```
sources/bar/barsub:

sources/foo:
subdir subdir2

sources/foo/subdir:
subsubdir

sources/foo/subdir/subsubdir:
sources/foo/subdir2:
```

# 列表 6-1: 目录结构

> 如果此目录结构存在于 `sources` 下，makefile 将输出：

`sources/foo sources/foo/subdir2 sources/foo/subdir sources/foo/subdir/subsubdir sources/bar sources/bar/barsub`

如果希望以深度优先的方式遍历目录树，可以使用栈函数来定义 `dfs`，它会搜索目录树并构建一个包含按深度优先排列目录的 `dirs` 栈：

```
_dfs = $(if $(call sne,$call depth,work),0),$call push,dirs,$(call \
peek,work)$(foreach d,$(patsub %%,%,$(wildcard $(call \
pop,work)*/.*)),$(call push,work,d))$(call __dfs)
```

```
dfs = $(if $(call push,work,$i)$$(call _dfs)
```

```
$(call dfs,sources)
```

```
dump-tree = $(if $(call sne,$call depth,dirs),0),$call pop,dirs)$$(call \
ndump-tree)
```

```
$(info $(call dump-tree,sources))
```

目录树函数没有变化（它通过连续调用 `pop` 输出栈中的所有内容）。但 `dfs` 函数是新引入。它使用一个名为 `work` 的工作栈来跟踪待访问的目录。它首先将起始目录推入栈中，然后调用 `dfs` 辅助函数。

实际工作由 `_dfs` 完成。它将当前目录推入 `d` 栈，将该目录的所有子目录推入 `work` 栈，然后进行递归。当 `work` 栈为空时递归停止。

列表 6-1 中目录结构的输出现在：

`sources/bar/barsub sources/bar sources/foo/subdir/subsubdir sources/foo/subdir sources/foo/subdir2 sources/.`

任何使用过栈的人对元素的推入（push）和弹出（pop）都很熟悉。GMSL 的栈函数非常相似。要向栈顶添加元素，调用 `push`：

### push

- 参数：1: 栈名称
  2: 推入栈顶的值（不能包含空格）
返回：无

### pop

要检索栈顶元素，调用 `pop`：

### pop

- 参数：1: 栈名称
返回：从栈中移除后的栈顶元素

### peek

`peek` 函数的操作类似于 `pop`，但它不会移除栈顶元素；它返回该元素的值：

### peek

- 参数：1: 栈名称
返回：不被移除的栈顶元素

### depth

最后，你可以调用 `depth`：

### depth

- 参数：1: 栈名称
返回：栈中的项数量

`depth` 决定了栈中存在多少元素。

## 函数记忆化 (Memoization)

为了减少对慢函数（如 `$(shell)`）的调用次数，提供了一个单一的记忆化函数。例如，假设 Makefile 需要知道各种文件的 MD5 值，并定义了一个函数 `md5`。

```
md5 = $(shell md5sum $1)
```

这是一个调用开销非常大的函数（因为执行 `md5sum` 需要时间），因此最好每个文件只调用一次。记忆化版本的 `md5` 函数如下：

```
md5sum = $(call memoize,md5,$1)
```

它会为每个输入的文件名调用一次 `md5sum` 函数，并在内部记录返回的值，这样后续使用相同文件名调用 `md5sum` 时将直接返回 MD5 值而无需再次运行 `md5sum`。例如：

```
$(info $(call md5sum,/etc/passwd))

$(info $(call md5sum,/etc/passwd))
```
