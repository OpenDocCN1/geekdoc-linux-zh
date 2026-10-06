# The vi Line Edit Mode 293

The current character is whatever character the cursor is on; we'll say more about the current character in a moment. You can enter vi commands only in command mode and that the commands are interpreted immediately upon typing them in, no Enter needed.

A typical problem you may encounter when typing in long commands is that it's only after typing it all that you notice an error. Inevitably, the error is at the beginning of the line!

In command mode, you can move the cursor and fix the errors without disturbing the command line. After you've moved the cursor to the place where the error is, you can change the letters to whatever you want. Then press Enter (regardless of where the cursor is on the line) and it'll be given for interpretation.

In the following examples, the underline (_) represents the cursor. A command line will be shown, followed by one or more keystrokes, followed by what the line looks like after applying the keystrokes

before keystrokes after

First, let's look at moving the cursor. Many systems will let you use the arrow keys on your keyboard, which makes it easy: left arrow to move left, right arrow to move right.

The more vi-inspired movement commands, are h to move the cursor to the left and l moves it to the right. Try this by entering command mode (press Esc) and pressing the h a few times. The cursor can move around the line. If you want to move the cursor to the left or right side of the line, the shell "beeps" at you.

```
$ mary had a little larb Esc $ mary had a little larb
$ mary had a little larb h $ mary had a little larb
$ mary had a little larb h $ mary had a little larb
$ mary had a little larb 1 $ mary had a little larb
```

After the cursor is the character you want to change, you can use the x command to delete the current character ("X" it out).

Note that the b moved to the left when the x was deleted and it is now the current character.

To add to the command line, you can use the i before or a commands. The i command inserts before the current character, and the a command adds after the current character. Both of these commands put you back into input mode, remember to press Esc to go back to command mode.

```
$ mary had a little lab im $ mary had a little lamb
$ mary had a little lamb m $ mary had a little lambm
$ mary had a little lambb Esc $ mary had a little lammb
$ mary had a little lambb x $ mary had a little lamb
$ mary had a little lamb a $ mary had a little lamb_
$ mary had a little lamb_ da $ mary had a little lambda_
```