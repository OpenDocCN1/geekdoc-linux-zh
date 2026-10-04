# 3.3 Tcl Commands

index
The position of a list entry to return. The first element element 0. If this value is larger than the list, then an empty string is returned.

# Example 3.3.6-1

# List Commands Example

```
% set simpleList "This is a six element list"
This is a six element list
% puts "item 3 is [lindex $simpleList 3]"
item 3 is six
% lappend complex This
This:
% lappend complex "is a three element"
This (is a three element)
% lappend complex "list with internal lists"
This (is a three element) (list with internal lists)
% puts complex
This (is a three element) {list with internal lists}
% puts "complex has [ength $complex] members"
complex has 3 members
% puts "complex is [string length $complex] characters long"
complex is 52 characters long
% list "this" "creates a" "list"
this (creates a) list
% split "splitting, this string, on commas, creates a list" ",
splitting (this string) on commas { creates a list
```

# 3.3.7 Associative Array Commands

The associative array uses a string for an array index instead of a number. The associative array is a powerful construct in its own right and can be used to implement composite data types resembling the C struct or even a C++ class object. We'll say more about using associative arrays in Chapter 5.

A variable is denoted as an associative array by placing an index within parentheses after the variable name.