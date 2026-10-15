

![](img/0c1fc10350aa06ca92e7921c96c628ec_189_0.png)

**Figure 10-3** The who -aH command tells you who's on the system and what's going on

different version of this command—whoami as a single word. If yours does, it can help you find out what account you are actually logged in to right now.

## Is there a command I can use to get just the real logins of people using my machine?

Try who -f. This option strips out any pseudo terminals that would be included in the command, giving you just a list of actual logins. If you are running the X Window System, this can be a more meaningful result.

## How can I find out more about the people on my machine?

Use finger. This command, which isn't supported on all versions of UNIX, tells you about not only the people who are logged in to your machine, but how long they have been active on your system, what their real names are, and all sorts of other stuff as well. You can also use this in a network to get information about other people not currently logged in.

## How can I find out where I am?

Use the hostname command. If you work in a distributed environment and you often have to log in to other machines, it can be a nuisance to keep track of which machine you're on at any point. This is especially true if you're working in X Windows and have several different terminal windows open. Use this command to find out where you are. If you find yourself doing this a lot, add it to your prompt by putting a pair of lines like this in your .profile:

```
host=$(hostname)
PS1='$host:$PWD \$ '
```

You will then get a prompt like this:

```
rci:/users/charlie $
```

which gives you a constant reminder of who and where you are. If you like multiple-line prompts, just insert a ^J into the string in front of the \$ and you will get a nice two-line version of the prompt.

## What's the best way to communicate with my workgroup?

Use mail or one of the many improved versions of it. Actually, mail makes it almost as easy to communicate with your friends across the world as with your coworker in the next office. There are almost as many different improved versions of the basic mail program as there are versions of UNIX, but one that is widely available, easy to use, supports both text modes and graphics modes, and works on virtually any system is the elm package. Written by Dave Taylor, this program is available in the public domain (in other words, you don't have to pay for it or license it in any way). If you don't have it on your system, and the mail package you do have is hard to use, ask your system administrator to get a copy of elm. Everyone will be happier. It's available from a variety of anonymous ftp sites (more on what that means shortly), including tut.cis.ohio-state.edu.

### What are the r commands and what can they do for me?

The r commands are a group of remote commands that make life much easier on a local network. Plus, they provide some useful tricks on your own local machine since they have some options that the more traditional commands lack. The commands in this group are:

- **rcp** — The remote version of the **cp** command
- **rlogin** — Logs in to another machine
- **rcmd** — Executes a command remotely
- **rsh** — Same as **rcmd** on systems where it exists

These commands make it simple to move around, execute programs, and manipulate files in a distributed environment. On many systems, the **rsh** command is reserved for a restricted form of the Bourne shell, and on these systems the command is called **rcmd**. But in either case, they allow you to open a shell on a remote system and execute a series of commands that are then displayed on your system. The **rlogin** command allows you to log in to the remote machine and execute commands just as if you were sitting at a terminal connected to it. And the **rcp** command allows you to copy files or whole directory structures between machines.

### Can you give me an example of how to use rlogin?

Let's try using **rlogin** to work interactively on another machine. This command is perfect when you want to work on the other machine just as if it were your own workstation. The syntax is

```
rlogin remotehost [-l username]
```

Depending on how the system administrator has set up permissions, you may not even need to give a password on the remote machine. And if you have to do this often, and have accounts on both machines, you can—and should—create a .rhosts file on both machines that allows you to log in without a password. Your account on the remote machine doesn’t even have to have the same username, as long as the

