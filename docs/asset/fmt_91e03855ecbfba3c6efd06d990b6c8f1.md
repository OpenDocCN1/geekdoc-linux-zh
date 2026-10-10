
- 如果 `&&` 成功，`command` 会执行。
- 如果 `&&` 失败，`command` 会执行。

## 第 10.2: if 语句

```bash
if [[ $1 -eq 1 ]]; then
  echo "1 was passed in the first parameter"
elif [[ $1 -gt 2 ]]; then
  echo "2 was not passed in the first parameter"
else
  echo "The first parameter was not 1 and is not more than 2."
fi
```

### 第 10.4 节：使用 For 循环遍历数字

```bash
#!/bin/bash
for i in {1..10}; do # {1..10} 展开为 "1 2 3 4 5 6 7 8 9 10"
  echo $i
done
```

此输出如下：

```
1
2
3
4
5
6
7
8
9
10
```

### 第 10.5 节：continue 和 break

`continue` 示例

```bash
for i in [series]
do
  command 1
  command 2
  if (condition); # 跳过 command 3 的条件
    continue # 跳到 "series" 中的下一个值
  fi
  command 3
done
```

`break` 示例

```bash
for i in [series]
do
  command 4
  if (condition); # 跳出循环的条件
    then
      command 5 # 满足跳出循环的条件
      break
  fi
  command 6 # 如果 "condition" 永远为真则执行的条件
done
```

### 第 10.6 节：循环中断

跳出多层循环：

```bash
arr={a b c d e f}
for i in "${arr[@]}"; do
  echo "$i"

  for j in "${arr[@]}";do
    echo '$j'
    break 2
  done
done
```

输出：

```
a
a
```

跳出单层循环：

```bash
arr=(a b c d e f)
for i in "${arr[@]}";do
  echo "$i"
  for j in "${arr[@]}";do
    echo "$j"
    break
  done
done
```

输出：

```
a
a
b
a
c
d
a
e
a
f
```

### 第 10.7 节：While 循环

```bash
#!/bin/bash
i=0
while [ $i -lt 5 ]; # 当 i 小于 5 时
do
```
