
4. You have a directory containing technical documents and want to give the technical writers the permission to use this directory to create and change various manual pages for your products. How should you do this?

- a. Put all the technical writers in a group and give this group read, write, and execute permissions for the directory.
- b. Put all the technical writers in a group and give this group read and write permissions for the directory.
- c. Put all the technical writers in a group and give this group read and write permissions for all the files in the directory.
- d. Make the head technical writer the owner of the directory and its files. He can then grant access to the various writers.

**Answer a is correct; this will give the technical writers access to the directory and its files.** Answer b is incorrect; the writers would not be able to make the directory their working directory. Answer c is incorrect; although the writers could change existing files, they could not create new files unless they had the write permission on the directory. Answer d is incorrect; without having a group defined, the head technical writer could grant the permissions only to all users instead of just the technical writers.

5. If you issued the command chgrp wp /home/letters but forgot to first create the group wp, what would happen?

- a. You would get an error message but the command would succeed.
- b. No one would be able to access the directory until after you created the group.
- c. Only the owner would be able to access the directory.
- d. You would get an error message and the command would fail.

Answer a is incorrect; if you give an invalid group name, the command will fail. Answer b is incorrect; the group would not have been changed, so access would have remained the same. Answer c is incorrect; the owner and the group would have remained the same and the access permissions would be the same. **Answer d is correct; the chgrp command would first check the /etc/group file to verify that you specified a valid group, and because you didn't, the command would fail.**

6. The permission block on `MyDir` is `drw-r-xr--` and you issue the command `chmod o+x` `MyDir`. What would be another way to do this?

- a. `chmod 777 MyDir`
- b. `chmod 754 MyDir`
- c. `chmod +x MyDir`
- d. `chmod 661 MyDir`

Answer a is incorrect; this would change the permissions to `drwxrwxrwx`. **Answer b is correct; the 7 gives the owner read, write, and execute permissions; the 5 gives the group read and execute and others read; and the 4 gives all others read.** Answer c is incorrect; this grants the execute permission to all (owner, group, and others). Answer d is incorrect; this gives the owner and group read and write and others execute.

7. You have a file with a permissions block of `-rw-rw-r--` and issue the command `chmod go= file`. What would be the new permission block?

- a. `-rw-rw-rw-`
- b. `-rwxrwxr---`
- c. `-rw----`
- d. `-rw-rw-r--`

Answer a is incorrect; to have this result, you would need to issue the command `chmod o+w file` or `chmod 666 file`. Answer b is incorrect; this permission block would result in either `chmod o+x file` or `chmod 764 file`. **Answer c is correct; the command uses the `-` symbol to explicitly remove all permissions from the group and others.** Answer d is incorrect; this shows no changes in permissions.

8. You inadvertently change the permission block on `/usr/bin/passwd` command to `-r-sr-xr-x`. What would be the effect of this change?

- a. Users could no longer change their passwords because they do not have write permissions to `/etc/passwd`.
- b. No changes in how the command runs would occur.
- c. Users' passwords would not expire.
- d. Shadow passwords would quit working.

**Answer a is correct; by removing the SUID on the command, users would run the command in their own context and attempts to write to the `/etc/passwd` file would fail.** Answer b is incorrect; users would not be able to change their passwords, although you might not realize this immediately. Answer c is incorrect; this would not affect any policy you might have established on password age. Answer d is incorrect; this would not disable shadow passwords.

9. You have a new script with a permission block of `-r-xr-xr-x` and issue the command `chmod 2555`. What would the new permission block be?

- a. `-r-sr-xr-x`
- b. `-r-xr-sr-x`
- c. `sr-xr-xr-x`
- d. `-r-xr-xr-x`

Answer a is incorrect; this permission block indicates that the SUID is set, but the command set the SGID. **Answer b is correct; the command sets the SGID so that anyone running the script runs it with the same permissions as the group.** Answer c is incorrect; the first character refers to the file’s type. Answer d is incorrect; these permissions are the same as the ones you started with.

10. One of your users says that she changed her umask to 664, but now her new files all have a permission block of `...x-x-xw-`. If she wanted her new files to have a permission block of `-rw-rw-r--`, what should she have used as a umask?

- a. 002
- b. 022
- c. 222
- d. 220

**Answer a is correct; this would result in a permission block of `-rw-rw-r--` on all newly created files.** Answer b is incorrect; this would result in a permission block of `-rw-r--r--`. Answer c is incorrect; this would result in a permission block of `-r--r--r--`. Answer d is incorrect; this would result in a permission block of `-r--r--rw-`.

## CHAPTER PREREQUISITE

Before beginning this chapter, you should understand the sequence of events that occur when you boot Linux as covered in Chapter 2, “Booting Linux.” You also need to understand how the filesystem is organized and where to locate specific types of files. Review the section on processes in Chapter 5, “GNU and UNIX Commands,” to ensure that you understand how to stop and start a process.

## Administrative Tasks

## WHILE YOU READ

1. You have an important meeting with your boss this afternoon and do not want to forget it. What should you do?
2. You need to re-index your database but want to do it when the system’s load is low to prevent adversely affecting your users. What should you do?
3. You have a user who every morning schedules a job to run at 8 a.m., which slows down your system. What can you do to prevent him from scheduling a job using at?
4. Your database administrator needs to run a script every day for system maintenance. You do not allow users to run cron jobs. How could you make her job easier?
5. You want to save all messages from mail to the maillog file. What should you do to make this happen?
6. You made the changes as to where the messages from mail are to be saved. When you look at the maillog file, it is empty. What happened?
7. You want to find out when was the last time each of your users logged in. How can you find this information?
8. You want to start a new mail log once a month. What should you do?

## Scheduling Jobs

A large part of a system administrator's job entails performing repetitive tasks. The ability to schedule these tasks becomes a great timesaver.

You might want to schedule an event to remind you of something or to run a program unattended. You might have events that occur only once and others that repeat at a regular interval. Linux has the capability to do both automatically.

### at

When you have a job that you want to run only once at a specific time, you can use the at command. The syntax for the at command is

```
at [options] time
```

The options that can be used with the at command are listed in Table 10.1.

| Table 10.1 Options That Can Be Used with the at Command |
|---|---|
| **Option** | **Action** |
| -b | Schedules job when system load is low; see the section on batch later in this chapter |
| -d | Deletes at job; same as atrm |
| -f *filename* | Reads job from specified file |
| -l | Lists all jobs for that user; same as atq |
| -m | Mails user when job completes |

Using the at command is very simple and consists of three simple steps:

1. Type at with any options and the time of execution.
2. Enter the command you want to run.
3. Press Ctrl-D to save the job.

After at runs a job, it can send you an email with any error messages or to notify you that the job completed. at can run a job only once, and after a job runs, it is deleted from the queue. You can use the at command to set a quick reminder:

```
$ at 17:00
at> xmessage -display:0.0 "Time to go home!"
at> <EOT>
warning: commands will be executed using /bin/sh
job 11 at 1999-05-11 17:00
```
