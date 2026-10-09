
# LAB 97

## Perform Security Administration Tasks: System Auditing

**Lab Objective:**

Learn how to manage and audit ports, processes, and other system aspects.

**Lab Purpose:**

In this lab, you will review a variety of tools used to manage services, ports, file permissions, and other features to maintain a secure Linux system.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

### Lab Walkthrough:

#### Task 1:

Open the Terminal and run:

```
sudo find / -perm /u+s,g=s -type f -exec ls -l {} \; 2>/dev/null
```

That's a hairy command, so let's break it down. Here, you're finding all files on the system with either the `setuid` or `setgid` bits set (or both), which are regular files (and not directories) or some other special file). Then you execute `ls -l` on each of those files. The `2>/dev/null` is just to silence some spurious errors about special filesystems like `/proc`.

The end result should be a detailed list of possibly “insecure” files on your system—files which are run with their owner and/or group permissions instead of the permissions of the user who executed them.
