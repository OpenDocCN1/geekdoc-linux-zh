
desktop installed. And as discussed in Chapter 1, “Installing SUSE LINUX Enterprise Server,” not all servers will have a GUI desktop installed because GUIs on a server consume system resources unnecessarily.

Perhaps we are from the old school, but we highly prefer the vi editor (pronounced vee eye). Many seasoned Linux/Unix system administrators and programmers echo this same preference because when you become familiar with vi’s somewhat unique command syntax, you will find that it is one of the most versatile—although not necessarily the most full-featured—text editors available. The other reason vi is a favorite among the hard-core Linux/Unix users is its universal availability. Other than the fact that you can find an implementation of vi for most operating systems, it is probably the only screen-oriented text editor that you can count on to be “always there” among all the Linux and Unix distributions available today. Being able to use vi ensures that you will always have an editor available to you, no matter what version or distribution of Linux/Unix you use.

## NOTE

Many modern Linux distributions include Vim in conjunction with or instead of vi. SLES 9 ships with Vim instead of vi. Because Vim falls into the category of being a “vi-clone,” knowledge of vi will serve you well in administering SLES systems.

vi (and thus Vim) has three different “modes” of operation:

- **Visual command mode**—This mode is used to issue short commands (of one character or sometimes a couple of characters) that allow you to manipulate the text or editor environment in a number of ways. You enter it by typing one of the text-entering commands shown in Table B.1 to control how and where text is entered.
- **Data-entry or input mode**—This mode is used for entering text into the editor’s work buffer before it is committed to the disk through a save operation, initiated in one of the command modes.
- **Status line command mode**—This mode is also referred to as the “Colon command mode” because you enter this mode from the visual command mode by typing a colon. This mode is used for issuing longer, more complex commands to the editor, such as to save files, quit the editor, set environment variables, and perform more global editor tasks. The commands are echoed back to the user in the status line of the editor (demarcated by a : at the bottom of the screen) and are executed when you press Enter.

## NOTE

To switch out of the input mode into the visual command mode, simply press the Esc key. Entering the status line command mode from the input mode is a two-step process: First press the Esc key to enter the visual command mode and then type a colon (:).

vi does not offer you much feedback as to which mode it is currently in. For instance, you may not realize that vi is currently in the visual command mode and you typed dd. Instead of adding two d's to your file, you just accidentally deleted the current line of text. (Fortunately, you can undo the change by using the u command; see Table B.1.) If you are unsure what mode vi is operating in, press the Esc key a few times to place vi in visual mode. Even if you are already in the visual mode, the worst you get is an error beep on the terminal.

## TIP

Often new users have difficulty knowing which mode they're working in because vi doesn't really offer much feedback. In a worst-case scenario, press Esc a few times and know that you will be in visual mode. Even if you are already in visual mode, the worst you will get is an error beep.

## TABLE B.1
### vi Single-Character Commands

| TEXT COMMAND | DESCRIPTION |
|---|---|
| `a` | Start appending text after the current cursor position. |
| `A` | Append text to the end of the current line. |
| `i` | Start inserting text to the left of the current cursor location. |
| `I` | Insert text at beginning of the current line. |
| `o` | Insert a new line below the current line. |
| `O` | Insert a new line above the current line. |
| `r` | Replace a single character at the present location. |
| `R` | Replace text starting at the current position (in other words, start overwriting the remainder of the line). |
| `u` | Undo the last change. |
| `U` | Undo all the changes to the current line. |

## CAUTION

vi commands are case sensitive.

There is a rather rich set of editing commands in vi. Many of them are two-character combinations, usually with the first character denoting the action (such as deleting) and the second character indicating the type of text object (such as a word or sentence) to be acted on. Table B.2 shows some of the commonly used vi editing commands.

## TABLE B.2
### vi Editing Commands

| TEXT COMMAND | DESCRIPTION |
|---|---|
| `cw` | Change the word at the current cursor position. |
| `D` | Delete from the current location to the end of the line. |
| `dd` | Delete the current line. |
| `dw` | Delete the word at the current cursor location. |
| `x` | Delete one character at the current cursor position. |
| `.` | Repeat last edit command. |
| `yy` | Copy the current line into the memory buffer (known as “yank”). |
| `yw` | Yank the word under the cursor. |
| `p` | Paste the text in the memory buffer (the “yanked” text) at the current cursor position. |
| `P` | Paste the yanked text before the current cursor position. |
| `ZZ` | Save the changes to disk and exit (i.e. You can use `:w` to write the modifications made so far to disk without exiting the editor.) |

## TIP

You can precede the editing commands with a number to indicate the command is to be repeated that number of times. For instance, instead of entering dd five times to delete five lines, you can use 5dd instead.

vi, which is a screen-oriented editor, uses the curses library for screen manipulation. That means it works with all supported terminal types, and you can navigate the cursor around the screen using the standard arrow keys. You can move up and down a full screen at a time by pressing Ctrl-B and Ctrl-F, respectively; or, to scroll half a screen up and down, you can press Ctrl-D and Ctrl-U, respectively. Because vi is text-based and does not depend on a mouse, it is most suited for remote management tasks, such as performing file edits over a Telnet or SSH link.

For more information about using vi, you can type `:help` inside the editor.
Other resources include the website dubbed "The Vi Lovers Home page"
(http://thomer.com/vi/vi.html) and the book *Learning the Vi Editor*
(ISBN 1-56592-426-6).

## TIP

You can start vi in *read-only* mode (`vi -R filename`). This is useful for viewing
long configuration files without the fear of accidentally changing them. vi also
has a recovery mode (`vi -r filename`) that recovers recent edits after a crash.
vi automatically detects this and displays a message similar to the following:

```
E325: ATTENTION
Found a swap file by the name ".test.txt.swp"
          owned by: tasha   dated: Sun Mar 13 13:20:37 2005
         file name: ~tasha/test.txt
          modified: no
         user name: tasha   host name: Athena
        process ID: 3250
While opening file "test.txt"
             dated: Sun Mar 13 13:20:32 2005

(1) Another program may be editing the same file.
    If this is the case, be careful not to end up with
    Two different instances of the same file when making
    changes.
    Quit, or continue with caution.

(2) An edit session for this file crashed.
    If this is the case, use ":recover" or
    "vim -r test.txt" to recover the changes (see
    :help recovery).
    If you did this already, delete the swap file
    ".test.txt.swp" to avoid this message.

Swap file ".test.txt.swp" already exists!
[O]pen Read-Only, (E)dit anyway, (R)ecover, (Q)uit,
(D)elete it:
```

## Website Resources

The Internet is a vast repository of information. Even with the help of search
engines such as Google, it is still a daunting task to sort through the various
sites for relevant information. One of the biggest challenges of administrating
