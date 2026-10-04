# Chapter 15. Tips and Techniques

# A procedure to call the variable changing procedure,
# to demonstrate getting information further up the
# call stack.


```
proc otherProc (newVal) {
    modifyVariable $newVal
}
```

# A variable to watch.
#

```
global tracedVariable
#
```

# Create a trace on the tracedVariable variable
# trace variable tracedVariable w traceProc

# Now, modify the variable, twice within procedures,
# and once from the global scope.


# This will modify the variable two levels deep
# in the call stack.

otherProc One
# This will modify the variable one level down the call stack.
modifyVariable 'Two'

# Notice that the change from global scope reports itself as
# coming from the 'traceproc' command

setTracedVariable Three

# Script Output

```
Variable tracedVariable is being modified in:
    'modifyVariable One'
Which was invoked from: 'otherProc One'
The current value of tracedVariable is: One
```

```
Variable tracedVariable is being modified in:
    'modifyVariable Two'
```