# 11.5 Incorporating a Megawidget into a Larger Megawidget

the selected items in the unfiltered listbox if nothing was selected in the filtered box.

The justification for this widget is that sometimes there are just too many items in a listbox for it to be easy to select the ones the user is interested in, but a simple filter could cut down the size to something manageable. This is similar to the effect that various file browsers get with the "filter" option, but it allows the user to see both the unfiltered list and the filtered list at the same time.

Like the scrolledListBox, this megawidget is implemented as a procedure for creating the widget in the global scope with support procedures maintained in a namespace scope.

There are some points to watch when using namespaces with Tk widgets. In particular, you should note the use of the namespace code construct for the button command string. When the command associated with a Tk widget is evaluated, it is evaluated in the global namespace. Since the DoFilter procedure is defined within a namespace, the button command string needs to include that namespace as part of the command string.

If we know the FilteredList would be defined at a top level, we could just define the command string as ::FilteredList::DoFilter, but just as the scrolledListBox megawidget is contained within the filteredList widget, the filteredList widget may be contained in a larger widget, as we will show in the file browser megawidget example in the next section.

The namespace code command adds information to the script argument to define the current namespace. You can get the same effect by using the namespace current command to find the current namespace and regsub or format to modify a script to the current namespace. Using the namespace code command is much simpler and guaranteed to continue working if anything should ever change in the Tcl namespace implementation.

Filtered.tcl

```
package provide widgets 1.0
package require widgets
```