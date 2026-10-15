
## Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

### Key Terms

**PostScript** This printout formatting language is designed to allow sophisticated page layout from various programs. Ghostscript is an open source implementation of the PostScript language and is included as part of the CUPS distribution.

**print job name** This is the unique name assigned to a print job by the `lpr` or `lp` command.

**print queue** All print jobs are placed in a queue, or list, for processing by a specific printer.

### Exercises

1. Use the `lpinfo -a` command or the `printers` command to find out what printers are available on your system. Which command is easier to use? How many printers are available?
2. Is your `PRINTER` variable already set to a printer? Is it the printer you would choose?
3. Use `man -k` to see what commands you have on your system that work with the printers and print queues. Use `man` to peruse them.
4. Show three ways to print the file `dickens.note` with `lpr`.
5. Add a print job to the queue and then remove it with `lprm`. What happened?
6. How would you use `pr` to add A Tale of Two Cities as a running title across each printout page of the file `dickens.note`? How would you start the printout on the second page of the file?

### Preview of the Next Hour

In the next hour, you’ll learn about the various ways you can archive backups and otherwise work with your file system as a whole. You’ll also learn about how Unixes now work with package management systems to make the process of installing software considerably less work.

## Hour 19. **Archives and Backups**

### Goals for This Hour

In this hour, you will learn

- About the `tar` tape archive utility
- About using zip to create PC-compatible ZIP archives
- How to use `compress` to shrink down large files, along with `gzip` and `bzip2`
- About `cpio` and `pax`
- About a common personal backup scheme
- How to work with package management systems

It’s your worst nightmare: You wake up, log in to your newly customized Unix account, and find that everything is gone. All your aliases, shell scripts, mail files, and HTML documents…missing. You email the administrator in a panic, and she responds, “Oh, yeah, sorry. Had to reformat the drive.”

Now, granted, it would be a pretty poorly run system in which the administrator thought it would be acceptable to reformat the drive without restoring all users’ data to the condition it was in immediately beforehand. But it does happen. Especially with hobbyist systems or university clusters, the policy will often be that they’ll try to restore your data after a reinstall, but they’ll make no guarantees. In any case, the techniques we’re about to go over will stand you in good stead if you’re ever running your own Unix system.

To avoid the sort of horrible situation just described, you need a solid archival and backup strategy for your own files, and that’s the focus of this lesson. In particular, we will explore the `tar` command as a simple tool for making single-file backup images of large amounts of information, and we will examine the `compress`, `gzip`, and `bzip2` commands to shrink the resultant archives as small as possible.

There are a number of ways to write your backup data to a tape unit, CD-RW, or network backup device. Most of them work with the `cpio` or `pax` commands, so they’ll be examined this hour, too. I’ve used Unix and Linux systems for 25-plus years, and `tar` remains the cornerstone of my own backup strategy.

With the rise of cloud storage, however, many people are backing up files and archives directly to a cloud drive like Dropbox, Google Drive, or even iCloud. Some are easy to access from the command line, others not so much. Since the cloud systems were designed for graphical user interfaces, they all require complicated programs to be installed and verified before you can use them from a command line, however, and that’s definitely beyond the scope of this book. If you’d like to learn more, do some Google searches for “google drive from linux command line” or similar. And be prepared for the complexity.

Finally, this hour wraps up with a brief discussion of modern Unix package management systems, notably Red Hat Linux’s RPM system. If you’re on a contemporary Unix system,
