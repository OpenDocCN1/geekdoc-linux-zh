![](bbox=[0.42, 0.12, 0.62, 0.2])

FIGURE 16.17 Tk OptionMenu display.

![](bbox=[0.42, 0.28, 0.62, 0.36])

FIGURE 16.18 Tk Message display.

# Example 16.48

OptionMenu widget

```
from Tkinter import *
def optionmenu():
    master = Tk()
    master.title("OptionMenu")
    variable = StringVar(master)
    variable.set("one") # default value
    w = OptionMenu(master, variable, "one", "two", "three")
    w.pack()
    mainloop()
optionmenu()
```

# Example 16.49

Message widget

```
from Tkinter import *
def message():
    master = Tk()
    master.title("Message")
    w = Message(master, text="the message")
    w.pack()
    mainloop()
message()
```

# 16.4.3.3 Hooking Tkinter Widgets to Applications in Python: Examples

Given the widget library of available core widgets in Tkinter, and armed with your knowledge of Python programming to this point, you are ready to do the following examples. The following simple example allows the user to enter a text string into a dialog box in a widget, and echoes that string as a label in another widget. A line-by-line description/explanation of the code follows the example (see Figures 16.19 and 16.20):