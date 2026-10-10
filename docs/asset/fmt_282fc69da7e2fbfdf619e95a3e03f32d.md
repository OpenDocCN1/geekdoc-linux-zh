
## Application-Level API Synopsis

Create a new instance of `GtkEventBox`:

```c
GtkWidget *gtk_event_box_new(void);
```

## Class Description

Many `Gtk+` widget classes do not create a X window for each instance they are asked by an application to instantiate. Many of these widget classes are container widget classes that create instances that are never visible to users and therefore do not need a window. Others rely on a panel in the widget instance hierarchy to provide a window into which their content is rendered.

The following is a list of some of the `Gtk+` widget classes that do not create a X window for each instantiated: `GtkFrame`, `GtkAspectFrame`, `GtkTree`, `GtkHBox`, `GtkVBox`, `GtkSeparator`, `GtkVSeparator`, `GtkImage`, `GtkLabel`, `GtkOptionMenu`, `GtkPack`, `GtkPixmap`, and `GtkTable`.

Let's focus on `GtkTable` for the remainder of the discussion. `GtkTable` does not create a window for itself or its cells. The content of the cell is either drawn into a window provided by the widget that occupies the cell or is drawn into a window created by a widget higher in the widget instance hierarchy (i.e., an ancestor of the `GtkTable` widget instance). In the tic-tac-toe example presented earlier in this chapter, the playing board is an instance of `GtkTable`. The table contains nine cells, organized as three rows of three columns each. Each cell in the table manages an instance of `GtkPixmap` (the pixmap represents the current occupant of the cell, either an X or a O move or an unoccupied cell). Each pixmap draws itself into the top-level window (instance of `GtkWindow`) based on the layout computed for it by the `GtkTable` widget instance. Figure 11.36 illustrates the instance hierarchy of the tic-tac-toe board I have just described:

![](img/1441ee0eb9a357efc9aff107f92bf0c0_593_0.png)

`GtkWindow`
  - `GtkTable`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`
    - `GtkPixmap`

Figure 11.36 Tic-Tac-Toe Instance Hierarchy

Let's say the window created by the `Gtk` instance receives an expose event (the window was mapped, or some portion of the window became obscured, perhaps due to the user moving a window that was higher in the window stacking order away and exposing a portion of the window). To handle this event, the `GtkWindow` instance will (in effect) pass this event down to each of its children (which in this case is a single instance of `GtkTable`). The `GtkTable` instance will receive the event and handle it by calling on each of its children (instances of `GtkPixmap` in this case) to handle the expose event. Each instance of `GtkPixmap` will, in turn, handle the expose event by drawing itself in the window it is provided. Clearly, there is no need in this case for a table to create a window for itself, or for each of its children, nor is it necessary for each instance of `GtkPixmap` to create a window.

Some widgets, on the other hand, do find it necessary to create their own windows. Such class is `GtkButton`. Besides needing to draw itself (if that is its requirement, it would not need a window), it must handle button press and key events and respond to enter and leave events, which triggers redraw as the transitions to and from prelight stage.

If we were to place buttons, instead of pixmaps, children of our tic-tac-toe table widget, we would gain the ability to click on them, and the buttons would respond to enter and leave notify events in the same way that any button would.
