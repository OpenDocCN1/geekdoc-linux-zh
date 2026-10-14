
`castle% fnlookup -L user/jsmith/service`

## 退出状态

- 0 操作成功。
- 1 操作失败。

### 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| 可性 | SUNwfns |

## 参见

`fnbind(1)`, `fnlist(1)`, `fnunbind(1)`, `fncreate(1M)`, `fdestroy(1M)`, `attributes(5)`, `fns(5)`, `fns_references(5)`

# `fnrename` — 重命名 FNS 的绑定

### 概览

```
/usr/bin/fnrename [-s] [-v] composite-name
```

# 描述

`fnrename` 重命名 `composite-name` 的联邦命名服务（FNS）绑定。

### 选项

- `-s` 设置搜索范围。范围可以是：
  * `object` 仅搜索 `composite-name`。
  * `context` 搜索直接绑定到 `composite-name` 的对象。
  * `subtree` 搜索绑定到 `composite-name` 或其任何子上下文的对象。
  * `constrained_subtree` Like `subtree`，但将搜索限制为由上下文定义的子上下文。

  你可以将范围缩写为任何唯一的的前缀，例如 `o` 或 `cont`。
  如果不指定 `-s` 选项，默认行为是 `-s context`。

- `-v` 显示正在重命名的绑定。

### 示例

以下示例显示了名称 `/usr/jsmith/service/calendar` 绑定的引用。
```
castle% fnrename user/jsmith/service/calendar
```

### 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
| 可性 | SUNwfs |

## 参见

`fnbind(1)`, `fnlookup(1)`, `fnunbind(1)`, `fncreate(1M)`, `fdestroy(1M)`, `attributes(5)`, `fns(5)`

# `fnlist`

### 操作数

`composite-name` 一个联邦命名服务命名对象。复合名称类似于 UNIX 文件名，依赖于所创建的子上下文。

带有有效 `composite-name` 操作数的命令示例为：

```
castle% fnlist thisorgunit

castle% fnlist thisorgunit/service

castle% fnlist thisorgunit/service/printer
```

### 示例

在以下示例中，不带操作数的命令提供了初始上下文的引用和地址类型列表。
```
castle% fnlist -1

name: _myorgunit

Reference type: onc_fn_nsid

Address type: onc_fn_files

context type: namespace id

name:...

Reference type: fn_global

Address type: initial

name: _orgunit

Reference type: onc_fn_organization

Address type: onc_fn_files

context type: organization

name: _x500

Reference type: fn_global

Address type: x500

Warning: empty X.500 reference

length: 0

data:

name: _thisens

Reference type: onc_fn_enterprise

Address type: onc_fn_files

context type: enterprise root
```
... `castle$`

在以下示例中，你指定了用户上下文（即 `composite-name = user/`），FNS 必须先使用 `fncreate(1M)` 进行部署，并使用 NIS、NIS+ 或 `files` 等一种命名服务。如果未部署 FNS，则没有用户上下文，且命令将以“Name not found”错误消息失败。

以下命令显示了绑定在 `user/` 上下中的名称。
```
castle$ fnlist user/
```

以下命令显示了绑定在 `user/` 上下文中名称和引用。
```
castle$ fnlist -l user/
```

## 退出状态

- 0 操作成功。
- 1 操作失败。

### 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
| 可性 | SUNwfns |

## 参见

`fnbind(1)`, `lookup(1)`, `fnunbind(1)`, `fncreate(1M)`, `fdestroy(1M)`, `attributes(5)`, `fns(5)`, `fns_references(5)`

# `fnsearch` — 使用指定属性搜索 FNS 对象

### 概览

```
/usr/bin/fnsearch [-Allv] [-n max] [-s scope] composite-name [-a ident]... [-O | -U] filter-expr [filter-arg]...
```

### 描述

`fnsearch` 命令显示绑定在 `composite-name` 或其下方满足过滤器表达式的联邦命名服务（FNS）对象的名称以及可选的属性和引用。

### 选项

- `-ident` 显示满足过滤器表达式的对象的给定属性使用。如果不使用 `-option`，则显示所有属性。空 `ident` 表示有需要显示的属性。`ident` 的语法详见第 392 页的“显示选定属性”。
- `-A` 咨询权威源获取信息。
- `-L` 显示满足过滤器表达式的对象的引用。在搜索期间遵循 X/Open 命名 (XFN) 链接。
- `-n max` 将显示的对象数量限制为给定的数字（正整数）。默认没有限制。
- `-s scope` 设置搜索范围。范围可以是：
  * `object` 仅搜索 `composite-name`。
  * `context` 搜索直接绑定到 `composite-name` 的对象。
  * `subtree` 搜索绑定到 `composite-name` 或其任何子上下文的对象。
  * `constrained_subtree` `subtree`，但将搜索限制为由上下文定义的子上下文。

  你可以将范围缩写为任何唯一的的前缀，例如 `o` 或 `cont`。
  如果不指定 `-s` 范围选项，默认行为是 `-s context`。

- `-v` 详细显示满足过滤器表达式的对象的引用。此选项优于 `-l`。

### 操作数

- `composite-name` 一个 FNS 命名对象。

### 用法

简单过滤器表达式
最简单的过滤器表达式形式是测试属性是否存在。
你只需通过提供属性名称来形成这种表达式。例如，以下命令搜索具有名为 `for_sale` 属性的对象。
```
% fsearch composite-name for_sale
```

# `fnsearch` 391

另一种简单的过滤表达式是测试特定属性的值。
以下命令查找年龄小于 17 的对象。
```
$ fnsearch composite-name "age < 17"
```

字符串值通过用单引号括起来来表示。例如，
以下命令查找所有红色对象。
```
$ fnsearch composite-name "color == 'red'"
```

注意，此示例中的双引号（`""`）并不是过滤表达式的一部分。
相反，它们防止 shell 解释表达式中的的空格和单引号。

# 逻辑运算符

你可以通过逻辑运算符 `and`、`or`、`and` 和 `not` 来组合成简单的过滤表达式，如下例所示。
```
$ fnsearch composite-name "age >= 35 and user_citizen"
```

你可以使用括号来分组表达式，如下例所示。
```
$ fnsearch composite-name "not (make == 'olds' and year == 1973)"
```

运算符的优先级如下，按优先级从低到高排序：

- `or`.
- `and`.
- `not`.
- 关系运算符。

逻辑运算符 `and`、`or` 和 `or` 是左结合的。

# 关系运算符

你可以使用以下关系运算符将属性与提供的值进行比较：

```
== 如果该属性的至少有一个值等于提供的值，则为真。

!= 如果该属性没有任何值等于提供的值，则为真。

< 如果该属性的至少有一个值小于提供的值，则为真。

<= 如果该属性的至少有一个值小于或等于提供的值，则为真。

> 如果该属性的至少有一个值大于提供的值，则为真。

>= 如果该属性的至少有一个值大于或等于提供的值，则为真。
```
