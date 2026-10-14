
`puts "staticVar: \n[namespace eval uniqueNumber {set staticVar}]"`

```
# 下一行将将产生错误条件，因为
# staticVar 在全局作用域中不存在。
```

```cl
puts "staticVar: $staticVar"
```

# 输出

```
Visible namespaces from the global scope are:

:uniqueNumber
```

```
Before import, global scope has these "get*" commands:

gets
```

```
After import, global scope contains these "get*" commands:

gets getUnique
```

```
first Unique val: 1

second Unique val: 2

staticVar: 2

can't read "staticVar": no such variable
```

## 7.1 命名空间与作用域规则

在此示例中有几点需要注意：

- 过程 `getUnique` 可以在定义之前声明为导出名称。
- 定义 `uniqueNumber` 命名空间后，从全局作用域有两个两个命名空间——`::uniqueNumber` 命名空间和 `::tcl` 解释器。当 Tcl 解释器运行时，`::tcl` 命名空间始终存在。
- `namespace import ::uniqueNumber:*` 将 `::uniqueNumber` 中的所有导出实体导入到全局作用域。
- 可以通过 `namespace eval ::uniqueNumber::staticVar` 访问 `staticVar` 变量的值。
- 当命名空间创建时，通过 `variable staticVar 0` 行初始化 `staticVar` 变量。此代码等同于向 `namespace eval` 传递 `set staticVar 0` 参数，这将导致变量在 `uniqueNumber` 命名空间的顶部定义。

### 7.1.7 命名空间嵌套

如果两个命名空间中的过程需要第三个命名空间中的功能，有两种选择。它们可以在前两个命名空间的作用域创建第三个命名空间的共享副本，或者它们可以在各自的命名空间作用域内创建一个嵌套的第三个命名空间的副本。

嵌套第三个命名空间的优势是为其中定义的持久数据创建一个唯一的副本。如果命名空间是共享的，那么数据也是共享的。

下一个示例显示将 `uniqueNumber` 命名空间嵌套在两个独立的命名空间（`Package1` 和 `Package2`）中。这允许 `Package1` 和 `Package2` 中的每个过程获取唯一数字，且数字之间没有间隔。

如果 `uniqueNumber` 命名空间是在级别创建并被 `Package1` 和 `Package2` 共享，那么每当任何一个包调用 `getUnique` 时，唯一数字就会增加。

### 示例 7.1.7-1

```cl
# # 此过程在调用它的脚本的作用域内创建一个 uniqueNumber 命名空间。

proc createUnique() {
    uplevel 1 {
        namespace eval uniqueNumber
        variable staticVal 0
        namespace export getUnique;
        proc getUnique() {
            variable staticVal
            return [incr staticVal]
        }
    }
}
```

# 创建 Package1 命名空间，
# 在 Package1 命名空间内创建一个 uniqueNumber 命名空间
# Package1 命名空间包含一个用于报告唯一
# 数字的过程

```cl
namespace eval Package1 {
    createUnique
    namespace import uniqueNumber::*
    proc pack1demo() {
        return "pack1demoUnique.[getUnique]"
    }
}
```

# 创建 Package2 命名空间，
# 在 Package2 命名空间内创建一个 uniqueNumber 命名空间
# Package2 命名空间包含一个用于报告唯一
# 数字的过程

```cl
namespace eval Package2 {
    createUnique
    namespace import uniqueNumber::getUnique
    proc pack2demo() {
        return "pack2demoUnique.[getUnique]"
    }
}
```

## 7.1 命名空间与作用域规则

```cl
puts "Package1 example returns: [::Package1::pack1demo]"
puts "invoking Package1::getUnique directly returns: \n[Package1::getUnique]"
puts "Package1 example returns: [::Package1::pack1demo]"
puts ""
puts "Package2 example returns: [::Package2::pack2demo]"
puts "Package2 example returns: [::Package2::pack2demo]"
puts "Package2 example returns: [::Package2::pack2demo]"
```

# 输出

```
Package1 example returns: pack1demoUnique.1
invoking Package1::getUnique directly returns: 2
Package1 example returns: pack1demoUnique.3
Package2 example returns: pack2demoUnique.1
Package2 example returns: pack2demoUnique.2
Package2 example returns: pack2demoUnique.3
```
