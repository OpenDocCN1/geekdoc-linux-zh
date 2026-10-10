![](bbox=[0.14, 0.08, 0.88, 0.36])

Figure 13.2 Invoking shell scripts that are executable.

# Option 3: Invoking Scripts in the Same Shell

It is possible to force shell scripts to execute in the current shell instead of opening all the other subshells. You perform this task by altering the syntax to what is shown here:

```
$ . scriptfilename<Enter>
```

or

```
$ source script1<Enter>
```

In the first syntax example, the "." denotes “in the current shell.” The process will ultimately resemble that shown in Figure 13.3.

# Example 13.8 Invoking Scripts in the Same Shell

Freston tells Lady Molinera that she can save a few CPU cycles and some nanoseconds if she forces her script1 to execute in the same shell she is in now. But to prove it, he has her check her shell’s PID’s again, just like she did for Options 1 and 2.