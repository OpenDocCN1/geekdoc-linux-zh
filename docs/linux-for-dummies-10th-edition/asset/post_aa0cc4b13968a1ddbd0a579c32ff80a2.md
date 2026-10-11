
## In This Chapter

- Understanding the user shell environment
- Customizing the bash environment
- Working with commands, wildcards, long commands, variables, redirections, and pipes

# Chapter 16

## Working without the GUI

Many computing old-timers speak fondly of the command line. Others who developed their skills by pointing and clicking refer to the command line as some antiquated tool used by crusty old-timers. The truth is that most skilled computing professionals recognize the merits of both the point-and-click graphical user interface (GUI), and the “lots of typing” command line interface (CLI). You must understand that the command line provides a powerful force for operating your computer. If you ever watch over the shoulder of a skilled Linux geek, you notice that, after logging in, the geek doesn’t take long to start tapping seemingly cryptic instructions by hand.

In this chapter, I explore the Linux program that provides the CLI, which is called the bash shell. Although many shells are available for Linux, bash is the most common, and for good reason. Basically, the creators of bash rolled many good features of other shells into one terrific package.

Each shell has its own way of handling commands and its own additional set of tools. I start by explaining what a shell really is, and when you understand that, you’re ready to get down and dirty with bash. I cover specifically what you can do with some of the best features of the bash shell. Then I continue with working at the command prompt and get into bash shell interior decorating.

Shells come equipped to perform certain functions. Most of these features have evolved over time to assist the command-line jockey with myriad tasks. I only scratch the surface here, and I encourage you to read the man page for bash because it’s likely one of the more complete and readable man pages in existence. You can read all about how to use man pages (the online Help system in Linux) in the "Help!" section, later in this chapter.

![](img/577d3bff979ee86b07f9836e0df274ce_320_0.png)

## Playing the Shell Game

You need a way to tell the computer what you want it to do. In Linux, one of the ways to communicate with the computer is through something called the shell. A shell isn’t a graphical thing; it’s the sum total of the commands and syntax you have available to you to do your work.

The shell environment is rather dull and boring by graphical desktop standards. When you start the shell, all you see is a short prompt, such as a $, followed by a blinking cursor awaiting your keyboard entry.

The default shell used in Linux is the *bash* shell. This work environment is based on the UNIX shell, which is called the Bourne shell and is also referred to as *sh*. The term *bash* stands for the Bourne again shell. The *bash* shell comes with most Linux distributions.

### Getting a shell

You can start a *bash* session by using a terminal application in your GUI desktop. The terminal application you use depends of course on your desktop:

- **Terminal** is the default terminal used in the GNOME 3 desktop. To start it, select the Terminal icon from the application launcher, or if you don’t see it, type Terminal in the Search text box. After you start Terminal, you see the interface, as shown in Figure 16-1.
- **Konsole** is the default terminal used in the KDE Plasma desktop. To start it, choose K menu ⚙ Applications ⚙ System ⚙ Konsole. The Konsole interface is shown in Figure 16-2.

Notice the prompt in the middle of the window — that’s the shell command line prompt. You enter your commands there.

Both Terminal and Konsole have a few additional cool features that can come in handy, such as cutting and pasting text, and changing the color of the text and background. You can even go old-school and have green text on top of a black background — just like the computer terminals you see in the old ‘70s movies!

![](img/577d3bff979ee86b07f9836e0df274ce_322_0.png)
![](img/577d3bff979ee86b07f9836e0df274ce_322_1.png)
![](img/577d3bff979ee86b07f9836e0df274ce_322_2.png)

If you use your shell prompt quite a bit like I do, add the terminal window to your favorites icons. See Chapters 4 and 5 to do so.

### The shell prompt

Often, our shell prompt includes helpful information. For example, if you’re logged in as rich on the machine testbox in Ubuntu, your prompt looks like this:

```
rich@testbox:~$
```

The tilde character (~) indicates that I'm in my Home folder (see Chapter 7). The dollar sign indicates that the bash shell is ready for me to enter a command.

Before surveying a few of the shell capabilities, I need to tell you about another method for starting a shell session. You may not use it much but you might find it helpful at some point. First of all, notice that your shell prompt is merely inside a window that is part of your GUI desktop. Suppose that you want your whole screen to be text only.

Each Linux distribution starts one or more virtual terminals when they boot. Each virtual terminal acts like a separate physical terminal, providing a separate shell. To switch to a different virtual terminal, press Ctrl+Alt+F#, where # is a virtual terminal number from 1 to 8. The trick, though, is that different Linux distributions place their default graphical shell on different virtual terminals (for example, Ubuntu uses terminal 2, while openSUSE uses terminal 7).

Use the Ctrl+Alt method to switch around between the different virtual terminals. Don't be alarmed when your familiar graphical desktop disappears. It's still running in the background, and you can get back to where you left off in a moment. Once you find a text-based virtual terminal, take a look at the screen layout.

You probably see something like this:

![](img/577d3bff979ee86b07f9836e0df274ce_323_0.png)

Go ahead and type your username and password, which you're prompted for. You see a message indicating your last login date followed by the bash prompt:

![](img/577d3bff979ee86b07f9836e0df274ce_323_1.png)

Notice the similarity between this prompt and the open window you left behind in the GUI desktop. Both prompts are an indication that you have a bash session open. Note that, although it's accurate to say they're both the results of using the bash shell, they're distinct and separate instances of the same program. In other words, the environment you're working with here is exclusive of the bash environment you still have open in the GUI terminal window.

Are you wondering where your GUI desktop has gone? Just to settle your nerves a bit, do some jumping around between the virtual terminals. Most of the virtual terminals provide a text-based login, while one or two provide the graphical desktop environment. Just find the one where your original desktop session was located and switch to that. Within a second or two, your screen should flash and return you to your graphical desktop. Neat, huh? And guess what? The bash session you left open on the other virtual terminal is still there; you never logged out.

Go back again to it by pressing the Ctrl+Alt plus the function key for that virtual terminal session. Voilà! — right where you left it. Feel free to jump back and forth a few times and try some other VTs (F1 through F8). Whoopee! This virtual terminal stuff rocks.

If you use the Lock Screen tool for your desktop (discussed in Chapters 4, 5, and 6), only your GUI session is locked. Anyone could use Ctrl+Alt to move to a virtual terminal. So, make sure you log out of your virtual terminals before walking away from your computer.

Okay, when you have grown weary and bored with this little trick, exit (literally, type exit) to log out from each VT you may have opened and press the appropriate Ctrl+Alt shortcut to return to the graphical desktop and your bash prompt. Then you can explore what all the fuss is about with this shell doohickey.

## Understanding bash Command Syntax and Structure

Many people happily skip through their Linux use without understanding the fundamentals of commands in the bash shell. Note that this approach makes you lose out on some cool capabilities available in bash. The more you know about how this shell's “language” works, the more interesting things you can do with it.

The basics of using bash at the command prompt often involve typing a command and any of its flags and values. For example, you enter the `ls -la ~` command to see a long-format listing of all files in your home directory, including those that start with a dot (.), which are hidden files. That other mysterious squiggle character is technically called a tilde. The tilde is a bash shortcut character that points to a user’s home directory. For this example, I merely list the contents of my home directory.

You can break a command into three distinct components:

- The command name
- The options or flags
- The arguments

Consider this example.

Start with a simple command. The du command (short for disk usage) lists the contents of the directory you're now in, and its subdirectories, and how much
