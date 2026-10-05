# Chapter 6

links /var/log/secure to /var/log/archived/secure with a relative path. It creates the symbolic link /var/log/secure with a target of “archived/secure”, as demonstrated by this output from ls:

```
$ -ls /var/log/secure
lrwxrwxrwx 1 root root 18 2019-07-05 12:54 /var/log/secure -> archived/secure
```

The entire /var/log directory could be moved elsewhere without causing the symbolic link to start working (not moving this directory is advisable).

It is a common mistake to think that the first argument to ln -s is interpreted relative to your current working directory. However, it is not resolved as a filename by; it's simply a literal string that becomes the target of the symbolic link.

# 6.5 File Attributes

Under the UNIX and Linux filesystem model, every file has a set of nine permission bits that control who can read, write, and execute the contents of the file. With three other bits that affect the operation of executable programs, these bits constitute the file “mode”.

The twelve mode bits are set together with four bits of file-type information. The four file-type bits are set when the file is first created and cannot be changed, but the file’s owner and the supervisor can modify the mode bits with the chmod (change mode) command. Use ls -l (or ls -ld for a directory) to inspect the values of these bits. An example is given on page 154.

# The permission bits

Nine permission bits determine what operations may be performed on a file and by whom. Traditional UNIX does not allow permissions to be per-user-(although all systems support access control lists of one sort or another; page 159). Instead, three sets of permissions define access for the owner of the file, the group owners of the file, and everyone else (in that order). Each has three bits: a read bit, a write bit, and an execute bit (also in order).

It’s convenient to discuss permissions in octal (base 8) numbers because each digit of an octal number represents three bits and each group of permission bits consists of three bits. The topmost three bits (with access values of 400, 200, and 100) control access for the owner. The second (40, 20, and 1) control access for every-one (“the world”). The last three (4, 2, and 1). In each triplet, the high bit is the read bit, the middle is the write bit, and the low bit is the execute bit.

+   6. The permissions that ls shows for a symbolic link, lrwxrwxrwx, are dummy values. Permission to create, remove, or move the link is controlled by the containing directory, whereas read, write, and execute permission on the link target are granted by the target’s own permissions. Symbolic links do not need (and do not have) any permission information of their own.
7. If you think the owner as the “user”, you can easily remember the order of permission sets with the word Yugo (like the car). This is also the letter coding used by the mnemonic version of chmod.