# Question 26

Answer b is correct. A striped virtual file system is composed of several partitions that are allocated and used in an interleaved fashion. RAID 1 is a configuration that uses mirroring in an identical (not interleaved) fashion. Therefore, answer a is incorrect. A concatenated virtual file system uses one partition at a time. Therefore, answer c is incorrect. Hot spare is not a type of virtual file system. Therefore, answer d is incorrect.

# Question 27

Answers a, c, and d are correct. If a filename is specified, the message is appended to the file. If a hostname is specified, the message is sent to the host. If a user account name is specified, the message is displayed on the standard output of the logged-in user. The only other valid action is an asterisk (*), which causes the message to be displayed on the standard output device of all logged-in user accounts. Therefore, answer b is incorrect.

# Question 28

Answers a and c are correct. The **share** command, used without arguments, lists all locally shared NFS resources. The **dfshares** command can be used to list locally or remotely shared resources. The **dfmounts** command can be used to list locally or remotely mounted resources. Therefore, answer b is incorrect. The **mountall** command is used to mount local file systems. Therefore, answer d is incorrect. The **mount** command is used to mount or list currently mounted local file systems and NFS resources. Therefore, answer e is incorrect.

# Question 29

Answer b is correct. To generate the data files used to create NIS maps, you should copy the /etc files to a different directory and clean up the copy. The /etc files can be modified, but the editing might adversely affect the system and is not the best approach. Therefore, answer a is incorrect. The **makedbm** and **buildm** commands do not exist. Therefore, answers c and d are incorrect.