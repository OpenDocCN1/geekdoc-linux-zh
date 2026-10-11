# 23 | LAB: Shell Scripting

**OBJECTIVES**

1. Basic Shell Scripts
2. Usage of Shell Scripts

**REQUIREMENTS**

1. FC6 or RHEL-5
2. Linux Distribution CDs/DVD

**CONCEPT**

Shell Script Basics

o A shell script is a plain-text file that contains shell commands. It can be executed by typing its name into a shell or by placing its name in another shell script.

o To execute a shell script file, you must meet some conditions, as follows:

o The file must have a special first line that names an appropriate command processor:

```
#!/bin/bash
```

If the preceding example does not work, then you need to find out the location of your executable Bash shell and substitute that location in the above example. You can also locate the Bash shell by using the following example:

```
$ whereis bash
```

o The file must be made executable by changing its permission bits by using the following example:

```
$ chmod +x (shell script filename)
```

o A shell script file may have an identifying suffix optionally, such as ".sh". This only helps the user to remember the types of files. The command processor is responsible to execute the file that uses the executable bit with the file's first line, to decide how to handle a shell script file.

o You can easily execute a shell script by using the following example:

```
$ ./scriptname.sh
```

The above example is a way to tell the command processor that the desired script is located in the current directory. Always remember that if you cannot run your shell script, you can provide its location as well as its name to run you shell script.