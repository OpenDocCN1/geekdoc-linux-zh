**optional** Another way to deal with the issue of redirecting output of a command run by **sudo** is to use **tee** (page 162):

```
`$ ls | sudo tee /root/ls.sam`
```

```
`...`
```

This command line sends standard output of **ls** through **sudo** to **tee**, which copies its standard input to the file named by its argument and to standard output. If you do not want to display the output, you can have the nonprivileged shell redirect the output to **/dev/null** (page 503). The next example uses this technique to do away with the displayed output and uses the **-a** option to **tee** to append to the file instead of overwriting it:

```
`$ ls | sudo tee -a /root/ls.sam > /dev/null`
```

# OPTIONS

You can use command-line options to control how **sudo** runs a command. Following is the syntax of an **sudo** command line:

```
`sudo [options] command`
```

where **options** is one or more options and **command** is the command you want to execute. Without the **-u** option, **sudo** runs **command** with **root** privileges. Some of the more common **options** follow; see the **sudo man** page for a complete list.

+   - **-b** (background) Runs **command** in the background.

+   - **-e** (**edit**) With this option, **command** is a filename and not a command. This option causes **sudo** to edit the file named **command** with **root** privileges using the editor named by the **SUDO_EDITOR**, **VISUAL**, or **EDITOR** environment variable. Default is the **vi** editor. Alternatively, you can use the **sudoedit** utility without any options. Using this technique, the editor does not run with **root** privileges. See the tip on page 430.

+   - **-i** (**initial login environment**) Spawns the shell that is specified for **root** (or another user specified by **-u**) in /etc/passwd, running **root**'s (or the other user's) startup files, with some exceptions (e.g., TERM is not changed). See “Spawning a **root** Shell” on page 426 for an example.

+   - **-k** (**kill**) Resets the timestamp (page 429) of the user running the command, which means the user must enter her password the next time she runs **sudo**.

+   - **-l** (**list commands**) Lists the commands the user who is running **sudo** is allowed to run on the local system. Does not take a **command**.

+   - **-s** (**shell**) Spawns a new **root** (or another user specified by **-u**) shell as specified in the /etc/passwd file. Similar to **-i** but does not change the environment. Does not take a **command**.

+   - **-u user** Runs **command** with the privileges of **user**. Without this option, **sudo** runs **command** with **root** privileges.