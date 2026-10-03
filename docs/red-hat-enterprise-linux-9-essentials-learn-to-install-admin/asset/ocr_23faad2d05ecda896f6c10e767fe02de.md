![](bbox=[0.31, 0.075, 0.74, 0.185])

Figure 1-1

# 1.3 Editing Files

Configuring a Linux system typically involves editing files. For those new to Linux it can be unclear which editor to use. If you are running a terminal session and do not already have a preferred editor we recommend using the nano editor. To launch nano in a terminal window simply enter the following command:

```
# nano <file>
```

Where <file> is replaced by the path to the file you wish to edit. For example:

```
# nano /etc/passwd
```

Once loaded, nano will appear as illustrated in Figure 1-2:

![](bbox=[0.245, 0.445, 0.805, 0.72])

Figure 1-2

To create a new file simply run nano as follows:

```
# nano
```

When you have finished editing the file, type Ctrl-S to save the file followed by Ctrl-X to exit. To open an existing file, use the Ctrl-R keyboard shortcut.

If you prefer to use a graphical editor within the GNOME desktop environment gedit is a useful starting point for basic editing tasks. To launch gedit from the desktop press Alt-F2 to display the Enter a Command window as shown in Figure 1-3: