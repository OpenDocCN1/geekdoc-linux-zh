# Chapter 15. Tips and Techniques

within that procedure as info level -1 Tcl will generate an error, but if the info level command is invoked as info level 0 Tcl will return the procedure name and argument that invoked the procedure.

# Example 15.1-4

```
proc debugPuts {args} {
    global stateArray

    # If lower bit set, print the message(s)
    if {$stateArray(debugLevel) & 1} {
        puts "DEBUG Message: $args"
    }

    # If bit two is set, print the proc name and args
    # invoked debugPuts
    if {$stateArray(debugLevel) & 2} {
        set level [info level]
        incr level -1;
        puts "DEBUG Invoked from:: [info level $level]"
    }

    # If bit four is set, print the contents of stateArray
    if {$stateArray(debugLevel) & 4} {
        foreach index [array names stateArray] {
            puts "DEBUG: stateArray($index): $stateArray($index)"
        }
    }

    # If bit 8 is set, print the call stack
    if {$stateArray(debugLevel) & 8} {
        set level [info level]
        for {set l1 1} {$l1 < $level} {incr l1} {
            puts "DEBUG CallStack $l1: [info level $l1]"
        }
    }
}
```

# Example Script

```
proc topProc {arg1 arg2} {
    lowerProc three four five
}
```