+   - Variables form part of the environment of a process.
+   - Processes cannot access or change variables in the environment of another process.

Example 12.5 illustrates these points.

# Example 12.5 Setting User-Defined Variables

Set a value of x in the bash shell:

```
$ x=4<Enter>
```

Now, create another bash subshell:

```
$ bash<Enter>
```

Search for the value of x in the subshell.

```
$ echo $x<Enter>
$
```

No record of x is found. So far, it looks like neither the variable nor its value was inherited. So, now, set the value of x in this subshell to 1:

```
$ x=1<Enter>
```

Exit from the bash subshell to the original bash shell and check the value of x.

```
$ <Ctrl>-d
$ echo $x<Enter>
4
```

The original value of 4 is returned. As expected, the subshell's variable x and its respective value 1 were not inherited backwards. They also had no effect on the original variable x and its value, 4.

# Exporting Shell Variables

In Chapter 11, “Shell Variables and the User Environment,” we encountered the export command when we discussed how to ensure that variables are inherited from the terminal environment to the shell environment.