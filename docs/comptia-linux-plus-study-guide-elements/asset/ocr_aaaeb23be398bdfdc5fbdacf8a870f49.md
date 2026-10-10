In this case, scope is the type of entity to which the ACL applies—typically u or user for a user, but g or group for a group is also possible, as is o or others to set a world ACL. The ID is a UID, GID, username, or group name. (This component is omitted if you use a scope of other.) The perms field specifies the permissions, either in octal form (as a single digit from 0 to 7) or in symbolic form (for instance, rw- or r-x).

As an example, consider a user who wants to create an ACL to enable another user (theo) to be able to read a file:

```
`$ setfacl -m user:theo:-- dinosaur.txt`
```

Once this command is issued, theo can read the dinosaur.txt file, even if the file’s ordinary Unix permissions would not permit this access. Because ordinary users may create and modify ACLs on their own files, the system administrator need not be bothered to create new groups. Users can create and modify ACLs only on files they own, though, much as they can modify the Unix permissions only on their own files.

If you want to see the ACLs on a file, you can use the getfacl command:

```
$ getfacl dinosaur.txt

# file: dinosaur.txt
# owner: amy
# group: users
user::rw-
user:theo:rw-
group::---
mask::rw-
other::---
```

Many Linux systems still have no need for ACLs; Unix-style permissions are adequate for many purposes. As more Linux tools are written to take full advantage of ACLs, they’re likely to become more important.

# # Setting Environment Variables

Computer programs, like people, exist in certain environments. The environments for computer programs are defined by features such as the current working directory, the user’s preferred language, and the type of terminal in use. In order to deliver this information to programs, Linux maintains environment variables. Like street signs in the physical world, environment variables convey information about the virtual “location” of the program and the resources that are available to it. Therefore, understanding how to set and use environment variables is important for both system administrators and users.

Programs query environment variables to learn about the state of the computer as a whole or what resources are available. These variables contain information such as the