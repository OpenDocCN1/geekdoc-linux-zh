-m newmembers Similar to -M, this option allows the addition of existing users to a group without replacing the existing list of members. Login names or user IDs may be used, and duplicate users are silently eliminated.
-d oldmembers Similar to -M, this option allows the deletion of existing users from a group without replacing the existing list of members. Login names or user IDs may be used and duplicate users are silently eliminated.
groupadd also has a -o option that allows allocation of an existing group ID to a new group. The default action is to reject an attempt to add a group, and this option overrides the check for duplicate group IDs. There is rarely any need to duplicate a group ID.
The groupmod command adds one additional option:
-l name This option allows changing of an existing group name to name. The new name must not already exist, and any attempt to duplicate an existing group name will be rejected.
Options for groupshow are the same as for usershow, with -g gid replacing -u uid to specify the group ID. The -7 option does not apply to the groupshow command.
The command groupnext returns the next available group ID on standard output.
For a summary of options available with each command, you can use:
pw [command] help
For example, pw useradd help lists all available options for the useradd operation.
Command Arguments: None

# Examples

+   1. Adding a group:
+   
+   # pw groupadd project0
+   # pw groupshow project0
+   project0:*:1100:
+   
+   In this example, 1100 is the GID of project0. Right now, project0 has no members.

+   2. Adding user accounts to a new group:
+   
+   # pw groupmod project0 -M mansoor
+   # pw groupshow project0
+   project0:*:1100:mansoor
+   
+   These commands will add mansoor as a member of project0 and show his UID number.

The argument to -M is a comma-delimited list of users to be added to a new (empty) group or to replace the members of an existing group. To the user, this group membership is different from (and in addition to) the user's primary group listed in the password file. This means that the user will not show up as a member when using