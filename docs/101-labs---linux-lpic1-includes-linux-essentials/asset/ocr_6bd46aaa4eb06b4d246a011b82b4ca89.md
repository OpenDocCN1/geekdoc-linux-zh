
# LAB 63

## Find System Files and Place Files in the Correct Location

**Lab Objective:**

Learn how to locate files on a Linux system.

**Lab Purpose:**

In this lab, you will learn multiple ways of locating files on a system, in accordance with the Filesystem Hierarchy Standard (FHS).

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

In previous labs, you've worked with `find`, a tool which can find files fitting a certain specification and even execute commands on those files. `find` is great for a limited scope, but becomes unwieldy when you don't actually know where a given file is located, because then it has to search the entire filesystem! There's another way. Open the Terminal and run:

```
sudo updatedb
locate updatedb.conf
```

As you might guess, `locate` operates from a database which is updated by `updatedb`. The `updatedb` command may take a couple of minutes, but once it's done, every subsequent `locate` will be very fast.

Here, you should have found two files: One is the actual `updatedb` config file, and the other is the man page. You can investigate these now if you like:

```
cat /etc/updatedb.conf
```
