# 11.4 A Scrolling Listbox Megawidget

```
proc processOptions {optionlist widgetlist (parent {})} {
  set return ""

  # Loop through the options and widgets.
  # If an option is not valid for a widget, fail silently
  # and continue processing

  foreach {option value} $optionlist {
    foreach widget $widgetlist {
      if {[string length $value] > 0} {
        lappend return \
          [catch "$parent$widget \
            configure $option\
            $value"]
      } else {
        catch "$parent$widget configure \
          option val
          lappend return $val
      }
    }
  }
  return $return
}
```

# 11.4 A Scrolling Listbox Megawidget

This section will show how a megawidget can be built using the two procedures described in Section 11.3 and the namespace and package commands. We'll start out with a simple megawidget—a scrolling listbox—and then use that megawidget to build a more complex megwidget that will take selected items from one scrolled listbox, place them into another, and finally put a wrapper around the latter megawidget to make a modal file selector.