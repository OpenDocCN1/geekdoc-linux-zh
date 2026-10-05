
```
(car (current-input-mode))
(nth 1 (current-input-mode)) 0
(global-set-key [delete] 'delete-char) ;Del: delete character
(global-set-key [home] 'beginning-of-line) ;Home: beginning of line
(global-set-key [end] 'end-of-line) ;End: end of line
```

Information on the everlasting problem of Back-space and Del can be found on page 243. If you are interested in more advanced Emacs configuration, you need to read about Emacs Lisp programming. Subsequently, this is described in a separate chapter from page 569 onward.

Current versions of GNU Emacs and XEmacs support input and processing of Asian and other foreign language special characters through the new Multilingual Enhancement (in short, MULE). However, this extension is not yet as mature as other Emacs functions. In the long run, Emacs will be adapted to Unicode. As long as you are happy with common 8-bit character sets (ISO Latin character sets), you do not need MULE. In this chapter, MULE is not.

## Loading and saving texts, quitting the program

Emacs is started by entering emacs xemacs. When you are working under X and Emacs is properly installed, it will automatically appear in its window with menus and scroll bars.

When you specify one or more file names when starting the program, the files are automatically loaded. Search patterns are allowed: emacs Makefile *.C *.h loads the Makefile together with all * and *. in the current directory. Independently of this, you can use Ctrl+X Ctrl+X Ctrl+F filename Return to load files at a later stage.

To save a modified file, use the keyboard command Ctrl+X Ctrl+S. If you want to quit Emacs use Ctrl+X Ctrl+C. If at that point Emacs detects any file that has not been saved, a safety confirmation request appears to ask you whether you really want to quit Emacs without saving. If you want to discard your changes, answer this request with arrow. You can also save the file under a different name by means Ctrl+X Ctrl+W filename_name.

If you use Emacs on a text console, you can temporarily leave the program with Ctrl+Z. With fg you can resume your work. (Under X, Ctrl+Z merely reduces the window to an icon.)

## Loading and saving files, terminating Emacs

```
Ctrl+X Ctrl+F load file (find)
Ctrl+X I insert file into existing text
```

## QUICK START 541

- save file
- save all open files
- save file under new name (write)
- save all files (with request for confirmation)
- quit Emacs

When saving, Emacs automatically creates a backup copy name~ which contains the original text. In addition, Emacs saves the current contents of the file at regular intervals into the file#. You can go back to this file if you had a power failure or were unable to quit Emacs in an orderly way. At the next attempt to process the file, Emacs automatically comes up with a warning that a backup file exists. When recover-file, the old file can be restored.

When Emacs is used under X, Emacs provides an extensive menu and GNU Emacs a rather limited menu allowing you to execute a large number of commands without having to know hundreds of keyboard shortcuts by heart. This chapter does not discuss the menu any further – its poses no problems anywhere.

## Elementary commands

Now to the elementary commands for processing a text: when the keyboard is stalled, you should be able to move the cursor with the cursor keys PgP and PgDn. If this does not work, it will defeat, function with the following commands:

Keyboard shortcuts the cursor keys doesn't work

| Ctrl+F | cursor character to the right (forwards) |
| Ctrl+B | cursor character to the left (backwards) |
| Ctrl+P | cursor line up (previous) |
| Ctrl+N | cursor line down (next) |
| Ctrl+V | text page up |
| Alt+V | text page down |

You can enter text at any position. When you want to delete characters, you can use Del and, in a correct installation, you can use the keyboard command Ctrl+D to delete the character at the cursor position.

With Ctrl+X, U or Ctrl+J you can undo the last changes. This undo function works for arithmetic complex commands and is practically unlimited!
When you make a mistake while executing a command, you can abort the command input with Ctrl+G. This is particularly useful if you press the Esc key by mistake.

## 16.2 Fundamentals

Emacs has various processing modes in which additional commands are available for the processing of special files. A difference is made between major and minor modes: only one major mode can be active at a time, but this can be complemented with several minor modes.

Among the most important major modes are C mode (for editing C programs) and LaTeX (for editing LaTeX files). When loading a file, Emacs automatically activates the mode it considers suitable (for example, the C mode when the file name ends with .c). When Emacs cannot identify a suitable mode, it activates the fundamental mode as a default.

Two of the most important minor modes are fill mode (for processing flow text over several lines) and ab mode (for automatic expansion of abbreviations).

The elementary Emacs commands function in the same way in all modes; whenever you want to deactivate Emacs' high-handed actions resulting from a special mode (for example, automatic indenting of program lines in C mode), simply switch back to fundamental mode with Alt-X. More information about processing modes can be found on page 558 onward.

## Keyboard conventions

Generally, there are three ways of selecting Emacs commands: the menu; using keyboard shortcuts (mostly, a combination involving Ctrl or Alt); or inputting the whole command name. This variation begins with Alt+X, for example, using Alt+X delete-char.

Input of commands and other parameters is facilitated by several mechanisms:

- During input, you can expand the command name with Tab in the same way as during command input in a shell terminal. Emacs differentiates between upper and lower case spelling. File names can be expanded. When several possibilities exist, Emacs displays them on screen.

- You can refer back to commands entered previously with Alt+X by opening a new command with Alt+X and then entering Alt+P (previous) or Alt+N (next).

In this book, keyboard sequences are specified in such a way that they can be entered on a correctly installed US/UK international keyboard. A plus sign means that several keys must be pressed at the same time, whereas a comma indicates that they must be pressed one after the other. Letters are always indicated in upper case inside their key frames (as they are on a real-life keyboard). Thus, the Shift key must only be pressed where explicitly indicated! for example, Alt+X means that you should press the Alt and X keys simultaneously, but not Shift!

## FUNDAMENTALS 543

In the Emacs documentation, keyboard shortcuts are represented slightly differently; DEL does not mean Del, but C stands for Control (meaning Ctrl and M for Meta.)

On most keyboards there is no direct correspondence for the Meta key. Instead of Meta+X, you must press Esc and X (one after the other). Alternatively, in some cases, you may use Alt+X (simultaneously) as well. In this book, we generally indicate the easier Alt key combination.

In some Emacs-compatible programs or when using Emacs in a text console, problems arise with the Alt key. Here, instead of Alt+X, you must employ Esc. Information about keyboard installation and Emacs configuration via the .emacs file can be found on page 17 from page 569.

Please note that Emacs differentiates between Ctrl+X, Ctrl+B and the very similar combination Ctrl+X, B. Thus, it really matters how long you keep the Ctrl key depressed.

## Mouse support

You will not be particularly surprised to know that you can use the mouse to change the position, select and copy text. (The usual X conventions apply, previously selected text is inserted with the mouse button.) If you are displaying several texts at a time, you can also move the separation bar between the text areas by means of the mouse button.

Somewhat confusing is the handling of the scroll bar: in GNU Emacs it can, as in xterm, only be moved with the middle mouse button, whereas in XEacs, the left mouse button can be used as well.

Further mouse functions depend on the Emacs version. In XEacs, a position-dependent context menu appears when the right mouse button is pressed. (Try out the right mouse button in different areas of the status line!) In GNU Emacs, in contrast, you can use Shift and Ctrl in combination with the mouse buttons to execute various commands.

## X-specific options and resources

When starting Emacs under X, you can perform numerous setting for colors, charset set, and so on, by means of command line options. The following table lists the most important options. A complete description can be found in the manual page for Emacs.

| Command line options |
|---||
| -nw | start standard Emacs in the shell window (not the X variation in a separate window) |
| -fg color | foreground color (text color; default: black) |
