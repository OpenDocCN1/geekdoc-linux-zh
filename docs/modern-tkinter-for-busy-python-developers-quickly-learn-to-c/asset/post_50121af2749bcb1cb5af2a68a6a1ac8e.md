
Want to associate some other value with each item in the list, so that your program can refer to some actual meaningful value, but it gets displayed in the combobox as something else? You'll want to have a look at the section entitled “Keeping Extra Item Data” when we get to the discussion of listboxes in a couple of chapters from now.

## The Grid Geometry Manager

We'll take a bit of a break from talking about different widgets (what to put onscreen), and focus instead on geometry management (where to put it). We introduced the general idea of geometry management in the “Tk Concepts” chapter; here, we focus on one specific geometry manager: grid.

As you've seen, grid lets you layout widgets in columns and rows. If you're familiar with using HTML tables to do layout, you'll feel right at home here. This chapter describes the various ways you can tweak grid to give you all the control you need for your user interface.

Grid is one of several geometry managers available in Tk, but it's mix of power, flexibility and ease of use, along with its natural fit with today's layouts (that rely on alignment of widgets) make it the best choice for general use. There are other geometry managers: “pack” is also quite powerful, but harder to use and understand; “place” gives you complete control of positioning each element; we'll see even widgets like paned windows, notebooks, canvas and text can act as geometry managers.

> Grid was first introduced to Tk in 1996, several years after Tk became popular, and took a while to catch on. Before that, developers had always used “pack” to do constraint-based geometry management. When grid came out, many developers kept using pack, and you'll still find it used in many Tk programs and documentation. While there's nothing technically wrong with it, the algorithm's behavior is often hard to understand. More importantly, because the order that widgets are packed is significant in determining layout, modifying existing layouts can be difficult.
>
> Grid has all the power of pack, generally produces nicer layouts (because it makes it easy to align widgets both horizontally and vertically), and is easier to learn and use. Because of that, we think grid is the right choice for most developers most of the time. Start your new programs using grid, and switch old ones to grid as you're making changes to an existing user interface.

The reference documentation for grid provides an exhaustive description of grid, its behaviors and all options.

## Columns and Rows

Using grid, widgets are assigned a “column” number and a “row” number, which indicates their relative position to each other. All widgets in the same column will therefore be above or below each other, while those in the same row will be to the left or right of each other.

Column and row numbers must be integers, with the first column and row starting at 0. You can leave gaps in column and row numbers (e.g. column 0, 1, 2, 10, 11, 12, 20, 21), which is handy if you plan to add more widgets in the middle of the user interface at a later time.

The width of each column (or height of each row) depends on the width or height of the widgets contained within the column or row. This means when sketching out your user interface, and dividing it into rows and columns, you don't need to worry about each column or row being equal width.

## Spanning Multiple Cells

Widgets can take up more than a single cell in the grid; to do this, you’ll use the “columnspan” and “rowspan” options when gridding the widget. These are analogous to the “colspan” and “rowspan” attribute of HTML tables.

Here is an example of creating a user interface that has multiple widgets, some that take up more than a single cell.

![](img/94378c1b05607c1dc5649c738af95c74_30_0.png)

```python
from tkinter import *
from tkinter import ttk

root = Tk()

content = ttk.Frame(root)
frame = ttk.Frame(content, borderwidth=5, relief="sunken", width=200, height=100)
namebl = ttk.Label(content, text="Name")
name = ttk.Entry(content)

onevar = BooleanVar()
twowar = BooleanVar()
threevar = BooleanVar()
onevar.set(True)
twowar.set(False)
threevar.set(True)

one = ttk.Checkbutton(content, text="One", variable=onevar, onvalue=True)
two = ttk.Checkbutton(content, text="Two", variable=twovar, onvalue=True)
three = ttk.Checkbutton(content, text="Three", variable=threevar, onvalue=True)
ok = ttk.Button(content, text="Okay")
cancel = ttk.Button(content, text="Cancel")

content.grid(column=0, row=0)
frame.grid(column=0, row=0, columnspan=3, rowspan=2)
namebl.grid(column=3, row=0, columnspan=2)
name.grid(column=3, row=1, columnspan=2)
one.grid(column=0, row=3)
two.grid(column=1, row=3)
three.grid(column=2, row=3)
ok.grid(column=3, row=3)
cancel.grid(column=4, row=3)

root.mainloop()
```

### Layout within the Cell

Because the width of a column (and height of a row) depends on all the widgets that have been added to it, the odds are that at least some widgets will have a smaller width or height than has been allocated for the cell its been placed in. So the question becomes, where exactly should it be put within the cell?

By default, if a cell is larger than the widget contained in it, the widget will be centered within it, both horizontally and vertically, with the master’s background showing in the empty space around it. The “sticky” option can be used to change this default behavior.

The value of the “sticky” option is a string of 0 or more of the compass directions “nsew”, specifying which edges of the cell the widget should be “stuck” to. So for example, a value of “n” (north) will jam the widget up against the top side, with any extra vertical space on the bottom; the widget will still be centered horizontally. A value of “nw” (north-west) means the widget will be stuck to the top left corner, with extra space on the bottom and right.

> In Tkinter, you can also specify this as a list, containing any of N, S, E and W.

Specifying two opposite edges, such as “we” (west, east) means that the widget will be stretched, in this case so it is stuck both to the left and right edge. So the widget will then be wider than its "ideal" size. Most widgets have options that can control how they are displayed if they are larger than needed. For example, a label widget has an “anchor” option which controls where the text of the label will be positioned.

If you want the widget to expand to fill up the entire cell, grid it with a sticky value of "nsew" (north, south, east, west) meaning it will stick to every side.

### Handling Resize

If you’ve taken a peek below and added the extra “sticky” options to our example, when you try it out you’ll notice things still don’t look quite right (the entry is lower on the screen then we’d want), and things are even worse if you try to resize the window — nothing moves at all!

It looks like “sticky” may tell Tk how to react if the cell’s row or column does resize, but doesn’t actually say that the row or columns should resize if extra room becomes available. Let’s fix that.

Every column and row has a “weight” grid option associated with it, which tells it how much it should grow if there is extra room in the master to fill. By default, the weight of each column or row is 0, meaning don’t expand to fill space.

For the user interface to resize then, we’ll need to give a positive weight to the columns we’d like to expand. This is done using the “columnconfigure” and “rowconfigure” methods of grid. If two columns have the same weight, they’ll expand at the same rate; if one has a weight of 1, another of 3, the latter one will expand three pixels for every one pixel added to the first.

Both “columnconfigure” and “rowconfigure” also take a “minsize” grid option, which specifies a minimum size which you really don’t want the column or row to shrink beyond.

### Padding

Normally, each column or row will be directly adjacent to the next, so that widgets will be right next to each other. This is sometimes what you want (think of a listbox and its scrollbar), but often you want some space between widgets. In Tk, this is called padding, and there are several ways you can choose to add it.
