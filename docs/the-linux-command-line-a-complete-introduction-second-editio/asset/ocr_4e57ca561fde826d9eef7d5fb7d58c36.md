# 33
FLOW CONTROL: LOOPING WITH FOR

![](bbox=[0.35, 0.25, 0.65, 0.47])

In this final chapter on flow control, we will look at another of the shell's looping constructs. The for loop differs from the while and until loops in that it provides a means of processing sequences during a loop. This turns out to be very useful when programming. Accordingly, the for loop is a popular construct in bash scripting.

A for loop is implemented, naturally enough, with the for compound command. In bash, for is available in two forms.

# for: Traditional Shell Form

The original for command's syntax is as follows:

```
for variable [in words]; do
    commands
done
```

where variable is the name of a variable that will increment during the execution of the loop, words is an optional list of items that will be sequentially assigned to variable, and commands are the commands that are to be executed on each iteration of the loop.