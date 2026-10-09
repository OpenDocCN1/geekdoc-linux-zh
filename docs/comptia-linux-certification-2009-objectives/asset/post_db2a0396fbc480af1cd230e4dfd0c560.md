
2. Fix multiple occurrences of the error.

- Type `*/Marker*` and press **Enter** to search for the next occurrence of the word “Marker”.
- Change the text “Marker” to “Maker.”

3. Change the casing of the first letter in “photoshop.”

- Press **J** to move to the next line.
- Press **H** to place the cursor below the first occurrence of the letter “h” in the word “Photoshop.”
- Press **C** followed by **B** to delete the first letter.
- In insert mode, type *P* to change the word to “Photoshop.”
- Press *Esc* to return to the command mode.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_169_0.png)

Students should press “C,” and then press “B” after releasing the “C” key. Both keys should not be pressed simultaneously.

4. Remove the duplicate entry of “Paintworks.”

- To navigate to the second occurrence of the word “Paintworks,” press the **Down Arrow** key two times.
- To delete the duplicated line, press **D** two times.
- Enter **`:wq`** to save and close the file.
- Clear the terminal screen.

## TOPIC B

### Locate Files

You created and edited files. As a user or administrator, you will have to frequently locate files within the Linux filesystem. In this topic, you will locate files within the Linux system.

Learning how to locate files within Linux will reduce the amount of time you spend searching for files. There are different techniques available for locating files within Linux. These will save you time and effort as you manage larger filesystems.

### The locate Command

The *locate command* performs a quick search for any specified string in file names and paths stored in the mlocate database. This database must be updated regularly for the search to be effective. The results displayed may be restricted to files users have permissions to access or execute.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_170_0.png)

```bash
[root@localhost ~]# locate Policy
/usr/include/xulrunner-sdk-1.9/content/nsIContentPolicyUtils.h
/usr/include/xulrunner-sdk-1.9/content/nsIContentPolicy.h
/usr/lib/xserver/SecurityPolicy
/usr/share/doc/deployment_Guide-en-US.5.2/images/Load_New_Policy.png
[root@localhost ~]# 
```

*Figure 4-10: Searching files using the locate command.*

#### Syntax

The syntax of the *locate* command is `locate [options] (string)`.

#### The locate Command Options

The *locate* command supports different options that enable you to make your search more effective. Some of the options are described in the table.

| Option | Description |
|:--------|:----------|
| -r | Uses regular expressions in searching for file names. |
| -c | Displays only the number of matching entries found, rather than the file names. |
| -e | Returns only files that exist at the time of search. |
| -i | Ignores the casing in file names or paths. |
| -n number of entries | Returns only the first few matches up to the specified number. |

#### Updating the mlocate Database

The updatedb command is used to update the /var/lib/mlocate/mlocate.db database. Though this is the default database searched by the locate command, there may be more databases containing file paths. If the database is not updated before performing a search, all files created after the last update will be excluded from the search.

#### The slocate Command

The slocate command, or secure locate command, searches a specific database that is built using the slocate -u command. The difference between the locate and slocate commands is that when a user types slocate file name, the slocate command searches the database and returns the location of the file only if the user has access permission to those files; whereas, the locate command returns the location of files whether or not the user has access permission to them.

### Using grep

In its simplest form, grep is a search tool. It allows you to perform search actions, such as finding any instance you are searching for, in a file. For example, entering `grep foo test` returns all the lines that have a string matching "foo" in the file "test." The grep command can also be used to search a directory for a certain file. The `ls -1 | grep audit` command returns a long listing of any files in the current directory whose name contains "audit."

![](img/477ccb2f05b6ba1b2d563ea74f18c197_171_0.png)

> The term grep is derived from "Globally matching a Regular Expression and Printing the lines."

![](img/477ccb2f05b6ba1b2d563ea74f18c197_171_1.png)

### The whereis Command

The whereis command is used to view various details associated with a command. It locates the binary, source, and manual page files for the command. The whereis command has various options. Some of the frequently used options are listed in the following table.

| Option | Used To |
| :--- | :--- |
| -b | Search only for binaries. |
| -m | Search only for manual sections. |
| -s | Search only for sources. |
| -u | Search for unusual entries. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_172_0.png)

*Figure 4-11: The path to the ls command.*

#### Syntax

The syntax of the *whereis* command is `whereis [-bmsu] [-BMS directory... -f] file name ...`.

#### An Example of Using the whereis Command

On entering `whereis ls`, the following output is displayed:

```
ls: /bin/ls /usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz
```

Where `/bin/ls` indicates the location of the `ls` command and `/usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz` indicates the location of the *man* pages for the `ls` command.

### The GNOME Search Tool

The *GNOME search tool* is a graphical utility used for searching files based on specific criteria. You can search for a file by its name, size, ownership, access time, or contents. This powerful GUI tool supports features such as case-insensitive search, search within a specific location, and wildcard searches. This tool uses a combination of search commands such as `locate`, `find`, and `grep`.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_172_1.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_173_0.png)

Figure 4-12: Searching files using the GNOME search tool.

### Kat

Kat is an application for KDE that is used to search for files with the help of meta information, full text, and thumbnails that are extracted and indexed from various types of files. It serves as a catalog and helps retrieve files quickly.

### Beagle

Beagle is a GNOME desktop search application, which can also be used in KDE by installing Kery. It is used to search for files, folders, documents, notes, images, videos, email messages, instant messaging content, web browser history, and RSS feeds. Beagle indexes files, which enables it to retrieve search results quickly. It also allows users to sort search results based on date modified, name, or relevance.

### The find Command

![](img/477ccb2f05b6ba1b2d563ea74f18c197_173_1.png)

The find command enables you to search a specific location for files and directories that adhere to some search criteria. It recursively searches the directory structure, including any subdirectories and their contents, beginning with the search location you enter. You can perform one or more actions on the files found.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_174_0.png)

#### Syntax

The syntax of the find command is `find [options] [search locations] [search criteria] [actions]`.

#### find vs. locate commands

The `locate` command searches a database and retrieves information on files present on your system. However, failure to keep this database updated may produce outdated results. The `find` command, on the other hand, performs a live search of the filesystem and may concentrate on a specific location. The `find` command may take more time to complete a search than the `locate` command.

#### Working of the find Command

You can use the `find` command to search the entire directory structure for a file even if you remember a portion of the file name. One or more search paths can be designated and directory notations can be used as the search path. If no directory is specified, the `find` command uses the current working directory as the location to start the search. One or more criteria can be used to specify the conditions of a file or directory. In case of more than one search criterion, the file or directory must meet all the conditions specified before the results are displayed. The results displayed may be restricted to files users have permissions to access or execute. You can check the manual pages of the `find` command for more options.

#### Options for Files Found

When the system finds a listing that meets your criteria, there are several actions that can be performed on the results. These options are outlined in the following table.

| **Option** | **Action Performed** |
| --- | --- |
| `-print` | Displays the location of the files found. |
