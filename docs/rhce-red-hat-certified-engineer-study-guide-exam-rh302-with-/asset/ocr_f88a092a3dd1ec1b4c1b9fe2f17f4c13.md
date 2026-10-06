# 72 Chapter 3 • Unix Basics

tests whether the /etc/hosts exists. Table 3.11 summarizes important arguments of the test command.

# TABLE 3.11 Important Command Arguments

| Condition | Meaning |
| - | - |
| -d file | file is a directory. |
| -e file | file exists. |
| -f file | file is a regular file. |
| -r file | file is readable. |
| -s file | file has size greater than 0. |
| -w file | file is writable. |
| -x file | file is executable. |
| file1 -nt file2 | file1 is newer than file2. |
| file1 -ot file2 | file1 is older than file2. |
| s1 = s2 | String s1 is identical to string s2. |
| s1 != s2 | String s1 is not identical to string s2. |
| n1 -eq n2 | Integer n1 is equal to integer n2. |
| n1 -ge n2 | Integer n1 is greater than or equal to integer n2. |
| n1 -gt n2 | Integer n1 is greater than integer n2. |
| n1 -le n2 | Integer n1 is less than or equal to integer n2. |
| n1 -lt n2 | Integer n1 is less than integer n2. |
| n1 -ne n2 | Integer n1 is not equal to integer n2. |
| ! cnd | True if and only if condition cnd is false. |

Copyright©2000 SYBEX, Inc., Alameda, CA www.syex.com