```
```
$ bash
$ export my_variable="Null"
$ echo $my_variable
Null
$ exit
exit
$
$ echo $my_variable
I am Global now
$
```
```

Even though the child shell redefined and exported the `my_variable` variable, the parent shell's `my_variable` variable kept its original value.

# ## Removing Environment Variables

Of course, if you create a new environment variable, it makes sense that you can also remove an existing environment variable. You can do this with the `unset` command. When referencing the environment variable in the `unset` command, remember not to use the dollar sign:

```
```
$ my_variable="I am going to be removed"
$ echo $my_variable
I am going to be removed
$
$ unset my_variable
$ echo $my_variable
$
```
```

**Tip**

It can be confusing to remember when to use and when not to use the dollar sign with environment variables. Just remember this: If you are doing anything with the variable, use the dollar sign. If you are doing anything to the variable, don't use the dollar sign. The exception to this rule is using `printenv` to display a variable's value, which does not require the dollar sign.

When dealing with global environment variables, things get a little tricky. If you're in a child process and unset a global environment variable, it applies only to the child process. The global environment variable is still available in the parent process:

```
```
$ export my_variable="I am Global now"
$ echo $my_variable
I am Global now
$
```
```