```
master = Tk()
master.title("Spinbox")
w = Spinbox(master, from_=0, to=10)
w.pack()
mainloop()
spinbox()
```

# Example 16.46

Text widget

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

# Example 16.47

LabelFrame widget

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

![](bbox=[0.38, 0.84, 0.62, 0.92])

FIGURE 16.15 Tk Text Box display.

![](bbox=[0.42, 0.95, 0.62, 1.0])

FIGURE 16.16 Tk LabelFrame display.