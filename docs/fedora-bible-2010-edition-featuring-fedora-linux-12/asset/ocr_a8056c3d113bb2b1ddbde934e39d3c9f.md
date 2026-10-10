| Operator | What Is Being Tested? |
| :------- | :------------------- |
| -k file | Does the file have the sticky bit set? |
| -L file | Is the file a symbolic link? |
| -n string | Is the length of the string greater than 0 bytes? |
| -N file | Has the file been modified since it was last read? |
| -O file | Do you own the file? |
| -p file | Is the file a named pipe? |
| -r file | Is the file readable by you? |
| -s file | Does the file exist, and is it larger than 0 bytes? |
| -S file | Does the file exist, and is it a socket? |
| -t fd | Is the file descriptor connected to a terminal? |
| -u file | Does the file have the set-user-id bit set? |
| -w file | Is the file writable by you? |
| -x file | Is the file executable by you? |
| -z string | Is the length of the string 0 (zero) bytes? |
| expr1 -a expr2 | Are both the first expression and the second expression true? |
| expr1 -o expr2 | Is either of the two expressions true? |
| file1 -nt file2 | Is the first file newer than the second file (using the modification timestamp)? |
| file1 -ot file2 | Is the first file older than the second file (using the modification timestamp)? |
| file1 -ef file2 | Are the two files associated by a hard link? |
| var1 = var2 | Is the first variable equal to the second variable? |
| var1 -eq var2 | Is the first variable equal to the second variable? |
| var1 -ge var2 | Is the first variable greater than or equal to the second variable? |
| var1 -gt var2 | Is the first variable greater than the second variable? |
| var1 > var2 | Does the first variable sort after the second variable? |
| var1 -le var2 | Is the first variable less than or equal to the second variable? |
| var1 -lt var2 | Is the first variable less than the second variable? |
| var1 < var2 | Does the first variable sort before the second variable? |
| var1 != var2 | Is the first variable not equal to the second variable? |
| var1 -ne var2 | Is the first variable not equal to the second variable? |