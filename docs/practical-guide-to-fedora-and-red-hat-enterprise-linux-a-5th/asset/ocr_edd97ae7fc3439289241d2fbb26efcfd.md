`/etc/fstab` **filesystem (mount) table** Contains a list of all mountable devices as specified by the system administrator. Programs do not write to this file but only read from it. Refer to “`fstab`: Keeps Track of Filesystems” on page 490.

`/etc/group` Groups allow users to share files or programs without giving all system users access to those files or programs. This scheme is useful when several users are working with files that are not public. The `/etc/group` file associates one or more user names with each group (number). Refer to “ACIs: Access Control Lists” on page 207 for another way to control file access.

An entry in the `/etc/group` file has four fields arranged in the following format:

```
`group-name:password:group-ID:login-name-list`
```

The *group-name* is the name of the group. The **password** is an optional encrypted password. This field frequently contains an x, indicating that group passwords are not used. The *group-ID* is a number, with 1–499 reserved for system accounts. The *login-name-list* is a comma-separated list of users who belong to the group. If an entry is too long to fit on one line, end the line with a backslash (\), which quotes the following RETURN, and continue the entry on the next line. A sample entry from a **group** file follows. The group is named `pubs`, has no password, and has a group ID of 503:

```
    pubs::x:503:alex, jenny, scott, hls, barbara
```

You can use the `groups` utility to display the groups that a user belongs to:

```
$ groups alex
    alex : alex pubs
```

Each user has a primary group, which is the group that user is assigned in the `/etc/passwd` file. By default, Fedora/RHEL user have private groups: Each user’s primary group has the same name as the user. In addition, a user can belong to other groups, depending on which *login-name-lists* the user appears on in the `/etc/group` file. In effect, you simultaneously belong both to your primary group and to any groups you are assigned to in `/etc/group`. When you attempt to access a file you do not own, the operating system checks whether you are a member of the group that has access to the file. If you are, you are subject to the group access permissions for the file. If you are not a member of the group that has access to the file and you do not own the file, you are subject to the public access permissions for the file.

When you create a new file, it is assigned to the group associated with the directory the file is being written into, assuming that you belong to that group. If you do not belong to the group that has access to the directory, the file is assigned to your primary group.

Refer to page 557 for information on using *system-config-users* to work with groups.

`/etc/hosts` The `/etc/hosts` file stores the name, IP address, and optional aliases of the other systems that the local system knows about. At the very least, this file must have the hostname and IP address that you have chosen for the local system and a special