
## The Getting Started Guide for Red Hat Linux 6.0

By now, of course, you've probably seen the word bash when you've mistyped commands at the shell prompt (as in bash: oops: command not found).

In Chapter 1, when we covered redirection and piping, we were also demonstrating the power of bash.

- **Tip:** You can learn more about bash by reading the bash man page. At the shell prompt, type man bash (or you can save the file as a text file by typing man bash | col -b > bash.txt, which you can then open to read with an editor like pico or a pager like less. You can also print the file with man bash | col -b | lpr, but be warned: it's a large file. If you want more information, O'Reilly & Associates publishes *Learning the bash Shell*, by Cameron Newham and Bill Rosenblatt.

Although your system came with several different shells, bash is the default shell for Red Hat Linux.

You might think of bash as a fleet-footed office assistant who has made a habit of keeping notes on ways to fulfill commands quickly. This assistant also keeps pointers on how you like to customize the way you work.

These “pointers” bash keeps are referred to as *environment variables*.

The shell uses an “environment” in the same way we use an environment, like a kitchen. We work in our kitchen, arrange pots, pans, and spices. We know where the dishes are, how things operate.

The same can be said for bash and its environment. There's a basic arrangement to bash as there would be to just about any kitchen. For example, we'd expect to see pots in a kitchen in the same way that we would expect to see certain commands in bash.

That's the idea behind environment variables.

As long as your assistant has the right pointers, he'll fulfill your commands quickly.

Let's take a look at our environment variables. At the shell prompt, type:

```
env
```

Quite a few “shortcuts” bash uses, aren’t there?

Each one of these helps bash customize the environment for you.

Among the most important environment variables is the PATH environment variable — which defines what is known as the default path.

The PATH environment variable for our account billy might look something like this:

```
PATH=/usr/local/bin:/usr/X11R6/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/billy/bin
```

It looks crowded, but the PATH statement is a great signpost, which points to where programs can be found.

- Tip: Remember the reference in the previous chapter to the FHS (Filesystem Hierarchy Standard)? The PATH statement is set according to that standard, and programs are installed in directories in accordance with the FHS as well. The end result is that the PATH statement will enable bash to automatically find nearly any program, assuming it has been installed in accordance with the FHS.

## Locating Files and Directories

There will be times when we know a file or directory exists but we won’t know where to find it. Searching for a file or directory can be made much easier with the locate command.

With locate, we’ll see every related file or directory which matches our search criterion. Let’s say we want to search for all files related to the finger command.

```
locate finger
```

The locate command uses a database to check for files and directories which match the string finger.

- Tip: To learn more about locate, read the locate man page by typing man locate at a shell prompt.

It’s a handy command which works very quickly — as long as the database is up to date. That database is automatically updated on a nightly basis, from cron. What’s cron? It’s a small program that runs in the background, performing various tasks — such as updating the locate database — at regularly scheduled intervals.

- Tip: cron is a daemon. Daemons handle tasks in the background. To read the cron man page, type man cron at the shell prompt.

So what happens if we:

- Have more than one operating system on our machine, and switch between them — causing us to halt and restart our Red Hat Linux system;
- Shutdown and turn off our machine at the end of the day.

This might mean that cron never has a chance to update the locate database. No problem. We can just update the database manually. Let’s give it a try.

First, su to root.

Now, at the shell prompt, type:

```
/etc/cron.daily/updatedb.cron
```

After a few minutes, the locate database will be current.

## Command History and Tab Completion

It doesn’t take long before the thought of typing the same command over and over becomes unappealing, at best.
