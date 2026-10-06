# The Right to Assemble

as a marker to show you very clearly where the end of the file was. Some of these text editors are still kicking around, and it's possible that you have one. (To see if you do, type in a simple sentence like "Where will it all end?" and save to disk. Go in debug and see if there is a 1AH byte immediately after the end of the sentence.) The 1AH marker is a holdover from even more ancient times, from the CP/M operating system, which was simpler than DOS and remembered only the num-ber of disk storage blocks the file occupied. The precise byte where the file's data ended within the final block was unknown to CP/M, so the text editors of the time used a 1AH byte to mark the tail end of the file.

There's a file on your CD-ROM, the OLDSAM.TXT, which was created with such a text editor and the 1AH marker. (Note the time stamp on OLDSAM.TXT!) OLDSAM is otherwise identical to SAM.TXT. Note that when you do a DIR command on the directory containing the two files, OLDSAM.TXT is 20 bytes long—the 1AH marker byte is considered part of the file and counted with all the rest of the data.

Most of the time, memory garbage is not entirely random, but may be part of the code or data left over from the last program to be loaded and executed in that area of memory. You can safely ignore memory garbage, but should know what it is and why it appears in your hex dumps.

You might occasionally see recognizable data strings from other pro- in memory garbage and wonder how they got into your current program. Note well: They didn't get into your current program. They were just there, and now show through beyond the end of the file you loaded under DEBUG. Knowing where legitimate information ends and where garbage begins is important and not generally clear-cut as it is here.

# Changing Memory with DEBUG

DEBUG can easily change bytes in memory, whether they are part of a file loaded from disk or not. The DEBUG command to change bytes is the E command. (Think, Enter new data.) You can use the E command to change some of the data in SAM.TXT. Part of this process is shown toward the bottom of Figure 4.6.

Notice the command line:

```
-e 010e
```