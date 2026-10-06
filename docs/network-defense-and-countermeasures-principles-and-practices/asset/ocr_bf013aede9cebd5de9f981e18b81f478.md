# Other Issues

Some account and password issues cannot be handled with computer settings. These involve setting organizational policies regarding user and administrator behavior. Chapter 11, “Security Policies,” discusses such organizational policies in greater depth. For now, simply consider this basic list of the most important organizational policies:

+   - Users must never write down passwords.
- Users must never share passwords.
- Administrators must use the least required access rule. That means most users should not have administrative privileges on their own desktops.

> FYI: Registry Settings

Incorrect editing of your registry can render parts of your operating system unusable. It can keep your machine from booting at all when you make any changes to the registry and documenting these changes are important. If you are new to registry manipulation it is recommended that you use a lab machine that does not contain any critical data or applications. Misconfiguring the registry so severely that the entire operating system must be reinstalled is possible.

# Registry Settings

Secure registry are critical to securing a network. Unfortunately, my experience has been that this area is often overlooked by otherwise secure practices. One thing to keep in mind is that if you don't know what you are doing in the registry, you can cause serious problems. If you are not comfortable with the registry, don't touch it. Even if you are comfortable registry changes, always back up the registry before any change.

The Windows Registry is a database used to store settings and options for Microsoft Windows operating systems. This database contains critical information and settings for all the hardware, software, users, and preferences on a particular computer. Whenever users are added, software is installed, or any other change is made to the system (including security policies), that information is stored in the registry.

# Registry Basics

The physical files that make up the registry are stored differently depending on which version of Windows you are using. Older versions of Windows (that is, Windows 95 and 98) keep the registry in two hidden files in your Windows directory, called USER.DAT and SYSTEM.DAT. In all versions of Windows XP, the physical files that make up the registry are stored in %SystemRoot%\System22Config. In Windows 8, the file has been nuser.dat. Regardless of the version of Windows you are using, you cannot edit the registry directly by opening and editing these files. Instead you use a tool, regedit.exe, to make changes. There are newer tools like regedit32. However, many users find that the older regedit has a more user-friendly “find” option for searching the registry. Either will work.