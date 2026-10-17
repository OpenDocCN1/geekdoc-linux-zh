
表 11-1 列出了从 `ZCatalog` 返回的大脑对象（即结果项）可用的方法。这些方法中的每一个都可以直接在遍历 `ZCatalog` 结果的 `dtml loop` 循环内部使用（如上面的 `queryForm` 中），因为 `dtml-in` 在遍历结果序列时，会将每个结果项置于命名空间的顶部。

表 11-1 中列出的最有用方法是 `getURL` 和 `getObject`。前者可以用于在结果页面中为每个对象轻松创建链接；后者用于访问除 `ZCatalog` 中缓存的元数据外可能需要的任何额外对象属性——例如属性和方法。

在许多结果对象上调用 `getObject` 可能会减慢你的 `ZCatalog` 搜索。在使用 `dtml-in` 时，请谨慎使用并保持较小的批大小。

# 表 11-1：`ZCatalog` 大脑方法

| `ZCatalog` 大脑方法 | 说明 |
| --- | --- |
| `has_key(key)` | 如果结果项具有名为 "key" 的元数据元素，则返回 true。 |
| `getPath()` | 返回结果项在你的 Zope 层级结构中的物理路径。 |
| `getURL()` | 如果你使用虚拟主机，返回结果项的绝对 URL（可能与 `getPath()` 不同）。 |
| `getObject()` | 返回与 `ZCatalog` 结果对应的实际 Zope 对象。 |
| `getRID()` | 返回结果项的 `ZCatalog` 内部记录 ID，这与 `ZCatalog` 返回的 `data_record_id_variable` 相同。这可以轻松地唯一标识结果。 |

让我们使用上述的 `getURL` 方法增强我们的 `queryReport` 页面（列表 11-4），这将允许我们为查询返回的每个对象构建链接。

# 列表 11-4：增强的 `queryReport` DTML 文档

```
<dtml-var standard_html_header>
<dtml-in name="Catalog">
  <a href="<dtml-var name="getURL">
    <dtml-var name="title">
  </a><br>
</dtml-in>
<dtml-var standard_html_footer>
```

通过向 `queryReport` 代码中添加锚点标签并使用 `ZCatalog` 大脑的 `getURL` 方法将对象的 URL 插入 `href` 属性，每个搜索结果现在都链接到查询找到的对象。

## 11.4.3 直接查询 `ZCatalogs`

要查询 `ZCatalog`，我们使用表达式调用 `ZCatalog` 并显式地将查询标准作为参数。参数名称与你想要查询的索引匹配，值包含每个命名索引的查询标准。你可以根据需要为少数或多个索引提供标准。（你也可以使用其他参数来控制 `ZCatalog` 返回的结果项的排序顺序。）

让我们在包含表 11-2 所示索引（这些是 Zope 创建的默认索引）的 `ZCatalog` 上创建一些示例查询。

# 表 11-2：`ZCatalog` 索引

| `ZCatalog` 索引 | 索引类型 |
| --- | --- |
| `PrincipiaSearchSource` | `TextIndex` |
| `bobobase_modification_time` | `FieldIndex` |
| `id` | `FieldIndex` |
| `meta_type` | `FieldIndex` |
| `title` | `TextIndex` |

### 11.4.3.1 字段索引查询

字段索引可以用于查找匹配特定值的对象。要匹配索引，我们只需要传递索引名称，以及我们期望的值。例如，要查找 `meta_type` 为 "Document" 的 `id` 索引对象，你可以使用以下表达式：

```
Catalog(meta_type="Document")
```

当你匹配多个索引时，需要以列表的形式传递期望值。例如，要查找 `id` 为 "html" 且 `meta_type` 为 "Document" 的对象，使用以下表达式：

```
Catalog(id="html", meta_type="Document")
```

当你使用上述表达式时，`meta_type` 为 "Document" 的将作为搜索结果。

> 注意：关键字的工作方式相同，只是搜索值需要匹配一个项（如属性值）。

### 11.4.3.2 字段索引的范围查询

对字段索引进行范围查询比匹配精确值要复杂一些。要匹配范围，我们必须指定索引的名称，以及范围值。用于范围匹配的用法值在表 11-3 所示。

# 表 11-3：范围匹配的用法值

| 范围用法值 | 说明 |
| --- | --- |
| `range:min` | 匹配大于等于范围值的索引。 |
| `range:max` | 匹配小于等于范围值的索引。 |
| `range:min:max` | 匹配指定最小值和最大值之间的索引值。 |

例如，让我们考虑如何通过日期使用 `bobabase_modification_time` 索引查询 `ZCatalog`。对于第一个示例，让我们找到过去 30 天内修改过的对象。这可以用于我们的商店应用程序查找最近添加或修改的实例。

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:min'
```

在第一个参数中（匹配索引名称），我们传递了当前 Zope 日期时间减 30，这计算出了搜索值之前的 30 天的日期。第二个用法指示 `ZCatalog` 返回大于或等于搜索值的对象。

通过简单更改用法值，我们可以找到所有 30 天未被修改过的对象，如下：

```
expr="Catalog(bobabase_modification_time=ZopeTime())-30,
bobabase_modification_time_usage='range:max'
```

要匹配落在两个值（最小值和最大值）之间的值，你必须传递包含至少两个项的列表作为搜索值。列表中值最小的项被视为最小搜索值，值最大的项被视为最大搜索值。例如，要找到昨天修改的所有目录对象，我们可以使用以下表达式：

（`ZopeTime()-1`）返回 24 小时的日期时间作为日期对象。为了确定前天的开始和结束时间以作我们的最小值和最大值，我们分别使用 `DateTime` 对象的 `earliest()` 和 `latestTime()` 方法。这些以双项列表的形式传递作为搜索值。然后我们使用 `range:min:max` 用法值指示 `ZCatalog` 执行边界查询。

### 11.4.3.3 使用字段索引排序结果

字段索引对于高效排序结果对象也非常有用。虽然 `dtoml-in` 标签允许你使用 `sort` 属性对序列进行排序，但这种排序是在 RAM 中进行的，这意味着无论 `ZCatalog` 的结果是否显示在当前批次，都需要将其加载到内存中。通常，只有显示的结果会被实际加载到内存中。

要使用字段索引进行高效排序，请向 `ZCatalog` 传递一个 `sort_on` 参数，其值为要排序的字段索引名称。你还可以指定一个可选的 `sort_order` 参数来确定排序是升序还是降序。这种排序在执行查询时发生，避免了 `dtoml-in` `sort` 属性带来的内存和性能损失。

让我们扩展之前的那个返回过去 30 天内修改过的对象的示例。要按修改日期返回结果并将最近修改的排在最前面，请使用此表达式：

```
expr="Catalog(bobobase_modification_time=ZopeTime()),
bobobase_modification_time_usage='range:min',
sort_on='bobobase_modification_time',
sort_order='descending"
```

> 因为 `sort_on` 可以与字段索引配合使用，你仍然需要通过其他属性值（如对象的标题）使用 `dtoml-in sort` 。要使用 `sort` 选项进行排序，所需的属性必须是 `ZCatalog` 的元数据元素。

### 11.4.3.4 文本索引查询

文本索引查询参数的编码方式与精确字段索引查询类似，不同之处在于值代表查询字符串而不是匹配的精确值。查询字符串允许对大量索引文本进行简单的布尔搜索和部分单词匹配功能（详情请见第 11.2.5 节）。

我们的示例 `ZCatalog` 有两个文本索引：`title` 和 `PrincipiaSearchSource`。前者是对象的 `title` 属性，后者是文档的正文。要找到包含“event”和“calendar”单词的分类对象，可以使用以下表达式：

```
expr="Catalog(title='event and calendar')"
```

> 你可以通过结合第 11.4.3 节中描述的其他技术，在单个表达式中同时搜索字段、文本和关键词索引。
