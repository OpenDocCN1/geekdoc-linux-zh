Go Team Banzai! Go Team Banzai! Go Team Banzai!

Can you see where the cursor is? To find out line number the cursor is on,
press ^g, and the information is listed on the status line at the bottom:

```
"buckaroo.confused" [Modified] line 10 of 11, column 1  --990--
```

There's lots of information here, including the name of the file
buckaroo.confused), an indication that vi thinks I've changed it since I started the
program ([Modified]), the current line (10), total lines in the file (11), what column
'm in (1), and finally, an estimate of how far into the file I am (90%).

+   2. Even lines? Count the display again. There are 12 lines. What's going on?
an answer will become clear if I turn on line numbering for the entire file. To do this,
I type : , which zips the cursor to the bottom of the screen, where I then enter

```
:set number_
```