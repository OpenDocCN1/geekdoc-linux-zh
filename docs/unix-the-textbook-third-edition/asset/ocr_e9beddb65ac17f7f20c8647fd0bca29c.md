The following script in the for_demo1 file shows the use of the for command with optional arguments. The variable people is assigned the words in argument-list one by one, and each time the value of the variable is echoed until no word remains in the list. At that time, control comes out of the for statement, and the command following done is executed. Then the code following the for statement, the exit 0 statement only in this case, is executed.

```
$ cat for_demo1
#!/bin/sh
for people in Debbie Jamie John Kitty Kuhn Shah
do
    echo "$people"
done
exit 0
$ ./for_demo1
Debbie
Jamie
John
Kitty
Kuhn
Shah
$
```

The following script in the user_info file takes a list of existing (i.e., valid) login names as command line arguments and displays each login name and the full name of the user who owns the login name, one per login. In the sample run, the first value of the user variable is dheckman. The echo command displays dheckman: followed by a <Tab>, and the cursor stays at the current line. The first grep command is used to check if dheckman has an entry in the /etc/passwd file. If the answer is no, the process is repeated for the second command line argument. If dheckman is found, the second grep command searches the /etc/passwd file for the login name dheckman and pipes it to the cut command, which displays the fifth field in the /etc/passwd line for dheckman (his full name). The process is repeated for the remaining two login names (ghacker and msarwar). No user is left in the list passed at the command line, so control comes out of the for statement and the exit 0 command is executed to transfer control back to shell. The command substitution "`echo $user:`" in the grep command can be replaced by "`$user:`".

```
$ cat user_info
#!/bin/sh
for user
do
# Don't display anything if a login name is not found in /etc/
passwd
grep "^"`echo $user:`" /etc/passwd 1> /dev/null 2>&1
if [ $? -eq 0 ]
```