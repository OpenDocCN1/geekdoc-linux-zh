

![](img/02e070097d401d3bf7de4bf1c470b267_685_0.png)

图 16.6 Tk TextEntry 显示。

```
e.pack()
mainloop()
entry()
```

## 示例 16.38

Frame 部件：

```
from Tkinter import *
def frame():
    master = Tk()
    master.title("Frame")
    Label(text="above Frame separator").pack()
    separator = Frame(height=2, bd=1, relief=SUNKEN)
    separator.pack(fill=X, padx=5, pady=5)
    Label(text="below Frame separator").pack()
    mainloop()
frame()
```

## 示例 16.39

ListBox 部件：

```
from Tkinter import *
def listbox():
    master = Tk()
    master.title("Listbox")
    listbox = Listbox(master)
```

![](img/02e070097d401d3bf7de4bf1c470b267_685_1.png)

图 16.7 Tk Frame 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_685_2.png)

图 16.8 Tk ListBox 显示。

```
listbox.pack()
for item in ["one", "two", "three", "four"]:
    listbox.insert(END, item)
mainloop()
```

## 示例 16.40 Menu 部件

```
from Tkinter import *
def menu():
    root = Tk()
    root.title("Menu")
    def hello():
        print "I am here"
    # create a toplevel menu
    menubar = Menu(root)
    menubar.add_command(label="1stMenu", command=hello)
    menubar.add_command(label="2ndMenu", command=root.quit)
    root.config(menu=menubar)
    mainloop()
menu()
```

## 示例 16.41 RadioButton 部件

```
from Tkinter import *
def radiobutton():
    master = Tk()
    master.title("RadioButton")
    v = IntVar()
    Radiobutton(master, text="One", variable=v, value=1).pack(anchor=W)
    Radiobutton(master, text="Two", variable=v, value=2).pack(anchor=W)
```

# 图 16.9 Tk Menu 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_686_0.png)

# 图 16.10 Tk RadioButton 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_686_1.png)

```
Radiobutton(master, text="Two", variable=v, value=2).
pack(anchor=W)
mainloop()
radiobutton()
```

## 示例 16.42

Scale 部件

```
from Tkinter import *
def scale():
    master = Tk()
    master.title("Scale")
    w = Scale(master, from_=0, to=100)
    w.pack()
    w = Scale(master, from_=0, to=200, orient=HORIZONTAL)
    w.pack()
    mainloop()
scale()
```

## 示例 16.43

Scrollbar 部件

```
from Tkinter import *
def scrollbar():
    master = Tk()
    master.title("Scrollbar")
```

![](img/02e070097d401d3bf7de4bf1c470b267_687_0.png)

图 16.11 Tk Scale "Slider" 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_687_1.png)

图 16.12 Tk Scrollbar 显示。

```
scrollbar = Scrollbar(master)
scrollbar.pack(side=RIGHT, fill=Y)
listbox = Listbox(master, yscrollcommand=scrollbar.set)
listbox.insert(END, "Listbox")
for i in range(1000):
    listbox.insert(END, str(i))
listbox.pack(side=LEFT, fill=BOTH)
scrollbar.config(command=listbox.yview)
mainloop()
scrollbar()
```

## 示例 16.44

PanedWindow 部件

```
from Tkinter import *
def panedwindow():
    m1 = PanedWindow()
    m1.pack(fill=BOTH, expand=1)
    left = Label(m1, text="PanedWindow left")
    m1.add(left)
    m2 = PanedWindow(m1, orient=VERTICAL)
    m1.add(m2)
    top = Label(m2, text="PanedWindow top")
    m2.add(top)
    bottom = Label(m2, text="PanedWindow bottom")
    m2.add(bottom)
    mainloop()
panedwindow()
```

## 示例 16.45

Spinbox 部件

```
from Tkinter import *
def spinbox():
```

![](img/02e070097d401d3bf7de4bf1c470b267_688_0.png)

图 16.13 Tk PanedWindow 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_688_1.png)

图 16.14 Tk Spinbox 显示。

```
master = Tk()
master.title("Spinbox")
w = Spinbox(master, from_=0, to=10)
w.pack()
mainloop()
spinbox()
```

## 示例 16.46

Text 部件

```
from Tkinter import *
def text():
    master = Tk()
    master.title("Text")
    textBox = Text(master,wrap=WORD)
    textBox.grid()
    mainloop()
text()
```

## 示例 16.47

LabelFrame 部件

```
from Tkinter import *
def labelframe():
    master = Tk()
    group = LabelFrame(master, text="LabelFrame", padx=5, pady=5)
    group.pack(padx=10, pady=10)
    w = Entry(group)
    w.pack()
    mainloop()
labelframe()
```

![](img/02e070097d401d3bf7de4bf1c470b267_689_0.png)

图 16.15 Tk Text Box 显示。

![](img/02e070097d401d3bf7de4bf1c470b267_689_1.png)

图 16.16 Tk LabelFrame 显示。

