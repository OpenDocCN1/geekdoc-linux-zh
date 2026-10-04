# Chapter 15. Tips and Techniques

```
puts "$name is an invalid index"
puts "Use one of [array names stateArray]"
}
""S" {
    if {[info exists $name]} {
        eval set $name $value
    } else {
        puts "$name is an invalid variable name"
    }
}
default {
    error "Unrecognized option: $arg"
}
}
```

# Use a single array for global variables.

Rather than use simple variables for global variables, group all the shared variables that a set of procedures will need in a single array variable.

This technique reduces the possibility of variable name collisions when you merge sets of code and makes it easy to add new variables when necessary without requiring changes to the global commands in all the procedures that will use the new value.

# Don't use this technique

```
proc initializeParameters {
    global height width linecolor
    set height 100
    set width 200
    set linecolor blue
}
```

# Use this technique

```
proc initializeParameters {
    global globalParams
    set globalParams(height) 100
    set globalParams(width) 200
    set globalParams(linecolor) blue
}
```