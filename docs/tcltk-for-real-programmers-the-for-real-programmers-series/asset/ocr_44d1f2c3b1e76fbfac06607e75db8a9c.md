# 6.1 Arguments to Procedures

Note that args must be the last argument in the argument list to get the excess arguments assigned to it. If there are other arguments after the args argument, then args is treated as a normal argument.

In the following example, the procedure showArgs requires at least one argument. If there are more arguments, they will be placed in the variable args.

# Example 6.1.1-1

```
#
# A proc accepts a variable number of args
#
proc showArgs {first args} {
puts "first: $first"
puts "args: $args"
}
```

# Example Script

```
puts "Called showArgs with one arg"
showArgs oneArgument
puts "\nCalled showArgs with two args"
showArgs oneArgument twoArgument
puts "\nCalled showArgs with three args"
showArgs oneArgument twoArgument threeArgument
```

# Script Output

Called showArgs with one arg
first: oneArgument
args:

Called showArgs with two args
first: oneArgument
args: twoArgument

Called showArgs with three args
first: oneArgument
args: twoArgument threeArgument