> **NOTE** *When setting options in the* `vsftpd.conf` *file, there are no spaces around the* `=` *sign.*

# Enabling Stand-Alone Access

To run `vsftpd` as a stand-alone server, you set the `listen` option to `YES`. This instructs `vsftpd` to continually listen on its assigned port for requests. You can specify the port it listens on with the `listen_port` option.

```
listen=YES
```

# Enabling Login Access

In the following example, taken from the `vsftpd.conf` file, anonymous FTP is enabled by assigning the `YES` value to the `anonymous_enable` option. The `local_enable` option allows local users on your system to use the FTP server.

```
# Allow anonymous FTP?
anonymous_enable=YES
#
# Uncomment this to allow local users to log in.
local_enable=YES
```

Should you want to let anonymous users log in without providing a password, you can set `no_anon_password` to `YES`.

# Local User Permissions

A variety of user permissions control how local users can access files on the server. If you want to allow local users to create, rename, and delete files and directories on their account, you have to enable write access with the `write_enable` option. This way, any files they upload, they can also delete. Literally, the `write_enable` option activates a range of commands for changing the file system, including creating, renaming, and deleting both files and directories.

```
write_enable=YES
```

You can further specify the permissions for uploaded files using the `local_umask` option (022 is the default set in `vsftpd.conf`, indicating read and write for the owner and read only for all other users, 644).

```
local_umask=022
```

Though ASCII uploads are disabled by default, you can also enable this feature. ASCII uploads entail certain security risks and are turned off by default. But if you are uploading large text files, you may want to enable them in special cases. Use `ascii_upload_enable` to allow ASCII uploads.

# Anonymous User Permissions

You can also allow anonymous users to upload and delete files, as well as create or remove directories. Uploading by anonymous users is enabled with the `anon_upload_enable` option. To let anonymous users also rename or delete their files, you set the `anon_other_write_enable` option. To also let them create directories, you set the `anon_mkdir_write_enable` option.