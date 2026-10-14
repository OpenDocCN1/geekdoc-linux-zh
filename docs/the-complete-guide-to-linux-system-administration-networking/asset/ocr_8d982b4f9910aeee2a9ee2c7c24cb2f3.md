# CASE PROJECTS

![](bbox=[0.02, 0.22, 0.09, 0.32])

# File Compression, Permissions and Archiving

Your most recent McKinney & Co. consulting project involves archiving large quantities of data in compressed form and granting certain users access to the archived data. You need to do some research to answer questions that have come up.

+   1. Review the list of compression tools available in Linux (see Table 4-4. All of these are included in Red Hat Linux and Fedora. Test each of these utilities by compressing a set of text files, program files, and image files. (You can use the find command to locate some of each on your system.) Determine the average compression ratio for each (what percentage of the original size the compressed file occupies). Also note the speed of compression by entering the date command immediately before and after each test. (You may need to work with large files to make the timing data reasonably easy to gather.)

+   2. Experiment with the touch and umask commands to determine what you think are the optimal default file permissions to be granted on newly created archive files in different circumstances. Create a grid outlining different settings and the default permissions to be used, with the umask command to implement each one.

+   3. Research the find man page to create a single find command that lists all files within the /usr/bin directory that have file permissions set to 755 and have more than three hard links to them. The find command should print out to STDOUT (the screen) the last access time, size in 1K blocks, and the file name of each matching file, with each of these three items being separated by a tab. Keep in mind the information in Chapter 3, "Using the Shell," about preventing command-line expansion so that the parameters you enter are passed intact to the find command rather than being expanded by the shell.