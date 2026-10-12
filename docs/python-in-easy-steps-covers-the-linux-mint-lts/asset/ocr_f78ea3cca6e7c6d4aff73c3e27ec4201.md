# # Listing options

A Listbox widget provides a list of items in an application from which the user can make a selection. A listbox object is created by specifying the name of its parent container, such as a window or frame name, and options as arguments to a **Listbox()** constructor. Popular options are listed below, together with a brief description:

| Option: | Description: |
| :--- | :--- |
| **bd** | Border width in pixels (default is 2) |
| **bg** | Background color |
| **fg** | Foreground color used to render the text |
| **font** | Font for the text |
| **height** | Number of lines in list (default is 10) |
| **selectbackground** | Background color of selected text |
| **selectmode** | SINGLe (the default) or MULTIPLE selections |
| **width** | Listbox width in letters (default is 20) |
| **yscrollcommand** | Attach to a vertical scrollbar |

![](bbox=[0.13, 0.63, 0.22, 0.72])

With Tkinter, a scrollbar is a separate widget that can be attached to Listbox, Text, Canvas and Entry widgets.

Items are added to the listbox by specifying a list index number and the item string as arguments to its **insert()** method.

You can retrieve any item from a listbox by specifying its index number within the parentheses of its **get()** method. Usefully, a listbox also has a **curselection()** method that returns the index number of the currently-selected item, so this can