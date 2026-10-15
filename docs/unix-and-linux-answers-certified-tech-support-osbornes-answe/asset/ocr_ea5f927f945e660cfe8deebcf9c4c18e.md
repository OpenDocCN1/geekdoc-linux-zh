# Chapter 2  Getting a Grip on UNIX

# Can I set the erase function to the DEL key instead of CTRL-H?

Yes. To do this, type `stty`, then a space, then `erase`, then a space, then `CTRL-V`, then the DEL key. However, the key combinations in Table 2-1 are by far the most common.

# How can I fix my keyboard when I log in from a PC?

When you log in to your UNIX network from a PC, sometimes the version of telnet that’s running on your PC doesn’t re-map the BACKSPACE key properly. You’ll think you have backspaced over a command, but when you press ENTER, you will find there are a bunch of control characters embedded in your command. So, change the setting yourself by typing in the following: `stty erase` followed by a space, then CTRL-V, then the BACKSPACE key, then the ENTER key. The result on screen will probably look like this:

```
stty erase ^?
```

Now the BACKSPACE key will behave normally. The CTRL-V key combination causes UNIX to read the next keystroke without performing the action.

# How can I put a little sanity back into my terminal when things go haywire?

What if you got a little carried away with the `stty` command, or worse, your terminal settings got seriously messed up by a program that got carried away? To get back to reality, try the following:

```
stty sane
```

If your keystrokes are getting really wild try entering the command bracketed by `<ctrl-j>`. Enter the `<ctrl-j>` sequence by holding down the CTRL key and pressing the J key.

```
<ctrl-j>stty sane<ctrl-j>
```

This command won’t get your preferred settings back, but it will get rid of any truly bizarre settings. Exactly what settings appear will vary depending on the system you’re on.