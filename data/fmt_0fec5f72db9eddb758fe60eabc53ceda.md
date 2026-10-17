
`fmt.Printf("Largest Group: %v\n", max)`

```
// 注意：这是洪泛填充问题的简化表示
// 实际算法遵循文本。
}
```

`func explore(tiles [][]int, x, y int, seen [][]bool) []pos`

```
// 文本描述的实现
return nil
}
```

*（等待，OCR文本非常乱。我将根据提供的逻辑提供一个正确的重构文本。）*

“后进先出”在运行时会被使用，它使用了 `add()` 函数，该函数接收包含所有瓦格的矩阵、起始位置以及已访问的记事本。在寻找 `explore()` 之前，它会执行“深度优先”搜索：首先向下钻取，以确保通过这种方式找到的邻居确实是邻居，这通过一个名为 `examine` 的待办列表直接查找相邻邻居。同样的逻辑，即确保它们不在边界之外，如果算法调用 `append()` 将 `examined` 范围之外的候选添加到在 `max` 或 `coord` 中定义的初始帧数组切片末尾，则该行为将适用。它随后会通过重新赋值切片减去新邻居后的切片来从切片头部移除处理项。在第 11 行中，将第一个元素 `examine[1:]` 重新赋值给 `examine` 变量。一个良好的候选方案可以对所有不同的实现策略进行权衡。图 3：算法已经找到了最大的。第 22 行调用的 `neighbors()` 函数定义在列表 3 中，它搜索所有相邻瓦格。它返回一个数组切片，其元素是彼此相邻的连续组，并在网格中高亮显示。

### 列表 2: explore.go

```go
package main

func explore(tiles [][]int, p pos, seen [][]bool) []pos {
results := []pos{}
examine := []pos{p}
color := tiles[p.x][p.y]

if max.x < 2 {
panic("Illegal array")
for len(examine) > 0 {
corpos := examine[0]
examine = examine[1:]
found := []pos{}
if seen[corpos.x][corpos.y] {
continue
}
add(&found, pos(cur.x - 1, cur.y), max)
add(&found, pos(cur.x + 1, cur.y), max)
add(&found, pos(cur.x, cur.y - 1), max)
add(&found, pos(cur.x, cur.y + 1), max)
if tiles[corpos.x][corpos.y] == color {
results = append(results, corpos)
}
seen[corpos.x][corpos.y] = true
examine = append(examine, neighbors(tiles, pos{corpos.x, corpos.y})...)
}
return results
}
```

### 列表 3: neighbors.go

```go
package main

func neighbors(tiles [][]int, cur pos) []pos {
var max pos
max.x = len(tiles) - 1
max.y = len(tiles[0]) - 1

found := []pos{}
add(&found, pos(cur.x - 1, cur.y), max)
add(&found, pos(cur.x + 1, cur.y), max)
add(&found, pos(cur.x, cur.y - 1), max)
add(&found, pos(cur.x, cur.y + 1), max)

return found
}

func add(found *[]pos, cand pos, max pos) {
if cand.x > 0 && cand.y > 0 && cand.x <= max.x && cand.y <= max.y {
*found = append(*found, cand)
}
}
```
