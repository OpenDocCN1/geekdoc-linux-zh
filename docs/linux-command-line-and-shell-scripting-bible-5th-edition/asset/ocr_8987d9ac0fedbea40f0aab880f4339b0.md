After you set a local variable, it’s available for use anywhere within your shell process. However, if you spawn another shell, it’s not available in the child shell:

```
```
$ my_variable="Hello World"
$ bash
$ echo $my_variable

$ exit
exit
$ echo $my_variable
Hello World
$ 
```
```

In this example, a child shell was spawned via the bash command. The user-defined my_variable was not available in the child shell. This is demonstrated by the blank line returned after the echo $my_variable command. After the child shell was exited and returned to the original shell, the local variable was available.

Similarly, if you set a local variable in a child process, after you leave the child process, the local variable is no longer available:

```
```
$ echo $my_child_variable

$ bash
$ my_child_variable="Hello Little World"
$ echo $my_child_variable
Hello Little World
$ exit
exit
$ echo $my_child_variable
$ 
```
```

The local variable set within the child shell doesn’t exist after a return to the parent shell. You can change this behavior by turning your local user-defined variable into a global variable.

# ### Setting global environment variables

Global environment variables are visible from any child process created by the parent process that sets the variable. The method used to create a global environment variable is to first create a local variable and then export it to the global environment.

This is done by using the export command and the variable name (minus the dollar sign):

```
```
$ my_variable="I am Global now"
$ 
$ export my_variable
$ 
$ echo $my_variable
I am Global now
```
```