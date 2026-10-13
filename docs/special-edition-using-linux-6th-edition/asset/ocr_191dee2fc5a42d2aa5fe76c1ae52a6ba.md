# Figure 11.1

The specific characteristics of the /etc/passwd file are shown here.

![](bbox=[0.333, 0.071, 0.767, 0.253])

The first set of dashes and letters represent the file type and permissions for this file. They are broken down into four logical groups. The first character indicates the file type. The file type will be one of the following:

| Character | File Type |
|---|---|
| `-` | Regular file (usually either a binary or ASCII text file) |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device (character special file) |
| `b` | Block device (block special file) |
| `s` | Socket (a network listener) |
| `p` | Named pipe (like a pipe (|), but with a name) |

Some of these will probably be foreign to you. The ones you’re most concerned with are the first three (`-`, `d`, `l`).

The next nine placeholders represent the permissions of each of the three levels: owner, group, and other. Each level uses three places to set permissions. For example, if you want to allow read, write, and execute privileges to the owner of a file, the letters `rwx` are present in positions 2–4. Figure 11.2 depicts the permission options for owner, group, and others.

# CHANGING PERMISSIONS

The access rights for any given file can be modified by using the change mode (chmod) command. To change the access rights, you must specify the following three elements:

+   - The level (owner level, group level, or other level) to modify
+   - The permission (read, write, or execute) to modify
+   - The file or files to modify

Table 11.4 lists the level options that can be used with the chmod command. The access rights or permissions that can be modified at each level are summarized in Table 11.5.