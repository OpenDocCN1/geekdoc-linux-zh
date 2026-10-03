It is the pwconv command that relies on the special value of “x” in the password field of the /etc/passwd file. The “x” indicates that the password for the user already exists in the /etc/shadow file. If the /etc/shadow file does not exist, pwconv re-creates everything in it from information found in the /etc/passwd file. If the /etc/shadow file does exist, the following is performed:

+   - Entries that are in the /etc/passwd file and not in the /etc/shadow file are added to the shadow file.
- Entries that are in the /etc/shadow file and not in the /etc/passwd file are removed from the shadow file.

Each line in the /etc/group file contains several fields, separated by colons (:). This line is formatted as follows:

```
group-name:group-password:gid:user-list
```

Table 8.5 defines each field in the /etc/group file.

# TABLE 8.5

# FIELDS IN THE /ETC/GROUP FILE

| Field Name | Description |
|---|---|
| group-name | Contains the name assigned to the group. For example, members of the accounting department might be called acct. Group names can have a maximum of nine characters. |
| group-password | Usually contains an asterisk or is empty. The group-password field is a relic of earlier versions of UNIX. |
| gid | Contains the group's GID number. It must be unique on the local system, and should be unique across the entire organization. Each GID number must be a whole number between 0–60002, but it can go as high as 2147483647. Numbers less than 100 are reserved for system default group accounts. User-defined groups can range from 100–60000 (60001 and 60002 are reserved and assigned to nobody and noaccess, respectively). See the previous Note regarding the use of UIDs and GIDs greater than 60000. |
| user-list | Contains a list of groups and a comma-separated list of user names, representing the user's secondary group memberships. Each user can belong to a maximum of 16 secondary groups. |