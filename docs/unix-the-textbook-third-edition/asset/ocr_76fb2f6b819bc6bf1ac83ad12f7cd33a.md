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

# Example 16.44

PanedWindow widget

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

# Example 16.45

Spinbox widget

```
from Tkinter import *
def spinbox():
```

![](bbox=[0.42, 0.82, 0.78, 0.92])

FIGURE 16.13 Tk PanedWindow display.

![](bbox=[0.48, 0.93, 0.78, 1.0])

FIGURE 16.14 Tk Spinbox display.