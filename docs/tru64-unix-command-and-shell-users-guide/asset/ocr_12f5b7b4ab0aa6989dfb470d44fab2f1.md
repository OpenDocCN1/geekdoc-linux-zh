In the sample text below, notice the use of the Escape key on the last line of input and the use of the :wq command to save the file and exit the vi editor. Type the sample text exactly as shown. If you make a mistake, use the Backspace key to correct it; press the Return key where indicated to move to the next line of text:

```
You can use this text file **Return**
 to experiment with vi. **Return**
 The examples shown here **Return**
 will teach you the basics of vi. **Escape**
~
~
~
~
~
:wq

"my.file" 4 lines, 108 characters
$
```

> **Note**
> 
> Depending upon how your terminal or workstation is set up, the Escape key may be programmed to perform a different function. It is possible that one of the function keys on your keyboard (possibly F11) may have been set up to perform the escape function. See your system administrator if your Escape key does not operate properly.

Pressing the Escape key while vi is in the input mode puts vi back into the command mode; once in the command mode vi interprets anything you type to be a command. The :wq command writes (saves) the file with the name my.file into your current directory and quits the vi editor.

The format of the :wq command is much different from other vi commands because :wq is not a vi command; it is an ex command. When you press a colon (:) when vi is in the command mode, notice that it appears at the bottom of the screen. The colon (:) begins all ex commands from within vi. All ex commands are executed when vi is in the command mode. You must press the Return key after the command to signify to ex that you are finished entering the command. See Section A.3 to learn more about ex commands.

If you lose track of which mode vi is in, press the Escape key a few times to make sure vi is in the command mode. If your system is so configured, you will hear a bell when you press the Escape key that signals that vi is indeed in the command mode.