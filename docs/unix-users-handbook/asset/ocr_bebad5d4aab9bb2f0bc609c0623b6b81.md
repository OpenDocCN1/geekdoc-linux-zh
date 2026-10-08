In the case of my Windows system there is no problem handling the file name .gnome_private as it appears on the Linux system. In the case of a DOS system, there would be extensive "mangling" of the file name that would have to take place. DOS uses only 8.3 file names, or those with eight characters and a three character extension.

Samba mangles files that start with a dot, such as the one in this example, by removing the leading dot, printing the first five characters and then a tilde, and then applying a hash algorithm to the original filename to come up with the last two characters. This results in a total of eight characters for the filename. All the characters are uppercase.

If the file does not begin with a dot, then the file name will be generated in the same way as described in the previous paragraph. The extension consists of the first three characters to the right of the dot converted to uppercase. This results in a total of eight characters for the filename and three for the extension.

In our example, the filename .gnome_private would be given a DOS name of GNOME~CZ. You have some control over mangling in the smb.conf file.

# # User Issues

I have avoided making a serious user-related configuration in this chapter, in the interest of keeping the examples simple. You will probably not have this luxury unless you are in an environment where you are the only user on both the Windows and UNIX systems.

Users and groups have always been an important part of every UNIX system. Users and groups were not as important in the Windows world until more recently. This change results in some Windows environments in which there is not a complete user and group policy in place which could be used by Samba.

Samba takes into account an environment in which you have set up Windows users and groups and one in which you may not have worked out all the issues related to Windows users and groups. User-level authentication in Samba is set up in such a way that a client can