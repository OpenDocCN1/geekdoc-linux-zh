
## The :make Command

To compile a C program with an accompanying make file, and correct the errors, you can type this command in Last Line mode:

```
make
```

This runs the make command and captures the output. When the command finishes the editor starts editing the first file. The next step is to fix the error. After that you need to go to the line causing the next error. This is done using the command:

```
cn
```

This command will go to the location of the next error even if it is in another file.

You can continue fixing problems and using cn until all your problems are over or you want to do a recompile. If you want to see the current error message again, use the command:

```
cc
```

## Last Line Mode Command History

When you are in Last Line mode, you can use the <Up> arrow key to recall an older command line entry, and then can use the <Down> arrow key to go forward to newer commands. Then, when you press <Enter> after you have indexed to that previous command in the history, that previous command is executed again.

There are four histories you can utilize in vim, but the two most important ones are for:

- Last Line mode command history
- / and ? search command history

Your search history is most useful to you, particularly because if you type complex search criteria, you do not want to have to retype them every time you want to repeat that search!

The two other histories are for expressions and input lines for the input() function.

As an example, you have done a Last Line mode command, typed five more Last Line mode commands, and then want to repeat the first command again. To do this, in Last Line mode press the <Up> arrow key five times. Another way of doing this is to type the first few letters of the Last Line mode command you want to return to.

The <Up> key will use the text typed so far and compare it with the lines in the history. Only matching lines will be used.

If you do not find the line you were looking for, use the <Down> arrow key to go back to what you typed and correct that. You can also type <Ctrl+U> to start all over again.

To see all the lines in your Last Line mode command history, while in Last Line mode, type:

```
history
```

You will then see a complete history of the Last Line mode commands for this session at the bottom of the screen display.

Your entire search history for this session is displayed by typing history/ in Last Line mode.

<Ctrl+P> will work like the <Up> arrow key, except that it doesn't matter what you already typed. <Ctrl+N> works like the <Down> arrow key.

### The Last Line Mode Command Line Window

Typing any text in the Last Line mode command history to modify a previous command and then execute it is possible but difficult.

A better way to use a modified form of a Last Line mode command from the history is to open the command line window while in Command mode by typing:

```
q:
```

Vim now opens a small utility window at the bottom of the screen. It contains the command line history and an empty line at the end, similar to this illustration:

```
+------------------------------------------------------------+
|other window |
|~ |
|:first.c==========================================|
|:w second.c |
|:w third.c |
|:w fourth.c |
|:w fifth.c |
|:w sixth.c |
|:history
|: |
|:command-line==================================|
||
~/project.c
+------------------------------------------------------------+
```

In the buffer in this small utility window, you are in Insert mode, and can use Insert mode commands to modify text and also move commands. You can use the arrow keys to move around.

Now press <Enter> when on that line, and this command will be executed. The command line window will then close. The <Enter> command will execute the line under the cursor. This works if vim is in Insert mode or in Command mode.

Unfortunately, changes you make in the command line window are lost! They do not result in any changes in the command history itself, but the command you execute when you are in the command line window will be added at the end of the history, similar to all other executed commands. Also, only one command line window can be open at a time.

The command line window is very useful when you want to see your old command history, index to a particular command, edit it, and execute it.

A search command in your history can be used to find something new if you index to it and modify it. For example, if in the command line window one of the lines contained :s/everyone/computer scientists/, you could index to it in the command line window and modify and execute it.

## Word Completion

When you are typing and you enter a partial word, you can cause vim to search for a completion by using <Ctrl+P> (search for previous matching word) and <Ctrl+N> (search for next match).

## Record and Playback

The . (period) command repeats the previous change in Command mode. To accomplish multiple, complex changes in vim Command mode, you can use the record and playback facility. There are three steps in record and playback:

1. The q(register) command starts recording keystrokes into the key named register. The register name must be a letter of the alphabet.
2. Type the commands you want to record in the register.
3. To end recording, press q.

You can now execute the macro by typing the command @register. For example, you have a list of filenames in a buffer that looks like this:

```
stdio.h
fcntl.h
unistd.h
stdlib.h
```

And what you want is the following:

```
#include "stdio.h"
#include "fcntl.h"
```
