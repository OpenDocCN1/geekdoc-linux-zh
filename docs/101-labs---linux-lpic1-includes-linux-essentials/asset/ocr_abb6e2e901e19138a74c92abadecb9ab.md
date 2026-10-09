# LAB 55

# Basic File Editing: vi Modes

**Lab Objective:**
Learn how to use modes within the $vi$ editor.

**Lab Purpose:**
In this lab, you will learn about one of the classic (but often opaque to new users) Linux text editors, $vi$.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

# **Lab Walkthrough:**

# *Task 1:*

Open the Terminal and run $vi\ Tab55.txt$. Now, explore the modes of $vi$:

+   * Type i to enter insertion mode, and enter a few lines of text. Type ESC to leave this mode.
+   * Navigate to the middle of a line and type a to enter insertion mode one character after the cursor's position. Enter more text or hit ESC to exit the mode.
+   * Navigate to the middle of a line and type I to insert text at the beginning of this line. Hit ESC to exit insertion mode.
+   * Type A to add text at the end of the current line. Again, hit ESC to exit.
+   * Navigate to a line and type o to add a line of text below it. Hit ESC to exit insertion mode.
+   * Type O to add a line of text above the line where your cursor is. Again, hit ESC to exit.
+   * Use y to copy ("yank") text; for example, y$ to yank from the cursor to the end of a line, or yy to yank the whole line. Then, press p to paste.