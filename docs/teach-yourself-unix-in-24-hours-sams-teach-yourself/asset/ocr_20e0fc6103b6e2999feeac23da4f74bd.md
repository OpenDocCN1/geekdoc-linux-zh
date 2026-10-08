4. What happens if I try to automatically move to the background a program that has background input or output?

```
% vi & &
[1] 28258
%
```

This looks fine. Pressing Return indicates otherwise, though:

```
%
[7] + Stopped (tty output) vi
%
```

You can see that this program has stopped because of some information (output) that it wants to display. If the program expected input, the message would be Stopped (tty input) program name.

I can use fg to bring this program into the foreground and work with it, or even just to quit vi.

Because so much of the UNIX design focuses on running streams of data through filters and saving the output to a file, there are a number of commands that you could be running in the background, freeing you up to do work in the meantime. Remember also that you can put in the background jobs that take a fair amount of processing time and then display information on the screen. When it's time to write to the screen, the program will stop automatically until you enter fg to pull it into the foreground.

# Task 17.3: Finding Out What Tasks Are Running

There are two ways to keep track of what programs are flying around the UNIX operating system. The easier way, shows what processes you've stopped and moved into the background in the shell. Enter jobs, and each (or ksh) tells you what programs, if any, are running.

The alternative is a complex command called ps, which shows the processor status for the entire computer. The processor is another name for the computer itself. Unfortunately, any arguments, it shows the active or stopped programs with your terminal only. The ps program actually has more flags than is, I think. The vast majority of them, however, are never going to be of value to any normal UNIX user. Worse, the flags are different from BSD systems and System V. The ones that are most helpful are summarized in Table 17.1.

# Table 17.1. Useful flags to the ps command, BSD-style.

| Flag | Meaning |
| -a | Shows all processes associated with terminals attached to the system. |
| -g | Shows all processes on the system (that is, all processes other than required by the operating system). |

![](bbox=[0.66, 0.887, 0.143, 0.962])