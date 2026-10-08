In the above example for the private share we have a valid users list of bob, larry, mark, and dave. Only these accounts will be able to attach to the private share. Maybe these guys are working on a project together and no one in the company needs access to the project files, which are stored on the private share. Maybe this is analogous to your accounting, which needs to have their data stored on the server for backup purposes, but we need to keep everyone else out. The valid users list is the mechanism for doing this.

Now, what is happening on the Linux system level? The directory is private and we created the private group in /etc/group. Now, edit /etc/group, and use the users bob, larry, mark, and dave edit into that group. When completed, the group line will look something like this.

```
private::30000:bob, larry, mark, dave
```

The GID is not really important. I just chose one that is out of the way of most everything. It will be automatically created by the groupadd command, you if you choose to use it.

Now, if we use bob, larry, mark, and dave want to access the data in the private directory, they can do so either through Samba or through their shell accounts. The directory permissions on /home/samba/private are 770, so anyone who is not a member of the private group will not be able to enter the directory, and the data remains secured.

# 3.8.12 Share Read and Write Lists. Samba has a much finer control over users' permissions than Posix normally. In the example of the private share, bob and larry read and write permissions, while mark and dave only have read-only permissions. These are accomplished by using the directives:

```
write list = bob, larry
read list = mark, dave
```

These work pretty well, until mark and dave log in using SSH. Because they are members of the private group, they now have write permissions in the private directory, where through Samba, they could only read. This is a great argument for real Access Control Lists, covered in "Real Access Control Lists" on page 169.

If you do not allow access to your Samba server by regular users, the read and write lists are quite capable of enforcing your desired level of security.

# 3.8.14 Pseudo Access Control Lists. The whole process I have describing is what could be defined as a posix access control list. Each privately shared resource has its own group. Only those in the group can gain access to the shared directory via Samba or other method. Those not in the group have no access. They work quite well until you want to be able to say, with those shared directories, bob and larry can write, while mark and dave can only read. Or, larry and bob can write to this file, but mark and dave cannot. The Posix permissions are not granular enough to accomplish this without the use of specialized groups. Other holes include the use of a shell account and the integration of other services like NFS or AppleTalk (which you may also wish to use on your server).