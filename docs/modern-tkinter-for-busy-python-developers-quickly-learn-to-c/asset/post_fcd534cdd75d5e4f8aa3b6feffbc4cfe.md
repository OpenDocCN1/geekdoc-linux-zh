
## Querying and Changing Item Options

  Like most everything in Tk, you can look at or change the value of an item’s options at any time. Items are referred to via an index. Normally, this is a number (0...n-1) indicating the item’s position in the menu, but you can also specify the label of the menu item (or in fact, a “glob-style” pattern to match against the item’s label).

```python
print( menu_.file.entrycget(0, 'label') )
menu_.file.entryconfigure('Close', state=DISABLED)
print( menu_.file.entryconfigure(0) )
```

## Platform Menus

  Each platform has a few menus that are handled specially by Tk.

### Mac OS X

  On Mac OS X, there are two menus that are treated specially. The application menu is the second menu in the menubar, titled with your application name. It will have any menu items you add to it, then following that, the standard application menu items (preferences, services, hide/show, and quit) are automatically added by Tk. The second special menu is the help menu, which is always placed as the last menu on the menubar. Again, along with the items you add, Tk will add others expected by the system (nothing on Tiger, a search box on Leopard).

```python
apple = Menu(menubar, name='apple')
help = Menu(menubar, name='help')
menubar.add_cascade(menu=apple)
menubar.add_cascade(menu=help)
```

> While normally Tkinter chooses a widget path name for us, here we’ve had to explicitly provide one using the 'name' option. Naming the menus 'apple' and 'help' are the cues that Tk needs to recognize them as special.

> The application menu, which is the one we’re dealing with here, is distinct from the apple menu (the one with the apple icon, just to the left of the application menu). Despite that we do really mean the application menu, in Tk it is still referred to as the “apple” menu. This is a holdover from pre-OS X days, when these sorts of items did go in the actual apple menu, and there was no separate application menu.

  It’s normal practice to add an “About appname” command item to the Application menu, followed by a separator item. When invoked this should display your application’s about box.

```python
# Python code placeholder from original OCR error "PYHONTODO"
```

### Windows

  On Windows, each window has a “System” menu at the top left of the window frame, with a small icon for your application. It contains items like “Close”, “Minimize”, etc. In Tk, if you create a system menu, you can add new items that will appear below the standard items.

```python
sysmenu = Menu(menubar, name='system')
menubar.add_cascade(menu=sysmenu)
```

> While normally Tkinter will choose a widget path name for us, here we’ve had to explicitly provide one with the name 'system'; this is the cue that Tk needs to recognize it as the system menu.

### X11

  On X11, if you create a help menu, Tk will ensure that it is always the last menu in the menubar.

```python
menu_help = Menu(menubar, name='help')
menubar.add_cascade(menu=menu_help, label='Help')
```

> The widget pathname of the menu must be explicitly provided, in this case with the name 'help'. This can be specified for any Tkinter widget using the 'name' option when creating the widget.

## Contextual Menus

  Contextual menus ("popup" menus) are typically invoked by a right mouse button click on an object in the application. A menu pops up at the location of the mouse cursor, and the user can select from one of the items in the menu (or click outside the menu to dismiss it without choosing any item).

  To create a contextual menu, you'll use exactly the same commands you did to create menus in the menubar. Typically, you'll create one menu with several command items in it, and potentially some cascade menu items and their associated menus.

  To activate the menu, the user will use a contextual menu click, which you will have to bind to. That however, can mean different things on different platforms. On Windows and X11, this is the right mouse button being clicked (the third mouse button). On Mac OS X, this is either a click of the left (or only) button with the control key held down, or a right click on a multi-button mouse. Unlike Windows and X11, Mac OS X refers to this as the second mouse button, not the third, so that's the event you'll see in your program.

> Most earlier programs that have used popup menus assumed it was only "button 3" they needed to worry about.

  Besides capturing the correct contextual menu event, you'll also need to capture the location the mouse was clicked. It turns out you need to do this relative to the entire screen (global coordinates) and not local to the window or widget you clicked on (local coordinates). The "%X" and "%Y" substitutions in Tk's event binding system will capture those for you.

  The last step is simply to tell the menu to popup at the particular location. Here's an example of the whole process, using a popup menu on the application's main window.

```python
from tkinter import *
root = Tk()
menu = Menu(root)
for i in ('One', 'Two', "Three"):
    menu.add_command(label=i)
if (root.tk.call('tk', 'windowingsystem')== 'aqua'):
    root.bind('<2>', lambda e: menu.post(e.x_root, e.y_root))
    root.bind('<Control-1>', lambda e: menu.post(e.x_root, e.y_root))
else:
    root.bind('<3>', lambda e: menu.post(e.x_root, e.y_root))
```

## Windows and Dialogs

  Everything we've done up until now has been in a single window. In this chapter, we'll cover how to use multiple windows, changing various attributes of windows, and use some of the standard dialog box windows that are available in Tk.

### Creating and Destroying Windows

  You've already seen that all Tk programs start out with a root toplevel window, and then widgets are created as children of that root window. Creating new toplevel windows works almost exactly the same as creating new widgets.

  Toplevel windows are created using the **Toplevel** function:

```python
t = Toplevel(parent)
```

  Unlike regular widgets, you don't have to “grid” a toplevel for it to appear onscreen. Once you've created a new toplevel, you can then create other widgets which are children of that toplevel, and grid them inside the toplevel. In other words, the new toplevel behaves exactly like the automatically created root window.

  To destroy a window, you can use the **destroy** method on a widget:

```python
window.destroy()
```

  Note that you can use **destroy** on any widget, not just a toplevel window. Also, when you destroy a window, all windows (widgets) that are children of that window are also destroyed. So if you happen to destroy the root window (that all other widgets are descended from), that will normally end your application.

### Changing Window Behavior and Styles

  There are lots of things about how windows behave and how they look that can be changed.

#### Window Title

  To examine or change the title of the window:

```python
oldtitle = window.title()
window.title('New title')
```

#### Size and Location

  In Tk, a window's position and size on the screen is known as its geometry. A full geometry specification looks like this:

```text
widthxheight+x+y
```

  Width and height (normally in pixels) are pretty self-explanatory. The “x” (horizontal position) is specified with a leading plus or minus, so “+25” means the left edge of the window should be 25 pixels from the left edge of the screen, while “-50” means the right edge of the window should be 50 pixels from the right edge of the screen. Similarly, a “y” (vertical) position of “+10” means the top edge of the window should be ten pixels below the top of the screen, while “-100” means the bottom edge of the window should be 100 pixels above the bottom of the screen.

> Remember that the geometry's position are the actual coordinates on the screen, and don't make allowances for systems like Mac OS X which have a menubar along the top, or a dock area along the bottom. So specifying a position of “+0+0” would actually place the top part of the window under the system menu bar. It's a good idea to leave a healthy margin (at least 30 pixels) from an edge of the screen.

  Here is an example of changing the size and position, placing the window towards the top righthand corner of the screen:

```python
window.geometry('300x200-5+40')
```
