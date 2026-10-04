# Chapter 3. Introduction to the Tcl Language

# Example 3.3.7-1

# Array Example

```
set count(apple) 5
set count(pear) 3
set cost(apple) .10
set cost(pear) .15
set total(apple) [expr $count(apple) * $cost(apple)]
set total(pear) [expr $count(pear) * $cost(pear)]
puts "Fruit Bill: [expr $total(apple) + $total(pear)]";
```

# Script Output

Fruit Bill: 0.95

As with lists, there is a set of commands for manipulating associative arrays. You get a list of indices for an array, get listing of array indices and values, set array indices and values, or step through an array.

Like the string commands, the array commands are arranged as a set of subcommands of the array command.

The command array names returns a list of the indices that exist for a given array name.

Syntax: array names arrayName ?pattern?

+   - array Defines this as an array command.
- names Returns a list of the indices used in this array.
- arrayName The name of the array.
- pattern If this option is present, array names will return only indices that match the pattern. Otherwise, array names returns all the indices.

The array get command returns a list of array indices and the associated values.

Syntax: array get arrayName

+   - array Defines this as an array command.