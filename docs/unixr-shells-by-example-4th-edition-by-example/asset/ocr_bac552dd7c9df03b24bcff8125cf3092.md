# # 1.7 Executing Commands from Scripts

When the shell is used as a programming language, commands and shell control constructs are typed in an editor and saved to a file, called a script. The lines from the file are read and executed one at a time by the shell. These programs are interpreted, not compiled. Compiled programs are converted to machine language before they are executed. Therefore, shell programs are usually slower than binary executables, but they are easier to write and are used mainly for automating simple tasks. Shell programs can also be written interactively at the command line, and for very simple tasks, this is the quickest way. However, for more complex scripting, it is easier to write scripts in an editor (unless you are a really great typist!). The following script can be executed by any shell to output the same results. Figure 1.15 and its following explanation illustrate the creation of a script called dot and how it fits in with already existing UNIX programs/utilities/commands.

# ## Figure 1.15 Creating a generic shell script.

![](bbox=[0.05, 0.42, 0.95, 0.72])

```
#!/bin/csh
echo hello
ls
who
cat
date
pwd
.
.
.
```

# ## EXPLANATION

+   1. Go into your favorite editor and type in a set of UNIX/Linux executables, one per line. Indicate what shell you want by placing the pathname of the shell after the #! on the first line. This program is being executed by the C shell and it is named dot.
+   
+   2. Save your file and turn on the execute permissions so that you can run it.
+   
+   3. Execute your program just as you would any other UNIX/Linux command.