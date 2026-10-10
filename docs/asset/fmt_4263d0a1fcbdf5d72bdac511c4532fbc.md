
```
db2 force application all
```
```
db2 "restore database musicdb from /home/instnn/backup"
```

## 使用 INSERT 选项加载数据到 CONCERTS

在本节中，你将使用 `INSERT` 加载 `CONCERTS` 表。
将数据加载到你的 `CONCERTS` 表。

1. 加载应指定以下内容：
- 在路径 `$HOME` 下进行操作
- 加载文件名为 `concerts.exp`
- 导入文件格式为 `ixf` 格式
- 以 `insert` 模式加载
- 将任何消息写入名为 `concerts.msg` 的文件

### Local

```
db2 connect to musicdb
```
```
db2 "? load" | more
```
```
db2 "load from $HOME/concerts.exp of ixf messages $HOME/concerts.msg insert into instnn.concerts"
```
