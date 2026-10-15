things, but when the compile or backup is done, you can quickly check to see where any problems were. Here we use a special way of describing the pipe of standard error.

```
make > /tmp/make.log 2>&1 &
```

This uses redirection to send normal messages from our **make** to a log file and any error messages will go to the same place. Here, **2>&1** means "take standard error and redirect it to standard output." But since we have already told standard output to go to a log file, both will go there.

# What can the tee command do for me?

Use **tee** to send output to both a log file and the screen. This lets you start a process, like a backup, where you want to be able to see if anything untoward happens but store all the messages from the command in a log file as well. This is particularly useful on a windowed system where you can continue to work and yet keep your eye on what's happening.

```
make 2>&1 | tee /tmp/make.log &
```

Now when your **make** hits a snag, you'll have the pleasure of watching all those lovely warning messages scroll by on the screen and you'll know they're saved to a log file. Later you can stare solemnly at them and pretend you actually know what they mean before you go twiddle with the **makefile** and try again.

> **Warning:** Don't use **nice** on a foreground job. If your system gets bogged down anyway and you have given your foreground job a **nice** command, you may not be able get its attention long enough to suspend or kill it. You'll essentially be locked out until the job finishes.

# SCHEDULING JOBS

# How can I put a job to sleep?

The simplest of the time-related commands is **sleep**. This command does just what its name implies—it puts commands or script files to sleep for the number of seconds