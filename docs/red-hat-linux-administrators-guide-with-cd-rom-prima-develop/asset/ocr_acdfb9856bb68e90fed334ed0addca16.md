# FIXING MISTAKES

Another flag option that you should consider when using the tar command is the -p or --preserve ownerships feature attempts to retain all file attributes. The -p option will doubly ensure that all the files tarred will keep the same permissions and ownerships that they had originally.

If you forget to place the correct extension at the end of the tarred file, you can always rename the newly created file later and give it the correct extension. To verify that you did in fact create a tar file, use the file command against the file in question. The file command prints out the type of file that you will examine. If, at the command line, I entered file docs.tar, the output would be as follows:

```
docs.tar: GNU tar archive
```

The file command is extremely useful for verifying other people's files and making sure they are, in fact, tar and not executable files. It also checks files whose identity is not certain. Some people simply forget to place the .tar extension at the end, or call it a .gz file when in fact it is both a tarred and gzipped file. Whenever an error occurs when you execute the tar command, use the file command to determine the file's correct file type.

The preceding was a rather simplistic example of tarring up directories. You can do the same with files just as readily. The same commands apply, only at the end of the command you type the names of all the files to be tarred. Remember that when you restore these files they will be placed within the directory in which they are untarred, exactly as they were saved. It is good etiquette among users to tar multiple files within a directory; then, when the files are untarred, they will be stored in a new directory rather than strewn about in a user's home directory or temporary location.

The tar command is also extremely important when you are backing up files onto tape drives or other backup devices. The tar command is often used with tape drives. In my own experience with tape backups and Linux, I have used tar heavily as an archival method. The syntax is simple and backing files up remotely onto a backup device on another machine involves the same methodology as does using tar to back up files to local backup directories. Because I did not have a tape backup on my Linux box but instead used a tape backup that sat on another Linux box, I was able to move many of my files offsite and thus make the data more secure. Here is an example of the syntax I used when tarring up files from my Linux machine onto another Red Hat machine that had a tape backup device. In this example, I call the remote machine nihilo.