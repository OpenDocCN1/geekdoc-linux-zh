
because the soft link still points to the file with pathname /tmp/Chapter3. This result is quite logical but is still a drawback; in hard links, the cat command would not fail so long as the moved file stays within the same file system.

Some other drawbacks of the symbolic links are that UNIX has to support an additional file type (the link type) and a new file has to be created for every link. Creation of the link file results in space overhead for an extra inode, disk space needed to store the pathname of the file to which it is a link, and other kernel data structures. Symbolic links also result in slower file operations because, for every reference to the file, the link file has to be opened and read in order for you to reach the actual file. The actual file is then processed for reading or writing, requiring an extra disk access to be performed if a file is referenced via a symbolic link to the file.

In the following in-chapter exercises, you will use the ln -s and ls -il commands to create and identify soft links, and to verify that you can create soft links across file systems.

## EXERCISE 8.3

Establish a soft link to the file Ch8Ex1 that you created in Exercise 8.1. Call the soft link Ch8Ex1.soft. Verify that the link has been established. What commands did you use to establish the link and verify its creation?

## EXERCISE 8.4

Execute the ln -s /tmp ~/tmp command on your UNIX system. What is the purpose of the command? What happens when you execute the command? Does the result make sense? Why or why not?

## SUMMARY

Any of several techniques can be used to allow a team of users to share UNIX files and directories. Some of the most commonly used methods of file sharing are duplicating the files to be shared and distributing them among team members, establishing a common account for team members, setting appropriate permissions on the files to be shared, setting up a UNIX user group for the team members, and establishing links to the shared files in the directories of all team members. File sharing via hard and soft links is the main topic of this chapter. However, the issue of simultaneous access of shared files by team members is not discussed here (see Chapter 17).

Hard links allow you to refer to an existing file by another name. Although hard links are the primary mechanism used by UNIX to glue the file system structure, they have several shortcomings. First, an existing file and its links must be in the same file system. Second, only a superuser can create hard links to directories. Third, moving a file to another file system breaks all links to it.

Soft links can be used to overcome the problems associated with hard links. When a soft link to a file is created, a new file is created that contains the pathname of the file to which it is a link. The type of this file is link. Soft links are expensive in terms of the time needed to
access the file and the space overhead of the link file. The time overhead during file access occurs because the link file has to be opened in order for the pathname of the actual file to be read (or written to, whatever the case may be), and only then does the actual process of file opening and reading (or writing) take place. The link file that contains the pathname of the original file causes the space overhead.

Hard and soft links are established with the ln command. For creating soft links, the -s option is used with the command. The ls -i -l command is used to identify (or confirm establishment of) links. The first field of the output of this command identifies the inode numbers for the files in a directory, and all hard links to a file have the same inode number as the original file. The first letter of the second field represents file type (l for soft link) and the remaining letters specify file permissions. The third field identifies the number of hard links to a file. Every simple file has one hard link at the time it is created. The last field identifies file names; a soft link's name is followed by -> filename, where filename is the name of the original file. The -f option can be used to force the creation of a link—that is, to overwrite an existing file with the newly created link.

## QUESTIONS AND PROBLEMS

- 1. What are the five methods that can be used to allow a team of users to share files in UNIX?
- 2. What is a link in UNIX? Name the types of link that UNIX supports. How do they differ from each other?
- 3. What are the problems with hard links?
- 4. Remove the file Ch8Ex1 that you created in Exercise 8.1. Display the contents of Ch8Ex1.hard and Ch8Ex1.soft. What happens? What command did you use for displaying the files? Does the result make sense? Why or why not?
- 5. Search the /usr/bin directory on your system and identify three links in it. Write down the names of these links. Are these hard or soft links? How do you know?
- 6. While in your home directory, can you establish a hard and soft link to /etc/passwd on your system? Why? What commands did you use? Are you satisfied with the results of the command execution?
- 7. Every UNIX directory has at least two hard links. Why?
- 8. Can you find the number of hard and soft links to a file? If so, what command(s) do you need to use?
- 9. Suppose that a file called shared in your present directory has five hard links to it. Give a sequence of commands to display the absolute pathnames of all of these links. (Hint: Use the find command.)
