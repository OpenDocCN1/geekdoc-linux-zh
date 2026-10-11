**NOTE** We'll discuss environment variables in more depth later in this chapter.

Let's practice using command history in the following exercise.

# Exercise 2-3: Using Command History

**VIDEO** For more information watch *Exercise 2-3*.

In this exercise, you will practice using command history in the bash shell. Complete the following:

+   1. Boot your Linux system to a shell prompt. If your system booted into a graphical system, log in and then press **CTRL-ALT-F1**.
+   2. Authenticate to your system.
+   3. At the shell prompt, enter `ls -l /var/log`.
+   4. At the shell prompt, enter `pwd`.
+   5. At the shell prompt, enter `whoami`.
+   6. Run the `ls` command in Step 3 again by pressing the UP ARROW key three times and then pressing **ENTER**.
+   7. Use the UP ARROW key to run the `pwd` command again.
+   8. Use the UP ARROW key to run the `whoami` command again.

In addition to command history, the bash shell also offers command completion. Let's talk about this feature next.

# Using Command Completion

In addition to command history, I also love the command completion feature offered by the bash shell. This feature is extremely helpful when you need to enter a very long filename in a command line. The command completion feature allows you to simply press the **TAB** key while entering a command at the shell prompt. When you do, the bash shell “guesses” what it is you want to type and then automatically completes the command for you.

For example, suppose a file named `vmware-linux-tools.tar.gz` exists in the /tmp directory. I need to extract this tarball archive so I can install the application it contains. If I wanted to, I could type out the full command `tar -zxvf /tmp/vmware-linux-tools.tar.gz` at the shell prompt and tar would extract the file for me.

**NOTE** We'll discuss how the `tar` command works in more detail later in this book.