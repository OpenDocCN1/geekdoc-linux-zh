# Chapter 3. Introduction to the Tcl Language

The append command appends new data to a list, creating and returning a new, longer list. Note that this command will modify the existing list, unlike the string tolower command, which returns new data without changing the original.

Syntax: append listName ?element1 ... ?elementN?

+   - append Joins the arguments into a list

+   - listName The name of the list to append data to

+   - member A unit of data to add to the list

The split command returns the input string as a list. It splits the string wherever certain characters appear. By default, the split location is a space, tab or newline.

Syntax: split data ?splitChar?

+   - split Split data into a list

+   - data The data to split

+   - ?splitChar An optional character (or list of characters) to split the data at

The length command returns the number of list elements in a list. Note that this is not the number of elements in a list, it's the number of list elements. List elements may be lists themselves. These lists within a list are counted as a single list element.

Syntax: length list

+   - length Returns the length of a list

+   - list The list

The index command returns a list element referenced by its position in the list.

Syntax: index list index

+   - index Returns a list entry

+   - list The list