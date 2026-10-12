The items field contains the number of auxiliary records that follow the syscall record.

# ppid=2686

The ppid field records the Parent Process ID (PPID). In this case, 2686 was the PPID of the parent process such as bash.

# pid=3538

The pid field records the Process ID (PID). In this case, 3538 was the PID of the cat process.

# auid=1000

The auid field records the Audit user ID, that is the loginuid. This ID is assigned to a user upon login and is inherited by every process even when the user's identity changes, for example, by switching user accounts with the su - john command.

# uid=1000

The uid field records the user ID of the user who started the analyzed process. The user ID can be interpreted into user names with the following command: ausearch -i --uid UID.

# gid=1000

The gid field records the group ID of the user who started the analyzed process.

# euid=1000

The euid field records the effective user ID of the user who started the analyzed process.

# suid=1000

The suid field records the set user ID of the user who started the analyzed process.

# fsuid=1000

The fsuid field records the file system user ID of the user who started the analyzed process.

# egid=1000

The egid field records the effective group ID of the user who started the analyzed process.

# sgid=1000

The sgid field records the set group ID of the user who started the analyzed process.

# fsgid=1000

The fsgid field records the file system group ID of the user who started the analyzed process.

# tty=pts0

The tty field records the terminal from which the analyzed process was invoked.

# ses=1

The ses field records the session ID of the session from which the analyzed process was invoked.