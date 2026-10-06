This generates the general exit status code of one, indicating an unknown error occurred in the command.

# The exit command

By default, your shell script will exit with the exit status of the last command in your script:

```
$ ./test6
The Result is 2
$ echo $?
0
$
```

You can change that to return your own exit status code. The exit command allows you to specify an exit status when your script ends:

```
$ cat test13
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$var1 + var2
echo The answer is $var3
exit 5
$
```

When you check the exit status of the script, you'll get the value used as the parameter of the exit command:

```
$ chmod u+x test13
$ ./test13
The answer is 40
$ echo $?
5
$
```

You can use variables in the exit command parameter:

```
$ cat test14
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$var1 + var2
exit $var3
$
```

When you run this command, it produces the following exit status:

```
$ chmod u+x test14
$ ./test14
```