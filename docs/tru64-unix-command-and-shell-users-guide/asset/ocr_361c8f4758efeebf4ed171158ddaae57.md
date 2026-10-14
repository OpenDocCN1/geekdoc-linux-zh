# Table 7-7: Description of Example Shell Script (cont.)

| Shell Command | Description |
|---|---|
| #lss: list and sort | Comment line that describes the purpose of the shell procedure. |
| ls -l | sort -n +4 | These are the commands in the shell procedure. This procedure lists the files in a directory (ls -l). Output from the ls -l command is then piped to the sort command ( sort -n +4). This command skips over the first four columns of the ls -l output, sorts the fifth column (the file size column) numerically, and writes the lines to the standard output. |

a See Section 7.10.2 for more information.

To run the lss procedure, enter lss. Sample system output looks similar to the following:

```
$ lss
-rw-rw-rw- 1 larry system 65 Mar 13 14:46 file3
-rw-rw-rw- 1 larry system 75 Mar 13 14:45 file2
-rw-rw-rw- 1 larry system 101 Mar 13 14:44 file1
$
```

# 7.10.2 Specifying a Run Shell

At times, you may want to specify the shell where a shell procedure should run. This is because of possible syntactic differences between the shells, but is especially true of differences between the C shell and the other shells.

By default, the operating system assumes that any shell procedure you run should be executed in the same shell as your login shell. For example, if your login shell is the Korn shell, by default your shell procedures will run in that same shell.

The ability to override the default is very useful for shell procedures that many users run because it ensures that the procedure executes in the correct shell, regardless of the user's login shell. To change this default run shell, include the following command as the first line of the shell procedure:

```
#!shell_path
```

The shell_path entry specifies the full pathname of shell where you want the procedure to run.