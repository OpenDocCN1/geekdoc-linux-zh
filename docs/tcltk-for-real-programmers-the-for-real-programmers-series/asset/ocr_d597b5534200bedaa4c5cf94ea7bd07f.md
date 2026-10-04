# Chapter 6. Procedure Techniques

```
# The next line prints out
#"The globalVar contains: I'm global"
puts "The globalVar contains: $globalVar"

proc badProc() {
  set globalVar "This 'globalVar' in the local scope"

  # The next line causes an error
  globalVar
}
```

When a procedure is evaluated, it creates a local scope. Variables are created in this scope as necessary and are destroyed when the procedure returns. The variables used within a procedure are visible to other procedures called from that procedure but not to procedures outside the current stack.

When a new procedure is defined within a procedure, the new procedure is defined in the global scope and is not deleted when the procedure that defines the new procedure returns.

Each time a procedure invokes another procedure, another local scope is created. These nested procedure calls can be viewed as a stack, with the global scope at the top and each successive procedure call stacked below the previous ones.

A procedure can access variables within the global scope or within the scope of the procedures that invoked it via the upvar and uplevel-commands. The upvar command will link a local variable to one in a previous (higher) stack scope.

# Example 6.5.1-1

# Example Script

```
proc top {topArg} {
  set localArg [expr $topArg+1]
  puts "Before calling bottom localArg is: $localArg"
  bottom localArg
  puts "After calling bottom, localArg is: $localArg"
}

proc bottom {bottomArg} {
```

158