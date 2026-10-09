# LAB 44

# Perform Basic File Management: Find and Globbing

**Lab Objective:**
Learn how to use advanced filename expansion in Bash, as well as the *find* command to locate and act on specific files.

**Lab Purpose:**
In this lab, you will learn about shell globbing, and how to use the *find* command to locate files based on type, size, etc. and execute commands on those files.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*
It is important to understand that, although shell globbing shares some commonalities with regular expressions, Bash itself does not recognize the full regex syntax. Instead, Bash simply recognizes and expands wild cards.

Open the **Terminal** and run:

+   • `mkdir lab44`
+   • `cd lab44`
+   • `touch a1 a2 a12 b1 b2 b12 c1 c2 c12`

*Task 2:*
To understand how advanced globbing works, run the following commands and observe the output (on the right):

+   • `ls a?` a1 a2