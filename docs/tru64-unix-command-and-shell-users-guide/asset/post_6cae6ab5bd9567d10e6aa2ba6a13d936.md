
```
% source .cshrc
```

For complete information on using aliases with the C shell, see the csh(1) reference page.

## 8.2.6 Built-In Variables

The C shell provides variables that can be assigned values. These variables can be very useful for storing values that can be used later in commands. In addition, you can affect directly shell behavior by setting those variables to which the shell itself refers.

Table 8-6 describes selected C shell built-in variables that are of the most interest to general users. For a complete list of C shell built-in variables, see the csh(1) reference page.

**Table 8-6: C Shell Built-In Variables**

| Variable | Description |
|---|---|
| `argv` | Contains a value or values that can be used by the shell or shell scripts. |
| `cwd` | Contains the pathname to your current directory. The value of this variable changes every time you use the `cd` command. |
| `home` | Contains the pathname of your home directory. The default value for this variable is specified in the /etc/passwd file. |
| `ignoreeof` | Specifies whether Ctrl/D can be used to log out from the system. If set, you must use either `logout` or `exit` to log out. If unset, you may use Ctrl/D to log out. This variable is usually set in the .cshrc file. |
| `cdpath` | Specifies alternative directories to be searched by the system when locating subdirectories with the `cd`, `chdir`, or `pushd` commands. This variable is usually set in the .login file. |
| `noclobber` | Specifies whether a file can be overwritten. If set, places restrictions on output redirection `>` to ensure that files are not accidentally destroyed, and that `>>` redirections refer to existing files. If set, a file cannot be overwritten. This variable is usually set in the .cshrc file. |
| `notify` | Specifies whether you want to be notified when a background process has completed. If set, you are notified; if unset, you are not notified. This variable is usually set in the .cshrc file. |
| `path` | Specifies the search path that the shell uses to find commands. This variable is usually set in the .login file. |
| `prompt` | Can be used to customize your C shell prompt. This variable is usually set in the .cshrc file. |
| `shell` | Specifies the shell to create when a program creates a subshell. This variable is usually set in the `.login` file. |
| `status` | Specifies whether the most recently executed command completed without error (a value of zero is returned) or with an error (a nonzero value is returned). |

## 8.2.7 Built-In Commands

Table 8-7 describes selected C shell commands that are of the most interest to general users. For a complete list of C shell built-in commands, or for more information on the commands listed here, see the csh(1) reference page.

**Table 8-7: Built-In C Shell Commands**

| Command | Description |
|---|---|
| `alias` | Assigns and displays alias definitions.<sup>a</sup> |
| `bg` | Puts a suspended process in the background.<sup>b</sup> |
| `echo` | Writes arguments to the shell’s standard output. |
| `fg` | Puts a currently running background process in the foreground.<sup>b</sup> |
| `history` | Displays the contents of the command history buffer.<sup>c</sup> |
| `jobs` | Displays the job number and the PID number of current background processes.<sup>b</sup> |
| `logout` | Terminates the login session. |
| `rehash` | Tells the shell to recompute the hash table of command locations. Use this command if you add a command to a directory in the shell’s search path and want the shell to be able to find it. If you do not use `rehash`, the command cannot be executed because it was not in the directory when the hash table was originally created. |
| `repeat` | Repeats a command a specified number of times. |
| `set` | Assigns and displays shell variable values.<sup>d</sup> |
| `setenv` | Assigns environment variable values.<sup>d</sup> |
| `source` | Executes commands in a file. This can be used to update the current shell environment.<sup>e</sup> |
| `time` | Displays the execution time of a specified command. |
| `unalias` | Removes alias definitions.<sup>a</sup> |
