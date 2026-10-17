
从图 7–16 的输出可以看出，从德国到达奥斯汀有三条不同的路径。让我们创建一个 SQL 语句，告诉我们每种情况的完整路径。

# 递归 SQL

```
WITH detail_path (origin,destination,route,distance,stops)
AS(
  SELECT f.origin, f.destination, f.destination, f.distance,0
  FROM flights f
  WHERE origin='Germany'
  UNION ALL
  SELECT p.origin, f.destination, p.route||->'||f.destination,
         p.distance+f.distance, p.stops+1
  FROM flights f, detail_path p
  WHERE p.destination=f.origin)
SELECT * FROM detail_path WHERE stops < 5
```

**图 7–17** 递归 SQL：从德国到奥斯汀的路径

图 7–15 所示的 SQL 语句如果在 `flights` 表中存在循环，可能会无限运行。当你编写此类 SQL 语句时，必须意识到无限循环的可能性。为了避免无限循环，你可以使用 `stops` 对查询进行限制。

假设你只对中转次数少于 5 次的路线感兴趣。你需要在最后一条 SQL 语句中添加以下限制：

获取从德国到奥斯汀的可能航班列表。

```
WHERE stops < 5
```

此条件可以用于避免相同思路下出现无限循环。

现在，让我们基于相同的思路创建一个更复杂的示例。我们想要获取一个从德国到奥斯汀的所有可能航班列表。这次，我们想要获取航班路线、距离和中转次数。

从图 7–16 的输出可以看出，从德国到达奥斯汀有三条不同的路径。让我们创建一个 SQL 语句，告诉我们每种情况的完整路径。

**图 7–17** 递归 SQL：从德国到奥斯汀的路径

```
WITH detail_path (origin,destination,route,distance,stops)
AS(
  SELECT f.origin, f.destination, f.destination, f.distance, 0
  FROM flights f
  WHERE origin='Germany'
  UNION ALL
  SELECT p.origin, f.destination, p.route||->'||f.destination,
         p.distance+f.distance, p.stops+1
  FROM flights f, detail_path p
  WHERE p.destination=f.origin)
SELECT * FROM detail_path WHERE stops < 5
```

图 7–15 所示的 SQL 语句如果在 `flights` 表中存在循环，可能会无限运行。当你编写此类 SQL 语句时，必须意识到无限循环的可能性。为了避免无限循环，你可以使用 `stops` 对查询进行限制。

获取从德国到奥斯汀的路径。
