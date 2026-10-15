# Table 8.4 String, Integer, and File Testing (continued)

| Test Operator | Test For |
|---|---|
| Logical Test | |
| expr1 -a expr2 | Logical AND |
| expr1 -o expr2 | Logical OR |
| ! expr | Logical NOT |
| File Test | |
| -b filename | Block special file |
| -c filename | Character special file |
| -d filename | Directory existence |
| -f filename | Regular file existence and not a directory |
| -g filename | Set-group-ID is set |
| -k filename | Sticky bit is set |
| -p filename | File is a named pipe |
| -r filename | File is readable |
| -s filename | File is nonzero size |
| -u filename | Set-user-ID bit is set |
| -w filename | File is writable |
| -x filename | File is executable |

# 8.5.1 Testing Exit Status: The test Command

The following examples illustrate how the exit status is tested.

The test command is used to evaluate conditional expressions, returning true or false. It will return a zero exit status for true and a nonzero exit status for false. The test command or brackets can be used. (Refer back to Table 8.4.)