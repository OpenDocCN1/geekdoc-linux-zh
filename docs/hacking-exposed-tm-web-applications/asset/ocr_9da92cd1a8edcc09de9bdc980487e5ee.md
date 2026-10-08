# Hacking Exposed Web Applications

C:\test1\test2\test2.exe Everyone:F
C:\test1\test2\test2.txt Everyone:F

Let’s say you want to change permissions on all executable files in test1 and all subdirectories to System:Full, Administrators:Full. Here’s the command syntax using cacs:

```
C:\cacs test1*.exe /T G System:F Administrators:F
Are you sure (Y/N) ?
processed file: C:\test1\test1.exe
processed file: C:\test1\test2.exe
```

Now run cacs to confirm your results. Note, the .txt files in all subdirectories have the original permissions, but the executable files are now more appropriately:

```
C:\cacs test1 /T
C:\test1 Everyone:(OI) (CI)F
C:\test1\test1.exe NT AUTHORITY\SYSTEM:F
BUILTIN\Administrators:F
```

```
C:\test1\test1.txt Everyone:F
C:\test1\test2.txt Everyone:(OI) (CI)F
C:\test1\test2\test2.exe NT AUTHORITY\SYSTEM:F
BUILTIN\Administrators:F
```

C:\test1\test2\test2.txt Everyone:F

Applying this to a typical server, a good idea would be to set ACLs on all executables in the %systemroot% directory to System:Full, Administrators:Full, like so:

```
C:\cacs %systemroot%*.exe /T G System:F Administrators:F
```

This blocks unmodified users from using these executables and helps prevent exploits like Nucle that rely on unprivileged access to these programs.
of course, such executables may also be moved, renamed, or deleted. This puts them out of reach of hackers with even more finality.

> NOTE The IISlock tool automates assigning ACLs to system utilities. See the previous section on ISAPI DLL flaws.

Remove the Executive and Guests from Write and Execute ACLs on the Server IUSR and IWAM are members of these groups. Be extra sure the IUSR and IWAM accounts don't have write access to any files or directories on your system—you’ve seen even a single writable directory can lead to! Also, seriously scrutinize Execute permissions for nonprivileged groups and especially don't allow any unprivileged user to have both write and execute permissions to the same directory!

Know What It Looks Like When You Are/Have Been Under Attack As always, treat incident response as seriously as prevention—especially with fragile Web servers. To identify