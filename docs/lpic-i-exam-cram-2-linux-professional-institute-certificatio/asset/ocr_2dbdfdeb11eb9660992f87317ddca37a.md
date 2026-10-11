Better yet, after comparing something or getting a filename straight, you can close all the other split windows and just have the current window open by entering the following:

```
:only
```

![](bbox=[0.08, 0.25, 0.18, 0.32])

> Many times I’ve opened a couple of split windows to see the difference between two files or used the **diff** command. The easiest way to compare two files and make edits to them is to use the **vimdiff** command, such as
> 
> **vimdiff file1 file2**
> 
> This loads the two files into a vertically split **vim** session and uses color and other symbols to show you what is similar or different between the two files. This is useful for comparing a log file before and after a problem or two configuration files to see why one doesn’t work.