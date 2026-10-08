# Hardening a Unix Server

You can play with the commands to get up to speed with Unix systems (create files, delete the files that you created, list permissions, and so on), but you can also play with conversions to get more familiar with the numeric mode. For example, you can use the permissions shown in Figure 7.10 and convert them to numeric mode by the table in Figure 7.9. This should give you the numeric representation of those permissions, which is 644.

> Tip
Have you noticed a case in which not even root has execute (x) permissions? If yes, don't panic, as that is normal and it may just indicate that the file is not an executable file.

The following figure shows an example of a file owned by root with no executable permissions. This, as explained, is expected because a log file is not an executable file:

```
-rw-r--r-- 1 root 0 Nov 23 09:54 alternatives.log
```

Figure 7.11 – File with no execute permissions

So far, we have seen how permissions are applied to files. Now, it's time to see how permissions work for directories (folders).

# Permissions in directories (folders)

Files and directories are managed differently/separately in Unix systems, which means also that the default permissions are configured separately. So, keep this in mind, as this could represent a security vulnerability if both are not configured properly.

As shown in the following figure, we created a mkdir {directory_name} directory and we use the ls -ld command to see the default permissions assigned by the system to the directory:

```
kalikali~$ mkdir bravito
kalikali~$$ ls -ld bravito
ddrwxr-xr-x 2 kali kali 4096 Nov 29 16:22 bravito
```

Figure 7.12 – Unix permissions in directories (folders)

As you can see, the permissions are very different from the default permissions applied to the files. Let's make a comparison.