# Starting a shell script

Shell scripts are written differently for different shells. This is important to remember if you use the more complex functions of scripting. The scripts in this section are geared toward bash, since it is the default shell for Linux and is the most used.

The first line of a shell script tells the system which interpreter to use. It begins with `#!`, which denotes the interpreter. An example is the following:

```
#!/bin/bash
```

There is no space anywhere in the line. This line should be found only once in any script. It tells the system that the `/bin/bash` interpreter should be used when executing. If a script is written for another interpreter such as the ksh shell, or perl, this line will be different. If you are unsure which language a script is written in, it is often useful to just check the first line.

> The first line of a shell script tells the system which interpreter to use when the script is run.

# Writing a basic script

You can start with a basic script, as shown in the following example. For this example, pretend that you do not know about aliases.

```
#!/bin/bash
# This is a simple script that can be used to display
# my documents in a folder, while pausing the output.
ls -al *.doc | more
```

As you can see, this is a simple script that runs `ls` with basic parameters. To make this script executable, you need to do the following:

```
chmod u+x script_name
```

`chmod` is covered in Chapter 6.

The script can also be run manually without making it executable. For example:

```
bash script_name
```

The `#` signs at the beginning of lines denote comments, except for the first line, which tells the system which interpreter to use. Be sure to use comments often in scripts so that later when editing them again, you can remember what you were doing.