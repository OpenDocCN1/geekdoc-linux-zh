# 19

# ADVANCED SECURITY FEATURES

![](bbox=[0.4, 0.21, 0.59, 0.34])

FreeBSD includes a variety of tools for securing network traffic and users. Some of these tools are invisible to sysadmins but work behind the scenes to increase security, such as the sandboxing API capsicum(4). Packet filtering lets you control who can access your system. You can also use blacklisting to block network addresses that keep poking at your host. In addition, FreeBSD has a whole bunch of optional security features you can enable either in the installation process or later. In this chapter, we’ll examine these tools and techniques, look at monitoring your system’s security, and discuss how to react if you suffer an intrusion.

Let’s start with a core security topic: unprivileged users.

# Unprivileged Users

An unprivileged user is a specific user for a specific task. He has only the rights necessary to perform that limited task. Many programs run as unprivileged users or use unprivileged users to perform specific duties.

“Only the rights needed to perform its duties” sounds like every user account, doesn’t it? That’s true, but the account used by the least privileged human being still has more rights than many programs need. Anyone with shell access has a home directory. The normal user may create files in their home directory, run text editors, or process email.