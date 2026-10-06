# Advanced Bash–Scripting Guide

```
| Keypress=$ (head -cl) | # $ (dd bs=1 count=1 2 > /dev/null)
| | # on non-GNU systems |
echo
echo "Key pressed was \"$Keypress\""
echo

stty $old_tty_settings # Restore old settings.

# Thanks, Stephane Chazelas.

exit 0
```

Also see [Example 9–3]().

# terminals and modes

Normally, a terminal works in the canonical mode. When a user hits a key, the resulting character does not immediately go to the program actually running in this terminal. A buffer local to the terminal stores keystrokes. When the user hits the ENTER key, it sends all the keystrokes to the program. There is a basic line editor inside the terminal.

```
bash$ tty -a
speed 9600; rows 36; columns 96; line = 0;
intr = ^C; quit = ^I; erase = ^H; kill = ^U; eof = ^E; deol = ^D; <undefined>; ed2 = <undefined>
start = ^Q; stop = ^S; susp = ^Z; rprnt = ^R; werase = ^W; lnext = ^V; flush = ^O echon -noflush -xcase -topost -echort
```

Using canonical mode, it is possible to redefine the special keys for the local terminal line editor.

```
bash$ cat filexxxx
wha<ctl-W-I-H-foo bar<ctl-Uhello world<ENTER>
<ctl-D
bash$ cat filexxxx
hello world
bash$ bash wc -c < file
13
```

The process controlling the terminal receives only 13 characters (12 alphabetic, plus a newline), although the user hits 26 keys.

In non-canonical ("raw") mode, every key hit (including special editing keys as ctrl–H) sends a character immediately to the controlling process.

The Bash prompt disables both icanon and echo, as it replaces the Bash terminal line editor with its own more elaborate version. For example, when you hit ctrl-A at the Bash prompt, it's ^A echoed by the terminal, but Bash gets a \ character, interprets it, and moves the cursor to the beginning of the line.

Stephane Chazelas

tset

Chapter 13. System and Administrative Commands

202