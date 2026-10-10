# ## Groups and Permissions

Groups and permissions are two of the most fundamental concepts of Linux, and unfortunately two of the most difficult concepts for the new user to grasp. I mentioned in the previous section that Linux offers considerably more security than Windows does for multi-user purposes.

This is due in a great part to the system of groups and permissions. To understand groups and permissions, you must also understand that each user falls into at least one of three different classifications: *owner* or *user*, *group*, and *other*. Every file and directory on your system has *permissions* set which tell the computer whether or not a user is allowed to read a file, create one, or run a program.

These permissions are organized into three groups of three permission bits: *read, write*, and *execute*. They are abbreviated r, w, and x, respectively.

# ### The Owner Classification

The owner classification refers to the owner of a file. You can become an owner of a file by creating one or having ownership of a file transferred to you. The owner is the only person who can change permissions to a file or directory.

# ### The Group Classification

The next classification is the group classification. Each file belongs to one owner. But the owner himself belongs to one or more *groups*. These groups may consist of many different users and for many different purposes. Most users, for instance, belong to the “users” group. Administrators might belong to the “adm” or “admin” group.

An owner of a file can also allow members of his group certain access levels to the file. This is helpful if you have memories that need to be shared or programs that need to be restricted from other users.

# ### Everyone Else (Other)

Users who are not the owner of a file or in the owner’s group are called “other” users. In common parlance, this means “everyone else” who isn’t included in those other classifications.