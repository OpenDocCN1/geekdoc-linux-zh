Without making that change, all downloads are done in binary mode. Although vsFTpd will seem to allow the user to change to ascii mode, ascii mode will not work if this setting is NO.

# Uploading (writing) files from local users

Two values set in the `vsftpd.conf` file allow the uploading of files during a vsFTPD session. These defaults allow any users with regular, local user accounts to upload files:

```
write_enable=YES
local_umask=022
```

The `write_enable` value must be YES if you intend to allow any users the ability to write to the FTP server. The `umask=022` value sets the default file permission used when a local user creates a file on the server. (The 022 value causes files created to have 644 permission, allowing the user read and write permission and everyone else only read permission.)

As with downloading, uploading in ascii mode is prohibited by default. Though ascii downloads create a potential security hole for draining resources from your server, ascii uploads are apparently not as dangerous and can be useful for uploading text files. To allow ascii uploads, add the following line:

```
ascii_upload_enable=YES
```

# Uploading (writing) files from anonymous users

The ability to upload files is turned off for anonymous FTP users. If you want to turn it on, add the following line to the `vsftpd.conf` file:

```
anon_upload_enable=YES
```

You must also make sure that the `/var/ftp` directory contains one or more directories with write permissions open to anonymous users. For example, you might want to create an `incoming` directory and open its permissions (`chmod 777 /var/ftp/incoming`).

Files uploaded by anonymous users will be created with 600 permission by default (read/write for the `ftp` user, not accessible to any other users so that even the user who uploaded the file can't remove it). To allow 644 permission, for example, you can add the following line:

```
anon_umask=077
```

Once you allow the anonymous user to upload files, you can grant limited ability to change the files he or she uploads. By adding the following line, you can allow anonymous users to rename or delete any files owned by anonymous users (providing the files are in directories for which the users have write permission):

```
anon_other_write_enable=YES
```

If you also want to allow anonymous users to create their own directories, add the following:

```
anon_mkdir_write_enable=YES
```