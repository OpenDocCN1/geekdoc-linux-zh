**TABLE 3.2** Common top Options (continued)

| Option Name | Meaning |
| :--- | :--- |
| -n *iter* | You can tell top to display a certain number of updates (*iter*) and then quit. (Normally, top continues updating until you terminate the program.) |
| -b | This option specifies batch mode, in which top doesn't use the normal screen update commands. You might use this to log CPU use of targeted programs to a file, for instance. |

You can do more with top than watch it update its display. When it's running, you can enter any of several single-letter commands, some of which prompt you for additional information. Table 3.3 summarizes these commands.

**TABLE 3.3** Common top Interactive Commands

| Option Name | Meaning |
| :--- | :--- |
| h or ? | These keystrokes display help information. |
| k | You can kill (terminate) a process with this command. The top program will ask for a PID number and signal number, and if it's able to kill it, it will do so. (The upcoming section "Killing Processes" describes other ways to kill processes.) |
| q | This option quits from top. |
| r | You can change a process's priority with this command. You'll have to enter the PID number and a new priority value—a positive value will decrease its priority, and a negative value will increase its priority, assuming it has the default 0 priority to begin with. Only root may increase a process's priority. The renice command (described shortly, in "Restricting Processes' CPU Use") is another way to accomplish this task. |
| s | This command changes the display's update rate, which you'll be asked to enter (in seconds). |
| p | This sets the display to sort by CPU usage, which is the default. |
| M | You can change the display to sort by memory usage with this command. |