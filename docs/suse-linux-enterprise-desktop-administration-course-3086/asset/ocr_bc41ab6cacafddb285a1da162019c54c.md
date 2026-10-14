external command (called by the shell), an alias, or a function. The option -a delivers all instances of a command bearing this name in the file system.

The following is an example of using the type command:

```
```text
geeko@da10:~ > type type
type is a shell built in
geeko@da10:~ > type grep
grep is /usr/bin/grep
geeko@da10:~ > type -a grep
grep is /usr/bin/grep
grep is /bin/grep
geeko@da10:~ >
```
```

![](bbox=[0.034, 0.322, 0.219, 0.393])

# Exercise 7-6: Find Files on Linux

In this exercise, find files with the **whereis**, **which**, and **find** commands and with the GNOME Search Tool.

# Detailed Steps to Complete This Exercise

+   - Part I: Use the Commands whereis and which
+   - Part II: Use the GNOME Search Tool
+   - Part III: Use the find Command

# Part I: Use the Commands whereis and which

To use the whereis and which commands, do the following:

+   1. Open a terminal window.
+   2. Find the type of the ll command by entering
+      ```text
+      type ll
+      ```
+   3. Find the manual pages of the find command by entering
+      ```text
+      whereis -m find
+      ```
+   4. Find the path of the Firefox program by entering
+      ```text
+      which firefox
+      ```

# Part II: Use the GNOME Search Tool

To use the GNOME Search Tool, do the following:

+   1. Start the GNOME Search Tool (Computer > More Applications > System > GNOME Search Tool).