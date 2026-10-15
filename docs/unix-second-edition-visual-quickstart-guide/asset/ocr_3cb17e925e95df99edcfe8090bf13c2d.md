# 3. hairy spiders lurk

In input mode, type anything you want. Everything you type will show up on the screen until you return to command mode by pressing Esc. When you are in command mode, you can use the arrow keys to navigate up and down in the file line by line and Ctrl F and Ctrl B to scroll one screen forward and backward, respectively.

# ✓ Tips

+   - To get help for vi, type man vi. See Chapter 1 for more about man pages.

+   - If you’re not sure what mode you’re in, press Esc to go into command mode. If you’re already in command mode, you’ll hear a beep. If you’re in input mode, you’ll change to command mode.

+   - Many Unix-like systems, including Linux and Mac OS, actually provide a program called vim in the place of vi. vim (VI iMproved) is like vi but feature-rich and more flexible, and you still start it with the command vi.

+   - You can open specific files or even multiple files when you access vi. At the shell prompt, type vi filetoedit (or whatever) to open a specific file. Or, for example, type vi *.html to open all of the HTML documents in a directory, then use Esc :n (for "next") to move to each subsequent file.

+   - See Adding and Deleting Text in vi later in this chapter for more details about editing in vi.