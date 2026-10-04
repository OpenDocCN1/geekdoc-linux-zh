would be created by the scrollbar and then evaluated by the Tcl interpreter.
listbox would change the display to show the requested area and
generate the following command:

```
.scroll set .25 .60
```

When this command is evaluated, the scrollbar will change its display to
put the slider in the proper location.

# 8.9.3 Intercepting scrollbar Commands

The next example shows how you can use this knowledge about how the
scrollbar works to use a single scrollbar to control two listbox widgets.

This example uses a couple of previously unmentioned subcommands of
tlistbox widget. These are:

Syntax: listName size

size Returns the number of entries in a listbox.

Syntax: listName yview moveto fraction

yview moveto

This is one of the subcommands designed for interaction
with the scrollbar. It moves the listbox display window
such that the top entry is the entry described by the frac-tion argument.

fraction A fraction representing the percentage of the list that
should be skipped before displaying the first list entry
(e.g., .25 means that 25% of the list should be skipped, and
t entry that is one fourth of the way down the list should
be the first entry displayed.

# Example 8.9.3-1

Example Script

```
# Create the two listboxes
```

```
listbox .leftbox -height 5 -exportselection 0
listbox .rightbox -height 5 -exportselection 0
```