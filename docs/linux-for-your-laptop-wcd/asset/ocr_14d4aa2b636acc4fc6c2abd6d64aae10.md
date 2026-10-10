| /dev/hdds | /d3 | ext2 | noauto,defaults | 1 2 |
| /dev/hdd6 | /d4 | ext2 | noauto,user | 1 2 |
| /dev/hdd7 | /d5 | ext2 | noauto,defaults | 1 2 |
| /dev/hdds | /home | ext2 | defaults | 1 2 |
| /dev/hdds | /music | ext2 | noauto,user | 1 2 |
| /dev/hdd5 | /opt | ext2 | noauto,defaults | 1 2 |
| /dev/hda9 | /tmp | ext2 | defaults | 1 2 |
| /dev/hda6 | /usr | ext2 | defaults | 1 2 |
| /dev/hda7 | /var | ext2 | defaults | 1 2 |
| /dev/hda10 | swap | swap | defaults | 0 0 |

At the very least, you should attempt to recover and back up the /home directory, followed by the /etc directory. Much of the remaining filesystem can be restored without losing any important data. This is another good reason to use different partitions for your filesystem!

# Undeleting Linux Files

Sorry. It can't be done. After you delete a file under Linux, it's gone. Actually, the file's inodes are deleted and reallocated. The file, for all intents and purposes, is gone. However, you did back up your files, right? If you didn't, and you delete an important text file, you might be able to recover a portion of the file by searching the entire contents of the partition on which the file resided, saving the search results, and then searching for known strings in the output file. This will not work for binary files, such as images or compiled programs.

This tip, by Michael Hamilton in the Linux Tips-HOWTO, relies on several factors:

+   - You can remember the approximate number of lines in the text file, and you know the Linux partition on which the file was created and then deleted.
+   - You can recall a text string close to the beginning of the file.
+   - You can recall a text string close to the end of the file.
+   - You have enough room on an available hard drive to save the search results.

For example, if you delete a file with the known string Introduction, followed by the text string Conclusion, and you know roughly how many lines (say 200) were in the file (which resided on /dev/hda5), you can use the egrep command to construct a recovery command line like this:

```
$ egrep -200 'Introduction.\*Conclusion' /dev/hda5 >/tmp/hope
```