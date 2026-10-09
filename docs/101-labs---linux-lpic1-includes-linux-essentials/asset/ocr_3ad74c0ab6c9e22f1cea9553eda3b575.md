# LAB 22
Basic Security and Identifying User Types

**Lab Objective:**
Learn how to identify the differences between the root user, standard users, and system users.

**Lab Purpose:**
In this lab, you will learn about the different types of Linux users and a few tools to identify and audit them.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*
Open the Terminal and run: `cat /etc/passwd`

This file is an inventory of all users on your system. The passwd file is a database with seven fields, separated by colons:

+   1. Username
+   2. Encrypted password (in practice, hardly ever used—see below)
+   3. User ID
+   4. Group ID
+   5. Comment
+   6. Home directory
+   7. Default shell

Take note of the *root* user, which should be listed on the first line. This is the administrative user, and is the only user that can unconditionally do anything on the system. By running