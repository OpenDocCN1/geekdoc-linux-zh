You can use tset within the startup files of a user who always logs in from a remote terminal (through a modem). If you put the command

```
`tset -m dialup:vt100`
```

in the shell startup file (.profile, .cshrc, and so on), the terminal type will be set to **vt100** every time a connection is made through the modem. Of course, this sets the terminal type even if someone isn't using a **vt100** terminal, so you can use the command

```
`tset -m dialup:?vt100`
```

to have the user connecting through the modem prompted for the terminal type. The prompt looks like this:

```
`TERM=(vt100)?`
```

If the user presses Enter, the **TERM** variable is set to **vt100**. If the user doesn't want to use that value, she can enter the correct string at the prompt.

So far, tset seems to be quite simple, but, in fact, it has a very complex structure when dealing with hard-wired terminals. To properly configure a terminal connected through a serial port, you need a command such as this:

```
`eval `tset -s -Q -m dialup:?vt100 -m switch:z29'`
```

The full details of this type of command are unimportant for most system administrators. If you want more information, check the man pages for tset and stty that came with your Linux system.

# ## Resetting a Screwvy Terminal

Every now and then a terminal connected through a serial port starts acting screwy, either not showing a prompt or generating garbage. There are two quick ways to try to reset the terminal. If they don't work, the terminal should be shut down and restarted. (You might have to kill the processes that were running on the terminal.)

The first approach is to issue a set of Ctrl+J characters on the screwvy terminal, and then type **stty sane** followed by another Ctrl+J. The command **stty sane** should reset the terminal characteristics to normal. You probably won't see the letters you are typing, so enter them carefully.

If the terminal isn't behaving at this point, try typing **reset** and pressing Enter or Ctrl+J. If this doesn't work, the terminal is hung and should be reset manually.