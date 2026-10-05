# Develop a media life cycle

# 297

# Verify your media

We've heard many horror stories about system administrators who did not cover problems with their dump regime until after a serious system failure. It is essential that you continually monitor your backup procedure and verify that it is functioning correctly. Operator error ruins more dumps than any other problem.

The first check is to have your backup software attempt to reread tapes immediately after it has finished dumping. Scanning a tape to verify that it contains the expected number of files is a good check. It's best if every tape is scanned, but no longer seems practical for a large organization that uses tapes every day. A random sample would be prudent in this environment.

It is often useful to generate a table of contents for each filesystem (dump use -t) and to store the restoring catalogs on directory tree. These catalogs should be named in a way that relates them to the appropriate tape; for example, okra:usr.Jan.13. A database of these records makes it easy to discover what piece of media a file is on. Just grep for the filename and the newest instance.

In addition to providing a catalog of tapes, successfully reading the table of contents is a good indication that the dump is OK and that you will be able to read the media when you need to. A quick attempt to restore to a random file gives you more confidence in your ability to restore from that media.

You should periodically attempt to restore from random media to make sure that restoration is still possible. Every so often, to restore from an old (months or years) piece of dump media. Tape drives have been known to wander out of alignment over time and become unable to read their old tapes. The media can be recovered by a company that specializes in its service, but it is expensive.

A related check is to verify that you can read the media on hardware other than your own. If your machine runs, it does not much good to know that the backup could have been read on a tape drive that has been destroyed. DAT tapes have been particularly susceptible to this problem in the past, but most recent versions of the technology have improved.

# Develop a media life cycle

All media has a finite life. It's great to recycle the media, but be sure to abide by the manufacturer's recommendations regarding the life of the media. Most tape manufacturers quantify this life in terms of the number of passes that a tape can stand: a backup, a restore, and mt fsf (file skip forward) each represent one

+   1. GNU units of restore include the -C option to verify a dump against a directory tree.
2. For example, restore -t reads only the contents of the dump, which is stored at the beginning of the tape. When you actually restore a file, you are testing a more extensive region of the media.
3. It's helpful to treat users who request the restore of accidentally deleted files as colleagues who are spot-checking your backup system rather than as incompetent, file-deleting annoyances. A positive attitude makes the experience more pleasant for both of you and increases the number of spot-checks.

![](bbox=[0.095, 0.327, 0.195, 0.373])

![](bbox=[0.945, 0.547, 0.985, 0.627])