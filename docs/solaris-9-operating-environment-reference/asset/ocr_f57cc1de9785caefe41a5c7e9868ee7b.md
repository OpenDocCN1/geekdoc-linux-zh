# 1400 test

-w file true fileexists and is writable. true indicates only that the write flag is on. The file is not writable on a read-only file system even if this test indicates true.

-x file true fileexists and is executable. true indicates only that the execute flag is on. If file is a directory, true indicates that filecan be searched.

-z string true if the length of string stringis 0.

file1 -nt file2

true if file1 exists and is newer than file2. (Not available in sh.)

file1 -ot file2

true if file1 exists and is older than file2. (Not available in sh.)

file1 -ef file2

true if file1 and file2 exist and refer to the same file. (Not available in sh.)

string true if the string stringis not the null string.

string1 = string2 true if the strings string1 and string2 are identical.

string1 != string2 true if the strings string1 and string2 are not identical.

nl -eq n2 true if the integers nl1 and n2 are algebraically equal.

nl -ne n2 true if the integers nl1 and n2 are not algebraically equal.

nl -ge n2 true if the integer nl1 is algebraically greater than or equal to the integer n2.

nl -gt n2 true if the integer nl1 is algebraically greater than the integer n2.

nl -le n2 true if the integer nl1 is algebraically less than or equal to the integer n2.

nl -lt n2 true if the integer nl1 is algebraically less than the integer n2.

condition -a condition2 true if both condition1 and condition2 are true. The -a binary primary is left associative and has higher precedence than the -o binary primary. New in the Solaris 9 release.

condition -o condition2 true if either condition1 or condition2 is true. The -o binary is left associative. New in the Solaris 9 release.

You can combine these primaries with the following operators.

! condition true if condition is false.