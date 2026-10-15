
In this way you create a disk image inside a disk image. If you want to move the Macintosh-created disk image to tape, CD-R, or some other medium, you can do so by mounting the Linux-created disk image with the Linux loopback driver and HFS support, as in

```
mount -t hfs -o loop image.img /mnt/image
```

You can then access the Macintosh-created image inside the /mnt/image directory in order to send it to its ultimate destination medium.

## Security Considerations

As with backups initiated by the backup server, those initiated by client computers present security issues. When backing up to disk shares, though, these issues aren’t any different from the issues involved in normal file-sharing security, as described in previous chapters. If you write a script on a remote system to initiate a backup, though, you should consider how the script will mount the share. If the script needs to know the share’s password, that’s a potential security problem. So is leaving a client computer running with a user logged in to obviate the need for a password.

## Restoring Files

Backing up is not very difficult. Restoring files to an intact client is also not very difficult. Restoring files to a system that has failed completely, however, can be much more difficult, or at least tedious. I can’t begin to cover every option or situation in this chapter, so I present some generalized advice and information that should help you to bring up a working system.

## Partial Restores

A partial restore is a restoration of some subset of the files that you’ve backed up. This section covers the subset of partial restores that involve restoring files to a working client. You might want to do a partial restore to a client that’s not working—for instance, if Windows 98’s C:\WINDOWS directory were damaged. To do that, see the section “Complete Restores and Disaster Recovery” later in this chapter.

## Server-Initiated Backups

If you’ve backed up data by using the Linux box’s ability to function as a file-sharing client to grab remote machines’ files, you must reverse the steps you took to back up the data. For instance, suppose you used smbtar to back up a remote system with the following command:

```
smbtar -s winbox -x cdrive -u billg -p mypassw -t /dev/nst0
```

Now, suppose you have cause to restore a file or directory, say C:\DOCS\BigFile.doc. You could use the following command to do so:

```
smbtar -s winbox -x cdrive -u billg -p mypassw -t /dev/nst0 -r DOCS/BigFile.doc
```

As you can see, this command is identical to the original backup command, except that it includes the -r switch and the name of the file to be restored. There are some important points to note about this command:

- You must use a read/write account or password to restore files, even if you used a read-only account or password to back up the share. If the client isn't set up for write access via SMB/CIFS, you might need to temporarily modify its settings.
- Linux is case sensitive, so you must specify the filename case correctly for this command to work. Note that Linux and Windows handle the case of short filenames differently. Therefore, if the client system dual-boots and you're not sure which OS you used when performing the backup, you might have to check the tape archive itself or try both possibilities (DOCS and docs in the case of the example). Keeping a log of the backed-up files can be extremely useful in this situation.
- Although Windows uses a backslash (\ ) to separate directories and smbtar displays the same, the files actually appear on the tape with forward slash (/ ) directory separators. You should use forward slashes to separate the directory names.
- You do not specify a leading slash when you list the filenames you want to restore.
- smbtar doesn't take well to filename specifications that contain spaces, so you might need to use smbmount and ordinary tar to restore files with spaces, if you need to list them by name. (The spaces are only a problem in specifying the files, so if you have filenames with spaces inside a directory with no spaces in its name, you can restore the entire directory with no problems.)

You can restore multiple files in this way, too—just list the filenames one after another. If you want to restore an entire directory, give the directory's name, and smbtar restores the whole thing.

Because smbtar stores files on tape in an ordinary tar format, you can use tar to restore smbtar-created archives. For instance, here's an alternative means to restore the file C:\DOCS\BigFile.doc:

```
smbmount //winbox/cdrive mypassw /mnt/winbox -U billg
Password: mypassw
cd /mnt/winbox
tar xvf /dev/nst0 ./DOCS/BigFile.doc
cd -
smbumount /mnt/winbox
```
