# Chapter 11. Tk Megawidget

}

```
namespace eval scrolledLB {
    # Force the load of the widgetLib package so that the
    # procedures can be imported.
    package require widgetLib
    if {[info exists::widgetLib::processOptions]}
        eval $auto_index(::widgetLib::processOptions)
    namespace import widgetLib::*\}
```

variable ScInfo
set ScInfo(unique) 0

```
####################################################################
# proc MakeScrolledListBox {args}
    # Create a scrolledListBox megawidget
    # Arguments
    # ?parentFrame? A frame to use for the parent.
    #     If this is not provided, the mega widget
    #     is a child of the root frame (".").
    # ?-scrollposition left/right?
    # The side of the listbox for the scrollbar
    # Results
    # Returns the name of the parent frame for use as a
    # megawidget
proc MakeScrolledListBox {args} {
    variable ScInfo
    # Set some defaults
    #
    set widgetName .scl$ScInfo(unique)
    set scrollPosition right
    set height 4
```

418