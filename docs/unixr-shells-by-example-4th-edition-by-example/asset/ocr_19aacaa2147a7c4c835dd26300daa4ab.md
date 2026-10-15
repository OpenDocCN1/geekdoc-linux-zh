# EXPLANATION (CONTINUED)

3 A numeric test is performed by the test command. If age is greater than or equal to 0 and less than or equal to 12, the test command returns exit status 0, true, and the statement after the then is executed. Otherwise, program control goes to the elif. If that test is false, the next elif is tested.

4 The else construct is the default. If none of the above statements are true, the else commands will be executed.

5 The fi terminates the initial if statement.

# 14.5.6 File Testing

Often when you are writing scripts, your script will require that there are certain files available and that those files have specific permissions, are of a certain type, or have other attributes. You will find file testing a necessary part of writing dependable scripts.

# Table 14.5 File-Testing Operators

| Test Operator | Tests True If |
|---|---|
| -b filename | Block special file |
| -c filename | Character special file |
| -d filename | Directory existence |
| -e filename | File existence |
| -f filename | Regular file existence and not a directory |
| -G filename | True if file exists and is owned by the effective group ID |
| -g filename | Set-group-ID is set |
| -k filename | Sticky bit is set |
| -L filename | File is a symbolic link |
| -p filename | File is a named pipe |
| -O filename | File exists and is owned by the effective user ID |
| -r filename | File is readable |
| -S filename | File is a socket |
| -s filename | File is nonzero size |
| -t fd | True if fd (file descriptor) is opened on a terminal |