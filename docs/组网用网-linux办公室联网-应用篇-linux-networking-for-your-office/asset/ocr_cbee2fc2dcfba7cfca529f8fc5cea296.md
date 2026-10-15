After you burn the CD-ROM, you should be able to mount it and access the files. There's no need to keep the outfile.iso image file after the CD-ROM has been created. If you prefer to use tar, you can substitute an appropriate tar command for the mkisofs command in this example.

# Note

> Because CD-R media are more reliable than tapes, using gzip to compress a tar archive is safer with CD-R than with tapes. The potential still exists for compression and a read error to render an archive unreadable, though.

Both mkisofs and cdrecord support many options that you might need to use. Check their manpages for more details.

In general, I find CD-R media to be too limiting for regular backups of entire systems. They can be useful, however, for backups of clients with small hard disks. The fact that most computers have CD-ROM drives means you can restore data from such backups locally, without involving the server. This can be a great boon in an emergency situation because all you need is an emergency Linux boot floppy to restore the client. Such restores are covered later in this chapter, in the section "Restoring Files."

# Server-Initiated Backups

Convincing users to back up their data can be an exercise in frustration. Many individuals are forgetful or find backup procedures to be tedious. Humans also have a common tendency to think that bad things won't happen to them, only to other people, which leads to a minimized sense of risk. As a network administrator, you can't afford to succumb to such attitudes because when a computer on your network experiences problems, your users will come to you for a solution.

For these reasons, server-initiated backups are often a good idea. All your users need do is leave their computers turned on at some specified time, such as Monday nights, and you configure the Linux server to back up the remote filesystem. Such backups work quite well with NFS and SMB/CIFS networks, but because Linux support for mounting Macintosh file shares is so weak, you can't use this technique with Macintoshes.