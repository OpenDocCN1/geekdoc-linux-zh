# WHERE TO LOCATE HOME DIRECTORIES

Typically, Linux systems place home directories as subdirectories of the `/home` directory. Each home directory is named after the account’s username so that the account user1 will have its home directory at `/home/user1/`.

As with UIDs, this is a simple organizational scheme that works well for a small system with a limited number of users. However, on a system with a large number of users, this scheme is problematic. Not only is it hard to keep track of a large number of subdirectories in `/home`, but all the subdirectories will exist on a single hard disk partition. This immediately creates a problem because the home directories will need to have severe storage limitations placed on them even with the largest available hard disks. For instance, if a single 20GB hard disk is allocated to the `/home` directory but you have 1,000 home directories, each home directory is restricted to an average disk consumption of roughly 20MB per disk.

Accordingly, with a large site, you need to segment your home directories into a logical structure. Generally, you will want to create several directories that in turn contain home directories. For instance, you might want to further subdivide `/home` into subdirectories reflecting some logical structure such as geographic location of users or organizational departments.

For instance, if an organization has users in Canada, Switzerland, Israel, Hong Kong, and the United States, you might want to create the following directories to hold home directories:

+   - `/home/ca`
+   - `/home/ch`
+   - `/home/il`
+   - `/home/hk`
+   - `/home/us`

Then, user1 in Hong Kong would have its home directory at `/home/hk/user1` and user2 in Canada would have its home directory at `/home/ca/user2`.

# EDITING THE `/etc/passwd` FILE

Never edit the `/etc/passwd` file directly. Instead, use the `vipw` command to set the necessary locks to enable safe editing of the passwd file and then open the file in an editor.

The `vipw` command uses your default editor as indicated by the `EDITOR` environment variable and if none is set, defaults to the `vi` editor. If you have a preferred editor, set the `EDITOR` environment variable and then launch `vipw` to edit the `/etc/passwd` file:

```
export EDITOR=emacs
/usr/sbin/vipw
```

> > **Note**  
> > If you are using the C Shell instead of Bash, set the `EDITOR` environment variable with the command `setenv EDITOR emacs`.