```
```
$ echo $my_variable
I am Global now
$
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

Even though the child shell redefined and exported the variable **my_variable** , the parent shell's *my_variable* variable kept its original value.

# # Removing Environment Variables

Of course, if you can create a new environment variable, it makes sense that you can also remove an existing environment variable. You can do this with the *unset* command. When referencing the environment variable in the *unset* command, remember not to use the dollar sign:

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

**TIP**

**It can be confusing to remember when to use and when not to use the dollar sign with environment variables. Just remember this: If you are doing anything with the variable, use the dollar sign. If you are doing anything to the variable, don't use the dollar sign. The exception to**