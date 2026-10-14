
```
[me@linuxbox ~]$ source ~/.bashrc
```

After doing this, we should be able to see the effect of our changes. Try one of the new aliases.

```
[me@linuxbox ~]$ ll
```

## Summing Up

In this chapter, we learned an essential skill: editing configuration files with a text editor. Moving forward, as we read man pages for commands, take note of the environment variables that commands support. There may be a gem or two. In later chapters, we will learn about shell functions, a powerful feature that you can also include in the bash startup files to add to your arsenal of custom commands.

## 12 A GENTLE INTRODUCTION TO VI

![](img/314a0280bc10c5c0d45be132de172677_191_0.png)

There is an old joke about a visitor to New York City asking a passerby for directions to the city’s famous classical music venue.

Visitor: Excuse me, how do I get to Carnegie Hall?

Passerby: Practice, practice, practice!

Learning the Linux command line, like becoming an accomplished pianist, is not something that we pick up in an afternoon. It takes years of practice. In this chapter, we will introduce the vi (pronounced “vee eye”) text editor, one of the core programs in the Unix tradition. vi is somewhat notorious for its difficult user interface, but when we see a master sit down at the keyboard and begin to “play,” we will indeed be witness to some great art. We won’t become masters in this chapter, but when we are done, we will know how to play the equivalent of “Chopsticks” in vi.

### Why We Should Learn vi

In this modern age of graphical editors and easy-to-use text-based editors such as nano, why should we learn vi? There are three good reasons.

- vi is almost always available. If we have a system with no graphical interface, such as a remote server or a local system with a broken X configuration, this can be a lifesaver. nano, while increasingly popular, is still not universal. POSIX, a standard for program compatibility on Unix systems, requires that vi be present.
- vi is lightweight and fast. For many tasks, it's easier to bring up vi than it is to find the graphical text editor in the menus and wait for its multiple megabytes to load. In addition, vi is designed for typing speed. As we will see, a skilled vi user never has to lift their fingers from the keyboard while editing.
- We don’t want other Linux and Unix users to think we are cowards.

Okay, maybe two good reasons.

### A Little Background

The first version of vi was written in 1976 by Bill Joy, a University of California at Berkeley student who later went on to cofound Sun Microsystems. vi derives its name from the word “visual,” because it was intended to allow editing on a video terminal with a moving cursor. Previous to visual editors, there were line editors that operated on a single line of text at a time. To specify a change, we tell a line editor to go to a particular line and describe what change to make, such as adding or deleting text. With the advent of video terminals (rather than printer-based terminals like teletypes), visual editing became possible. vi actually incorporates a powerful line editor called ex, and we can use line editing commands while using vi.

Most Linux distributions don’t include real vi; rather, they ship with an enhanced replacement called vim (which is short for “vi improved”) written by Bram Moolenaar. vim is a substantial improvement over traditional Unix vi and is usually symbolically linked (or aliased) to the name vi on Linux systems. In the discussions that follow, we will assume that we have a program called vi that is really vim.

### Starting and Stopping vi

To start vi, we simply enter the following:

```
[me@linuxbox ~]$ vi
```

A screen like the following should appear.

```
~
~
~                VIM - Vi Improved
~                version 8.0.707
~                by Bram Moolenaar et al.
~                Vim is open source and freely distributable
~                Sponsor Vim development!
~                type :help sponsor<Enter>      for information
~                type :q<Enter>                 to exit
~                type :help<Enter> or <F1>      for on-line help
~                type :help version8<Enter>     for version info
~
~                Running in Vi compatible mode
~                type :set nocomp<Enter>        for Vim defaults
~                type :help cp-default<Enter> for info on this
~
~
~
```

### COMPATIBILITY MODE

In the example startup screen, we see the text “Running in Vi compatible mode.” This means that vim will run in a mode that is closer to the normal behavior of vi rather than the enhanced behavior of vim. For the purposes of this chapter, we will want to run vim with its enhanced behavior. To do this, you have a few options. Try running vim instead of vi. If that works, consider adding alias vi='vim' to your .bashrc file. Alternatively, use this command to add a line to your vim configuration file:

```
echo "set nocomp" >> ~/.vimrc
```
