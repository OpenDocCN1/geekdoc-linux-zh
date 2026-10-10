
![](img/cae5c706c216875d12d4b7d28144cc71_150_0.png)

Figure 5.2 Linking files; Sancha's directory structure.

## Viewing File Contents

File contents can be viewed in several ways. In this section, we cover the most popular methods: using the cat command and using the more and less commands.

### Listing File Contents: cat Command

The cat (concatenate) command displays the contents of all specified files:

```
$ cat filename1 filename2 . . .<Enter>
```

If you want cat to number all the lines in a file, use the -n option as such:

```
$ cat filename -n<Enter>
```

The most obvious problem with cat is that when viewing files that are longer than a single screen, the file scrolls until the bottom of the file is reached. Thus, you can easily miss what was at the top of the file. You can mitigate this situation in a couple of ways. First, while the file is actually being displayed, you could press Ctrl-S to freeze the scrolling of the screen during output. To resume scrolling, you could then press Ctrl-Q. This action might not be appropriate, however, if the scrolling happens quickly.

The second and recommended method is to use the \| more ("pipe-more") and \| less ("pipe-less") commands in conjunction with cat, as such:

```
$ cat filename | more<Enter>
```

"Pipe-more" and "pipe-less" cause cat to display the first screenful of file contents and then stop and wait for the user to go forward only (with pipe-more) or backward *and* forward (with pipe-less) through the file contents at the user’s preferred pace. We will discuss the more and less commands in more detail in the next section.

In Chapter 10, “The vi Editor,” we will also discuss how cat can read from a device called standard in and display to a device called standard out. You can also use the cat command to create or even print a file by combining it with the redirect output symbol ( > ). In fact, we tell you how to use cat for printing at the end of this chapter, in the section cat Can Print, Too. Otherwise, please check the man pages and other sources for additional options.

#### Example 5.3 Listing File Contents with cat

As mentioned earlier, Don Quixote had asked Sancho to start a file called *manuals* that will eventually list materials that must be studied by those Reuel Figures, Inc. staff members who aspire to be knights. Now, the Don would like to have a look at the file. Here is what he enters:

```
$ cd<Enter>
$ pwd<Enter>
/home/quixote
$ cat manuals<Enter>
```

### Displaying a File Page by Page: The more and less Commands

In the previous section, we mentioned the problem of file contents on the terminal screen scrolling by so rapidly that you cannot comprehend the contents. We mentioned that you could use **Ctrl-S** and **Ctrl-Q** to stop and restart scrolling, but it is probably a better idea to use the **more** and **less** commands to display the contents of a file one screen at a time. Both commands pause after the first screenful of information is displayed and await instruction.

To invoke **more**, the syntax could not be simpler:

```
$ more filename<Enter>
```

When you use the **more** command, the `--more--` status message appears at the bottom of each screenful of file contents (with the exception of the last screenful of information, when the word **END** appears in parentheses). When **more** is reading from a file, a percentage appears alongside the **more** text indicating the proportion of the file already displayed.

To maneuver through the file contents, you use special keypresses that are listed in Table 5.1.

| Table 5.1 Moving through a File Displayed with the more Command | KEYPRESS | EXPLANATION |
| :--- | :--- | :--- |
|  | <Spacebar> | Moves down through the file one screen at a time |
|  | <Enter> | Moves down through the file one line at a time |
|  | <Ctrl>-c or <Ctrl>-z | Ends more and returns to the command line |

The **less** command is a more recent (and still not really as well known) improvement over **more**, and the syntax is very similar:

```
$ less filename<Enter>
```

You get more mobility when you examine files with the **less** command, as shown with the additional keypresses listed in Table 5.2.

| Table 5.2 Moving through a File Displayed with the less Command | KEYPRESS | EXPLANATION |
| :--- | :--- | :--- |
|  | <Spacebar> | Moves down through the file one screen at a time |
|  | <Enter> | Moves down through the file one line at a time |
|  | d or u | Moves down or up through the file half a screen at a time |
|  | down or up arrow | Moves down or up through the file one line at a time |
|  | <Ctrl>-c or <Ctrl>-z | Ends less and returns to the command line |

When you use the **less** command, only a colon (: ) appears at the bottom of each screenful of output, again with the exception of the last screenful.

The **more** and **less** commands have several more handy options in their man pages. (In fact, the man pages themselves use the **less** command to display their contents.)

#### Example 5.4 Listing File Contents Screen by Screen with `cat | less`

Because of the support requests he has recently received, Freston cannot help but notice that RFI staff members have been adding to and changing their individual portions of the corporate directory structure. To monitor the dimensions of the home directory portion of the RFI directory structure, Freston lists, recursively, the home directory structure. He redirects the information to a file called rfi_home_trees_jul_21 in his home directory (later, in Chapter 10, “The vi Editor,” we will discuss the commands that he might have used to do that). Then, he lists the contents of that file to his terminal screen with the following command:

```
# cat rfi_home_trees_jul_21 | less<Enter>
```

## Copying, Moving, and Deleting Files

Users and system administrators alike consider printing to be the most important file manipulation function. That is certainly true from the standpoint of accomplishments in the workplace, but more goes into those accomplishments than simply printing. For example, you might print a draft document for review, finalize it, and then print the document again. But you probably performed a lot of file manipulation before that draft review or crowning moment. And you probably did more file manipulation afterward; perhaps you copied the document or moved the file in the directory for housecleaning, security, sharing, or collaboration.

### Copying a Single File: The cp Command

At first glance, the cp (copy) command appears to be fairly straightforward:

```
$ cp source target<Enter>
```

![](img/cae5c706c216875d12d4b7d28144cc71_154_0.png)

You follow the command with the source filename (if the file is not in the current working directory, you must specify either the relative or full path name) and the target (also called the destination). See Example 5.5.

The `cp` command has many options. We recommend that you check the `man` pages. You might want to look at other sources of information as well. For example, you could check out the `help` utility by typing the following:

```
$ cp -h | more<Enter>
```

What effect does `cp` have on inode information? All information on the source file remains unchanged except that the last access time and date are updated. New inode numbers, permissions, and other relevant entries are created for the new files.

#### Example 5.5 Copying Single Files with cp

One part of Freston’s responsibilities is to report on system activity to Lady Dulcinea. One aspect of this reporting includes creating a copy of his latest rfi_home_trees_mmmdd file and sending it to Lady Dulcinea's /home/dulcinea/repts directory. Here is how he does that:

```
$ pwd<Enter>
/root
cp rfi_home_trees_jul21 /home/dulcinea/repts/<Enter>
```

Example 5.5 might be a little misleading for new users. You can change the name of the source file in flight, as seen in the example, only if the target directory is also the current working directory. Otherwise, you must execute a separate renaming process (if such is desirable) after the copy of the file has arrived. Renaming files is discussed later in this chapter.

### Copying Multiple or Special Files: The cp Command

When copying multiple files, the target must be a directory:

```
$ cp -i file1 file2 . . . target_dir<Enter>
```

> **WARNING** We used the -i option with the cp command just in case the cp target is the name of a file that already exists. Otherwise, without the -i, if the target file does already exist it would be overwritten without any error or notification message appearing. To prevent that from happening and to ensure that the system prompts the user, the -i option should be included.

Note that the copies will have the same name as the originals.

#### Example 5.6 Copying Multiple Files with cp

Don Quixote's existing structure is shown in Figure 5.4. He decides that copies of his manuals and test1 files also belong within the noble subdirectory. Here is how he copies them:

```
$ cd<Enter>
$ pwd<Enter>
/home/quixote
cp manuals test1 /noble<Enter>
$ cd noble<Enter>
$ ls
manual windmills test
```

As indicated in Example 5.6, this situation was also an opportunity to use relative path names.
