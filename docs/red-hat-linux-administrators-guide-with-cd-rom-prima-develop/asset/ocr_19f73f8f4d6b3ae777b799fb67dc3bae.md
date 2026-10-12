# ## Defining ps variables

The preceding definitions are based on the sample output in Listing 7.1. In the last line of Listing 7.1, you can see that the ps auxw command listed in the last field is the command that requested the process that generated the output. The process was executed by the user kjkoo and was given a PID of 3384. It took up 0 percent of the CPU but consumed 1.1 percent of the available physical memory. The virtual size of the process was 2360 kilobytes. The resident set size, or amount of physical memory used, was 732. The process was run from a pseudoterminal located on another machine from which the command was issued. It had the identifying number of pts/7. The other terminals, or ttys, as listed in the ps output were issued locally on the Linux machine itself. The start time for the process was 14:14 hours, or 2:14 p.m. It used up 0:00 time on the CPU at the time that the snapshot was taken. It obviously did use some CPU time earlier, but when the ps aux command was executed, the process had already completed its required CPU time.

A quick glance through the other processes in Listing 7.1 finds that the main system processes all begin with a PID less than 10. The output also shows what day the machine was started. Once a process has been alive for more than 24 hours, the output simply states the day that the process began rather than the hours it has been alive. Most of the processes are also in a sleep state. This is the default state when processes are not executing instructions. All the processes required to operate a Linux system do not need to run continuously and there can be lag times. During these periods of inactivity, they enter a sleep state until they are called again to perform their task.

# ## Narrowing Down Process Searches

Because each Linux box can run more processes than a single terminal window can display, the method of displaying all the processes and then scrolling through all the entries is to invoke the pipe (|) command along with the more or less options. Here's an example command:

```
ps aux | more
```

This command enables you to press either the space bar or the Enter key to paginate through all the entries. The pipe command is very versatile and allows you to use other functions as well for locating specific processes.