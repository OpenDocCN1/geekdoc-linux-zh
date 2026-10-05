this chapter, use bold text for the bits you type and use normal text for the computer's output:

```
pi@raspberry ~ ls
Desktop Downloads Pictures python-games Videos
Documents Music Public Templates
```

Linux is case-sensitive, which means LS, ls, and l are completely different instructions. Linux doesn't see uppercase and lowercase letters as related to each other, so an a 5 and an l look like completely different symbols to the computer, in the same way that an A and a look different to humans. If you get the capitalization wrong in your command, it won't work, and applies everything in the shell. If you place a capital letter in a filename, Linux thinks the file you doesn't exist. When you come to use more-advanced command options, you might find that some commands use upper- and lowercase options mean different things.

![](bbox=[0.175, 0.218, 0.238, 0.282])

# # Changing directories

The output is all blue, which means these are all directories, so you can go into them to look at the files they have inside. The command to change directory is cd, and you use it with the name of the directory you would like to go into:

```
pi@raspberry ~ cd python_games
```

The prompt changes to show the directory you have changed after the tilde character, and you can double-check that the current directory has changed by ls to view the files.

# # Checking file types

If you want to find out about a particular file, you can use the file command. After the command name, the name of the file you'd like more information on. You can list several files in one command by separating them with spaces, like:

```
pi@raspberry ~/python_games file body.png match0.wav wormy.py
body.png: PNG image data, 50 x 85, 8-bit/color RGBA, non
interaced
match0.wav: RIFF (little-endian) data, WAVE audio, Microsoft
PCM, 16 bit, mono 44100 Hz
wormy.py: Python script, ASCII text executable
```

CHAPTER 5 Using the Linux Shell 89