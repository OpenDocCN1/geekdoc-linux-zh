
# LAB 34

## Manage Shared Libraries

### Lab Objective:

Learn how to identify and install shared libraries.

### Lab Purpose:

Shared libraries provide common functionality to one or more (often many more) Linux applications. In this lab, you will learn how to manage these very important libraries.

### Lab Tool:

Ubuntu 18.04 (or another distro of your choice)

### Lab Topology:

A single Linux machine, or virtual machine

### Lab Walkthrough:

**Task 1:**

Open the Terminal and run:

```
cat /etc/ld.so.conf*../d/*)
```

(The above syntax is a shortcut for `/etc/ld.so.conf/d/*`.)

These files are used to define shared library directories to be used by `ldconfig`. When run as root, `ldconfig` creates links and cache (used when linking a new program) to the most recent libraries in those directories, plus the “trusted” directories of `/lib`, `/usr/lib`, `/lib64`, and `/usr/lib64`.

**Task 2:**

Now run `ldd $(which passwd)`

This command tells you which shared libraries are linked by the `passwd` tool. The results will vary by implementation, but nearly every program should link to `libc.so.6`, among several others, at a minimum.
