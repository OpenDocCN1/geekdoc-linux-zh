scrolled widget. When the scrollbar is manipulated, it will tack on some number of parameters to the method call, indicating how it was scrolled, to what position, etc.

The scrolled widget also needs to communicate back to the scrollbar, telling it what percentage of the entire content area is now visible. Besides the yview and/or xview methods, every scrollable widget also has a"yscrollcommand" and/or "xscrollcommand" configuration option. This is used to specify a method call, which must be the scrollbar's "set" method. Again, additional parameters will be automatically tacked onto the method call.

If for some reason you want to move the scrollbar to a particular position from within your program, you can call the "set first last" method yourself. Pass it two values between 0 and 1 indicating the start and end percentage of the content area that is visible.

# Example

Listboxes are one of several types of widgets that are scrollable. Here we'll build a very simple user interface, consisting just of a vertically scrollable listbox that takes up the entire window, with just a status line at the bottom.

![](bbox=[0.35, 0.32, 0.65, 0.51])

```
```python
from tkinter import *
from tkinter import ttk

root = Tk()

l = Listbox(root, height=5)
l.grid(column=0, row=0, sticky=(N,W,E,S))
s = ttk.Scrollbar(root, orient=VERTICAL, command=l.yview)
s.grid(column=1, row=0, sticky=(N,S))

l["yscrollcommand"] = s.set

ttk.Sizegrip().grid(column=1, row=1, sticky=(S,E))

root.grid_columnconfigure(0, weight=1)
root.grid_rowconfigure(0, weight=1)

for i in range(1,101):
    l.insert('end', 'Line %d of 100' % i)

root.mainloop()
```
```

# SizeGrip

+   - Widget Roundup
+   - Reference Manual

We actually snuck in one new widget in that last example, the **sizegrip**. This is the little box at the bottom right corner of the window that allows you to resize it.