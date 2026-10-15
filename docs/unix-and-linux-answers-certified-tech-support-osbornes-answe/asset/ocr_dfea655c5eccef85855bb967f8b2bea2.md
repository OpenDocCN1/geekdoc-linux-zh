sorts of other stuff as well. You can also use this in a network to get information about other people not currently logged in.

# How can I find out where I am?

Use the hostname command. If you work in a distributed environment and you often have to log in to other machines, it can be a nuisance to keep track of which machine you're on at any point. This is especially true if you're working in X Windows and have several different terminal windows open. Use this command to find out where you are. If you find yourself doing this a lot, add it to your prompt by putting a pair of lines like this in your .profile:

```
host=$(hostname)
PS1='$(hostname.*):$PWD \$ '
```

You will then get a prompt like this:

```
rci:/users/charlie $
```

which gives you a constant reminder of who and where you are. If you like multiple-line prompts, just insert a ^J into the string in front of the \$ and you will get a nice two-line version of the prompt.

# What's the best way to communicate with my workgroup?

Use mail or one of the many improved versions of it. Actually, mail makes it almost as easy to communicate with your friends across the world as with your coworker in the next office. There are almost as many different improved versions of the basic mail program as there are versions of UNIX, but one that is widely available, easy to use, supports both text modes and graphics modes, and works on virtually any system is the elm package. Written by Dave Taylor, this program is available in the public domain (in other words, you don't have to pay for it or license it in any way). If you don't have it on your system, and the mail package you do have is hard to use, ask your system administrator to get a copy of elm. Everyone will be happier. It's available from a variety of anonymous ftp sites (more on what that means shortly), including tut.cis.ohio-state.edu.