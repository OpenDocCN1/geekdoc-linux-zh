
## `ps`

`ps` 显示正在运行的进程。我通常这样运行 `ps`：

`wchan` 代表 wide（宽通道）。`ps auxwww` 会显示每个进程的所有命令行参数。

你可以用 `ps` 选择要显示的列（`ps -eo ...`）。

其中一个很酷的列是 `wchan`，如果进程处于睡眠状态，它会告诉你内核函数的名称。试一试：

```
$ ps aux
a+ttx
u means include together（包含用户）
username 列显示所有进程
ps -ef 也可以）
```

`e` 代表 environment（环境）。`ps auxe` 会显示环境变量：

```
$ ps -eo user,pid,wchan,cmd
```

## ★ 进程状态 ★

`f` 代表 "forest"（树森林）ツ。`ps auxf` 会向你展示一个 ASCII 艺术风格的进程树：

`ps` 有 3 组不同的命令行参数 💔

以下是 `s STATE` 状态列中字母的含义：

1. UNIX (一个横杠)
2. BSD (无横杠)
3. GNU (两个横杠)

- `R`: 运行 (running)
- `S/D`: 睡眠 (asleep)
- `Z`: 僵尸 (zombie)
- `I`: 多线程 (multithreaded)
- `t+`: 前台 (in the foreground)

你可以写类似这样的参数：

```
$ ps f -f
```

全格式 (UNIX)

`pstree` 也可以显示进程树。

### `top`

系统资源占用最高用户的实时更新摘要。

> 谁在用所有内存
> `chrome` 显而易见

让我们解释一下 `top` 中的一些数字！

### 负载平均值 (load average)

3 个数字大致反映了系统在过去 1、5 和 15 分钟内对 CPU 的需求。

如果它高于你拥有的 CPU 数量，那通常是不好的。

### 内存 (memory)

4 个数字：

- `total`（总计）
- `free`（空闲）
- `used`（已用）
- `cached`（缓存）

一个可能意料之外的是：`total` 并不等于 `free + used`！

`total = free + used + cached` （文件系统缓存）

### % CPU

![](img/5f5d02ddabdd2009c88fde2963d57414_14_0.png)

这一列是以单核百分比形式给出的。如果你有 4 个核心，这个值可以达到 400 %！

### RES

这一列是“驻留集合大小”（resident set size），即你的进程正在使用的 RAM 数量。

`SHR` 是 `RES` 中与其他进程共享的部分。

### `htop`

比 `top` 更漂亮且更具交互性的版本 ★

```
1 [## ] 10% 
2 [#### ] 20% 
3 [### ] 5% 
4 [##### ] used cached 5% 
mem [####################] 4176
swp [##] 2/256
```

### `sort` & `uniq`

`sort` 对其输入进行排序。

```
$ sort names.txt
```

默认排序是字母顺序。

`sort -n` 数字排序：

| `'sort'` 顺序 | `'sort -n'` 顺序 |
| :--- | :--- |
| 12 | 12 |
| 15000 | 48 |
| 48 | 96 |
| 6020 | 6020 |
| 96 | 15000 |

`sort -h`: 人类可读排序：

| `'sort -n'` 顺序 | `'sort -h'` 顺序 |
| :--- | :--- |
| 15 | 6 |
| 30 M | 30 M |
| 45 K | 15 G |
| 200 G | 200 G |

实用的示例：

```
du -sh * | sort -h
```

`uniq` 去除重复。

注意 `a b` 仍然有 2 个 `b` => 2 个 `'a'`！

`uniq` 只合并相邻的匹配行。

`sort` + `uniq` 等于：

将某些内容通过到 `'sort | uniq'`，你将得到一个去重后的列表！

`sort -u` 执行的是相同的操作。

例如：
`a`
`b`
`b`

通过 `sort -u` 或 `sort | uniq` 后：
`a`
`b`

`uniq -c` 统计它看到的每行的次数。

配方：获取文件中出现次数最多的前 10 行：

```
$ cat foo.txt | uniq -c | sort -n | tail -n 10
```

![](img/5f5d02ddabdd2009c88fde2963d57414_15_0.png)

## 杂命令 ❤

| 命令 | 描述 |
| :--- | :--- |
| `rlwrap` | 为尚不支持这些功能的 REPL 添加历史记录和 ctrl 支持（`rlwrap` 代表 `readline`）。<br>`$ rlwrap python` |
| `watch` | 每隔 2 秒重新运行一次命令。 |
| `pv` | "管道查看器"，为你提供通过管道的数据统计信息。 |
| `file` | 弄清楚一个文件是哪种类型的文件（png? pdf?）。 |
| `cal` | 一个微型日历 ♡ |
| `ts` | 在每一行输入前添加时间戳。 |
| `ncdu` | 弄清楚哪些文件占用了你所有的磁盘空间。 |
| `diff` | 比较 2 个文件。运行时使用 `'-U 8'` 查看上下文。 |
