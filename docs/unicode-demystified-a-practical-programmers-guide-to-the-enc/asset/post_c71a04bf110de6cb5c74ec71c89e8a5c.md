
## Minimize Use of Setuid and Setgid Programs Owned by root

Executable files that are setuid and owned by root have Supervisor privileges which are run even if they are not run by root. This type of program is very powerful because it can do anything the user can do (that the program is designed to do). Similarly, executable files that are setgid and belong to the group root have extensive privileges.

Because of the power they hold and the potential destruction they can do, avoid creating and using setuid and setgid programs owned or belonging to the group root indiscriminately. Because of the inherent dangers, many sites do not allow these programs on their machines at. See page 898 for information on setuid and Superuser.

## Setuid and Setgid Permissions

When you execute a file that has setuid (set user ID) permission, the process executing the file takes the privileges of the owner of the file. For example, if you run a setgid program that removes all the files in a directory, you can remove files in any of the file owner's directories if you do not normally have permission to do so. In a similar manner setgid (set group ID) permission means that the process executing the file takes the privileges of the group the file is associated with. The utility shows setuid permission as an s in the owner's executable position and setgid as an s in the group's executable position:

```
$ ls -l program
-rwxrxr-xr-x 1 alex pubs 15828 Nov 5 06:28 program
$ chmod u+s program
$ ls -l program
-rwsr-xr-x 1 alex pubs 15828 Nov 5 06:28 program
$ chmod g+s program
$ ls -l program
-rwsr-sr-x 1 alex pubs 15828 Nov 5 06:28 program
```

## Do Not Write Setuid Shell Scripts

Never write shell scripts that are setuid. Several techniques for subverting them are well known.

## Directory Access Permissions

Access permissions have slightly different meanings when used with directories. Although the three types of users can read from or write to a directory, the directory cannot be executed. Execute access permission is redefined for a directory: It means that you can cd into the directory and/or examine files that you have permission to read from the directory. It has nothing to do with executing a file.

When you have only execute permission for a directory, you can use ls to list a file in the directory if you know its name. You cannot use ls without an argument to list the contents of the directory. In the following Jenny verifies that she is logged on as herself. Then she checks the permissions on Alex's info directory and cds into it. (You can view the access permissions associated with a directory by running with the -d [directory] and -l [long] options. The d at the left end of the line that ls indicates that /home/alex/info is a directory.) Because Jenny does not read permission for the directory, the -l command without any arguments returns error. The period (.) in the error message represents the working directory:

```
$ who am i
jenny pts/7 Aug 21 10:02
$ ls -ld /home/alex/info
drw--x 2 alex pubs 512 Aug 21 09:31 /home/alex/info
$ cd /home/alex/info
$ ls -l
:: Permission denied
total 2
```

When Jenny specifies the names of the files she wants information about, she is not reading new directory information, just searching for specific information, which she is allowed to do with execute access to the directory. She cannot display financial, because she does not have read access to it. She does have access to notes, so she has no problem using cat to display the file.

```
$ ls -l memo.1 memo.2 financial notes summary
-rw------ 1 alex pubs 34 Aug 21 09:31 financial
-rw-r--r-- 1 alex pubs 21 Aug 21 09:31 memo.1
-rw-r--r-- 1 alex pubs 21 Aug 21 09:32 memo.2
-rw-r--r-- 1 alex pubs 30 Aug 21 09:32 notes
-rw-r--r-- 1 alex pubs 32 Aug 21 09:32 summary
$ cat financial
cat: cannot open financial
$ cat notes
This is the file named notes.
```

Next, Alex uses the following command to give everyone access to his info directory:

```
$ chmod o+r /home/alex/info
```

Now when Jenny checks permissions on info, she finds that she has both read and execute access to the directory. Now ls -l works just without arguments, but she still cannot read financial. (This is an issue of file permissions, directory permissions.) Finally, she tries to create a file named newfile by redirecting output from cat (page 145). If Alex were to give her permission to the info directory, she would be able to create new files in it:

```
$ ls -ld /home/alex/info
drw--r-x 2 alex pubs 512 Aug 21 09:31 /home/alex/info
$ ls -l
total 10
-rw------ 1 alex pubs 34 Aug 21 09:31 financial
-rw-r--r-- 1 alex pubs 21 Aug 21 09:31 memo.1
-rw-r--r-- 1 alex pubs 21 Aug 21 09:32 memo.2
-rw-r--r-- 1 alex pubs 30 Aug 21 09:32 notes
-rw-r--r-- 1 alex pubs 32 Aug 21 09:32 summary
$ cat financial
cat: cannot open financial
$ cat > newfile
bash: Permission denied
```

## Links

A link is a pointer to a file. Every time you create a link using a filename, you are associating a filename with the information located. Sharing files can be useful when two or more people are working on a project and need to share some information. To share a file with another user, first give the user read and write to the file (In addition, you may have to change the access permission of the parent directory of the file). Once the permissions are appropriately set, the user can access it from your directory. A link can also be useful to a single user with a large directory. You can create links to cross-classify files, using different classifications for tasks. For example, if your directory is the one depicted in Figure 4-2, you might have a file named to_do in each of the subdirectories—that is, in personal, memos, and business. If you find it difficult to keep track of everything you need to do, you can create a separate directory, named to_do in the corresponding directory, and link each to-do-list into that. You could link the file named to_do in the memos directory to a file named memos. This set of links is shown in Figure 4-13.

Figure 4-13 Using links to cross-classify files![](img/aa8214d49e1cf50152c432845129fb3b_173_0.png)

There are two kinds of links: hard links and symbolic, or soft, links. Hard links, discussed first, are older and becoming dated. The section on hard links is marked optional; you can skip it, although it discusses nodes and gives you insight into how the filesystem is structured.

### About the Discussion of Hard Links

Optional

## Hard Links

The ln utility (without the -s or --symbolic option) creates an additional hard link to an existing file. The new link appears as another file in the file structure. If the file appears in the same directory as the one it is linked with, the links must have different filenames. This restriction does not apply if the linked file is in another directory. The syntax for ln is

ln existing-file new-link

The following command makes the link shown in Figure 4-14 by creating a new link named /home/alex/letter to an existing file named draft in Jenny's home directory:

```
$ pwd
/home/jenny
$ ln draft /home/alex/letter
```
