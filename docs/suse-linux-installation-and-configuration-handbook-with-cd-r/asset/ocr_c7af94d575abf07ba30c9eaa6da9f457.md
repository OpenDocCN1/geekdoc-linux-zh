# Scripting in Bash

A script is a text file that contains commands for bash to execute. It is similar to writing a program, but is on a higher level. Bash scripts are similar to batch files in MS-DOS, for example.

To write a shell script, you must write the commands you want to execute in a text file and run that file. Let's look at an example of the simplest possible shell script to see how one is constructed. Using your favorite editor, enter the following in a new text file:

```
#!/bin/bash
ls
```

Save the file as myls and exit. Now, you can run this shell script in two ways—either by feeding it to bash or by making it executable. The following is an example of the first method:

```
$ bash myls
```

The previous command starts a new bash that will read your script and execute it. You can, however, make the script executable so you can run it as a normal program. To do that, you must change the permission of the file to be executable:

```
$ chmod u+x myls
$ myls
```

Now, the shell script will run as a normal program. When you run it, the first line in the file, #!/bin/bash, indicates that this file is a bash shell script. This is why you should make sure this line is the first line in the script. The actual script is really simple, it just runs the ls command.

You can add to the shell script to make it more complex, for example:

```
#!/bin/bash
clear
ls
```