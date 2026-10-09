
## The --display Option

For a single command, you can usually specify the X server on the command line:

```bash
sam@guava:~$ gnome-calculator --display plum:0.0
```

Many X programs accept the `--display` option. Those that do not accept this option send their output to the display specified by the `DISPLAY` variable.

## Stopping the X Server

How you terminate a window manager depends on which window manager is running and how it is configured. If X stops responding, switch to a virtual terminal, log in from another terminal or a remote system, or use *ssh* to access the system. Then *kill* (page 465) the process running *Xorg*.

## Remapping Mouse Buttons (CLI)

Throughout this book, each description of a mouse click refers to the button by its position (left, middle, or right, with left implied when no button is specified) because the position of a mouse button is more intuitive than an arbitrary name or number. X numbers buttons starting at the left and continuing with the mouse wheel. The buttons on a three-button mouse are numbered 1 (left), 2 (middle), and 3 (right). A mouse wheel, if present, is numbered 4 (rolling it up) and 5 (rolling it down). Clicking the wheel is equivalent to clicking the middle mouse button. The buttons on a two-button mouse are 1 (left) and 2 (right).

If you are right-handed, you can conveniently press the left mouse button with your index finger; X programs take advantage of this fact by relying on button 1 for the most common operations. If you are left-handed, your index finger rests most conveniently on button 2 or 3 (the right button on a two- or three-button mouse).

"Left-handed mouse" on page 110 describes how to use a GUI to change a mouse between right-handed and left-handed, causing X to swap the functions of the left and right buttons. You can also change how X interprets the mouse buttons using *xmodmap*. If you are left-handed and using a three-button mouse with a wheel, the following command causes X to interpret the right button as button 1 and the left button as button 3:

```bash
$ xmodmap -e 'pointer = 3 2 1 4 5'
Warning: Only changing the first 5 of 24 buttons.
```

The warning says that *xmodmap* is not changing the settings of the last 19 buttons, which is fine. Omit the 4 and 5 if the mouse does not have a wheel. The following command works for a two-button mouse without a wheel:

```bash
$ xmodmap -e 'pointer = 2 1'
```

Use the `xmodmap -pp` option to display all the buttons X has defined for the mouse and how those buttons are mapped. After making the changes described above for the mouse with a wheel, `xmodmap` shows the following mapping.

```bash
$ xmodmap -pp
There are 24 pointer buttons defined.
```

| Physical | Button |
| :------- | :----- |
| Button   | Code   |
| 1        | 3      |
| 2        | 2      |
| 3        | 1      |
| 4        | 4      |
| 5        | 5      |
| 6        | 6      |
| 7        | 7      |
| ...      | ...    |

Changing the order of the first three buttons is critical to making the mouse suitable for a left-handed user. When you remap the mouse buttons, remember to reinterpret the descriptions in this book accordingly. When this book asks you to click the left button or does not specify which button to click, use the right button, and vice versa.

# SYSTEM ADMINISTRATION TOOLS

This section describes a few of the textual (command-line) tools that can help you be an efficient and thorough system administrator. Some are simply mentioned here and are described in detail elsewhere in the book. It also presents a list of graphical administration tools available under Fedora/RHEL. You can learn more about these tools by reading the appropriate `man` or `info` pages.

## TEXTUAL ADMINISTRATION UTILITIES

### blkid: DISPLAYS BLOCK DEVICE INFORMATION

The `blkid` utility, which must be run with root privileges, displays the label, UUID value, and filesystem type for block devices:

```bash
# blkid
/dev/sda1: UUID="c87cf9ea-df3c-42a6-8bca-38dcb154a52c" TYPE="ext4"
/dev/sda2: UUID="kyxKaK-k5W1-u1J0-sbXD-2X75-M67C-fhkpnl" TYPE="LVM2_member"
/dev/mapper/fedora-swap: UUID="ca353a55-5739-4aa0-a114-1a1783606d8f" TYPE="swap"
/dev/mapper/fedora-root: UUID="10f4196d-b561-4830-a603-8ebb8e5784c0" TYPE="ext4"
/dev/mapper/fedora-home: UUID="5d5391fe-252a-4a06-a117-aadC81994057" TYPE="ext4"
```

### chsh: CHANGES THE LOGIN SHELL FOR A USER

The `chsh` utility changes the login shell for a user. When you call `chsh` without an argument, you change your login shell. When an ordinary user changes his login shell with `chsh`, he must specify an installed shell that is listed in the file /etc/shells, exactly as it is listed there; `chsh` rejects other entries. When working with **root** privileges, you can change any user’s shell to any value by calling `chsh` with the username as an argument. The `chsh --list-shells` command displays the list of available shells. In the following example, a user working with **root** privileges changes Sam’s shell to `tcsh`:

```bash
# chsh sam
Changing shell for sam.
New shell [/bin/bash]: /bin/tcsh
Shell changed.
```

See page 329 for more information.

### clear: CLEARS THE SCREEN

The `clear` utility clears the screen. You can also use **CONTROL-L** from `bash` to clear the screen. The value of the environment variable **TERM** (page 1153) determines how to clear the screen.

### dmesg: DISPLAYS SYSTEM MESSAGES

The `dmesg` utility displays recent system log messages (the kernel ring buffer; page 595).

### e2label: WORKS WITH VOLUME LABELS

The `e2label` utility displays or creates a volume label on an `ext2`, `ext3`, or `ext4` filesystem. You must run this utility with **root** privileges. An `e2label` command has the following format:

`e2label device [newlabel]`

where `device` is the name of the device (e.g., `/dev/hda2`, `/dev/sdb1`, `/dev/sr0`) you want to work with. When you include the optional `newlabel` parameter, `e2label` changes the label on `device` to `newlabel`. Without this parameter, `e2label` displays the label. You can also create a volume label using the `-L` option of `tune2fs` (page 526). See also `blkid` on the previous page.

### kill: SENDS A SIGNAL TO A PROCESS

The `kill` builtin sends a signal to a process. This signal might or might not terminate (kill) the process, depending on which signal it is and how the process is designed. Refer to “**trap: Catches a Signal**” on page 1047 for a discussion of the various signals and their interaction with a process. Running `kill` is definitely not the first method to try when a process needs to be aborted. See also `killall` (page 467) and `pkill` (page 468).

Usually a user can kill a process by working in another window or by logging in on another terminal. Sometimes, however, you might have to work with **root** privileges to kill a process for a user. To kill a process, you need to know its PID. The `ps` utility can provide this information once you determine the name of the program the user is running and/or the username of the user. The `top` utility (page 612) can also be helpful in finding and killing a runaway process (use the `top` + `k` command).

#### Use the kill signal (–KILL or –9) as a method of last resort

When you do need to use kill, send the termination signal (kill -TERM or kill -15) first. Only if the termination signal does not work should you attempt to use the kill signal (kill -KILL or kill -9). Because of its inherent dangers, using a kill signal is a method of last resort, especially when you are working with **root** privileges. One **kill** command issued while working with **root** privileges can bring the system down without warning. The kill signal can also cause the target program to corrupt its configuration or state.

In the following example, Sam complains that `gnome-calculator` is stuck and that he cannot do anything from the `gnome-calculator` window—not even close it. A more experienced user could open another window and kill the process, but in this case you kill it for Sam. You use `ps` to produce a long list of all processes and a pipeline to send standard output of `ls` to `grep` to find which one is running `gnome-calculator`:

```bash
$ ps -ef | grep gnome-calculator
sam 3730 2424 0 14:07 ? 00:00:00 gnome-calculator
sam 3766 3568 0 14:14 pts/3 00:00:00 grep gnome-calculator
```

If several people are running `gnome-calculator`, look in the left column to find the correct username so you can kill the correct process.

You can also use the `pgrep` utility to list all processes owned by Sam with the string `calc` in the name of the program the process is running:

```bash
$ pgrep -u sam -l calc
3730 gnome-calcuato
```

Now that you know Sam’s process running `gnome-calculator` has a PID of 3730, you can use `kill` to terminate it. For the safest way to do so is to log in as Sam (perhaps you could allow him to log in for you or `su` to sam [su sam] if you are logged in as **root**) and give any of the following commands (all of which send a termination signal to process 3730):

```bash
$ kill 3730
or
$ kill -15 3730
or
$ kill -TERM 3730
```

Only if this command fails should you send the kill signal:

```bash
$ kill -KILL 3730
```

The -KILL option instructs `kill` to send a **SIGKILL** signal, which the process cannot ignore. Although you can give the same command while you are working with **root** privileges, a typing mistake in this situation can have much more far-reaching consequences than if you make the same mistake while you are working as a nonprivileged user. A nonprivileged user can kill only her own processes, whereas a user with **root** privileges can kill any process, including system processes.
