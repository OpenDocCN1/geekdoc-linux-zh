# 11.4 A Scrolling Listbox Megawidget

We can do this because scrolled procedure names and window names are resolved from separate tables. When you create a frame .foo, the Tk interpreter creates a window named .foo and a procedure named .foo to access that window. You can rename the procedure .foo without affecting the window .foo.

Being able to disconnect the frame .sll1 from the procedure .sll1 allows us to duplicate the Tk convention of declaring a name for the megawidget and then using that name as the widget procedure. If we didn't rename the frame widget procedure, there would be no way to interact with the frame after we create a new procedure with that name.

# 11.4.4 The scrolledListBox Code

ScrolledList widgets 1.0

```
############################################################################
# proc scrolledListBox(args)
#   Create a scrolledListBox megawidget
#   External entry point for creating a megawidget
# Arguments
#   ?parentFrame?      A frame to the parent, if this is not provided, the mega widget
#                   is a child of the root frame (\.").
#   ?-scrollposition left/right?
#                   The side of the listbox for the scrollbar
# Results
#   Creates a procedure with the megawidget name for processing
#   widget commands
#   Returns the name of the megawidget
proc scrolledListBox {args} {
  set newWidget [eval scrolledLB::MakeScrolledListBox $args]
  proc newWidget {args} "
    return \[scrolledLB::ScrolledListBoxProc \
      $newWidget \$args]
"
return $newWidget
```