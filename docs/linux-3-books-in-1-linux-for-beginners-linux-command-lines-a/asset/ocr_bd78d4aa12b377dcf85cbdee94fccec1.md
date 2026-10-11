# ## Chapter Nine

# ## Using Access Control Lists in Linux

Now that you know how to encrypt and protect your files and data using a password, let us understand how you can control access to the servers in Linux.

# ### Introduction to Access Control Lists (ACL)

An ACL is one that provides flexible and additional permissions for your files and directories. It is designed so you can work with the different file permissions in Linux. ACL also allows you to identify the permissions you need to set for each user or a group of users. You can also use it to protect any disc resource.

# ### Uses of ACL

Consider a situation where you have a user who is not a part of any user group on the server or network. This user needs to access files and make changes to them, so you will need to give him access using commands. This is where the concept of Access Control Lists comes into the picture. Using ACLs, you can grant flexible permissions to specific users in the system. If you are an administrator, you can use an ACL to define the fine-grained access rights for directories and files. You can use the keywords setfacl and getfacl to set up an ACL and view the ACL on your server or system. For instance, if you run the following command: getfacl test/declarations.h, you will receive the output below:

```
# file: test/declarations.h
# owner: mandeep
# group: mandeep
user::rw-
group::rw-
other::r—
```

# ## List of Commands to Set Up ACLs