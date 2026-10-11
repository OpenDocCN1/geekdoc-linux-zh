![](bbox=[0.06, 0.14, 0.11, 0.2])

This is not a backup, archival, or version control solution!
With Samba or Windows servers, shadow\_copy is designed to be an end-user tool only. It does not replace or enhance your backup and archival solutions and should in no way be considered as such. Additionally, if you need version control, implement a version control system. You have been warned.

The shadow\_copy module allows you to setup functionality that is similar to MS shadow copy services. When setup properly, this module allows Microsoft shadow copy clients to browse “shadow copies” on Samba shares. You will need to install the shadow copy client. You can get the MS shadow copy client here.1. Note the additional requirements for pre-Windows XP clients. I did not test this functionality with any pre-Windows XP clients. You should be able to get more information about MS Shadow Copy from the Microsoft’s site2.

The shadow\_copy VFS module requires some underlying file system setup with some sort of Logical Volume Manager (LVM) such as LVM1, LVM2, or EVMS. Setting up LVM is beyond the scope of this document; however, we will outline the steps we took to test this functionality for *example purposes only*. You need to make sure the LVM implementation you choose to deploy is ready for production. Make sure you do plenty of tests.

Here are some common resources for LVM and EVMS:

+   • Sistina’s LVM1 and LVM23
+   • Enterprise Volume Management System (EVMS)4
+   • The LVM HOWTO5
+   • See *Learning Linux LVM, Part 1*6 and *Learning Linux LVM, Part 2*7 for Daniel Robbins’ well-written, two part tutorial on Linux and LVM using LVM source code and reisersfs.

# 22.3.6.1 Shadow Copy Setup

At the time of this writing, not much testing has been done. I tested the shadow copy VFS module with a specific scenario which was not deployed in a production environment, but more as a proof of concept. The scenario involved a Samba-3 file server on Debian Sarge