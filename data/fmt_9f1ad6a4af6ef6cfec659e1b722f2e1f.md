
该列名对所有人（即所有者、组和世界）具有读取权限，且仅对所有者具有修改权限。`hobby` 列对所有人可读，但任何人不能修改。

在以下示例中，如果没有指定访问权限，表的访问权限将来自标准默认值或 `NIS_DEFAULTS` 变量。以下示例向此表添加条目。

```
castle nistblad -c hobby_tbl name=S,a+r,o+m hobby=S,a+r
hobbies.foo.com.
```

如果未指定访问权限，表的访问权限将来自标准默认值或 `NIS_DEFAULTS` 变量。以下示例向此表添加条目。

```
castle nistblad -c hobby_tbl name=S,a+r,o+m hobby=S,a+r
hobbies.foo.com.
```
