# 3.3 Tcl Commands

get  Returns a list of the indices and values used in this associative array.

arrayName  The name of the array.

# Example 3.3.7-2

# Array Example

```
set fruit(apple.cost) .10
set fruit(apple.count) 5
set fruit(pear.cost) .15
set fruit(pear.count) 3
```

```
foreach item [array names fruit *cost] {
    set type [split $item "."] 0]
    puts "There are ${fruit($type)} units in stock"
    puts "The cost is ${fruit($item)} in stock"
    puts "The ${type} inventory is worth: \
    [expr $fruit($item) * $fruit($type.count)]"
}
```

```
puts ""
puts "Indices and values of fruit are:\n    [array get fruit]"
```

# Script Output

The cost for apple is .10
There are 5 units in stock
The apple inventory is worth: 0.5
The cost for pear is .15
There are 3 units in stock
The pear inventory is worth: 0.45

Indices and values of fruit are:
    apple.count 5 apple.cost .10 pear.count 3 pear.cost .15