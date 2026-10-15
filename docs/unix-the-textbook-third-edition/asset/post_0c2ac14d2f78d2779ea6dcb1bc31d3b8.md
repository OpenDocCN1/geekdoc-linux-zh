
# EXERCISE 6.4

Give commands for displaying the first and last seven lines of the student_records file.

## 6.3 COPYING, MOVING, AND REMOVING FILES

In this section, we describe commands for performing copy, as well as move/rename and remove/delete operations on files in a file structure. The commands discussed are cp, mv, and rm.

### 6.3.1 Copying Files

The UNIX command for copying files is cp. The following is a brief description of the command.

```
SYNTAX
cp [options] file1 file2

Purpose: Copy file1 to file2. If file2 is a directory, make a copy of file1 in this directory.
Commonly used options/features:
-f Force copying if there is no write permission on file2
-i If file2 exists, prompt before overwriting
-p Preserve file attributes such as owner ID, group ID, permissions, and modification times
-r Recursively copy files and subdirectories
```

You must have permission to read the source file (file1) and permission to execute (search) the directories that contain file1 and file2. In addition, you must have the write permission for the directory that contains file2 if it does not already exist. If file2 exists, you don't need the write permission to the directory that contains it, but you must have the write permission to file2. If the destination file (file2) exists, by default, it will be overwritten without informing you if you have permission to write to the file. To be prompted before an existing file is overwritten, you need to use the -i option. If you do not have permission to write to the destination file, you will be informed of this. If you do not have permission to read the source file, an error message will appear on your screen.

The following cp command line makes a copy of temp in temp.bak. The ls commands show the state of the current directory before and after execution of the cp command. Figure 6.1 shows the same information in pictorial form.

```
$ ls
memo  sample      temp
$ cp temp temp.bak
$ ls
memo  sample      temp  temp.bak
$
```

![](img/02e070097d401d3bf7de4bf1c470b267_258_0.png)

# FIGURE 6.1 State of the current directory before and after the temp file has been copied to temp.bak.

The command returns an error message if temp does not exist or if it exists but you do not have permission to read its content. The command also returns an error message if temp.bak exists and you do not have permission to write to it. The following session illustrates these points. The first error message is reported because the letter file does not exist in the current directory. The second error message is reported because you do not have permission to read the sample file. The last command reports an error message because temp.bak exists and you do not have write permission for it. You can override the absence of write permission and force copying by using the -f option, as shown in the next command. The ls -l memo temp.bak command is used to show that copying has actually taken place; that is, the data has been copied, but the time stamp for the file is the current time. If you want to copy both the data and attributes of the source file, you need to use the cp command with -f and -p options, as in the last cp command that follows. The last ls -l memo temp.bak command is used to show that both data and file attributes such as the time stamp have been copied.

```
% ls -l
total 3
-rw-r----- 1 sarwar faculty 371 Aug 28 07:01 memo
--wxx----- 1 sarwar faculty 164 Jul 25 12:35 sample
-r-xr----- 1 sarwar faculty 792 Aug 28 07:01 temp
-r-xr----- 1 sarwar faculty 792 Aug 28 07:05 temp.bak
% cp letter letter.bak
cp: letter: No such file or directory
% cp sample sample.new
cp: sample: Permission denied
% cp memo temp.bak
cp: temp.bak: Permission denied
% cp -f memo temp.bak
% ls -l memo temp.bak
-rw-r----- 1 sarwar faculty 0 Aug 28 07:01 memo
--wxx----- 1 sarwar faculty 0 Aug 28 07:22 temp.bak
% cp -fp memo temp.bak
% ls -l memo temp.bak
```

```
-rwxr---- 1 sarwar faculty 0 Aug 28 07:01 memo
-rwxr---- 1 sarwar faculty 0 Aug 28 07:01 temp.bak
%
```

The following command makes a copy of the .profile file in your home directory and puts it in the .profile.old file in the sys.backups subdirectory, also in your home directory. This command works regardless of the directory you are in when you run the command because the pathname starts with your home directory. You should execute this command before changing your runtime environment specified in the ~/.profile file, so that you have a backup copy of the previous working environment in case something goes wrong when you set up the new environment. The command produces an error message if ~/.profile does not exist, if you do not have permission to read it, if the ~/sys.backups directory does not exist or you do not have the execute (search) and write permissions for it, or if .profile.bak exists but you do not have permission to read it.

```
% cp ~/.profile ~/sys.backups/.profile.bak
%
```

The following command copies all the files in the current directory, starting with the string lab to the directory ~/courses/ee446/backups. The command also prompts you for overwriting if any of the source files already exist in the backups directory. In this case (in which multiple files are being copied), if backups is not a directory, or if it does not exist, an error message is displayed on the screen informing you that the target must be a directory.

```
% cp -i lab* ~/courses/ee446/backups
%
```

If you want to copy a complete directory to another directory, you need to use the cp command with the -r option. This option recursively copies files and subdirectories from the source directory to the destination directory. It is a useful option that you can use to create backups of important directories periodically. Thus, the following command recursively copies the ~/courses directory to the ~/backups directory.

```
$ cp -r ~/courses ~/backups
$
```

This command creates copies the ~/courses directory, including all the files and directory hierarchies under the ~/courses directory, and places it under the ~/backups directory. Figure 6.2 shows the state of your home directory (~) before and after the execution of the command.

### 6.3.2 Moving Files

Files can be moved from one directory in a file structure to another. This operation in UNIX can also result in simply renaming a file if it is on the same file system. The renaming
