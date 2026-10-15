# 14.2 RUNNING A C SHELL SCRIPT

statements that allow the writers of shell scripts to implement multiway branching and repeated execution of a block of commands.

There are three ways to run a C shell script. The first step for all three methods is to make the script file executable by adding the execute permission to the existing access permissions for the file. You can do so by running the following command, where script_file is the name of the file containing the shell script.

```
% chmod u+x script_file
%
```

Clearly, in this case you make the script executable for yourself only. However, you can set appropriate access permissions for the file if you also want other users to be able to execute it. Once you have made the script file executable, you can type ./script_file as a command to execute the shell script, as follows:

```
% ./script_file
... Output of the script if any ...
%
```

If your search path (the path variable) includes your current directory (.), you can simply use the script_file command, instead of using the ./script_file command. For the rest of this chapter, we assume that your path variable includes your current directory.

As described in Chapter 10, a child of the current shell process executes the script. Thus, with this method, the script executes properly if you are using the C shell but not if you are using any other shell. If you are currently using some other shell, first execute the /bin/csh command to run the C shell and then run the script_file command, as shown in the following example. Here, we assume that your current shell is the Bourne shell (with the $ prompt). After the script has completed its execution, we press <Ctrl+D> to terminate the Bourne shell and return to the C shell.

```
$ /bin/csh
% ./script_file
... Output of the script if any ...
% <Ctrl+D>
$
```

The second method of executing a shell script is to run the /bin/csh command with the script file as its parameter. Thus, the following command executes the shell script in script_file.

```
% /bin/csh script_file
... Output of the script if any ...
%
```