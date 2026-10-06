# 610 Part IV Implementing Network Services in SUSE Linux

If you want to enable local users to upload files, you need to set the following-ing in /etc/vsftpd.conf:

```
write_enable=YES
```

If you have done this, a new FTP session like the one shown in Listing 23-2 will succeed in uploading to the user's home directory.

If you also want to allow anonymous logins (ftp or anonymous), you need to enable the following:

```
anon_upload_enable=YES
```

There will be directories on the server with permissions allowing these writes: By default, this will not be the case. We cannot stress the dangers of allowing anonymous FTP unless you have carefully thought about what you are doing. In particular, the writable directory should not be the root of the FTP directory structure /srv/ftp/ You should also consider creating a writing-only setup, by creating a directory such as /srv/ftp/incoming/ owned by user ftp group, and with restrictive permissions. The permissions on this directory should not allow others to write it or list it. In fact, the setup verify if you set permissions 300 on /srv/ftp/incoming/

Listing the root FTP directory shows:

```
rootable------ /srv/ftp # ls -la
d-xr------ 2 ftp ftp 144 Aug 10 17:31 incoming
```

These permissions mean that the anonymous FTP user cannot list the directory, but the FTP daemon can write to the directory, so uploading will work. The setting for the anonymous umask in the configuration file is left at its default value of 077, files that are uploaded will not be downloadable because they will have permissions 600 on the server and will not be readable by others.

If you

```
anon_umask=022
```

/etc/vsftpd.conf, then files that have been uploaded are anonymous-downloadable, although the incoming directory is still listable. This is almost very undesirable, except in a trusted environment, because confederates of anyone who has posted files on your server will be able to download them.

The root FTP directory /srv/ftp/ itself should be owned by user root and group root, and there should be no subdirectory that is readable, writable, and listable.

See Chapter 2 for more information about permissions.

![](bbox=[0.125, 0.883, 0.203, 0.923])