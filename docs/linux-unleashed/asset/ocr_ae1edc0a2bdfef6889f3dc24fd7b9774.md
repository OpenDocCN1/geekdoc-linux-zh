particular process. You must know a process's PID to be able to kill it. Every process on the system has a PID, and the numbers range from 0 to 65,565 then restart from the beginning, making sure each number is used only once at any one time. Linux uses numbers instead of names for each process because it's faster and easier that way.

The **TTY** column shows you which terminal the process was started from. You will see your own terminal listed when you try the **ps** command.

The **STAT** column give the status of the process. The two most common entries in the status column are **S for sleeping** and **R for running**. A sleeping process is one that isn't currently active. However, don't be misled. A sleeping process might just be taking a very brief catnap! In fact, a process can switch between sleeping and running many times every second.

The **TIME** column shows the amount of system time used by the process. Clearly, neither of our processes is taking up any appreciable system time! That's often the case with modern machines, as most processes execute so quickly that the time column scarcely moves above a single digit.

Finally, the **NAME** column contains the name of the program you're running. This is usually the command you type at the command line. However, sometimes the command you enter starts one or more processes, called children, and in this case, you'll see these additional processes show up as well, without ever having typed them yourself. Your **login** shell will have a - before it, as in **-bash** in the previous example. This helps to distinguish this *primary* shell from any other shells you may enter from it. These will not have the - in front.

# ## Note

If you are logged in as *root*, you see a list of *all* processes on the system. This is because the *root* username, being the superuser, owns everything that happens on the Linux system.

If you are an "ordinary" user, but have also logged in on another terminal (including another virtual terminal you have selected by pressing Alt+Fn as discussed in Chapter 6, "Getting Started"), you see the processes you are running on the other terminal (or terminals), as well.

Don't be worried if you see slightly different columns of information when you use *ps*. The output tends to vary a little bit, especially with options in use, with different versions of Linux. The basic information is much the same, though.