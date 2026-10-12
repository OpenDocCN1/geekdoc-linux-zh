
- 优惠有效期至 1 月 31 日
- `Imagine Publishing` 保留权利

## 三种简单的订阅方式

1. 线上
   - `0844 249 0282`
2. 电话
   - `4`
3. 邮寄或电子邮件

请填写表格并寄回：

- `Linux User & Developer`
- 订阅部门
- `800 Gull Avenue`
- `Kent Science Park`
- `Sittingbourne`
- `ME9 6BU`

或发送邮件至 `support@linuxuser.co.uk`

# 编写实用的 shell 脚本 – 部分 3

函数、重构以及 Bash 语法的一些奇特分支

教程

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_0.png)

> 让我们让备份脚本成为某种我们需要向其他程序员隐藏的内容

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_1.png)

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_2.png)

```bash
BACKUPFILE="$HOME/backup.tar.bz2"
DESDIR="/home/richard/backup"
if [ -d "$DESDIR" ]; then
  echo "already exists"
  exit 1
fi
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_3.png)

## 01. 独特

这比旧的反引号引用方法更有一致性——它在本地与 `( )` 使用 shell 保持一致。反引号并没有死，但在你的偏好中你可能永远不需要使用它们。

## 04 持续测试

在你制作时，规则依然适用——通过你认为的代码来测试它仍然如你认为的那样通过。`echo` 每一条语句，这样在更改后遇到问题的概率就会更小。

## 07 为了蓬勃发展

通过组合，我们在文件名上可能会遇到潜在问题，所以使用通配符（globbing）来获取文件名——然后你就可以安全地使用它们。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_4.png)

## 02. 埋怪 GUI

有些人习惯于用 GUI 编写文件名，而可怜的协调者将尝试解析空格——以避免文件名。我们通过这种方法绕过它。

```bash
# $(HOME)/Documents Files
dir_backup.sh [ -f $1 ] backup.sh
# $@ Shell 在文件名中解释
## 为文件名之间的空格
IFS='\n'
for i in $@; do
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_5.png)

## 08 见鬼吧

我们使用 `--` 表示当前目录——这样以破折号开头的文件名就不会被传递给它的命令所解释。

## 09 双横杠

对于 `cp`，我们可以放置两个破折号 `--` 来停止解释任何后续的破折号。使用相对 `/` 或绝对路径对于 `cp` 和以破折号开头的文件名也是安全的。

## 03 间距

直接在循环中使用输出可能足够了；所以我们稍后会返回这一点（步骤 7）——但我们的首要任务是从反引号中提取它，让 shell 将文件名解释为文件名之间的空格。

## 06 重新解释的变量

未引号的变量用于文件名扩展（通配符）。一旦你所有的文件和目录名称都无法被分割，你就没有问题。但对于现实世界的名称，你的变量是——一项繁琐的任务。

## 10 冗余

我们应该留意可能不必要的增加错误的冗余代码。我们的脚本在最后删除了 `_bak` 文件，所以为什么要在这里费心去匹配它们呢？

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_6.png)

## 05 Echo

`echo` 还给了你一个机会传递不同的参数来检查代码在不同情况下的行为。当 `Bash` 到达脚本的某些部分时，以及处于正确的文件夹时，使用 `echo`。

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_34_7.png)

`www.linuxuser.co.uk`

## 教程

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_0.png)

# `bak-test.sh` | `vi` | 编辑

## 一个函数

两个

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_1.png)

## 验证

但由于编程逻辑可以切换以处理包含特定后缀的目录（作为命令行的第二个参数传递），为了备份特定文件类型...

```bash
## test-suffix.sh
echo "you don't have $1 in this directory"; exit 1
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_2.png)

## `backupaac()`

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_3.png)

## `backupodt()`

```bash
for f in ./*.odt; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_4.png)

## `backuppng()`

```bash
for f in ./*.png; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

![](img/bab7f65683e8ebca10d1e8aa808ba7ff_35_5.png)

## 重新解释变量

```bash
for f in ./*.png; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

## 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

## 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

## 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

## 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

## 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

# 重新解释变量 备份

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```

```bash
for f in ./*.aac; do
  cp "$f"
  cp "$f" "$f.bak"
done
```
