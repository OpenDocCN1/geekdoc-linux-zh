
# LAB 64

## Customize and Use the Shell Environment: User Profiles

### Lab Objective

Learn about global and user profiles.

### Lab Purpose

In this lab, you will manage shell profiles and learn which files can be used to customize both global profiles and those for specific users.

### Lab Tool

`Ubuntu 18.04` (or another distro of your choice)

### Lab Topology

A single Linux machine, or virtual machine

### Lab Walkthrough

#### Task 1

Open your favorite editor via the terminal, and take a look at the following files (some of these files may not exist, that's normal):

- `/etc/profile`
- `/etc/skel/bash_profile` and/or `~/.bash_profile`
- `/etc/skel/bash_login` and/or `~/.bash_login`
- `/etc/skel/profile` and/or `~/.profile`
- `/etc/bash.bashrc`
- `/etc/skel/bashrc` and/or `~/.bashrc`
- `/etc/skel/bash_logout` and/or `~/.bash_logout`

Bash attempts to read the first four files (in preference order) every time you start a `login` shell, while it reads the latter two whenever you start an `interactive` shell. Typically, a `login` shell is started once per boot, or once per `SSH` login, while an `interactive` shell is started every time you open the Terminal application (or a new tab within it)—but, as with all things, there are exceptions. Finally, Bash reads `~/.bash_logout` when a `login` shell is exited.
