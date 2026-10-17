
![](img/d06b1f1cf83677f6647237f0c7827141_238_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_238_2.png)

`command` 选项只指定函数名称。不要在赋值中添加尾部括号。

![](img/d06b1f1cf83677f6647237f0c7827141_238_3.png)

‘gray’ 颜色是窗口的原始默认颜色。

### 显示消息

程序可以通过调用“`tkinter.messagebox`”模块提供的方法来向用户显示消息。必须单独导入该模块，并且其较长的名称可以方便地通过 *import as* 语句分配一个短别名。

消息框通过向这些方法之一提供框标题和要显示的消息作为两个参数来创建：

| 方法 | 图标 | 按钮 |
| :--- | :---: | :--- |
| `showinfo()` | ⓘ | 确定 |
| `showwarning()` | ⚠ | 确定 |
| `showerror()` | ⊗ | 确定 |
| `askquestion()` | ❓ | 是（返回字符串 ‘yes’）和 否（返回字符串 ‘no’） |
| `askokcancel()` | ❓ | 确定（返回 1）和 取消 |
| `askyesno()` | ❓ | 是（返回 1）和 否 |
| `askretrycancel()` | ❓ | 重试（返回 1）和 取消 |

![](img/d06b1f1cf83677f6647237f0c7827141_240_0.png)

只有 `askquestion()` 方法返回两个值 – `askyesno()` 的 No 按钮和两个 Cancel 按钮均不返回任何值。

那些包含单个 OK 按钮的消息框方法在用户点击按钮时不返回任何值。那些确实返回值的方法可以通过测试该值来执行条件分支。

1. 通过使 GUI 功能可用，并将 messagebox 功能作为简短别名可用，开始一个新的 Python 程序

```
from tkinter import *
import tkinter.messagebox as box
```

![](img/d06b1f1cf83677f6647237f0c7827141_241_0.png)

2. 接下来，创建一个窗口对象并指定标题

```
window = Tk()
window.title(‘Message Box Example’ )
```

3. 添加一个函数以显示各种消息框

```
def dialog() :
    var = box.askyesno(‘Message Box’, ‘Proceed?’ )
    if var == 1 :
        box.showinfo(‘Yes Box’, ‘Proceeding...’ )
    else :
        box.showwarning(‘No Box’, ‘Canceling...’ )
```

4. 然后，创建一个按钮，以便在点击时调用该函数

```
btn = Button( window , text = ‘Click’ , command =dialog )
```

5. 将按钮以位置填充的方式添加到窗口中

```
btn.pack( padx = 150 , pady = 50 )
```

6. 最后，添加循环以捕获此窗口的事件

```
window.mainloop()
```

7. 将该文件保存在你的脚本目录中，然后在那里打开一个命令提示符窗口，并使用命令 `python tk_message.py` 运行此程序 – 点击按钮以查看消息框出现

![](img/d06b1f1cf83677f6647237f0c7827141_242_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_242_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_242_2.png)

![](img/d06b1f1cf83677f6647237f0c7827141_242_3.png)

![](img/d06b1f1cf83677f6647237f0c7827141_243_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_243_1.png)

可以将选项作为第三个参数添加到这些方法调用中。例如，添加 `type='abortretryignore'` 以获取三个按钮。

### 收集输入项

`Entry` 小部件在应用程序中提供一个单行输入字段，程序可以从中收集用户的输入项。`Entry` 对象通过指定其父容器的名称（如窗口或框架名称）以及作为 `Entry()` 构造函数的参数的选项来创建。每个选项都指定为一个 `option=value` 对。常用选项及其简要描述如下：

| 选项 | 描述 |
| :--- | :--- |
| `bd` | 边框宽度（像素）（默认为 2） |
| `bg` | 背景颜色 |
| `fg` | 用于渲染文本的前景色 |
| `font` | 文本的字体 |
| `highlightcolor` | 获得焦点时的边框颜色 |
| `selectbackground` | 所选文本的背景颜色 |
| `selectforeground` | 所选文本的前景色 |
| `show` | 使用 `show='*'` 隐藏密码字符 |
| `state` | 启用状态为 NORMAL 或 DISABLED |
| `width` | 以字符为单位的 Entry 宽度 |

多个小部件可以分组在框架中以实现更好的定位。框架对象通过指定窗口名称作为 `Frame()` 构造函数的参数来创建。然后，该框架的名称可以指定为小部件构造函数的第一个参数，以将其标识为该小部件的容器。

![](img/d06b1f1cf83677f6647237f0c7827141_244_0.png)

如果你希望允许用户输入多行文本，请使用 `Text` 小部件代替 `Entry` 小部件。

在实际将小部件添加到框架时，你可以使用 `TOP`, `BOTTOM`, `LEFT` 或 `RIGHT` 常量指定在框架中向哪一侧填充它们。例如，`entry.pack(side=LEFT)`。

通常，`entry` 小部件会与一个描述期望用户输入类型的标签并排出现，或者与一个用户可以点击以对其输入的数据执行某些操作的按钮小部件并排出现，因此在框架中定位是理想的。

当前输入到 `entry` 小部件中的数据可以通过程序使用该小部件的 `get()` 方法获取。

1. 通过使 GUI 功能可用，并将 messagebox 功能作为简短别名可用，开始一个新的 Python 程序

```
from tkinter import *
import tkinter.messagebox as box
```

![](img/d06b1f1cf83677f6647237f0c7827141_245_0.png)

2. 接下来，创建一个窗口对象并指定标题

```
window = Tk()
window.title(‘Entry Example’ )
```

3. 现在，创建一个框架以容纳用于输入的 entry 字段

```
frame = Frame( window )
entry = Entry( frame )
```

4. 然后，添加一个函数以显示当前输入的数据

```
def dialog() :
    box.showinfo(‘Greetings’, ‘Welcome’ + entry.get() )
```

5. 现在，创建一个按钮，以便在点击时调用该函数

```
btn = Button( frame, text = ‘Enter Name’, command=dialog )
```

6. 将按钮和 entry 添加到框架的指定侧边

```
btn.pack( side = RIGHT, padx = 5 )
entry.pack( side = LEFT )
frame.pack( padx = 20, pady = 20 )
```

7. 最后，添加循环以捕获此窗口的事件

```
window.mainloop()
```

8. 将该文件保存在你的脚本目录中，然后在那里打开一个命令提示符窗口，并使用命令 `python tk_entry.py` 运行此程序 – 输入你的名字并点击按钮以查看问候消息出现

![](img/d06b1f1cf83677f6647237f0c7827141_246_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_246_1.png)

![](img/d06b1f1cf83677f6647237f0c7827141_246_2.png)

如果你希望显示用户无法编辑的文本，请使用 `Label` 小部件代替 `Entry` 小部件。

### 列出选项
