Working with ps Don't be alarmed if your ps command doesn't return exactly these results. This is one of the places where different versions of UNIX have commands that are similar, but not identical. The ps command has many options for formatting its display, so you might want to take a look at the man page for your system.

If you run ps and see this result, it means that these are all the commands you currently have running. The columns are the system process ID (PID), the controlling terminal, the status of the process (running, sleeping, and so on), and the process itself. These are just the processes that you own. If you want to see everything anybody is running, try running ps -ax—this lists all the users' processes (-a) and all processes that don't have a controlling terminal (-x). If this doesn't work, then try ps -ef The ps command has a huge number of options that can return tons of information. Take a look at the man page for more information. The primary concern right now is that you can list what you have running on the system and get your process IDs.

# KILLING A PROCESS: kill, kill, kill!

*Killing might sound a bit harsh for ending a process, but it does sum up the result quite nicely. When you kill a process you stop whatever it is doing, no matter what. If you're editing a file, you risk losing the entire file if you kill the process instead of exiting out of the editor normally.*

# USING kill

Although the kill command is mainly used to stop processes, it can also be used to send signals to a process. SIGKILL is one such signal, but there are others that are less severe. Depending on the signal that you send, the process might reload its configuration files and reinitialize itself. This is extremely nice when you're running something such as a Web server and need to add a MIME-type or change some server option without shutting down the server. To see a list of the signals that you can send using kill, invoke the command with kill -l, as follows: