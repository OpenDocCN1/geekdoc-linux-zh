
## 使用 `dialog` 实用工具创建输入框 (`inputbox`)

```
$ cat > dia4
dialog --title "输入框 - 接收你的输入" --backtitle "Linux Script Tutorial" --inputbox "请输入你的名字" 8 60 2>/tmp/input.\$

ssel=$?

na=$(cat /tmp/input.\$.
case $sel in
0) echo "Hello $na" ;;
1) echo "点击了取消" ;;
255) echo "按了 [ESCAPE] 键" ;;
esac

rm -f /tmp/input.\$
```

如下所示运行：

```
$ chmod +x dia4

$ ./dia4
```

![](img/219cb7c6e1c9c4c56d73838282f4b69b_101_0.png)

`inputbox` 用于接收用户输入。在这个示例中，我们将用户的姓名作为输入。但我们将输入的名称存储在哪里呢？答案是通过 `dialog` 命令末尾的语句 `2>/tmp/input.$` 将输入重定向到文件，这意味着将屏幕输出发送到名为 `/tmp/input.$` 的文件中，随后可以通过以下方式检索输入的名称并存储到变量中：`na=cat /tmp/input.$`。`inputbox` 的退出状态参考下表：

| 输入退出状态 | 含义 |
|---|---|
| 0 | 命令执行成功 |
| 1 | 用户点击了取消按钮 |
| 255 | 用户点击了 `Escape` 键 |

### 使用 `dialog` 实用工具创建确认框 (`yesno`) 及用户界面整合演示

![](img/219cb7c6e1c9c4c56d73838282f4b69b_99_0.png)

### 使用 `dialog` 实用工具创建消息框 (`msgbox`)

### 使用 `dialog` 实用工具创建输入框 (`inputbox`)

```
$ cat > dia4
dialog --title "输入框 - 接收你的输入" --backtitle "Linux Script Tutorial" --inputbox "请输入你的名字" 8 60 2>/tmp/input.\$

ssel=$?

na=$(cat /tmp/input.\$.
case $sel in
0) echo "Hello $na" ;;
1) echo "点击了取消" ;;
255) echo "按了 [ESCAPE] 键" ;;
esac

rm -f /tmp/input.\$
```

如下所示运行：

```
$ chmod +x dia4

$ ./dia4
```

![](img/219cb7c6e1c9c4c56d73838282f4b69b_101_0.png)

`inputbox` 用于接收用户输入。在这个示例中，我们将用户的姓名作为输入。但我们将输入的名称存储在哪里呢？答案是通过 `dialog` 命令末尾的语句 `2>/tmp/input.$` 将输入重定向到文件，这意味着将屏幕输出发送到名为 `/tmp/input.$` 的文件中，随后可以通过以下方式检索输入的名称并存储到变量中：`na=cat /tmp/input.$`。`inputbox` 的退出状态参考下表：

| 输入退出状态 | 含义 |
|---|---|
| 0 | 命令执行成功 |
| 1 | 用户点击了取消按钮 |
| 255 | 用户点击了 `Escape` 键 |

### 使用 `dialog` 实用工具创建确认框 (`yesno`) 及用户界面整合演示

![](img/219cb7c6e1c9c4c56d73838282f4b69b_99_0.png)

### 使用 `dialog` 实用工具创建消息框 (`msgbox`)

### 使用 `dialog` 实用工具创建输入框 (`inputbox`)

```
$ cat > dia4
dialog --title "输入框 - 接收你的输入" --backtitle "Linux Script Tutorial" --inputbox "请输入你的名字" 8 60 2>/tmp/input.\$

ssel=$?

na=$(cat /tmp/input.\$.
case $sel in
0) echo "Hello $na" ;;
1) echo "点击了取消" ;;
255) echo "[ESCAPE] 键按了" ;;
esac

rm -f /tmp/input.\$
```

如下所示运行：

```
$ chmod +x dia4

$ ./dia4
```

![](img/219cb7c6e1c9c4c56d73838282f4b69b_101_0.png)

`inputbox` 用于接收用户输入。在这个示例中，我们将用户的姓名作为输入。但我们将输入的名称存储在哪里呢？答案是通过 `dialog` 命令末尾的语句 `2>/tmp/input.$` 将输入重定向到文件，这意味着将屏幕输出发送到名为 `/tmp/input.$` 的文件中，随后可以通过以下方式检索输入的名称并存储到变量中：`na=cat /tmp/input.$`。`inputbox` 的退出状态参考下表：

| 输入退出状态 | 含义 |
|---|---|
| 0 | 命令执行成功 |
| 1 | 用户点击了取消按钮 |
| 255 | 用户点击了 `Escape` 键 |

### 使用 `dialog` 实用工具创建确认框 (`yesno`) 及用户界面整合演示

![](img/219cb7c6e1c9c4c56d73838282f4b69b_99_0.png)

### 使用 `dialog` 实用工具创建消息框 (`msgbox`)

### 使用 `dialog` 实用工具创建输入框 (`inputbox`)

```
$ cat > dia4
dialog --title "输入框 - 接收你的输入" --backtitle "Linux Script Tutorial" --inputbox "请输入你的名字" 8 60 2>/tmp/input.\$

ssel=$?

na=$(cat /tmp/input.\$.
case $sel in
0) echo "Hello $na" ;;
1) echo "点击了取消" ;;
255) echo "按了 [ESCAPE] 键" ;;
esac

rm -f /tmp/input.\$
```

如下所示运行：

```
$ chmod +x dia4

$ ./dia4
```

![](img/219cb7c6e1c9c4c56d73838282f4b69b_101_0.png)
