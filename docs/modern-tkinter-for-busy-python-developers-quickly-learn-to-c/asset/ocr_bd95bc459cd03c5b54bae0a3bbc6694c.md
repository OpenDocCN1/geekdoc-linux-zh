```
canvas.create_line(10, 10, 200, 50)
```

The `create_line` method will return an item id (an integer) that can be used to uniquely refer to this item; every item created will get its own id. Though often we don't need to refer to the item later and will therefore ignore the returned id, we'll see how it can be used shortly.

Let's start our simple sketchpad example. For now, we'll want to be able to draw freehand on the canvas by dragging the mouse on it. We'll create a canvas widget, and then attach event bindings to it to capture mouse clicks and drags. When we first click the mouse, we'll remember that location as our "start" position. Every time the mouse is moved with the mouse button still held down, we'll create a line item going from this "start" position to the current mouse position. The current position will then be the "start" position for the next line segment.

```
from tkinter import *
from tkinter import ttk

lastx, lasty = 0, 0

def xy(event):
    global lastx, lasty
    lastx, lasty = event.x, event.y

def addLine(event):
    global lastx, lasty
    canvas.create_line((lastx, lasty, event.x, event.y))
    lastx, lasty = event.x, event.y

root = Tk()
root.columnconfigure(0, weight=1)
root.rowconfigure(0, weight=1)

canvas = Canvas(root)
canvas.grid(column=0, row=0, sticky=(N, W, E, S))
canvas.bind("<Button-1>", xy)
canvas.bind("<B1-Motion>", addLine)

root.mainloop()
```

Try it out - drag the mouse around the canvas to create your masterpiece.

# ## Item Attributes

When creating items, you can also specify one or more attributes for the item, that will affect how it is displayed. For example, here we'll specify that the line should be red, and three pixels wide.

```
canvas.create_line(10, 10, 200, 50, fill='red', width=3)
```

The exact set of attributes will vary according to the type of item.

Like with Tk widgets, changing attributes for canvas items after you've already created them can also be done.

```
id = canvas.create_line(0, 0, 10, 10, -fill red)
...
canvas.itemconfigure(id, fill='blue', width=2)
```