
In Listing 3.43, the `/usr/bin` directory is being audited for the potentially dangerous SUID permission by using the find utility and its -perm option. The expression used is /4000, which will ask the find utility to search for SUID settings (octal code 4) and, due to the forward slash (/) in front of the number, ignore the other file permissions (octal codes 000). The resulting file-names all legitimately use SUID, and thus, nothing suspicious is going on here.

> **TIP**
> On older Linux systems, to enact a search as shown in Listing 3.41, you would enter +4000 to designate the permission. The plus sign (+) is now deprecated for this use and has been replaced by the forward slash (/) symbol for the find command.

Earlier in this chapter we briefly covered the grep command for the purpose of reading a portion of a text file. You can also use this clever utility to search for files on your system.

Suppose it has been a while since you last modified your `/etc/nsswitch.conf` configuration file. A problem arises that requires you to make a change to the hosts: setting within the file and you can’t remember its exact name. Instead of digging around using the ls command, just employ the grep command as shown in Listing 3.44 and quickly find the file’s name.

# Listing 3.44: Using the grep command to find a file

```
$ sudo grep -d skip hosts: /etc/*
/etc/nsswitch.conf:hosts:    files [...]
$
```

In Listing 3.44, the grep command is used to search all the files within the `/etc/` directory for the hosts: setting. The -d skip option is used to skip any directory files in order to eliminate messages concerning them. The grep utility displays the configuration filename, followed by a colon (: ) and the file’s line where the setting is located. If you are not sure where in the /etc/ directory tree the configuration file is placed, you can tack on the -R (or -r, or -recursive) option to recursively search through the specified directory tree. If you don’t have permission to search through various files, the grep command will issue annoying error messages. You’ll learn in the next chapter how to redirect those error messages.

Quickly finding files as well as various types of information on your Linux server can help you be a more effective and efficient system administrator. It is a worthwhile investment to try any of this section’s commands or their options that are new to you.

# Summary

Being able to effectively and swiftly use the right commands at the shell command line is important for your daily job. It allows you to solve problems, manage files, gather information, peruse text files, and so on.

This chapter’s purpose was to improve your Linux command-line tool belt. Not only will this help you in your day-to-day work life, but it will also help you successfully pass the CompTIA Linux+ certification exam.

# Exam Essentials

**Explain basic commands for handling files and directories.** Typical basic file and directory management activities include viewing and creating files, copying and moving files, and deleting files. For viewing and creating files and directories, use the `ls`, `touch`, and `mkdir` commands. When needing to duplicate, rename, or move files, employ one of the `mv`, `cp`, or `rsync` commands. For local large file copies, the `rsync` utility is typically the fastest. You can quickly delete an empty directory using the `rmdir` utility, but for directories full of files, you will need to use the `rm -r` command. Also, if you need to ensure that you are removing the correct files, be sure to use the `-i` option on the `rm` utility.

**Describe both structures and commands involved in linking files.** Linking files is easy to do with the `ln` command. However, it is important for you to describe the underlying link structure. Hard-linked files share the same inode number, whereas soft-linked files do not. Soft or symbolic links can be broken if the file they link to is removed. It is also useful to understand the `readlink` utility to help you explore files that have multiple links.

**Summarize the various utilities that can be employed to read text files.** To read entire text files, you can use the `cat`, `bat`, and `pr` utilities. Each utility has its own special features. If you need to read only the first or last lines of a text file, employ either the `head` or `tail` command. For a single text line out of a file, the `grep` utility is useful. For reviewing a file a page at a time, you can use either the `less` or the `more` pager utility.

**Describe how to find information on your Linux system.** To determine two text files' differences, the `diff` utility is helpful. With this utility, you can also employ redaction and modify the files to make them identical. When you need to quickly find files on your system and want to use simple tools, the `which`, `whereis`, and `locate` commands will serve you well. Keep in mind that the `locate` utility uses a database that is typically updated only one time per day, so you may need to manually update it via the `updatedb` command. When simple file location tools are not enough, there are more complex searching utilities, such as `find` and `grep`. The `grep` command can employ regular expressions to assist in your search.

# Review Questions

1. You are looking at a directory that you have not viewed in a long time and need to determine which files are actually directories. Which command is the best one to use?
   - A. `mkdir -v`
   - B. `ls`
   - C. `ls -F`
   - D. `ls -i`
   - E. `ll`

2. You are using the `ls` command to look at a directory file's metadata but keep seeing metadata for the files within it instead. What command option will rectify this situation?
   - A. `-a`
   - B. `-d`
   - C. `-F`
   - D. `-l`
   - E. `-R`

3. You have just created an empty directory called MyDir. Which command did you most likely use?
   - A. `mkdir -v MyDir`
   - B. `touch MyDir`
   - C. `cp -R TheDir MyDir`
   - D. `mv -r TheDir MyDir`
   - E. `rmdir MyDir`

4. You have a file that is over 10 GB in size, and it needs to be backed up to a locally attached drive. What is the best utility to use in this situation?
   - A. `readlink -f`
   - B. `mv`
   - C. `cp`
   - D. `scp`
   - E. `rsync`

5. A long-time server administrator has left the company, and now you are in charge of her system. Her old user account directory tree, /home/Zoe/, has been backed up. Which command is the best one to use to quickly remove her files and still indicate that you are removing the correct directory, but without forcing you to confirm every file deletion?
   - A. cp -R /home/Zoe/ /dev/null/
   - B. mv -R /home/zoe/ /dev/null/
   - C. rm -Rf /home/Zoe/
   - D. rm -ri /home/Zoe/
   - E. rm -rI /home/Zoe

6. There is a large directory structure that needs to be renamed. What mv command options should you consider employing? (Choose all that apply.)
   - A. -f
   - B. -i
   - C. -n
   - D. -r
   - E. -v

7. You are trying to decide whether to use a hard link or a symbolic link for a data file. The file is 5 GB, has mission-critical data, and is accessed via the command line by three other people. What should you do?
   - A. Create a hard link so that the file can reside on a different filesystem for data protection.
   - B. Create three hard links and provide the links to the three other people for data protection.
   - C. Create three symbolic links and protect the links from the three other people for data protection.
   - D. Create a symbolic link so that the file can reside on a different filesystem.
   - E. Create a symbolic link so that the links can share an inode number.

8. A short text-based control file is no longer working properly with the program that reads it. You suspect the file was accidentally corrupted by a control code update you performed recently, even though the file's control codes are all correct. Which command should you use next on the file in your problem investigation?
   - A. cat -v
   - B. cat -z
   - C. cat -n
   - D. cat -s
   - E. cat -E
