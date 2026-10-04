# Chapter 5. Using Lists and Arrays

Syntax: join ?joinString?
join Join the elements of a list into a single string.
?joinString Use this string to separate list elements. Defaults to a space.

The lreplace command will replace one or more list elements with new elements or can be used to delete list elements.

Syntax:lreplace list first last ?element element ...?
lreplace Return a new list with one or more elements replaced by zero or more new elements.

+   list The original list.
first The position of the first element in the list to be replaced.
last The position of the last element in the list to be replaced.
element A list of elements to replace the original elements. If this list is shorter than the number of fields defined by first and last, elements will be deleted from the original list.

# Example 5.1.1-1

# Position-Oriented Data Example

```
# Set up a list
lappend data [split KEY1:Flynt:Clif:clif@cflynt.com :];
lappend data [split KEY2:Doe:John:jxd@example.com :];
lappend data [split KEY3:Doe:Jane:janed@example.com :];

# data Flynt is a list of lists.
# {(KEY1 Flynt Clif@cflynt.com}
# {KEY2 Doe John jxd@example.com) ...}

# Find the record with KEY2
set position [lsearch $data "KEY2 *"]
```