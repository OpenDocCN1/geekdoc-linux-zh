An example of using the `kill` command to restart a process is shown below.

```
# kill -1 408
```

Some processes occupy the shell until they are completed. These processes are said to run in the foreground. No other processes can be started at the shell until these processes are completed. Other processes are said to run in the background. When a process runs in the background, the shell is available so that new processes can be started while the background process is running. Whether a process runs in the foreground or background depends on the process and how it is started. Typically, commands run from the command line are run in the foreground. To start a command-line process in the background the `&` symbol is placed at the end of the command. The following is an example of starting the `netscape` process as a background process.

```
# netscape &
```

Running the process this way frees the shell to receive other commands while the `netscape` process runs. If you wish to move a current process from the foreground to the background another method is used. The `^Z` command will stop a process running in the foreground. Once the process has been stopped, it can be moved into the background using the `bg jobnumber` command. The jobnumber will be discovered using the `jobs` command. This command will display the processes currently running in the background as well as stopped jobs. An example of the correct use of these commands is as follows:

```
# netscape
^Z
# jobs
[2]- Stopped netscape
# bg 2
```

In the above example the `netscape` process is started and then stopped using the `^Z` command. The `jobs` command is then used to view the jobs currently running in the background as well as those that are stopped. Then the `bg` command is used to move the `netscape` process to the background.

It is also possible to move a process from the background to the foreground. This is done using the `fg jobnumber` command. To move the `netscape` process in the example above back to the foreground the following command would be used:

```
# fg 2
```