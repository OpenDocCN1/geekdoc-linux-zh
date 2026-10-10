In Listing 10.4, the ls command was employed with the -a option so that hidden files (files starting with a dot) are displayed. Recall that hidden files do not normally display without the -a option on the ls command. These files are account environment files as well as a Mozilla Firefox web browser configuration file directory. We'll cover environment files later in this chapter. You can modify any of these files or add new files and directories, if needed.

![](bbox=[0.14, 0.22, 0.24, 0.33])

> **NOTE** The /etc/skel files are copied to user account home directories only when the account is created. Therefore, if you make changes to the files later, you'll have to migrate those changed files to current user accounts either by hand or by shell scripts.

Now that we've covered the files in the creation side of the user account creation process, let's look at the files and directories that are built or modified as part of the process. Go back and look at Figure 10.1, if necessary, to refresh your memory of the various file and directory names.

# The /etc/passwd File

Account information is stored in the /etc/passwd file. Each account's data occupies a single line in the file. When an account is created, a new record for that account is added to the /etc/passwd file. A snipped example is shown in Listing 10.5.

+   **Listing 10.5:** Account records in the /etc/passwd file

```
```
$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
[...]
tcpdamp:x:72:72::/:/sbin/nologin
user1:x:1000:1000:User One:/home/user1:/bin/bash
Christine:x:1001:1001:Christine B:/home/Christine:/bin/bash
[...]
$
```
```

The /etc/passwd file records contain several fields. Each field in a record is delimited by a colon ( : ). There are seven fields in total, as described in Table 10.3.

**TABLE 10.3** The /etc/passwd file's record fields

| Field No. | Description |
| :--- | :--- |
| 1 | User account's username. |
| 2 | Password field. Typically this file is no longer used to store passwords. An x in this field indicates passwords are stored in the /etc/shadow file. |