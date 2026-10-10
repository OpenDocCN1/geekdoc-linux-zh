TABLE 30.1 continued
| Variable | Meaning |
| :--- | :--- |
| # | The number of positional parameters. |
| ? | The exit status of the most recently executed command. |
| $ | The process-ID of the shell. |
| 0 | The name of the shell script. |
| n | The nth positional parameter. |

If you invoke a shell script with additional arguments, the extra arguments are called positional parameters. Create a shell script called `paramtest` with the following contents:

```
```
#!/bin/sh
echo "My name is $0"
echo "My process-ID is $$"
echo "I have $# positional parameters."
n=0
for PARAM in "$@" ; do
n=`expr $n + 1`
echo "Parameter $n: $PARAM"
done
echo "Here is a random number: $RANDOM"
echo "The previous echo command exited with status: $?"
```
```

Now test the script:

```
```
$ sh paramtest one "two and a" three
My name is paramtest
My process-ID is 1363
I have 3 positional parameters.
Parameter 1: one
Parameter 2: two and a
Parameter 3: three
Here is a random number: 13011
The previous echo command exited with status: 0
```
```

Your output will differ slightly; the process-ID and random value should be different. The previous example illustrates several of the shell’s built-in variables and parameters. Consult the `bash(1)` manual page and the `bash` info page for more details.

# ## Functions

The shell allows you to define functions, which are lists of shell commands. When you have defined a function, you can call it as if it were a normal shell command. During the execution of a function, the positional parameters take on the values of arguments passed to the function call.