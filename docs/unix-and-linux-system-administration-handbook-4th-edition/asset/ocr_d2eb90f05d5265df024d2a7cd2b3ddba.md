# Verify your media

We’ve heard many horror stories about system administrators who did not discover problems with their dump regime until after a serious system failure. It is essential that you continually monitor your backup procedure and verify that it is functioning correctly. Operator error ruins more dumps than any other problem.

The first check is to have your backup software attempt to reread tapes immediately after it has finished dumping. Scanning a tape to verify that it contains the expected number of files is a good check. It’s best if every tape is scanned, but this no longer seems practical for a large organization that uses many tapes every day. A random sample would be most prudent in this environment.

It is often useful to generate a table of contents for each filesystem (dump users can use restore -t and to store the resulting catalogs on disk. These catalogs should be named in a way that relates them to the appropriate tape; for example, okra:usr:Jan.13. A database of these records makes it easy to discover what piece of media a lost file is on. Just grep for the filename and pick the newest instance.

In addition to providing a catalog of tapes, successfully reading the table of contents from the tape is a good indication that the dump is OK and that you will probably be able to read the media when you need to. A quick attempt to restore a random file gives you even more confidence in your ability to restore from that piece of media.

You should periodically attempt to restore from random media to make sure that restoration is still possible. Every so often, try to restore from an old (months or years) piece of dump media. Tape drives have been known to wander out of alignment over time and become unable to read their old tapes. The media can be recovered by a company that specializes in this service, but it is expensive.

A related check is to verify that you can read the media on hardware other than your own. If your machine room burns, it does not do much good to know that the backup could have been read on a tape drive that has now been destroyed. DAT tapes have been particularly susceptible to this problem in the past, but more recent versions of the technology have improved.

# Develop a media life cycle

All media have a finite life. It’s great to recycle your media, but be sure to abide by the manufacturer’s recommendations regarding the life of the media. Most tape manufacturers quantify this life in terms of the number of passes that a tape can stand: a backup, a restore, and an mt fsf (file skip forward) each represent one

See page 310 for more information about restore.

2. GNU versions of restore include the -C option to verify a dump tape against a directory tree.