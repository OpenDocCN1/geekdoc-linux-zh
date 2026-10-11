
The geometry manager takes all the information about the slaves, as well as the information about how large the master is, and uses its internal algorithms to determine the area each slave will be allocated (if any!). The slave is then responsible for drawing etc. within that particular rectangle. And of course, any time the size of the master changes (e.g. because the top-level window was resized), the natural size of a slave changes (e.g. because we've changed the text in a label), or any of the geometry manager parameters change (e.g. like "row", "column", or "sticky") we repeat the whole thing.

This all works recursively as well. In our example, we had a content frame inside the top-level window, and then a number of other controls in the content frame. We therefore had a geometry manager working on two different masters. At the outer level, the top-level window was the master, and the content frame was the slave. At the inner level, the content frame was the master, with each of the other widgets being slaves. So the same widget can be both a master and a slave. This hierarchy can of course also be nested much more deeply.

> While each master can have only one geometry manager (e.g. grid), it's entirely possible for different masters to have different geometry managers; while grid is generally used, others may make sense for a particular layout used in one part of your user interface. Also, we've been making the assumption that slave widgets are the immediate children of their master in the widget hierarchy. While this is usually the case, and mostly there's no good reason to do it any other way, it's also possible (with some restrictions) to get around this.

## Event Handling

In Tk, as in most other user interface toolkits, there is an event loop which receives events from the operating system. These are things like button presses, keystrokes, mouse movement, window resizing, and so on.

Generally, Tk takes care of managing this event loop for you. It will figure out what widget the event applies to (did the user click on this button? if a key was pressed, which textbox had the focus?), and dispatch it accordingly. Individual widgets know how to respond to events, so for example a button might change color when the mouse moves over it, and revert back when the mouse leaves.

### Command Callbacks

Often though you want your program to handle particular events, for example doing something when a button is pushed. For those events that are pretty much essential to customize (what good is a button without something happening when you press it?), the widget will provide a callback as a widget configuration option. We saw this in the example with the "command" option of the button.

Callbacks in Tk tend to be simpler than in toolkits used with compiled languages (where a callback must generally be directed at a procedure with a certain set of parameters or an object method with a certain signature). Instead, the callback is just a normal bit of code that the interpreter evaluates. While it can be as complex as you want to make it, most times though you'll just want your callback to call some other procedure.

### Event Bindings

For events that don't have a command callback associated with them, you can use Tk's "bind" to capture any event, and then (like with callbacks) execute an arbitrary piece of code.

Here is a (silly) example that shows how a label can have bindings set up for it to respond to different events, which it does so by just changing what is displayed in the label.

```python
from tkinter import *
from tkinter import ttk
root = Tk()
    l = ttk.Label(root, text="Starting...")
    l.grid()
    l.bind('<Enter>', lambda e: l.configure(text='Moved mouse inside'))
    l.bind('<Leave>', lambda e: l.configure(text='Moved mouse outside'))
    l.bind('<1>', lambda e: l.configure(text='Clicked left mouse button'))
    l.bind('<Double-1>', lambda e: l.configure(text="Double clicked"))
    l.bind("<B3-Motion>", lambda e: l.configure(text='right button drag to %d,%d' % (e.x, e.y)))
    root.mainloop()
```

The first three event bindings are pretty straightforward, just looking at simple events. The double click binding introduces the idea of an event modifier; in this case we want to trigger the motion on a left mouse click (the "1"), but only when it's a double click (the "Double-").

The last binding also uses a modifier: capture mouse movement ("Motion"), but only when the right mouse button ("B3") is held down. This binding also shows an example of how to use event parameters, through the use of percent substitutions. Many events, such as mouse clicks or movement have as parameters additional information like the current position of the mouse. These percent substitutions let you capture them so they can be used in your script.

> *Tkinter expects you to provide a function as the event callback, whose first argument is an event object representing the event that triggered the callback. It's usually not worth the bother of defining regular named functions for one-off callbacks such as in this example, so we've just used Python's anonymous functions via lambda. The earlier feet to meters example used a regular defined function (calculate).*

For a complete description of all the different event names, modifiers, and the different event parameters that are available with each, the best place to look is the "bind" command reference.

## Virtual Events

Beyond the low-level operating system events like mouse clicks and window resizes, many widgets generate higher level events called virtual events. For example, a listbox widget will generate a "ListboxSelect" virtual event anytime the selection changes, regardless of whether that was because the user clicked on an item, moved to it with the arrow keys, or whatever. This avoids the problem of setting up multiple, possibly platform-specific event bindings to capture the change. Virtual events for a widget, if any, will be listed in the widget's documentation.

## Multiple Bindings

Widgets can actually have a number of different event bindings trigger for a single event. Normally, events can be set up for: the individual widget itself, all widgets of a certain class (e.g. buttons), the toplevel window containing the widget, and all widgets in the application. Each of these will fire in sequence.

We saw this in our example when we set up a binding for the Return key on the toplevel window, and that applied to every widget within that window.

> *The default behavior of each widget class in Tk is itself defined with script-level event bindings, and so can be introspected and modified to alter the behavior of all widgets of a certain class. You can even completely modify the handling of this multiple sequence of events for each widget; see the "bindtags" command reference if you're curious.*

## Basic Widgets

This chapter introduces you to the basic Tk widgets that you'll find in just about any user interface: frames, labels, buttons, checkbuttons, radiobuttons, entries and comboboxes. By the end, you'll know how to use all the widgets you'd ever need for a typical fill-in form type of user interface.

This chapter (and those following that discuss more widgets) are meant to be read in order. Because there is so much commonality between many widgets, we'll introduce certain concepts in an earlier widget that will also apply to a later one. Rather than going over the same ground multiple times, we'll just refer back to when the concept was first introduced.

At the same time, each widget will also refer to the widget roundup page for the specific widget, as well as the reference manual page, so feel free to jump around a bit too.

### Frame

- Widget Roundup
- Reference Manual

A **frame** is a widget that displays just as a simple rectangle. Frames are primarily used as a container for other widgets, which are under the control of a geometry manager such as grid.

![](img/94378c1b05607c1dc5649c738af95c74_20_0.png)

Frames are created using the **ttk.Frame** function:
`frame = ttk.Frame(parent)`

Frames can take several different configuration options which can alter how they are displayed.

#### Requested Size

Like any other widget, after creation it is added to the user interface via a (parent) geometry manager. Normally, the size that the frame will request from the geometry manager will be determined by the size and layout of any widgets that are contained in it (which are under the control of the geometry manager that manages the contents of the frame itself).

If for some reason you want an empty frame that does not contain other widgets, you should instead explicitly set the size that the frame will request from its parent geometry manager using the "width" and/or "height" configuration options (otherwise you'll end up with a very small frame indeed).

> *Normally, distances such as width and height are specified just as a number of pixels on the screen. You can also specify them via one of a number of suffixes. For example, "350" means 350 pixels, "350c" means 350 centimeters, "350i" means 350 inches, and 350p means 350 printer's points (1/72 inch).*

#### Padding

The "padding" configuration option is used to request extra space around the inside of the widget; this way if you're putting other widgets inside the frame, there will be a bit of a margin all the way around. A single number specifies the same padding all the way around, a list of two numbers lets you specify the horizontal then the vertical padding, and a list of four numbers lets you specify the left, top, right and bottom padding, in that order.
`frame["padding"] = (5,10)`
