
mail waiting for you (see section Email). Finally, the system puts you in a shell—the environment in which you interact with the system and give it commands. Use of the default shell on most Linux systems, bash, is discussed in The Shell.

The dollar sign (` $ `) displayed to the left of the cursor is called the shell prompt; it means that the system is ready and waiting for input. (You can change this prompt to any text of your liking; to learn how, see section Changing the Shell Prompt.) By default, the shell prompt includes the name of the current directory, which it places to the left of the ` $ ` character. The tilde character (` ~ `), is a shell symbol that denotes the user's home directory—when you log in, you are in your home directory (these terms are defined in Files and Directories).

## 3.2.2 Logging Out of the System

To end your session on the system, type logout at the shell prompt. This command logs you out of the system, and a new login: prompt appears on your terminal.

- To log out of the system, type:

```
$ logout RET

Debian GNU/Linux 2.2 bardo tty1

bardo login:
```

What works equally well to typing the logout command is to just type C-d (hold down CTRL and press D). You don't even have to type RET afterwards. Many users prefer this quick shortcut.

Logging out of the system frees the terminal you were using—and ensures that nobody can access your account from this terminal.

If you are the only person using your system and have just ended a session by logging out, you might want to power down the system. See section Turning Off the System, earlier in this chapter.

## 3.3 Console Basics

A Linux terminal is a place to put input and get output from the system, and usually has at least a keyboard and monitor.

## The Linux Cookbook: Tips and Techniques for Everyday Use:

When you access a Linux system by the keyboard and monitor that are directly connected to it, you are said to be using the console terminal. (Linux systems can be accessed in other ways, such as through a network or via another terminal connected to a serial line; see section Communications).

Linux systems feature virtual consoles, which act as separate console displays that can run separate login sessions, but are accessed from the same physical console terminal. Linux systems are configured to have seven virtual consoles by default. When you are at the console terminal, you can switch between virtual consoles at any time, and you can log in and use the system from several virtual consoles at once.

The following recipes explain the basic things you will need to do with virtual consoles.

- 3.3.1 Switching between Consoles Switching between consoles.
- 3.3.2 Scrolling the Console Text Scrolling the text on the screen.
- 3.3.3 Keys for Console Manipulation Keystrokes for manipulating the console.

### 3.3.1 Switching between Consoles

To switch to a different virtual console, press ALT-Fn, where n is the number of the console to switch to.

- To switch to the fourth virtual console, press ALT-F4.

This command switches to the fourth virtual console, denoted by `tty4`:

```
Debian GNU/Linux 2.2 bardo tty4

bardo login:
```

You can also cycle through the different virtual consoles with the left and right arrow keys. To switch to the next-lowest virtual console (or wrap around to the highest virtual console, if you're at the first virtual console), press ALT-LeftArrow. To switch to the next-highest virtual console, press ALT-RightArrow. [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.]

- To switch from the fourth to the third virtual console, press:

```
ALT-LeftArrow
[GNU INFO BUG: any 60;62; in the preceding line should be the one of the cursor arrow ke
```

This keystroke switches to the third virtual console, `tty3`:

## The Linux Cookbook: Tips and Techniques for Everyday Use:

```
Debian GNU/Linux 2.2 bardo tty3
```

```
bardo login:
```

The seventh virtual console is reserved for the X Window System. If X is installed, this virtual terminal will never show a login: prompt, but when you are using X, this is where your X session appears. If your system is configured to start X immediately, this virtual console will show an X login screen.

You can switch to a virtual console from the X Window System using CTRL in conjunction with the usual ALT and function keys. This is the only console manipulation keystroke that works in X.

- To switch from X to the first virtual console, press:

```
CTRL-ALT-F1
```

### 3.3.2 Scrolling the Console Text

When you are logged in at a virtual console, new lines of text appear at the bottom of the console screen, while older lines of text scroll off the top of the screen.

- To view this older text, press SHIFT-PgUp to scroll back through it.

- Once you have scrolled back, press SHIFT-PgDn to scroll forward through the text toward the most recent text displayed on the console.

The amount of text you can scroll back through depends on system memory.

> NOTE: This technique is for scrolling through text displayed in your shell session (see section The Shell). It does not work for scrolling through text in a tool or application in the console—in other words, you can't use this technique to scroll through text that is displayed by a tool for perusing text files. To scroll through text in an application, use its own facilities for scrolling, if it has any.

### 3.3.3 Keys for Console Manipulation

Some keystrokes for manipulating the console display, including those for switching between virtual consoles, are described below. It's a good idea to experiment with these commands until you are comfortable with them, because knowing how to use virtual consoles is basic to using Linux.
