
Here we used `sed` with the `-n` parameter so `sed` will not print anything except for what matches with the expression `processor`, as instructed by the `p` command. As we did in the `grep` solutions, `wc -l` will count the number of lines, thus the number of processors we have.

Study this next example:

```
$ sed -n /processor/p /proc/cpuinfo | sed -n '$='
```

This command sequence provides identical results to the previous example where the output of `sed` was piped into a `wc` command. The difference here is that instead of using `wc -l` to count the number of lines, `sed` is again invoked to provide equivalent functionality. Once more, we are suppressing the output of `sed` with the `-n` option, except for the expression that we are explicitly calling, which is '$='. This expression tells `sed` to match the last line ($) and then to print that line number (=).

### 2. Explore your local `/etc/passwd` file with the `grep`, `sed`, `head` and `tail` commands per the tasks below:

- Which users have access to a Bash shell?

```
$ grep ":/bin/bash$" /etc/passwd
```

We will improve this answer by only displaying the name of the user that utilizes the Bash shell.

```
$ grep ":/bin/bash$" /etc/passwd | cut -d: -f1
```

The user name is the first field (-f1 parameter of the `cut` command) and the `/etc/passwd` file uses `:` as separators (-d: parameter of the `cut` command) we just pipe the output of the `grep` command to the appropriate `cut` command.

- Your system has various users that exists to handle specific programs or for administrative purposes. They do not have access to a shell. How many of those exist in your system?

The easiest way to find this is by printing out the lines for accounts that do not use the Bash shell:

```
$ grep -v ":/bin/bash$" /etc/passwd | wc -l
```

- How many users and groups exist in your system (remember: use only the `/etc/passwd` file)

The first field of any given line in your `/etc/passwd` file is the user name, the second is typically an x indicating the user password is not stored here (it is encrypted in the `/etc/shadow` file). The third is the user id (UID) and the fourth is the group id (GID). So this should give us the number of users:

```
$ cut -d: -f3 /etc/passwd | wc -l
```

Well, most of the time it will. However, there are situations where you will set different super users or other special kinds of users sharing the same UID (user id). So, to be on the safe side we will pipe the result of our cut command to the sort command and then count the number of lines.

```
$ cut -d: -f3 /etc/passwd | sort -u | wc -l
```

Now, for the number of groups:

```
$ cut -d: -f4 /etc/passwd | sort -u | wc -l
```

- List only the first line, the last line and the tenth line of your `/etc/passwd` file

This will do:

```
$ sed -n -e '1'p -e '10'p -e '$'p /etc/passwd
```

Remember that the parameter -n tells sed not to print anything other than what is specified by the p command. The dollar sign ($) used here is a regular expression meaning the last line of the file.

- Consider this `/etc/passwd` file example. Copy the lines below to a local file named mypasswd for this exercise.

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
nvidia-persistenced:x:121:128:NVIDIA Persistence Daemon,,,:/nonexistent:/sbin/nologin
libvirt-qemu:x:64055:130:Libvirt Qemu,,,:/var/lib/libvirt:/usr/sbin/nologin
libvirt-dnsmasq:x:122:133:Libvirt Dnsmasq,,,:/var/lib/libvirt/dnsmasq:/usr/sbin/nologin
carol:x:1000:2000:Carol Smith,Finance,,Main Office:/home/carol:/bin/bash
dave:x:1001:1000:Dave Edwards,Finance,,Main Office:/home/dave:/bin/ksh
emma:x:1002:1000:Emma Jones,Finance,,Main Office:/home/emma:/bin/bash
frank:x:1003:1000:Frank Cassidy,Finance,,Main Office:/home/frank:/bin/bash
grace:x:1004:1000:Grace Kearn,Engineering,,Main Office:/home/grace:/bin/ksh
henry:x:1005:1000:Henry Adams,Sales,,Main Office:/home/henry:/bin/bash
john:x:1006:1000:John Chapel,Sales,,Main Office:/home/john:/bin/bash
```

List all users in group 1000 (use sed to select only the appropriate field) from your mypasswd file:

The GID is the fourth field in the /etc/passwd file. You might be tempted to try this:

```
$ sed -n /1000/p mypasswd
```

In this case you will also get this line:

```
carol:x:1000:2000:Carol Smith,Finance,,Main Office:/home/carol:/bin/bash
```

You know this is not correct since Carol Smith is a member of GID 2000 and the match occurred because of the UID. However, you may have noticed that after the GID the next field starts with an upper case character. We can use a regular expression to solve this problem.

```
$ sed -n /1000:[A-Z]/p mypasswd
```

The expression [A-Z] will match any single upper case character. You will learn more about this in the respective lesson.

List only the full names of all the users for this group (use sed and cut):

Use the same technique you used to solve the first part of this exercise and pipe it to a cut command.

```
$ sed -n /1000:[A-Z]/p mypasswd | cut -d: -f5
Dave Edwards,Finance,,Main Office
Emma Jones,Finance,,Main Office
Frank Cassidy,Finance,,Main Office
Grace Kearns,Engineering,,Main Office
Henry Adams,Sales,,Main Office
John Chapel,Sales,,Main Office
```

Not quite there! Do note how the fields inside your results can be separated by `,`. So we will pipe the output to another `cut` command, using the `,` as a delimiter.

```
$ sed -n /:1000:[A-Z]/p mypasswd | cut -d: -f5 | cut -d, -f1
Dave Edwards
Emma Jones
Frank Cassidy
Grace Kearns
Henry Adams
John Chapel
```

## Answers to Explorational Exercises

1. Once more using the mypasswd file from the previous exercises, devise a Bash command that will select one individual from the Main Office to win a raffle contest. Use the sed command to only print out the lines for the Main Office, and then a cut command sequence to retrieve the first name of each user from these lines. Next you will want to randomly sort these names and only print out the top name from the list.

First explore how the parameter -R manipulates the output of the sort command. Repeat this command a couple times on your machine (note you will need to enclose 'Main Office' within single quotes, so sed will handle it as a single string):

```
$ sed -n /'Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f1 | sort -R
```

Here is a solution to the problem:

```
$ sed -n /'Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f1 | sort -R | head -1
```

2. How many people work in Finance, Engineering and Sales? (Consider exploring the uniq command.)

Keep building on top of what you learned from the previous exercises. Try the following:

```
$ sed -n /'Main Office'/p mypasswd
$ sed -n /'Main Office'/p mypasswd | cut -d, -f2
```

Notice now we do not care about the : as a delimiter. We just want the second field when we split the lines by the , characters.

```
$ sed -n /'Main Office'/p mypasswd | cut -d, -f2 | uniq -c
      4 Finance
      1 Engineering
      2 Sales
```

The uniq command will only output the unique lines (not the repeating lines) and the parameter -c tells uniq to count the occurrences of the equal lines. There is a caveat here: uniq will only consider adjacent lines. When this is not the case you will have to use the sort command.

3. Now you want to prepare a CSV (comma separated values) file so you can easily import, from the mypasswd file in the previous example, the file names.csv into LibreOffice. The file contents will have the following format:

```
First Name,Last Name,Position
Carol,Smith,Finance
...
John,Chapel,Sales
```

Tip: Use the sed, cut, and paste commands to achieve the desired results. Note that the comma (,) will be the delimiter for this file.

Start with the sed and cut commands, building on top of what we learned from the previous exercises:

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d" " -f1 > firstname
```

Now we have the file firstname with the first names of our employees.

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d" " -f2 | cut -d, -f1 > lastname
```

Now we have the file lastname containing the surnames of each employee.

Next we determine which department each employee works in:

```bash
$ sed -n '/Main Office'/p mypasswd | cut -d: -f5 | cut -d, -f2 > department
```

Before we work on the final solution, try the following commands to see what type of output they generate:

```bash
$ cat firstname lastname department
$ paste firstname lastname department
```

And now for the final solution:

```bash
$ paste firstname lastname department | tr '\t' ','
$ paste firstname lastname department | tr '\t' ',' > names.csv
```
