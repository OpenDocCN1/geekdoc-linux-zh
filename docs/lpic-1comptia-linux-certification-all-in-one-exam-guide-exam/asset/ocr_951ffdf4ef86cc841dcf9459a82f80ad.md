# Managing Ownership, Permissions, and Quotas

In this chapter, you will learn about

+   Managing file ownership
+   Mounting file and directory permissions
+   Administering disk quotas

Recall that in an earlier chapter we identified two tasks for you to accomplish when managing user access to a Linux system:

+   Control who can access the system.
+   Define what users can do after they have logged in to the system.

We addressed the first point earlier. We control who accesses the system by implementing users and groups. In this part of this chapter, we're going to address the second point. We need to define what users can do after they have logged in to the system. Let's begin by discussing file and directory ownership.

# Managing Ownership

To effectively control who can do what in the file system, you need to first consider who “owns” files and directories. We're going to discuss the following in this regard:

+   How ownership works
+   Managing ownership from the command line

Let's start by discussing how ownership works.

# How Ownership Works

Anytime a user creates a new file or directory, his or her user account is assigned as that file or directory's “owner.” For example, suppose the ksanders user logs in to her Linux system and creates a file named contacts.odt using OpenOffice.org in her home directory. Because she created this file, ksanders is automatically assigned ownership of contacts.odt. By right-clicking on this file in the system's graphical user interface and selecting Properties | Permissions, you can view who owns the file. This is shown in Figure 11-1.