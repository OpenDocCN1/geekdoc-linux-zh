If you’re under the gun to get a client working, you may just want to disable client-side encryption using the regedit scripts that come with Samba’s source code (see the docs subdirectory).

+   Monitor cached passwords. Windows often caches passwords in files that end in pwl. Not only is this a security risk (the pwl files are poorly encrypted), but if your password has changed on the server, Windows may continue feeding the cached password instead of prompting you for a new one. Simply remove the pwl files to force Windows to prompt you for a password.

# Module Summary

In this chapter, we discussed the process of compiling, installing, and configuring Samba so that your Linux server can integrate into a Windows-based network. Samba is a powerful tool with the potential to replace Windows servers dedicated to disk and printer sharing.

Reading through tons of documentation probably isn’t your favorite way to pass the day, but you’ll find the Samba documentation to be complete, helpful, and easy to read. At least skim through the files to see what’s there, so you know where you can go to get additional information when you need it. Plus, with the entire Using Samba book (referred to in the introduction to this module) as part of the distribution, you should have everything you need for configuring even the most complex setup. If you would rather read more about Samba in print, you can purchase the same book that is shipped with the distribution.

# Module 18 Mastery Check

+   1. When dealing with encrypted passwords, what are two ways of handling the incompatibility between UNIX and Windows?
+   2. Do smbd and nmbd both have to be started in order for Samba to work?
+   3. What is Samba?
+   4. What is the main advantage of using Samba?
+   5. What does SMB stand for?
+   6. Give an example of command lines that start and stop Samba.
+   7. What is SWAT?