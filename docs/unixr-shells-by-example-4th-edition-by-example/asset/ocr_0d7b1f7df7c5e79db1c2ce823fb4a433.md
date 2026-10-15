# 16.4.3 Writing a Portable Script

System administrators often write shell scripts that work on multiple UNIX versions. Because commands change from UNIX to UNIX, your script will need to determine the UNIX version on which it is being run. This can be done using the uname command. Listed below are some popular versions of UNIX and the output of the uname command from each version. To create a script that will port to these different UNIX versions, your script should check the uname output and modify commands accordingly.

| UNIX Version: | uname Output: |
|---|---|
| AIX | AIX |
| FreeBSD | FreeBSD |
| HP-UX | HP-UX |
| IRIX | IRIX |
| Linux | Linux |
| Mac OS X | Darwin |
| NetBSD | NetBSD |
| OpenBSD | OpenBSD |
| SCO OpenServer 5 | SCO_SV |
| Solaris | SunOS |

A case command is commonly used to check for the operating system you are using. Example 16.15 checks for Linux (any brand), HP-UX, Solaris, FreeBSD, and Mac OS X UNIX.

# EXAMPLE 16.15

```
1  uname_out=`uname`
2  case "$uname_out" in
3  HP-UX) echo "You are running HP-UX"
4  SunOS) echo "You are running Solaris"
;;
FreeBSD) echo "You are running FreeBSD"
;;
Linux) echo "You are running Linux"
;;
Darwin) echo "You are running Mac OS X"
;;
*) echo "Sorry, $uname_out UNIX"
   echo "is not supported by this script"
;;
6  esac
```