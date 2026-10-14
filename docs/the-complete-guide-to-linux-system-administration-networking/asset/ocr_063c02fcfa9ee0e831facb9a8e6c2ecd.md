Similarly, when you use the :q command to exit from vi, vi warns you if you have made changes to the file but have not saved them (you haven't used :w). In this case you have several options:

+   - Enter :wq in command mode to write the file (save it) and quit (exit from vi) at the same time.
+   - Press ZZ in command mode. This operates just like entering :wq but is a bit quicker. Be careful about getting into too much of a habit of using ZZ, however, because sometimes you don't really want to save changes you might have made!
+   - Enter :q! to override the safety feature and quit vi without saving your work—discarding your changes.

# Screen Repositioning

In addition to the arrow keys (along with the h,j,k, and l keys, which imitate arrow keys in command mode), and Page Up and Page Down, vi supports many additional methods of positioning your cursor within the text of a file you are editing. These are especially useful when you are editing (or just viewing) a very large text file.

In Figure 5-5, notice the 92,20 in the bottom-right corner of the screen. These numbers indicate the line number and cursor position on the line, respectively. You can watch them change as you move around in a file.

![](bbox=[0.17, 0.75, 0.75, 0.9])

Figure 5-5 Cursor position information in vi