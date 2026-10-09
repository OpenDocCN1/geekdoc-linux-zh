# LAB 85

# Mail Transfer Agent (MTA) Basics: Other MTAs

Lab Objective:

Learn about other major MTAs, like Sendmail and Exim.

Lab Purpose:

In this lab, you will experiment with MTAs other than Postfix (which was featured in Lab 84).

Lab Tool:

Ubuntu 18.04 (or another distro of your choice)

Lab Topology:

A single Linux machine, or virtual machine

Lab Walkthrough:

Task 1:

First, install Exim: `sudo apt install exim4`

Like Postfix, Exim also has an emulation layer for the classic Sendmail. If you check the man pages for commands like `newaliases` or `mailq`, you will instead see the man page for `exim4`.

You can do all of the things with Exim that you did in Lab 84, including aliases and sending mail with `sendmail`. (The `mail` command is actually part of a different package, `mailutils`.)

Task 2:

Now, install the venerable Sendmail: `sudo apt install sendmail-bin sendmail`

This is the classic MTA, so it doesn’t have an emulation layer… though it may feel like it does, just because of how long some commands can take. (Compare the run time, for instance, of `newaliases` under Sendmail vs. under Postfix.)