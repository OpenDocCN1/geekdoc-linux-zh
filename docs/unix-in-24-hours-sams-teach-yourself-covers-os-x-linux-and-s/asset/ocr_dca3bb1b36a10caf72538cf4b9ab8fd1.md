line above the current line.

+   1. For this task, you need to start with a clean file, so quit from the big.output editing session and start vi again, this time specifying a nonexistent file called buckaroo:

```
% vi buckaroo
```

![](bbox=[0.12, 0.19, 0.9, 0.52])

Notice that vi reminds you that this file doesn’t exist; the bottom of the screen says New file instead of indicating the number of lines and characters.

+   2. Now it’s time to try using insert mode. Try to insert a k into the file by typing k once:

![](bbox=[0.12, 0.69, 0.9, 0.79])

The system beeps at you because you haven’t moved into insert mode yet, and the k still has its command meaning of moving down a line (and, of course, there isn’t another line yet).

Type i to move into insert mode and then type k again:

![](bbox=[0.12, 0.94, 0.9, 1.04])

There you go! You’ve added a character to the file.

+   3. Press the Backspace key to move the cursor over the letter k:

![](bbox=[0.12, 1.16, 0.9, 1.26])