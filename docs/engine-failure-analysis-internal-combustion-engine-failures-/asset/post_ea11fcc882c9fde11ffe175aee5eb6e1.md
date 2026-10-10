
# XF86Setup

```
XF86Setup [ option ]
```

Launches a menu-driven utility that configures an XFree86 server. This utility can be used to install a server for the first time or to change the default configuration. A change is needed if you change your video adapter, mouse, keyboard, or monitor. To use XF86Setup, you may need some or all of the following information: the brand and model of your video adapter, the amount of video RAM (VRAM) installed on the video adapter, the brand and model of your monitor, and the type of keyboard you are using (such as 102-key U.S.).

See also Xconfigurator.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -sync | Enable synchronization for all communications with the X server |
| -name appname | Use appname as the name for the configuration window |
| -display n | Use the nth display instead of the next available one |
| -nodiag | Suppress the menu-based interactive system |
| -geometry specification | Use the specified geometry for the window |
| -script | Run the specified script |

# xterm

```
xterm [ option ]
```

Starts the xterm terminal emulation program. Requires the X Window System. Certain xterm options are toggles. Precede this option with a plus sign (+) to turn it on or a minus sign (−) to turn it off.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| +\|-132 | Enable 132 column mode. |
| +\|-ah | Always highlight the cursor, even when the window is inactive. |
| +\|-ai | Disable active icon support. |
| +\|-aw | Enable text word-wrapping. |
| -b n | Specify the width of the border in n pixels. |
| -bd color | Specify the color to use for window borders. |
| +\|-bdc | Disable bold characters. |
| -bw n | Specify the window border width in n pixels. |
| -C | Enable the window to receive console output. |
| +\|-cb | Set the VT100 variable CutToBeginningOfLine to false. |
| +\|-cm | Disable ANSI color changes. |
| +\|-cn | Disable cutting new lines in line-mode selections. |
| -cr color | Specify the text cursor color. |
| +\|-cu | Work around bugs in more program (see Chapter 8) that display lines incorrectly when the line equals the window width. |
| +\|-dc | Disable dynamic colors. |
| -e command | Run the specified command in an xterm window. |
| -fb font | Use the specified font. |
| -fg color | Specify the foreground color. |
| -fl fontname | Set the font for active icons. |
| −fn font | Specify the font to be used for normal text. |
| −hc color | Set the color to be used for the foreground. |
| +\|−le | Enable detection of the *stty* *erase* value. |
| +\|−im | Enable the insert mode. |
| +\|−j | Enable jump scrolling. |
| −leftbar | Force the scroll bar to the left of the window. |
| +\|−ls | Start the shell as a login shell. |
| +\|−mb | Ring the margin bell when the user types near the right border. |
| −mc time | Specify the maximum time (in milliseconds) between multi-click selections. |
| −ms color | Specify the *default* pointer color. |
| −nb n | Specify the number of characters (*n*) from the right border at which the margin bell rings if the bell is enabled. |
| +\|−nul | Enable the display of underlining. |
| +\|−pc | Enable bold colors. |
| −rightbar | Force the scroll bar to the right window border. |
| −rv | Simulate reverse video by swapping the foreground and background colors. |
| +\|−rv | Enable reverse wrap-around. |
| +\|−s | Enable asynchronous scrolling. |
| +\|−sb | Save all lines scrolled off the top and display scroll bar. |
| +\|−sf | Enable Sun function keys. |
| +\|−si | Finish output at the bottom of the window. |
| +\|−sk | Enable automatic repositioning of window when scrolling. |
| −sl n | Specify the number (*n*) of lines to save that are scrolled off the top of the screen. |
| +\|sp | Enable Sun keyboard mapping. |
| +\|t | Start in Tektronix rather than VT102 mode. |
| –title string | Use the specified string for the window title. |
| –tm keyword | Indicate the terminal setting that should be used, which is specified by keyword. Options include `intr`, `quit`, `erase`, `kill`, `eof`, `eol`, `swtch`, `start`, `stop`, `brk`, `sup`, `dsup`, `rprnt`, `flush`, `weras`, and `inext`. |
| –tn name | Specify the name of the terminal type to be used. |
| +\|–ulc | Disable the display of underlining with color. |
| +\|–ut | Skip making entries in system log. |
| +\|–vb | Enable the visual rather than audible bell. |
| +\|–wf | Wait for window to be mapped before enabling subprocesses. |
| –ziconbeep percentage | Sound bell at the specified percentage of full volume. |

# CHAPTER 2

## Getting Help and Finding Your Bearings

![](img/e85417bb52fc523c6fc7b3b77b124ecb_62_0.png)

In this chapter, you'll learn the commands you can use to get help with Linux. You'll also learn the commands that can help you get your bearings. The latter category includes commands that remind you where you're positioned in the Linux filesystem, what user groups you belong to, and much more—including a command that displays or prints nicely-formatted calendars for the current month or year (or for any month or any year).

### AT A GLANCE

| How Do I | See This Entry | Examples |
| :--- | :--- | :--- |
| Find out which man page has the information I'm looking for? | apropos, man | apropos fonts |
| Display or print a calendar? | cal | cal -y 2003 \| 1pr |
| See the current system date and time? | date, rdate | date |
| Find out who else is using computers on the network? | finger, rwho | finger suzanne |
| Find out what the various bash shell commands do? | help | help cd |
| Display this system's IP address? | hostname | hostname -i |
| Change the system date and time? | hwclock | hwclock --set --date='05/21/03 12:56' |
| Find out my user and group names and IDs? | id, groups, whoami | id |
| Get information about GNU utilities? | info | info emacs |
| Get detailed information about a command? | man | man cdrecord |
| See the full path name of the current directory? | pwd | pwd |
| Set the time zone correctly? | tzselect | tzselect |
| Find out which version of the Linux kernel I'm running? | uname | uname |
| Find out how long I've been using Linux during this session? | uptime | uptime |
| Find out who else is using this system? | w, who | w |

### Getting Help with Linux

This section introduces the following:

- Getting help with Linux
- Getting help online

For getting help on Linux commands, the star of the show is the **man** command, which displays command documentation on-screen. Almost all Linux commands and utilities have manual pages, called *man pages*. These documents provide information about the command in a standard format. Less useful is the **info** command, which provides a text-based, and rather confusing hypertext environment for information concerning GNU utilities; and the **help** command, which provides brief, one- or two-sentence descriptions of the bash shell's built-in commands. In general, the information available within info is also available in man pages. Similarly, you'll find information on built-in bash commands—much more information than is available with the *help* command—in the bash man page. You may also try browsing the /usr/doc directory, which contains additional documents for installed application programs.

**TIP** If you've forgotten which options you can use with a command, type the command name followed by a space and − **help**, as in the following example: **cal −help**. This option isn't available with all commands, but it works with most of them.
