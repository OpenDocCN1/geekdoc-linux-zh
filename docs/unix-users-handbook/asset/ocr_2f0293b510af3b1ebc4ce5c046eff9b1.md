![](bbox=[0.03, 0.07, 0.13, 0.16])

available from Microsoft Press, Redmond, WA. The POSIX utilities include such useful commands as cat, chmod, find, ls, mv, and others. The commands that are available on the *Resource Kit* vary somewhat from architecture to architecture. In this chapter, I focus on only the "I386" utilities and not the utilities for other architectures.

![](bbox=[0.03, 0.2, 0.13, 0.3])

The *Resource Kit* has on it the file **POSIX.WRI**, which describes the POSIX utilities in detail. In this chapter, I'll just provide a brief overview of the utilities and examples of using some of the utilities. Most UNIX system administrators are familiar with these utilities in UNIX but may find differences in the options to these utilities when using the *Resource Kit* version.

![](bbox=[0.03, 0.31, 0.13, 0.4])

I have made every effort to limit the number of "add-on" products, to Windows and UNIX covered in this book. The *Resource Kit*, however, is so useful to Windows system administrators that not covering at least some part of it, such as the POSIX utilities, would leave a void in the discussion of Windows system administration. You can find out more information about the *Resource Kit* on the Microsoft Web site. You can buy it at many computer, electronic, and book stores. Be sure to buy the *Resource Kit* for the version of Windows you are running. There is also a *Resource Kit* for both the Server and Workstation versions of Windows. I used the Server *Resource Kit* for the POSIX commands covered in this chapter.

![](bbox=[0.03, 0.41, 0.13, 0.5])

![](bbox=[0.03, 0.52, 0.13, 0.61])

Both the source code and executables for the POSIX utilities are on the *Resource Kit*. The following is a listing of the POSIX executables for I386 on the *Resource Kit* CD-ROM. I used the POSIX utility *ls-l* to produce this listing:

```
```
F:\I386\GNU\POSIX> ls -l
-rwxrwxrwx 1 Everyone Everyone   101748 Sep  6 12:39 CAT.EXE
-rwxrwxrwx 1 Everyone Everyone   116188 Sep  6 12:39 CHMOD.EXE
-rwxrwxrwx 1 Everyone Everyone   110920 Sep  6 12:39 CHOWN.EXE
-rwxrwxrwx 1 Everyone Everyone   111208 Sep  6 12:39 CP.EXE
-rwxrwxrwx 1 Everyone Everyone   173580 Sep  6 12:39 FIND.EXE
-rwxrwxrwx 1 Everyone Everyone   144256 Sep  6 12:39 GREP.EXE
-rwxrwxrwx 1 Everyone Everyone     9060 Sep  6 12:39 LN.EXE
-rwxrwxrwx 1 Everyone Everyone   128532 Sep  6 12:39 LS.EXE
-rwxrwxrwx 1 Everyone Everyone    88984 Sep  6 12:39 MKDIR.EXE
-rwxrwxrwx 1 Everyone Everyone    90096 Sep  6 12:39 MV.EXE
-rwxrwxrwx 1 Everyone Everyone   114564 Sep  6 12:39 RM.EXE
-rwxrwxrwx 1 Everyone Everyone    85004 Sep  6 12:39 RMDIR.EXE
-rwxrwxrwx 1 Everyone Everyone   362528 Sep  6 12:39 SH.EXE
-rwxrwxrwx 1 Everyone Everyone    91244 Sep  6 12:39 TOUCH.EXE
-rwxrwxrwx 1 Everyone Everyone   287628 Sep  6 12:39 VI.EXE
```
```