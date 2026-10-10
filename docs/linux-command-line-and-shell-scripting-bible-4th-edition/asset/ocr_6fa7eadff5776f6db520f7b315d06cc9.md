# ## Controlling the Loop

You might be tempted to think that after you start a loop, you're stuck until the loop finishes all its iterations. This is not true. A couple of commands help us control what happens inside a loop:

+   * The `break` command
+   * The `continue` command

Each command has a different use in controlling the operation of a loop. The following sections describe how you can use these commands to control the operation of your loops.

# ## The `break` command

The `break` command is a simple way to escape a loop in progress. You can use the `break` command to exit any type of loop, including `while` and `until` loops.

You can use the `break` command in several situations. This section shows each of these methods.

# ### Breaking out of a single loop

When the shell executes a `break` command, it attempts to break out of the loop that's currently processing:

```
```bash
$ cat test17
#!/bin/bash
# breaking out of a for loop

for var1 in 1 2 3 4 5 6 7 8 9 10
do
    if [ $var1 -eq 5 ]
    then
        break
    fi
    echo "Iteration number: $var1"
done
echo "The for loop is completed"
$ ./test17
Iteration number: 1
Iteration number: 2
Iteration number: 3
```
```