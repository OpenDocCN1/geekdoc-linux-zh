Note that the status line displays **?is**. The ? tells you that you are searching backward in the file for the pattern is.

+   g. Press <N> to continue the search in the opposite direction.

Note that the status line now indicates /is to tell you that you are searching forward in the file for the pattern is.

+   5. In this exercise you will search for “right.”

+   a. Move the cursor to the first character in the file.

+   b. Press </>

+   c. Type **right**

+   d. Press <Enter> to search forward in the file for the pattern **right**.

Note that the pattern **right** is part of the larger pattern **bright**.

In the next group of exercises, you will **yank**, **delete**, and **put** to copy and move text. In the Windows and Mac environments, we use the term “copy” to mean just what it says. In vi terminology, we use “yank” to copy. In the Windows and Mac environments, we “paste” to insert the contents of the buffer known as the “Clipboard.” In vi terminology, we “put” to insert the contents of the unnamed buffer. “Yank” = “copy.” “Put” = “paste.”

+   6. In this exercise, you will use <yw> to copy a small word forward.

+   a. Move the cursor to the first character in the file.

+   b. Press <6w> to place the cursor on the word “good.”

+   c. Press <yw> to copy a word forward to the unnamed buffer.

+   d. Press <nj> to move the cursor down to the line and position you see in Figure 13-1. (The value of n will be either 3 or 4, depending on the number of columns your terminal displays.)

![](bbox=[0.17, 0.72, 0.83, 0.83])

+   e. Press <3B> to move the cursor back to the word “time” in the previous sentence.