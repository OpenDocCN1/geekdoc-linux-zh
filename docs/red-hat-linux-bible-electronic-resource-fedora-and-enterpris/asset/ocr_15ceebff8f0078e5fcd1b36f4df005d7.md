```
383  ls /usr/bin | sort -a | more
384  man sort
385  cd /usr/local/bin
386  man more
387  useradd -m /home/chris -u 101 chris
388  passwd chris
389  history 8
```

A number precedes each command line in the list. There are several ways to run a command immediately from this list, including:

+   - **Run Command Number (1n)** — Replace the $n$ with the number of the command line, and the command line indicated is run.
+   - **Run Previous Command (!!)** — Runs the previous command line.
+   - **Run Command Containing String (!?string?)** — Runs the most recent command that contains a particular *string* of characters.

Instead of just running a *history* command line immediately, you can recall a particular line and edit it. You can use these keys to do that:

+   - **Step (Arrow Keys)** — Press the up ($\uparrow$) and down ($\downarrow$) arrow keys to step through each command line in your history list to arrive at the one you want. (Ctrl+p and Ctrl+n do the same functions, respectively.)
+   - **Reverse Incremental Search (Ctrl+r)** — After you press these keys, you are asked to enter a search string to do a reverse search. As you type the string, a matching command line appears that you can run or edit.
+   - **Forward Incremental Search (Ctrl+s)** — After you press these keys, you are asked to enter a search string to do a forward search. As you type the string, a matching command line appears that you can run or edit.
+   - **Reverse Search (Alt+p)** — After you press these keys, you are asked to enter a string to do a reverse search. Type a string and press Enter to see the most recent command line that includes that string.
+   - **Forward Search (Alt+n)** — After you press these keys, you are asked to enter a string to do a forward search. Type a string, and press Enter to see the most recent command line that includes that string.
+   - **Beginning of History List (Alt+<)** — Brings you to the first entry of the history list.
+   - **Beginning of History List (Alt+>)** — Brings you to the last entry of the history list.

Another way to work with your history list is to use the `fc` command. Type `fc` followed by a history line number, and that command line is opened in a text editor. Make the changes that you want. When you exit the editor, the command runs. You could also give a range of line