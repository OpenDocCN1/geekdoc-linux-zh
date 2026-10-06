# 412 CHAPTER 15 Techniques Used by Attackers

+   6. Reboot into Windows (whatever version is on that workstation). When the machine boots up, instead of logging in, choose Accessibility Options and Magnifier.

What launches is a command prompt with system-level privileges.

# Using OphCrack

One popular tool for getting into a machine locally is OphCrack, which you can download from http://ophcrack.sourceforge.net/. It is based on an understanding of how Windows passwords work. Windows passwords are stored in a hash file in one of the system directories, usually C:\WINDOWS\system32\config in a Security Accounts Manager (SAM) file. Because the file contains hashed entries, you cannot simply read the usernames and passwords. If you try random passwords, most systems will lock you out after a few tries, so it would be great if you get the SAM file from Windows and try to crack it. However, it is a locked file. The operating system will not let you copy or do anything with it. OphCrack boots the system in Linux so that the Windows operating system is not loaded, and the SAM file is not protected. It uses a process that creates a rainbow table to all possible character combinations. OphCrack searches the SAM for a match. When it finds it, it knows the username and password, as shown in Figure 15-17.

![](bbox=[0.07, 0.506, 0.738, 0.893])

Figure 15-17 OphCrack