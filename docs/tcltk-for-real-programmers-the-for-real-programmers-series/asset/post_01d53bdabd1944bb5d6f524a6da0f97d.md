
## 3.3 Tcl Commands

of the field in characters, and the second represents the number of digits to the right of the decimal point to display for floating-point formats.

+   The format definition is the last character. It must be one of:

-   c The argument should be a decimal %c 65 integer. Replace the field with the ASCII character value of this integer.

-   d The argument should be a decimal %d 0xff 255 integer. Replace the field with the decimal representation of this integer.

-   e The argument should be a numeric %e 0xffff 2.550000e+02 value. Replace the field with the scientific notation representation of this integer.

-   f The argument should be a numeric %f 1.234 value. Replace the field with the decimal fraction representation.

-   g The argument should be a numeric %g 1.234e2 value. Replace the field with the scientific notation or floating-point representation.

-   o The argument should be an integer %o 0xf value. Replace the field with the octal representation of the argument.

-   s The argument should be a string %s 0xf value. Replace the field with the argument.

-   u The argument should be an integer %u -1 429497295 value. Replace the field with the decimal representation of this integer treated as an unsigned value.

-   x The argument should be an integer %x -1 ffffffff Replace Replace the field with the hexadecimal representation of this integer.

## Chapter 3. Introduction to the Tcl Language

The following example shows how you might use the string match, string first, and string tolower case commands to check for certain fields in a set of data. In this case, the data is a list of field names and values separated by colons, similar to the export format of a spreadsheet or database program.

### Example 3.3.5-1

### String and Format Command Examples

```
% set dataString "field4:Value4:Field1:Value1:FIELD2:
VALUE2:field3:value3"
field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3

if [[match *FIELD2* $dataString]] {
    puts "Matched FIELD2 in dataString"
}
Matched FIELD2 in dataString
% set lowercaseDataString [string tolower $dataString]
field1:value1:field2:value2:field3:value3

if [[string first field2 lowercaseDataString] != -1] {
    puts "Found field2 in lowercaseDataString"
}
Found field2 in lowercaseDataString

for {set i 1} {$i < 5} incr i {
    set srch [format "field&%d" $i]
    set position($i) [string first $srch $dataString]
    if {$position($i) != -1] {
        puts "$srch is found in dataString"
    } else {
        puts "$srch is NOT found in dataString"
    }
}

field1 is NOT found in dataString
field2 is NOT found in dataString
field3 is found in dataString
field4 is found in dataString

% if {$position(3) > $position(4)} {
    puts "field3 is after field4"
} else {
    puts "field4 is after field3"
}
```

## 3.3 Tcl Commands

field3 is after field4

```
% # The next code splits field3:value3 from the dataString
# And then splits the value3 from the Field/Value pair
#
set x [string range $dataString $position(3) end]
field3:value3
set separator [string first "":" $x]
incr separator
set value [string range $x $separator end]
value3
```

### 3.3.6 List Processing Commands

A list is an ordered set of strings. Lists may be arbitrarily long, and list members can be arbitrarily long. Lists members may be single words or lists. The elements of a list are separated by spaces. If a list element contains a space, then that element is grouped with braces ({}).

A list can be created in several ways:

-   By using the set command to assign a list to a variable
-   By grouping several arguments into a single list element with the lapp command
-   By appending data to an unused variable with the append command
-   By splitting a single argument into list elements with the split command

The list command takes several units of data and combines them into a single list. It adds whatever braces may be necessary to keep the list members separate.

Syntax: list element1 ?element2? ... ?elementN?

```
list      Joins the arguments into a list
member    A unit of data to become part of the list
```

## Chapter 3. Introduction to the Tcl Language

The append command appends new data to a list, creating and returning a new, longer list. Note that this command will modify the existing list, unlike the string tolower command, which returns new data without changing the original.

Syntax: append listName ?element1 ... ?elementN?

-   append Joins the arguments into a list
-   listName The name of the list to append data to
-   member A unit of data to add to the list

The split command returns the input string as a list. It splits the string wherever certain characters appear. By default, the split location is a space.

Syntax: split data ?splitChar?

-   split Joins the arguments into a list
-   data The data to split
-   ?splitChar An optional character to split

The length command returns the number of elements in a list. Note that this is the number of elements.

Syntax: length list

-   length Returns the number of elements
-   list The list

The index command returns a list element referenced by its position.

Syntax: index list

-   index Returns a list element
-   list The list

## 3.3 Tcl Commands

index
The position of a list to return. If this is larger than the list, then an empty string is returned.

### Example 3.3.6-1

### List Commands Example

```
% set simpleList "This is a element list"
% set dataString "field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3"
field4:Value4:Field1:Value1:FIELD2:VALUE2:field3:value3

if [[match *FIELD2* $dataString]] {
    puts "Matched FIELD2 in dataString"
}
Matched FIELD2 in dataString
% set lowercaseDataString [string tolower $dataString]
field1:value1:field2:value2:field3:value3

if [[string first field2 lowercaseDataString] != -1] {
    puts "Found field2 in lowercaseDataString"
}
Found field2 in lowercaseDataString

for {set i 1} {$i < 5} incr i {
    set srch [format "field&%d" $i]
    set position($i) [string first $srch $dataString]
    if {$position($i) != -1] {
        puts "$srch is found in dataString"
    } else {
        puts "$srch is NOT found in dataString"
    }
}

field1 is NOT found in dataString
field2 is NOT found in dataString
field3 is found in dataString
field4 is found in dataString

% if {$position(3) > $position(4)} {
    puts "field3 is after field4"
} else {
    puts "field4 is after field3"
}

```

% # The next code splits field3:value3 from the dataString
# And then splits the value3 from the Field/Value pair
#
set x [string range $dataString $position(3) end]
field3:value3
set separator [string first "":" $x]
incr separator
set value [string range $x $separator end]
value3
```

### 3.3.7 Associative Array Commands

The associative array uses a string for an array index instead of a number. The associative array is a powerful construct in its own right and can be used to implement composite data types resembling the C struct or even a C++ class object. A variable is denoted as an associative array by placing an index within parentheses after the name.

### Example 3.3.7-1

### Array Example

```
set count(apple) 5
set count(pear) 3
set cost(apple) .10
set cost(pear) .15
set total(apple) [expr $count(apple) * $cost(apple)]
set total(pear) [expr $count(pear) * $cost(pear)]
puts "Fruit Bill: [expr $total(apple) + $total(pear)]";
```

Script Output

Fruit Bill: 0.95

As with lists, there is a set of commands for manipulating associative arrays. You get a list of indices for an array, get listing of array indices and values, set array indices and values, or step through an array. Like the string commands, the array commands are arranged as a set of subcommands of the array command.

The command array names returns a list of the indices that exist for a given array name.

Syntax: array names arrayName ?pattern?

-   array Defines this as an array command.
-   names Returns a list of the indices used in this array.
-   arrayName The name of the array.
-   pattern If this option is present, array names will return only indices that match the pattern. Otherwise, array names returns all the indices.

The array get command returns a list of array indices and the associated values.

Syntax: array get arrayName

-   array Defines this as an array command.
