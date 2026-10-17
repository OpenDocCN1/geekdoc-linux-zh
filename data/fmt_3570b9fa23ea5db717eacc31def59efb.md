
| Title | Id | Summary | Meta type | Base modification time | Data record id |

|---|---|---|---|---|---|

| | ThirdCatalog | ZCatalog | 2000/09/11 11:09:24 65 GMT+2 | | |

| Vocabulary | Vocabulary | | 2000/09/11 11:09:24 65 GMT+2 | | 1 |

| User Folder | acl_users | User Folder | | 2000/09/11 11:09:33 21 GMT+2 | | 2 |

| index_html | | | DTML Method | 2000/09/11 11:09:41 12 GMT+2 | | 3 |

图 11-13：以表格形式呈现的搜索结果

ThirdZCatalog, ZCatalog, 2000/09/11 11:09:24 65 GMT+2, 0

Vocabulary, Vocabulary., 2000/09/11 11:09:24 65 GMT+2, 1

User Folder, acl_users., User Folder, 2000/09/11 11:09:33 21 GMT+2, 2

index_html., DTML Method, 2000/09/11 11:09:41 12 GMT+2, 3

图 11-14：以记录形式呈现的搜索结果

如果搜索页和结果页适用于多个可搜索对象，相应的结果将彼此显示并用线条分隔，如图 11-15 所示。

| Title | Meta type | Id | Summary | Base modification time | Data record id |

|---|---|---|---|---|---|

| ZCatalog | ThirdZCatalog | 2000/09/11 11:24:65 GMT+2 | | 0 |

| Vocabulary | Vocabulary. | 2000/09/11 11:24:65 GMT+2 | | 1 |

| User | acl_users | 2000/09/11 10:33:21 GMT+2 | | 2 |

| DTML | index.html | 2000/09/11 09:41:12 GMT+2 | | 3 |

| ID | Name | Z search results |

|---|---|---|

| 1 | John | 5th Ave, ZCatalog |

| 2 | Jane | Conchor, 3rd Street |

| 3 | Bob | Richmond |

图 11-15：`ZCatalog` 和 `Z SQL` 方法的搜索结果

## 11.3.3 分页大小

标准生成的页面每个选定的 `ZCatalog` 或 `Z SQL` 方法显示 50 条结果。换句话说，标准分页大小为50。如果结果超过 50 条，会出现“下一页”(`Next`)和“上一页”(`Previous`)链接，允许你导航结果（如图 11-16 所示）。

| Title | Meta type | Id | Base modification time | Data record id |

|---|---|---|---|---|

| Installed product Standard&CacheManagers | Product Standard&CacheManagers | 2000/05/20 22:30:31 GMT+2 | -44784125 |

| Installed product Size:Access | Product Size:Access | 2000/05/20 22:30:31 GMT+2 | -44784128 |

![](img/43a28cce5475b2f487bf455365567fb6_235_0.png)

图 11-16：带有显示结果及“上一页/下一页”链接的页面

要更改显示的结果，只需将结果 DTML 方法中的 50 分页大小替换为你想要显示的数量（如果有多个结果对象，则在其他行中）：

```html
<dtml-in ZCatalog size=50 start=query_start>
```

如果你有多个可搜索对象，可能需要通过重命名每个 `query_start` 变量来更改分页逻辑（例如 `query_start1`、`query_start2` 等）。`query_start` 变量决定每个批显示的起始点。创建独立的变量可以防止在显示单个对象时显示 50 条结果。

记得更改源代码中所有相关位置的变量。除了 `in` 标签中的 `size` 外，其他位置还包括创建的“上一页”和“下一页”链接。

图 11-17 展示了具有不同搜索结果分页大小的修改报告页。

| Title | Meta type | Summary | Base modification time | Data record id |

|---|---|---|---|---|

| DateTime | Help: Topic DateTime.py | | 2001/05/28 23:44:24 GMT+2 | -447984247 |

| Cache manager associations | Help: Topic CacheManager-associate its | 2001/05/28 23:44:24 GMT+2 | -447984247 |

| (Next 2 results) | | | | |

| index_title | DTML Method | | 2001/06/22 22:39:14 GMT+1 | -187285419 |

| index_body | DTML Document | | 2001/05/27 13:20:23 GMT+2 | -187285418 |

| login_id | DTML Method | 2001/05/27 13:24:53 GMT+2 | -187285417 |

| search_body | DTML Method | 2001/05/22 23:44:51 GMT+2 | -187285416 |

| report_mail | DTML Method | 2001/05/20 06:07:53 GMT+2 | -187285415 |

| (Next 5 results) | | | | |

图 11-20：具有不同分页大小（2 和 5）的 `ZCatalog` 结果

## 11.4 ZCatalog 查询

虽然 `Z Interface` 有助于快速创建用于搜索 Zope 站点内容的简单用户界面，但对于特殊查询，它往往是不够的。为了增加灵活性，让我们来看看如何使用 `ZCatalog` 定制一个 `Z Interface` 以更好地满足你的需求。

### 列表 11-2：queryForm DTML 文档代码

```
<dtml-var standard_html_header>
<form action="queryReport">
<p>Title:<input type="text" name="title" size="40"></p>
<input type="submit">
</form>

<dtml-var standard_html_footer>
```

列表 11-3 显示了 `queryReport` 的代码，它根据 `queryForm` 中输入的标题项，列出找到的目录对象的标题。

### 列表 11-3：queryReport DTML 文档

```
<dtml-var standard_html_header>
<dtml-in name="Catalog">
<dtml-var name="title"><br>
</dtml-in>
<dtml-var standard_html_footer>
```

`queryReport` 中最重要的代码行是第二行的 `dtml-in` 语句。该语句通过名称调用 `Catalog`，并将从表单提交的任何值传递给它。如果用户在表单的标题字段中输入单词并提交，这些单词将用作针对 `Catalog` 中标题索引的搜索标准。

## 11.4.2 Catalog 大脑 (Brains)

当调用 `ZCatalog` 时（例如在我们简单的示例查询 `queryForm` 中），它并不会返回匹配查询标准的实际对象。相反，它会创建一个系列“大脑对象”(`brain objects`)，这些对象包含了匹配对象的缓存元数据值，以及可以用于各种用途的方法。非常重要的一点是，当你处理 Catalog 结果时，你处理的不是找到实际对象，而是它们的元数据。不过，如果你需要，你也可以显式地访问实际对象。
