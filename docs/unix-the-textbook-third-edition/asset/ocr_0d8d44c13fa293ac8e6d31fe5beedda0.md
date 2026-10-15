# TABLE 5.5 Examples of the chmod Command and Their Purposes

| Command | Purpose |
|---|---|
| chmod 700 * | Sets access privileges for all files, including directories, in the current directory to read, write, and execute for the owner, and provides no access privilege to anyone else |
| chmod 740 courses | Sets access privileges for courses to read, write, and execute for the owner and read-only for the group, and provides no access for others |
| chmod 751 ~/courses | Sets access privileges for ~/courses to read, write, and execute for the owner, read and execute for the group, and execute-only permission for others |
| chmod 700 ~ | Sets access privileges for the home directory to read, write, and execute (i.e., search) for the owner, and no privileges for anyone else |
| chmod u=rwx courses | Sets owner's access privileges for courses to read, write, and execute and keeps the privileges of group and others at their present values |
| chmod ugo-rw sample or chmod a-rw sample | Does not let anyone read or write sample |
| chmod a+x sample | Gives everyone execute permission for sample |
| chmod g=u sample | Makes sample's group privileges match its user (owner) privileges |
| chmod go= sample | Removes all access privileges to sample for group and others |

"privilege" field. Some useful examples of the chmod command and their purposes are listed in Table 5.5.

The following session illustrates how access privileges for files can be determined and set. The chmod command is used to change (or set) access privileges, and the ls -l (or ls -ld) command is used to show the effect of the corresponding chmod command. After the chmod 700 courses command has been executed, the owner of the courses file has read, write, and execute access privileges for it, and nobody else has any privilege. The chmod g+rx courses command adds read and execute access privileges to the courses file for the group; the privileges of the owner and others remain intact. The chmod o+r courses command adds the read access privilege for the courses file for others. The chmod a-w * command takes away the write access privilege from all users for all the files in the current directory. The chmod 700 [l-t]* command sets the access permissions to 700 for all the files that start with letters "l" through "t," as illustrated by the output of the last ls -l command, which shows access privileges for the files labs and temp changed to 700.

```
$ cd
$ ls -l
drwxr-x--- 2 sarwar faculty 512 Apr 23 09:37 courses
-rwxrwxrwx 1 sarwar faculty 12 May 01 13:22 labs
-rwxrwxr-- 1 sarwar faculty 163 May 05 23:13 temp
$ chmod 700 courses
$ ls -ld courses
drwx------ 2 sarwar faculty 512 Apr 23 09:37 courses
```