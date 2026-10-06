# Part I The Linux Command Line

The touch command created the default permissions assigned to my user account. The umask command shows and sets the default permissions:

```
$ umask
0022
```

Unfortunately, the umask command setting isn't clearly, and trying to understand exactly how it works makes things even muddier. The first digit represents a special feature called the sticky bit. We'll talk more about later on in this chapter in the "Sharing Files" section.

The next three digits represent the octal values of the umask for a file or directory. To understand how umask works, you first need to understand octal mode security settings.

Octal mode security settings take the three rwx permissions values and convert them into a 3-bit binary value, represented by a single octal value. In the binary representation, each position is a binary bit. Thus, if the read permission is the only permission set, the value becomes r--, relating to a binary value of 100. Table 6-5 shows the possible combinations you'll run into.

Octal mode takes the octal permissions and lists three of them in order for the security levels (user, group, and everyone). Thus, the octal mode 664 represents read and write permissions for the user and group, but read-only permission for everyone else.

Now that you know about octal mode permissions, the umask value becomes even more confusing. The octal mode shown for the default umask on my Linux system is 0022, but the file I created had an oct mode permission of 644. How did that happen?

# TABLE 6-5
Linux File Permission Codes

| Permissions | Binary | Octal | Description |
| --- | --- | --- | --- |
| --- | 000 | 0 | No permissions |
| -x | 001 | 1 | Execute-only permission |
| -w | 010 | 2 | Write-only permission |
| -wx | 011 | 3 | Write and execute permissions |
| r-- | 100 | 4 | Read-only permission |
| r-x | 101 | 5 | Read and execute permissions |
| rw- | 110 | 6 | Read and write permissions |
| rwx | 111 | 7 | Read, write, and execute permissions |