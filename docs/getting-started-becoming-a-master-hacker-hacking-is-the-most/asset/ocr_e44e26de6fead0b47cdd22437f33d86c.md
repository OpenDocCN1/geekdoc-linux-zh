```
root@kali-2019:~ # shred -f .bash history
root@kali-2019:~ # cat .bash history
```

kali > shred -h As we saw above, the user’s command history is viewable using the history command, but the command history is actually stored in the user’s profile file named .bash_history. We can shred that file by using the command: kali > shred -f .bash_history Now, when we go back and view the .bash_history, but can see nothing intelligible!

Kali > cat .bash_history 253 | P a g e

# ## Summar y

After compromising a system or network, the hacker needs to make certain that little or no evidence is left behind. A skilled and diligent digital forens ic investigator can recreate the events and determine what took place on the system. To remain stealthy, the hacker/pentester must make certain to remove any evidence of their activities. Most importantly, this includes removing any log files or command history files.

# ## Exercises

+   1. Use the clearev command to clear the event logs on a compromised Windows system from the meterpreter.