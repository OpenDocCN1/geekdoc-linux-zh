*script*, consists of shell commands to be executed in a shell, one command at a time, and is stored in an ordinary UNIX file. The shell allows use of a read/write storage place, known as a *shell variable*, for users and programmers to use as a scratch pad for completing a task. The shell also contains program control flow commands (also called *statements*) that allow nonsequential execution of the commands in a shell script and repeated execution of a block of commands—similar to high-level programming languages like C.

# 12.2 RUNNING A BOURNE SHELL SCRIPT

There are three ways to run a Bourne shell script. The first step for all three methods is to make the script file executable by adding the execute permission to the existing access permissions for the file. You can do so by running the following command, where *script_file* is the name of the file containing the shell script.

```
$ chmod u+x script_file
$
```

Clearly, in this case you make the script executable for yourself only. However, you can set appropriate access permissions for the file if you also want other users to be able to execute it. Once you have made the script file executable, you can type ./script_file as a command to execute the shell script, as shown:

```
$ ./script_file
... Output of the script if any ...
$
```

If your search path (the PATH variable) includes your current directory (.), you can simply use the *script_file* command, instead of using the ./script_file command. For the rest of this chapter, we assume that your PATH variable includes your current directory.

As described in Chapter 10, a child of the current shell process executes the script. Thus, with this method, the script executes properly if you are using the Bourne shell but not if you are using any other shell. If you are currently using some other shell, first execute the /bin/sh command to run the Bourne shell and then run the script_file command, as shown in the following example. Here, we assume that your current shell is C shell (with the % prompt). After the script has completed its execution, we press <Ctrl+D> to terminate the Bourne shell and return to C shell.

```
% /bin/sh
$ script_file
... Output of the script if any ...
$ <Ctrl+D>
%
```

The second method of executing a shell script is to run the /bin/sh command with the script file as its parameter. Thus, the following command executes the shell script in script_file.