# 604

# ksh, rksh

+   -s file true if file exists and has size greater than 0.
-t ildes true if file descriptor number ildes is open and associated with a terminal device.
-u file true if file exists and has its setuid bit set.
-w file true if file exists and is writable by current process.
-x file true if file exists and is executable by current process. If file exists and is a directory, then the current process has permission to search in the directory.
-z string true if length of string 0.
-L file true if file exists and is a symbolic link.
-O file true if file exists and is owned by the effective user ID of this process.
-G file true if file exists and its group matches the effective group ID of this process.
-S file true if file exists and is a socket.
file1 -nt file2 true if file exists and is newer than file2.
file1 -ot file2 true if file exists and is older than file2.
file1 -ef file2 true if file1 and file2 exist and refer to the same file.
string true if the string is not the null string.
string = pattern true if string matches pattern.
string != pattern true if string does not match pattern.
string1 = string2 true if the strings string1 and string2 are identical.
string1 != string2 true if the strings string1 and string2 are not identical.
string1 < string2 true if string1 comes before string2 based on strings interpreted as appropriate to the locale setting for category LC_COLLATE.
string1 > string2 true if string1 comes after string2 based on strings interpreted as appropriate to the locale setting for category LC_COLLATE.
expl -eq exp2 true if exp1 is equal to exp2.