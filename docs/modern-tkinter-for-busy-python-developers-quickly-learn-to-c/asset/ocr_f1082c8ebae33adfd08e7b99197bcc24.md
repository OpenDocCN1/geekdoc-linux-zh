# # Paned Windows

+   - Widget Roundup
+   - Reference Manual

A **panedwindow** widget lets you stack two or more resizable widgets above and below each other (or to the left and right). The user can adjust the relative heights (or widths) of each pane by dragging a sash located between them. Typically the widgets you're adding to a panedwindow will be frames containing many other widgets.

![](bbox=[0.12, 0.2, 0.88, 0.41])

Panedwindow Widgets (Shown here managing several labelframes)

Panedwindows are created using the ttk.Panedwindow function:

```
```
p = ttk.Panedwindow(parent, orient=VERTICAL)
# first pane, which would get widgets gridded into it:
f1 = ttk.Labelframe(p, text='Pane1', width=100, height=100)
f2 = ttk.Labelframe(p, text="Pane2", width=100, height=100); # second pane
p.add(f1)
p.add(f2)
```
```

A panedwindow is either "vertical" (it's panes are stacked vertically on top of each other), or "horizontal". Importantly, all of the panes that you add to the panedwindow must be a direct child of the panedwindow itself.

Calling the "add" method will add a new pane at the end of the list of panes. The "insert position subwindow" method allows you to place the pane at the given position in the list of panes (0...n-1); if the pane is already managed by the panedwindow, it will be moved to the new position. You can use the "forget(subwindow)" to remove a pane from the panedwindow; you can also pass a position instead of a subwindow.

Other options let you sign relative weights to each pane so that if the overall panedwindow resizes, certain panes will get more space than others. As well, you can adjust the position of each sash between items in the panedwindow. See the command reference for details.

# # Notebook

+   - Widget Roundup
+   - Reference Manual

A **notebook** widget uses the metaphor of a tabbed notebook to let the user switch between one of several pages, using an index tab. In this case, unlike with paned windows, we're only allowing the user to look at a single page (akin to a pane) at a time.

59