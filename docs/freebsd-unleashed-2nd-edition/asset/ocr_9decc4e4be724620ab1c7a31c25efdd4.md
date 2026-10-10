# CHAPTER 9

# Users, Groups, and Permissions

U sers and file permissions are the concepts that form the
 central pillars of a Unix system. Administering a system that
 is designed for multiuser operation imposes many more
 restrictions than you experience when administering single-
 user desktop systems. These restrictions serve to prevent
 much of the uncontrollable complexity that occurs when
 every operation on a machine is, in effect, done by the
 “super-user” (as is the case in Windows and other such
 systems).

Traditional desktop operating systems, such as Windows
 95/98/Me and classic Mac OS, give the impression of being
 multiuser operating systems; however, strictly speaking, they
 are not. What they use, instead, are simply profiles, or ways
 of presenting data according to each user's preferences. Any
 action the user wants to take on the local machine, such as
 reading files, installing programs, or shutting down the
 computer, is permitted because there is only one “user” with
 absolute control over the machine. Access to network
 resources is done on a “guest user” basis, without the user or
 the machine participating in any true authentication with a
 domain or its equivalent.

Windows NT and 2000, however, have taken successive steps
 toward becoming true multiuser operating systems like
 FreeBSD. Each user in the system has a separate account and a
 set of permissions that control access to files, printers, and
 other resources. Windows and FreeBSD both have the concept
 of a “root” user, or administrator, who has absolute power
 over the local machine. Both systems have groups and differ-
ent layers of accessibility. In fact, Windows NT/2000 permis-
sions have such complexity—inherence upward, inheritance
 downward, domain users versus local users, and up to three

# IN THIS CHAPTER

+   • Introduction to Users and
+    Groups
+   • Why Use Groups?
+   • File Ownership
+   • File and Directory Permissions
+   • Access Control Lists (ACLs)
+   • Adding and Removing Users