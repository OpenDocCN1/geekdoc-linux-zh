+   7. Create a subshell.

```
$ bash<Enter>
```

Check to see what value the x variable holds in the subshell.

```
$ echo $x<Enter>
```

What is the value of x? List the subshell’s current variables.

```
$ set<Enter>
```

Do you see a listing for x?

+   8. Return to your parent process.

```
$ exit<Enter>
```

Set the value of the x variable so that its value will be inherited by your child processes.

```
$ export x=10<Enter>
```

Verify by creating a subshell and checking the value of x in the subshell.

```
$ bash<Enter>
$ echo $x<Enter>
```

+   9. Change the value of x in the subshell to 200.

```
$ x=200<Enter>
```

Verify that the value was changed.

```
$ echo $x<Enter>
```