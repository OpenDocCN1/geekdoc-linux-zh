
editors such as vi important. Make a point of opening some of the editors and playing around with them; you never know—you might just thank me someday!

Another reason to learn how to use a text-based editor under the Linux console mode is so that you can edit text files through dial-up or network shell sessions because many servers do not support graphical desktops.

## Working with vi

The editor found on nearly every Unix and Linux system is, without a doubt, the vi editor, originally written by Bill Joy. This simple-to-use but incredibly capable editor features a somewhat cryptic command set, but you can put it to use with only a few commands. Although more experienced Unix and Linux users continue to use vi extensively during computing sessions, many newer users might prefer learning an easier-to-use text editor such as pico or GNU nano. Die-hard GNU fans and programmers definitely use emacs.

That said, learning how to use vi is a good idea. You might need to edit files on a Linux system with a minimal install, or a remote server without a more extensive offering of installed text editors. Chances are better than good that vi will be available.

You can start an editing session by using the vi command like this:

```
$ **vi file.txt**
```

The vi command works by using an insert (or editing) mode, and a viewing (or command) mode.

When you first start editing, you are in the viewing mode. You can use your cursor or other navigation keys (as shown later) to scroll through the text. To start editing, press the i key to insert text or the a key to append text. When finished, use the Esc key to toggle out of the insert or append modes and into the viewing (or command) mode. To enter a command, type a colon (:), followed by the command, such as w to write the file, and press Enter.

Although vi supports many complex editing operations and numerous commands, you can accomplish work by using a few basic commands. These basic vi commands are

- **Cursor movement**—h, j, k, l (left, down, up, and right)
- **Delete character**—x
- **Delete line**—dd
- **Mode toggle**—Esc, Insert (or i)
- **Quit**—:q
- **Quit without saving**—:q!
- **Run a shell command**—:sh (use `exit` to return)
- Save file—:w
- Text search—/

> NOTE
> Use the vimtutor command to quickly learn how to use vi's keyboard commands. The tutorial takes less than 30 minutes, and it teaches new users how to start or stop the editor, navigate files, insert and delete text, and perform search, replace, and insert operations.

## Working with emacs

Richard M. Stallman's GNU emacs editor, like vi, is included with Linux and nearly every other Linux distribution. Unlike other Unix and Linux text editors, emacs is much more than a simple text editor—it is an editing environment and can be used to compile and build programs, act as an electronic diary, appointment book and calendar, compose and send electronic mail, read Usenet news, and even play games. The reason for this capability is that emacs contains a built-in language interpreter that uses the Elisp (emacs LISP) programming language. emacs is not installed in Ubuntu by default; instead you'll need to install it using apt-get or synaptic. The package you need is simply emacs.

You can start an emacs editing session like this:

```
$ emacs file.txt
```

> TIP
> If you start emacs when using X11, the editor launches in its own floating window. To force emacs to display inside a terminal window instead of its own window (which can be useful if the window is a login at a remote computer), use the -nw command-line option like this: emacs -nw file.txt.

The emacs editor uses an extensive set of keystroke and named commands, but you can work with it by using a basic command subset. Many of these basic commands require you to hold down the Ctrl key, or to first press a meta key (generally mapped to the Alt key). The basic commands are listed in Table 4.2.

### TABLE 4.2 Emacs Editing Commands

| Action | Command |
|---|---|
| Abort | Ctrl+g |
| Cursor left | Ctrl+b |
| Cursor down | Ctrl+n |
| Cursor right | Ctrl+f |
| Cursor up | Ctrl+p |
