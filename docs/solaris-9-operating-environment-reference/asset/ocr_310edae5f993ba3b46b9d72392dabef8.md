# w — Display Information About Currently Logged-in Users

**Synopsis**
/usr/bin/w [-hlsuw] [-user]

# Description

The command displays a summary of the current activity on the system, including what each user is doing. The heading line shows the current time, the length of the time system has been up, the number of users logged in to the system, and the average number of jobs in the run queue over the last 1, 5, and 15 minutes is a combination of w, time, and ps -.

The fields displayed are the user's login name, the name of the TTY the user is on, the idle time (that is, the number of minutes since the user last typed anything in hours:minutes), the CPU time used by all processes and their children on that terminal (in minutes:seconds), the CPU time used by the currently active processes (in minutes:seconds), and the name and arguments of the current process.

# Notes

The notion of the current process is unclear. The current algorithm is the highest-numbered process on the terminal that is not ignoring interrupts, or if there is none, the highest-numbered process on the terminal. This algorithm fails, for example, in critical sections of programs like the shell and editor or when faulty programs running in the background fork and fail to ignore interrupts. In cases where no process can be found, w prints -.