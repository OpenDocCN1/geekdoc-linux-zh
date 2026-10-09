# LAB 74

# Manage User and Group Accounts and Related System Files:  
Special Purpose Accounts

**Lab Objective:**  
Learn how to manage special-purpose user accounts.

**Lab Purpose:**  
In this lab, you will learn about the special purpose and limited user accounts, and how to create and manage them.

**Lab Tool:**  
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**  
A single Linux machine, or virtual machine

# **Lab Walkthrough:**

*Task 1:*  
Open the Terminal and add a system user: `sudo useradd -r foo`

When adding a system user, `useradd` does not any account or password aging information, and sets a user ID appropriate for a system user (typically below 1000). It also does not create a home directory unless you specify -m.

`getent` is a cleaner way of getting entries from `passwd`, `group`, and other administrative databases. Inspect the new user with: `sudo getent passwd foo`

`getent --help` will tell you which databases are supported.