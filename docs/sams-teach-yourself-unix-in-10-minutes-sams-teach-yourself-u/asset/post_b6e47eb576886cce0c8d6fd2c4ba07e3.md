
machine that you sit down in front of. Because of its ubiquity, knowing the basics of vi will enable you to work with your files even if there are no more-convenient editors available.

Follow these steps if you need to use vi:

- 1. Determine what file you want to edit.
- 2. Issue the vi command as `vi <filename>`. The vi editor can also be started with no filename if you'd prefer to start a new document and haven't decided on a name.

When you start vi there are a number of things you need to know to make it useful. The Return key has been included here because although some of these commands take effect immediately upon pressing the respective keys, others require Return to be pressed after them.

vi operates in one of two modes: command mode or insert mode. In command mode, you have control of things such as cursor position, deleting characters, and saving files. In insert mode, you can insert characters. This distinction is bound to be confusing at first, but you'll find that vi's speed and universal presence outweigh its odd interface when performing some tasks. Some of the most-used tasks are featured in Table 8.1.

### TABLE 8.1 COMMON vi ACTIONS

| MODE | Key(s)/Key COMBINATION(s) | ACTION |
|---|---|---|
| Command | l | Move right |
|  | h | Move left |
|  | j | Move to the next line |
|  | k | Move to the previous line |
|  | Put cursor on the character to delete and then hit the x key | Delete a character |

### TABLE 8.1 CONTINUED

| Mode | Key(s)/Key Combination(s) | Action |
|---|---|---|
|  | Press the d key twice | Delete an entire line (including to delete an empty line) |
|  | Position cursor on the line to append and hit A | Append the end of a line |
|  | i (before the character under the cursor) or a (after the character under the cursor) | Changes to insert mode |
|  | :w Return | Save the file |
|  | :w<filename> | Save the file to a new name |
|  | :q Return | To exit vi |
|  | :q! Return | Quit without saving |
| Insert mode | Esc key | Changes to command |
|  | Backspace and Delete keys | Backspaces or deletes, but only for data just inserted |

Because it is impossible to walk through a step-by-step example, try typing the following example; remember to compare what you're typing, refer to the preceding list of commands, and see what happens. Although the finer details are not revealed by this example, you will pick up enough to at least enable you to do useful work, and to get you out of any sticky vi situations you get yourself into.

Try typing the following exactly as it appears here and see what happens. Where a new line appears in the text, hit Return. Remember that Esc is the escape key.

```
> vi mynewfile
!This is my new file
This is line one of my new file
This is a test
This is line four of my new file<esc>kddkA
This is line three of my new file<esc>
==khhhhhhhhhhhhhhxxitwo<esc>:wq!
```

Your machine will respond:

"mynewfile" [New file] 4 lines, 119 characters

Now, look at what you've got.

```
> cat mynewfile
This is my new file
This is line two of my new file
This is line three of my new file
This is line four of my new file
```

## THE KING OF EDITORS: emacs

On the other end of the spectrum from vi's odd syntax and tiny footprint is emacs. In certain circles it is thought that emacs is an acronym for "emacs makes a computer slow" because emacs is certainly the editor of all editors. Including an email-reading client, a news-reading client, a programming language, an online help database, and a windowing system (to name only a few of its features), emacs can almost certainly do anything that you want an editor to do. With today's faster machines and nearly unlimited memory, emacs might even be able to work fast enough that you don't need a coffee break while it starts up.

From the point of view of the average user, emacs has a much more intuitive interface than vi. You're always in insert mode, and Control functions are handled by using Control+key sequences instead of a separate mode. To make use of emacs, you need to do the following:

- 1. Determine the name of the file you want to edit.
- 2. Issue the emacs command as emacs <filename>. The emacs editor can also be started without a filename if you want to create a new file.

After you've started emacs, you'll need to know some basics to make it useful. (But you hardly need the list that follows because emacs starts up by immediately giving you a list of ways to get help.) In the following list, whenever you see Ctrl+ preceding a character, it means that you need to hold down the Control key and type that character:

- The emacs editor doesn't have a separate mode for entering commands. You are always either typing a command or typing text—no switching modes between them. This is just like most word processors that you might be familiar with. To enter text, just type what you want to appear; to enter a command, just type the command (usually Ctrl+something, or Esc x something).
- You can position the cursor in emacs by using the arrow-key keypad in most every version of emacs and terminal combination. If the arrow keys don't work, you can also position the cursor by using Ctrl+f to move forward, Ctrl+b to move backwards, Ctrl+p to move to the previous line, and Ctrl+n to move to the next line. Newer versions of emacs also enable you to position the cursor using the mouse, but many users actually find this less convenient than the cursor keys.
- You can delete everything from the cursor to the end of the current line by typing Ctrl+k.
- Ctrl+g is the emacs "quit what you're doing" command—if you've started typing a command and change your mind, use Ctrl+g.
- If you use Ctrl+k to delete a line or lines, you can type Ctrl+y to yank them back again.
- To save the file you're currently editing, type Ctrl+x Ctrl+s.
- To save the file to a new filename, type Ctrl+x Ctrl+w <filename>Return.
- To exit emacs type Ctrl+x Ctrl+c. If emacs proceeds to ask you about unsaved buffers, it's because you have unsaved work. You can either go back and save your work, or answer Yes to the "quit anyway?" question and go about your business.

## COMMAND BASICS

Beyond the set of Ctrl+ commands available in emacs, there’s also an amazingly extensible set of commands which come in to play if you use the escape key. These commands are usually known as emacs meta commands, even though the machine with the meta key from which they draw their name has long since faded into history. Although they’re too complicated and too specific to cover in this book, access to many of the interesting emacs meta commands is accomplished by typing Esc x, and then typing a command of some sort, such as info, what-line, or goto-line. As a matter of fact, you can find many useful emacs commands by entering Esc x and then typing a few characters (that is, the beginning of what you think the command might be named), followed by a space. The editor then gives you a list of all commands with similar names; frequently, one that does what you want is on the list!

One useful meta command that you might want to try is as follows: start emacs, and then type Esc+xhelp+Spacebar (and a second space, if the first one just results in the help you typed being extended by a dash). This will bring up a list of emacs commands that start with help—including useful things such as "help-for-help," a very good place to start.

## THE emacs TUTORIAL

Instead of a quick example for you to pick through, emacs provides its own help and tutorial functions. New users are always encouraged to take the emacs tutorial to introduce themselves to the features of the editor, and to learn how to ask it for help on other features.

To enter the emacs tutorial, all you need to do is start emacs, and type Ctrl+h (hold the Ctrl key down, hit h, release the Ctrl key, and hit i). If you type a ? after the Ctrl+h—instead of the i—you’ll see that there’s actually a whole world of alternatives to the i; these alternatives give you a large range of different types of helpful information. For now, take the tutorial. If you’re curious, you can probably spend a few months exploring the other options.
