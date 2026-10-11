What is your name? --> Fred
Hello Fred
[root@server1 root]# _

Note from the preceding output that the `echo` command used to pose a question to the user ends with `-->` to simulate an arrow prompt on the screen and the `\c` escape sequence to place the cursor after the arrow prompt; this is common among Linux administrators when writing shell scripts.

# ## Decision Constructs

**Decision constructs** are the most common type of construct used in shell scripts; they alter the flow of a program based on whether a command in the program completed successfully or based on a decision that the user makes given a question posed by the program. This is reflected in Figures 8-4 and 8-5.

![](bbox=[0.18, 0.415, 0.55, 0.67])

![](bbox=[0.13, 0.71, 0.6, 0.935])