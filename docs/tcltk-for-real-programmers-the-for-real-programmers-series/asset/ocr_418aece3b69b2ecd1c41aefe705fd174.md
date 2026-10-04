# 11.6 Making a Modalawidget: The grab Command

```
return $widgetName.$subwidget
} else {
    error "bad subwidget: $subwidget -\
    must be one of:\ $validSubList
}
selection {
    # If something is selected in the filter
    # listbox, return that item/items text.
    set 11 [eval $widgetName.filterList selection]

    # Else, check for items selected in the full
    # listbox.
    if ($11 == "") {set 11 \
        eval $widgetName.fullList selection
    }
    return $11
}
def {
    # Should not be here, this is an error
    set methods {insert configure delete selection
    error "Bad method: $subCommand\n use $methods"
}
}
```

# 11.6 Making a Modalawidget: The grab Command

In this section we'll take the filteredList megawidget we just developed and make a modal file selection widget. This widget is far from the last word in file selection widgets, but it makes a good example of how a modal widget can be constructed.