# # Answers to Explorational Exercises

+   1. Both **screen** and **tmux** can enter command line mode through *command prefix* `:` (we already saw a brief example with **tmux**). Do some research and the following tasks in command line mode:
+      * Make **screen** enter copy mode:
+        `Ctrl + a`—then, we type `copy`.
+      * Make **tmux** rename the current window:
+        `Ctrl + b`—then, we type `rename-window`.
+      * Make **screen** close all windows and terminate session:
+        `Ctrl + a`—then, we type `quit`.
+      * Make **tmux** split a pane into two:
+        `Ctrl + b`—then, we type `split-window`.
+      * Make **tmux** kill the current window:
+        `Ctrl + b`—then, we type `kill-window`.
+      2. When you enter copy mode in **screen** not only can you use the arrow keys and `PgUp` or `PgDown` to navigate the current window and the scrollback buffer. There is also the possibility of using a vi-like full screen editor. Using this editor, perform the following tasks:
+         * Echo `supercalifragilisticexpialidocious` in your `screen` terminal:
+           
+           ```bash
+           echo supercalifragilisticexpialidocious
+           ```
+         * Now, copy the five consecutive characters (left-to-right) in the line right above your cursor:
+           We enter copy mode: `Ctrl + a` or `Ctrl + b` and then type `copy`. Then, we move to the line above using `k` and press `space` to mark beginning of selection. Finally, we move forward four characters using `l` and press `space` again to mark the end of the selection.
+         * Finally, paste the selection (`stice`) back at your command prompt:
+           `Ctrl + a`