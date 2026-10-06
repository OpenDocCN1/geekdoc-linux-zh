# 106 Linux Administration: A Beginner's Guide

![](bbox=[0.338, 0.115, 0.661, 0.252])

Figure 4-2 DPMS triangle

# # APT

APT is a highly regarded and sophisticated toolset. It is an example of a wrapper tool that interacts directly with **dpkg**. APT is actually a library of programming functions that is used by other middle-ground tools, such as **apt-get** and **apt-cache**, to manipulate software on Debian-like systems. Several user-land applications have been developed to rely on APT. (*User-land refers to programs and tools.*) Examples of such applications are **synaptic**, **aptitude**, and **dselect**. The user-land tools are generally more user-friendly. APT has also been successfully ported to other operating systems.

One difference between APT and **dpkg** is that APT does not directly deal with .deb packages; instead, it manages software via the locations (repositories) specified in configuration files. The main file is **sources.list**. APT utilities use the **sources.list** file to locate archives (or repositories) of the package distribution system in use on the system.

It should be noted that any components of the DPMS (**dpkg**, APT, or the GUI tools) can be used to manage software directly on Debian-like systems. The tool of choice depends on the user's level of comfort and familiarity with the tool in question.

Figure 4-2 shows what can be the “DPMS triangle.” The tool at the apex of the triangle (*dpkg*) is the most difficult to use and the most powerful, followed by the next easiest to use (APT), and the user-friendly user-land tools.

# # Software management in Ubuntu

As mentioned earlier, software management in the Debian-like distros as Ubuntu is done using DPMS and all the attendant applications built around it, such as APT and **dpkg**. In this section, we will look at how to perform basic software management tasks on Debian-like distros.

# # Querying for Information

On your Ubuntu server, the equivalent command to list all currently installed software is

```
master@ubuntu:~~$ dpkg -1
```