```
```
0 bash
1 ps
2 yetanotherwindow
```
```

While working with windows it is important to remember the following:

+   - Windows run their programs completely independent of each other.
+   - Programs will continue to run even if their window is not visible (also when the screen session is detached as we will see shortly).

To remove a window, simply terminate the program running in it (once the last window is removed, screen will itself terminate). Alternatively, use Ctrl + a-k while in the window you want to remove; you will be asked for confirmation:

```
```
Really kill this window [y/n]
Window 0 (bash) killed.
```
```

# ### Regions

screen can divide a terminal screen up into multiple regions in which to accommodate windows. These divisions can be either horizontal (Ctrl + a-s) or vertical (Ctrl + a-|).

The only thing the new region will show is just -- at the bottom meaning it is empty:

```
```
1 ps
--
```
```

To move to the new region, type Ctrl + a-Tab. Now you can add a window by any of the methods that we have already seen, for example: Ctrl + a-2. Now the -- should have turned into 2 yetanotherwindow:

```
```
$ ps
  PID TTY          TIME CMD
 1020 pts/2    00:00:00 bash
 1033 pts/2    00:00:00 ps
$ screen -t yetanotherwindow
```
```