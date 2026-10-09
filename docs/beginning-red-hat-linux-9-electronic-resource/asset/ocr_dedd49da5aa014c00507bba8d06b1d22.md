+   - Linux can be configured to execute user-specific setup procedures at the time that user logs in. In particular, a user is prevented from performing special (often sensitive) tasks, such as the following, unless that user has administrator privileges:
+   
+   - Every program started by the user is associated to that user's account, and can be identified afterward. Moreover, each program will have access only to those resources that the owner can access.

# ### Superusers and Normal Users

Many large systems make a distinction between an **administrator** (or **superuser**) and a **normal user**. In particular, a user is prevented from performing special (often sensitive) tasks, such as the following, unless that user has administrator privileges:

+   - Global maintenance, personalization, and upgrade of the system
+   - Global installation of applications, devices, and their drivers
+   - Periodic backup of data
+   - User account management

It is the administrator's work that leaves normal users free to carry out their day-to-day tasks. Indeed, in very large environments with many thousands of users, system administration is a full-time job. In these environments, it's easy to see why it makes sense to differentiate between superusers and normal users. If administration were left down to the individual users, regardless of their expertise or authority, then the lack of policy and control could be catastrophic – risking the stability of the system, performance levels, security violations, and so on.

In fact, the distinction between superusers and normal users is also enforced in *all* Linux installations – even on small Linux computers that are used by only one person. Why? Well, many of the same arguments that apply on large networks *also* apply on the smallest installations! For example, while the superuser account is very useful for performing certain tasks, it's definitely a mistake to work as superuser when you're performing more "everyday" tasks like reading e-mails. It's not only that you don't *need* superuser privileges to read your e-mail – it's also about protecting yourself from accidentally damaging your system integrity.

The administrator account in Red Hat Linux (as in almost every other operating system of Unix heritage) is called **root**. The power of *root* is so extensive that almost no task is forbidden for this account. While it's impossible for a normal user to delete system files, root is able to delete them all too easily.

For this reason, the root account should be used with great care. Red Hat recommends that you create a personal account as part of the Linux installation, and we did that back in Chapter 1. If you are currently logged into your Linux system using the root account, it is a good idea to log out now and log back in with a normal (non-root) account.