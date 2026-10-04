# 11.4 A Scrolling Listbox Megawidget

#
# If the first argument is a window path, use that as
# the base name for this widget.

```
if {[string first ". [lindex $args 0]] == 0} {
    set widgetName [lindex $args 0]
    set args [lreplace $args 0 0]
}

# -scrollposition option is specific to this
# megawidget. Look for that option, and set
# scrollPosition if it's defined.
# Wipe from the arg list after finding it.

for {set i 0} {$i < [length $args]} {incr i} {
    switch -- tolower [lindex $args $i]] {
        -sp
        -scrollposition {
            set j [expr $i +1]
            set scroll [string tolower \
                [lindex $args $j]]
            set args [lreplace $args $i $j]
        }
    }
}
```

frame $widgetName
#
# Create the scrollbar and listbox.
#
scrollbar $widgetName.scroll -command "$widgetName.list yview"
listbox $widgetName.list -height $height \
-yscrollcommand "$widgetName.scroll set"