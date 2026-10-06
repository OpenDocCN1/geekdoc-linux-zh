# The emacs Line Mode Edit 297

emacs commands any time you want there are no separate “modes” like the vi line. Note that emacs commands are not followed by an Enter.

(For a complete list of emacs commands, refer to the documentation for Bash or Korn shell.)

First, let's look at how to move the cursor around the command line. Ctrl+b moves the cursor back (to the left), and Ctrl+f moves it forward (to the right). Try by pressing Ctrl+b and Ctrl+a a few times while entering a command on the command line. The cursor should move around the line. If you want to move the cursor the left or right side of the line, the shell simply ignores your command.

```
$ mary had a little larb Ctrl+b $ mary had a little larb
$ mary had a little larb $ mary had a little larb
$ mary had a little larb Ctrl+b $ mary had a little larb
$ mary had a little larb Ctrl+f $ mary had a little larb
```

After the cursor is on the character you want to change, use the Ctrl+d command to delete the current character.

```
$ mary had a little larb Ctrl+d $ mary had a little lab
```

Note that the b moved to the left when the r was deleted and is now the current character.

To add characters to the command line, simply type them in. The characters are inserted before the current character.

```
$ mary had a little lab m $ mary had a little lab
$ mary had a little lamb m $ mary had a little lambb
$ mary had a little lambm Ctrl+h $ mary had a little lamb
```

Note that the erase character (either Backspace or Ctrl+h) will always delete the character to the left of:

The Ctrl+a and Ctrl+e commands can be used to move the cursor to the beginning and end of the command line, respectively.

```
$ mary had a little lab Ctrl+a $ mary had a little lab
$ mary had a little lab Ctrl+e $ mary had a little lamb_
```

Note that the Ctrl+e command places the cursor one space to the right of the last character on the line. (When you're not in emacs mode, the cursor is at the end of the line, one space to the right of the last character typed in.)

This is because when you're at the end of the line, whatever you type will be appended to whatever is already on the line.

```
$ mary had a little lamb_ da $ mary had a little lambda_
```

Two other useful movement commands are the Esc f and Esc b commands. The Esc f moves the cursor forward forward to the end of the current word. The Esc b moves the cursor backward to the beginning of the previous word. Note for these commands you press and release the Esc key, then press the key that corresponds to the desired command (f, b, and so on).