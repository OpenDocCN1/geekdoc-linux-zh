
Your job is comparatively pretty easy. Almost all of the work can be done using Samba controls; however, if you plan to allow itself access, such as Telnet (bad) or SSH (good), then your job becomes a bit more difficult.

The process and mechanism I propose use here has been tested in many different settings and has been found to be sufficiently secure to keep the riff-raff off while allowing normal users to do the work they need, both from their Windows computers and shell accounts. It may work for you. Using the Rings of Security, we will start at the file system. These techniques will work on any Posix file system (ext2, ext3, reiserfs, XFS, JFS, etc.).

Here is a quick note about users. When I set up a system, every user has a common primary group. This is my users group, and it has a GID of 100. It is roughly equivalent to the NetWare “Everyone” group. This makes setting up permissions in public shares easier. When using a distribution like Red Hat, by default each user is in their own primary group, I create a users group and add everybody as a member. The result is the same, but having everyone’s primary group “users” is easier to manage.

### 3.8.12 File and Directory Masks for Shares

When setting up shares to be shared via Samba, first never share the root directory. If you do, you are just asking for trouble. I typically have my /home directory on a separate partition, so network users cannot fill up the root partition with their latest collection of MP3 files. All of my Samba share points out of the /home/samba directory.

There are two general types of Samba shares. In one, you want to allow everyone access; in the other we go through this exercise with two shares called “public” and “private.” The techniques discussed can then be tailored to your particular application.

We will now create the two directories.

```bash
mkdir /home/samba/public
mkdir /home/samba/private
```

Now, change the mode on the public directory to 2775. Change the mode on the private directory to 2270. Change the group on the public directory from root to “users.” Add a group called “private” with the groupadd command. Finally change the group (chgrp) on the private directory to “private.”

Why? All access to the directory will be group permissions. Since we plan to have a guest account, the public directory will be read-only to the guest user, and the private directory will be inaccessible. The group permissions on both directories will be sufficient for allowed users to read and write files.

The sticky bit has been set on both directories to more closely mimic the default behavior of a Windows NT server. When a user creates a file, his UID and GID will cause each new file to be created with the users group. The default mask of 022 will prevent anyone else from modifying it. The sticky bit will cause the file to be created so that the default group on the file is the “users” group. Thus, when the file owner chooses to allow others to modify the files he has created, the group is suitable. It is a way of forcing group inheritance.

For example:

User Larry creates a document called Customer_Proposal.doc. The file owner is Larry and the group is “users” (thanks to the sticky bit). Bob now wants to read and modify the file. The default permissions on the file are 755. Bob will be able to read the file but not modify it. This is close to Windows default behavior, but [he] needs rights to modify the file, so at this stage we're close, but not enough, to Windows default behavior.

To fix the problem described in the example, you can use the “create mode” option to be 0775. This will allow group permissions to be set. When working on a private share, you will want the “create mode” to be a bit more restrictive and not allow the file contents [to be read/written by all]. Do this by setting the create mode to 0771. I will explain more about this “Real Access Control Lists” for your use.

So, you have it. We have now mimicked the default behavior of NT using Samba and Linux, along with some judicious settings. I have included some smb.conf stanzas for your use.

```ini
[public]
path = /home/samba/public
public = yes
writable = yes
directory mask = 0775
# this is necessary if you do not have a common primary group
create mask = 0775
hide dot files = true
```

```ini
[private]
path = /home/samba/private
public = no
writable = yes
directory mask = 0771
create mask = 0771
hide dot files = true
# see sections below for explanation of these parameters
force group = @private
valid users = @private, bob, larry, mark, dave
write list = bob, larry
read list = mark, dave
```

### 3.8.12.2 Share Attach Permission Lists

On a public share, public = everyone has access. The permissions are generally pretty lax, allowing for a free exchange of files. On a private share, where access is controlled, you will want to specify who can have access and who cannot. This is done using setting public = no and then having a valid users list.

In the above example for the private share we have a valid users list of bob, larry, mark, and dave. Only these accounts will be able to attach to the private share. Maybe these guys are working on a project together and no one in the company needs access to the project files, which are stored on the private share. Maybe this is analogous to your accounting, which needs to have their data stored on the server for backup purposes, but we need to keep everyone else out. The valid users list is the mechanism for doing this.

Now, what is happening on the Linux system level? The directory is private and we created the private group in /etc/group. Now, edit /etc/group, and use the users bob, larry, mark, and dave [to] edit into that group. When completed, the group line will look something like this.

```text
private::30000:bob, larry, mark, dave
```

The GID is not really important. I just chose one that is out of the way of most everything. It will be automatically created by the groupadd command, you if you choose to use it.

Now, if we use bob, larry, mark, and dave want to access the data in the private directory, they can do so either through Samba or through their shell accounts. The directory permissions on /home/samba/private are 770, so anyone who is not a member of the private group will not be able to enter the directory, and the data remains secured.

### 3.8.12 Share Read and Write Lists

Samba has a much finer control over users' permissions than Posix normally. In the example of the private share, bob and larry [have] read and write permissions, while mark and dave only have read-only permissions. These are accomplished by using the directives:

```ini
write list = bob, larry
read list = mark, dave
```

These work pretty well, until mark and dave log in using SSH. Because they are members of the private group, they now have write permissions in the private directory, where through Samba, they could only read. This is a great argument for real Access Control Lists, covered in "Real Access Control Lists" on page 169.

If you do not allow access to your Samba server by regular users, the read and write lists are quite capable of enforcing your desired level of security.

### 3.8.14 Pseudo Access Control Lists

The whole process I have describing is what could be defined as a posix access control list. Each privately shared resource has its own group. Only those in the group can gain access to the shared directory via Samba or other method. Those not in the group have no access. They work quite well until you want to be able to say, with those shared directories, bob and larry can write, while mark and dave can only read. Or, larry and bob can write to this file, but mark and dave cannot. The Posix permissions are not granular enough to accomplish this without the use of specialized groups. Other holes include the use of a shell account and the integration of other services like NFS or AppleTalk (which you may also wish to use on your server).

### 3.8.12 Real Access Control Lists

Real Access Control Groups are possible on Linux. You just have to be willing to get off the beaten track by a bit. There is, as of the writing of this book, an effort to standardize Posix Access Control Lists (ACLs). The reason? There are competing methods available for achieving the goal of real Access Control Groups. One is a patch available from Bestbits (acl.bestbits.at) that works with the ext2 and ext3 file systems. Another is the XFS file system available from SGI (oss.sgi.com). Each of these has advantages and disadvantages.

- **Bestbits advantage:** If you already have a functioning Samba server based on ext2 or ext3 file system (which most are), this is a relatively easy add-on. You download the patch, patch your kernel, and recompile. You will not have to change all of files, users, and so forth.
- **XFS advantage:** If you are setting up a new Samba server from scratch, using the XFS file system to protect your user's data with a mature journaling file system that has thousands of high-end servers running on it. Another advantage is that SGI has a version of the Red Hat CD-ROM with XFS already set up and ready to use. Additionally, there is a patch available to extend XFS and Samba to use all of the Windows NT permissions. Check the XFS mailing list for a link to the patch.

With BestBits or XFS, Samba will need to be recompiled with the with-acl-support option before you can use this feature. The respective pages and HOWTOs will give you the correct syntax for each method to create, modify, and delete the ACLs. In case, you will also need to modify your backup procedure so the ACLs will be backed up and restored in the event of a system crash. Samba has a utility called fsdump. I have seen other techniques where all of the ACLs are enumerated and stored in a special file prior to backup standard tools tar and cpio can use.

### 3.8.126 Home Directories

Samba has the ability to share a user's home directory by default. To ensure the highest level of protection to the user's home directory, you will want to ensure the permissions to 700 and no more. Then, in the special "homes" share that the share is not publicly accessible or browsable, and that it has a valid user list of only the user. The Posix permissions 700 will ensure that if Samba lets an invalid user through he will not have any rights. However, I have never seen Samba make this kind of mistake.

## 3.8.13 User Security

There are three types of user access allowed under Samba. The first is shared level. I have not found many reasons to employ it, if you need it, I kindly refer you to the Samba documentation. The parameter to this set is:

```ini
[global]
  security = share
```

The second and most common for stand-alone Samba servers is the user-level security. This, generally stated, is that all rights to the shared resources are granted on a per-account basis, and that the account database is the /etc/passwd and smbpasswd pair.
