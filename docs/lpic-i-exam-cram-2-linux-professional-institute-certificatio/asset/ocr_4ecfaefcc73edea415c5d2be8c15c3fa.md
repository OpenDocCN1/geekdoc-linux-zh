# Editors

The LP1 exams focus on *vi* as the default editor for Linux. No matter how much you think *emacs* rocks, or that *pico/nano* is much easier to use with the onscreen menus, it’s essential that you have basic *vi* skills.

# Modes in vi

One of the most confusing things about *vi* is the presence of *modes*, or states, in the editor. The three modes are

+   - Command
+   - Insert
+   - LastLine

# Editing in Vi

*vi* always starts in Command mode. True editing takes place in what’s known as Insert mode. The keys you commonly use to invoke Insert mode from Command mode are

+   - *i*—The most common method of moving into Insert mode is to press the i key, leaving the cursor at the current position. All typing from that point pushes existing text to the right.
+   - *I*—The uppercase I key moves to the beginning of the current line and from there acts like the i key.
+   - *a*—The second most common method is to press the a key, moving the cursor one character to the right, essentially behaving like an i key after that.
+   - *A*—The uppercase A moves to the end of the current line and from there acts like an a key.
+   - *o*—Use this key to open a new line under the present line. For example, if you’re on line 3 in Command mode, pressing o drops line 4 down to become 5 and opens a new line 4 that’s empty.
+   - *O*—The uppercase O opens a new line at the current line. For example, if you’re on line 3, pressing O drops line 3 down to become line 4 and opens a new empty line 3 for editing.