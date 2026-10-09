
# LAB 98

## Setup Host Security: User Security

**Lab Objective:**

Learn how to use login-related features to secure a Linux host.

**Lab Purpose:**

In this lab you will review shadow passwords and login restriction features to secure a Linux host.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

We've discussed the `/etc/shadow` file in previous labs, but now we're going to take a closer look at it. The second field in a given shadow file entry is the password, obfuscated by a one-way hashing algorithm. Most users are probably system users and thus don't have passwords, but at least your user should.

Take a look at `man 3 crypt`—this is how those hashes are created. The man page notes that a hash is split into 3 sections, delimited by dollar signs. The first is an ID denoting the encryption method. Look at your shadow hash again—what is the ID number in the first field? If it's a 6, then your password is hashed with SHA-512 and you're in good shape. If it's a 5, your hash is SHA-256—not the best, but still pretty good. A password hash beginning with a 1 is MD5, and only likely if the hash was copied from an older system. (If you have any hashes like that, you should run `passwd` for those users to change them.)
