
## Immediate Solutions

### Maneuvering In vi

To practice maneuvering in vi, do the following:

1. Place this book's companion CD-ROM into your CD-ROM drive.
2. Mount the CD-ROM.
3. Type `cp /mnt/cdrom/textfiles/aesops_fables.txt ~` to copy this file into the home directory for the account you are using.
4. Type `cd ~` to go to the directory where you placed the file.
5. Type `vi aesops_fables.txt` to open the file used in this example.
6. Type `/S FABLES` and press Enter to skip the introductory text--which is worth a read sometime--and jump forward to the beginning of the fables themselves. You now should be on the following line:

```
AESOP'S FABLES
```

7. First, because this file has 82 fables, you need to pick one particular fable to experiment with. Thus, for this example, cursor down to the following line:

```
The Wolf and the Lamb                    Androcles
```

8. Type `0` to jump to the beginning of this line.
9. Type `^` to jump to the first letter in the line, T.
10. Type `w` to jump to Wolf. Do so three more times, jumping first to `and`, and then to `the`, and then to `Lamb`.
11. Type `+` to jump forward to the first letter, T, in the next line:

```
The Dog and the Shadow              The Bat, the Birds, and the
Beasts
```

12. Press `$` (Shift+4) to jump to the last letter in the line, s.
13. Press Ctrl+D four times. Now you should be past all the listings and into the fables themselves.
14. If you are done for now, type `:ZQ` to close the file without saving.

### Filtering Text in vi

To practice filtering text—taking text as input, running a process on it, and then outputting it possibly in another format—in vi, do the following:

1. Log in to the account you want to practice with vi in.
2. Type `vi ~/filter_practice` to create and open the new file filter_practice in your home directory.
3. So far, you have a blank file. Type “i” to enter Insert mode.
4. Type the following:

```
The contents of /var/log are:

ls /var/log
```

5. Press the Esc key to return to Command mode.
6. Type “!!” to tell vi that you want to filter the entire line. At the bottom left of your screen, you should now see:

```
:!
```

7. This prompt is waiting for you to input which filter vi should use to process the line. In the case of ls, you want to process a shell command. Type “sh”—for the bash shell—and press Enter. The entire contents of the /var/log directory are displayed, one item per line. The first six lines of this file are (possibly) now:

```
The contents of /var/log are:

boot.log
boot.log1
boot.log2
boot.log3
```

8. Use the arrow keys to move to the line that contains boot.log.
9. Type “4!!” to tell vi that you want to filter this line and the three after it. You get the filter prompt once again, but this time it looks like this:

```
:..,+3!
```

10. Type “wc” and press Enter to get a word count of each of these files. In the example, this changes the first six lines of the file to the following:

![Image Placeholder](img/e612d46dba3c9205aa19fee9eb8dd0a4_608_0.png)

```
The contents of /var/log are:

4 4 42
cron
cron.1
cron.2
```

11. Type "1G" to go to the beginning of the file.

> *TIP:* Want to see which line is which? Type " :" to enter Line mode, and then type "set number". Press Enter, and now all of your lines are numbered.

12. Type "20!" to filter from lines 1 to 20.

> *NOTE:* You can only filter whole lines.

13. At the prompt, type "sort -r" and press Enter. This rearranges the file in reverse alphabetical order. The first six lines are now as follows:

```
netconf.log
messages.3
messages.2
messages.1
messages
maillog.3
```

Other commands that act as filters are listed in Table 19.17.

**Table 19.17 Some commands that act as filters.**

| Command | Use |
| :--- | :--- |
| awk | A simple programming language that allows manipulation of text patterns |
| grep | A tool for locating text patterns |
| sed | A text editor that does not require you to open a file |
| sh | The bash shell |
| sort | A tool for arranging data |
| tr | A tool for substituting or deleting characters |
| wc | A tool for obtaining word, character, and line counts |

### Copying And Pasting Text In vi

To practice copying and pasting text in vi, do the following:

1. If you have not already installed the “Aesop’s Fables” practice file, place this book’s companion CD-ROM into your CD-ROM drive. If you have already mounted it, skip to Step 4.
2. Mount the CD-ROM.
3. Type “cp /mnt/cdrom/textfiles/aesops_fables.txt ~” to copy this file into the home directory for the account you are using.
4. If the Aesop’s Fables practice file is not already open, type “cd ~” to go to the directory where you placed the file. Otherwise, skip to Step 6.
5. Type “vi aesops_fables.txt” to open the file used in this example.
6. If you are not at the beginning of the file, type “1G” to jump there.
7. Type “/Wolf and the Kid” and press Enter to jump forward to the title in the title list.
8. Type “n” to jump forward to the story “The Wolf and the Kid.”
9. Type “12Y” to copy the entire fable into the buffer. The text “12 lines yanked” appears at the bottom-left portion of your screen.
10. Often, either copy and paste or cut and paste is used to share or move data between different files. Type “:e WolfKid” to enter Line mode and open a second file.
11. Type “p” to paste the fable. Now you have two files open simultaneously.
12. Type “:w” to enter Line mode and save the contents of WolfKid. The following text appears at the bottom of the screen:

```
"WolfKid" [New] 13L, 411C written
```

13. You still have two files open. Type “:rew” and press Enter. Now, you return to the original file.
14. Type “:ZQ” to close the pair of files.

### Indenting Text In vi

To practice indenting text in vi, do the following:

1. Log in to the account you want to practice with vi in.
2. Type “vi ~/indent_practice” to create and open a practice file.
3. Type “i” to enter Insert mode.
4. Type:

```
Left justified.
    Indented.
```

5. Press the Esc key to return to Command mode. Be sure the cursor is on the second line of text still.
6. Type “>” and then press the right-arrow key. Now your text looks like this:

```
Left justified.
    Indented.
```

7. Type “o” to move to the next line and enter Insert mode.
8. Type:

```
The quick
brown fox
jumped over
the lazy
dog.
```

9. Notice that the text here is not indented at all. You do not have the autoindent option enabled. Press the Esc key to return to Command mode.
10. Type “.” to enter Line mode. *(Note: In standard vi/vim, " is usually register selection, but in context of "Line mode" often implying Ex mode ':', it might be a typo for ':', however, strictly following OCR text "Type "." to enter Line mode" is retained, but logically in vi, ':' enters Ex mode. The text says "Type "." to enter Line mode". I will keep it as is but usually it's ':'. Let's look at step 11: "Type 'set autoindent'". This confirms it's Ex mode. The OCR might have misread ':' as '.'. I will correct '.' to ':' based on context of 'Line mode' (Ex mode) and subsequent command 'set autoindent'.)*

*Correction Note:* Step 10 in OCR says `Type “.” to enter Line mode.` Contextually, entering Ex/Line mode in vi is done with `:`. The next step is `Type “set autoindent”`. It is highly probable the OCR misread `:` as `.`. I will correct this to `:` for accuracy.

10. Type “:” to enter Line mode.
11. Type “set autoindent” and press Enter.
12. Make sure the cursor is on the last line of text.
13. Type “o” to start a new line at the end and enter Insert mode.
14. Type:

```
Start of automatic indent.
```

15. Press the Esc key to return to Command mode.
16. Type “>” and press the right arrow to indent the line.
17. Type “o” to start yet another new line and enter Insert mode. Notice that the cursor is directly under the start of the indented text. It should look like this:

```
    Start of automatic indent.
```

18. Type:

```
The indents should follow
whatever is above them.
But I can change the indent level
```

19. Press the Esc key to return to Command mode.
20. Make sure the cursor is on the last line of text. Type “>” and press the right arrow to indent this line.
21. Type “o” to start yet another new line and enter Insert mode. Notice that the cursor is now under the indented B.
22. Type:

```
whenever I want.
```

You should now have the following:

```
Left justified.
Indented.
The quick
brown fox
jumped over
the lazy
dog.
Start of automatic indent.
The indents should follow
whatever is above them.
But I can change the indent level
whenever I want.
```

> TIP: To shut off automatic indenting, go to Command mode and type “:set noautoindent”.

23. To close this file without saving it, type “:q!”. The exclamation point over-rides the warning you would otherwise get for trying to quit without saving.

## Using Regular Expressions

To practice using regular expressions with *ls*, do the following:

1. Place this book’s companion CD-ROM into your CD-ROM drive. If you already have it mounted, skip to Step 3.
2. Mount the CD-ROM.

19. Text processing tools
