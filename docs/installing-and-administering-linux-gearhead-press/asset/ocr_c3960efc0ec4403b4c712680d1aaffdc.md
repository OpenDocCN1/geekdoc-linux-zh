```
$ now=$(date)<Enter>
```

Now, he checks to see whether the variable works:

```
$ echo $now<Enter>
Mon Jul 16 16:14:34 CST 2001
```

Note that you can carry out the command only once. The result is then available for use until the variable is removed or reassigned.

# Changing Variable Settings with the unset Command

At some point, you might no longer need or want some variables. To remove them, you use the unset command as follows:

```
$ unset variablename<Enter>
```

After using unset, it is a best practice to check that the variable is indeed gone by echoing it (do not forget to add the dollar sign):

```
$ echo $variablename<Enter>
```

It will seem to you that the shell did not react to the command. But that lack of a response is a good thing. The shell is telling you that variablename no longer has a value set for it.

> **NOTE** Similar to `echo $variablename`, you can also unset variablename on variables whose values were set through command substitution.

# Example 11.6 Changing Variable Settings with the unset Command

After creating the variable abc and assigning the value “day” to it, Juana finds that she does not use the variable as much as she thought she would and that the syntax is a little cumbersome those few times she uses it. So, she decides to remove abc. Then, she checks to see whether it has really been removed.

```
$ unset abc<Enter>
$ echo $abc<Enter>
```