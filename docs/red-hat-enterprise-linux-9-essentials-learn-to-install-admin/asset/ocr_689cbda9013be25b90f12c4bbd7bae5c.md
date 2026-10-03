# Sharing Files between RHEL 9 and Windows Systems with Samba

For this example, we will create the /sampleshare directory referenced previously in the smb.conf file and change the enforcement type to make it accessible to the Samba service. Begin by creating the directory as follows:

```
# mkdir /sampleshare
```

Next, check the current SELinux context on the directory:

```
$ ls -Z /sampleshare/
unconfined_u:object_r:root_t:s0 .
```

In this instance, the context label of the folder has been assigned a type of root_t. To make the folder sharable by Samba, the enforcement type needs to be set to samba_share_t using the semanage tool as follows:

```
# semanage fcontext -a -t samba_share_t "/sampleshare(/.*)?"
```

Note the use of a wildcard in the semanage command to ensure that the type is applied to any sub-directories and files contained within the /sampleshare directory. Once added, the change needs to be applied using the restorecon command, making use of the -R flag to apply the change recursively through any sub-directories:

```
# restorecon -R -v /sampleshare
Relabeled /sampleshare from unconfined_u:object_r:default_t:s0 to
unconfined_u:object_r:samba_share_t:s0
```

Once these changes have been made, the folder is configured to comply with SELinux policy for the smb process and is ready to be shared by Samba.

# 19.7 Creating a Samba User

Any user that requires access to a Samba shared resource must be configured as a Samba User and assigned a password. This task is achieved using the smbpasswd command-line tool. Consider, for example, that a user named demo is required to be able to access the /sampleshare directory of our RHEL 9 system from a Windows system. To fulfill this requirement, we must add demo as a Samba user as follows:

```
# smbpasswd -a demo
New SMB password:
Retype new SMB password:
Added user demo.
```

Now that we have completed the configuration of an elementary Samba server, it is time to test our configuration file and then start the Samba services.

# 19.8 Testing the smb.conf File

The settings in the smb.conf file may be checked for errors using the testparm command-line tool as follows:

```
# testparm
Load smb config files from /etc/samba/smb.conf
Loaded services file OK.
```