
# THE REVISION CONTROL SYSTEM (rcs) 343

# Modification logs with rlog

The rlog program displays the modification history of a file. A series of selection criteria can be chosen, for example, modifying user (-w), versions (option -r), or periods of time (option -d). The precise format of the options and the corresponding parameters can be found in the man page for rlog.

# Managing archives with rcs

The rcs program is generally used for management of rcs archives. Archives can be newly created or locked. The owner of an archive can deactivate locks by other users or change the access rights to this archive. Furthermore, it is possible to use a symbolic name for a version. Because the rcs is central to the entire system, here is a complete description of all options.

- -i
  - With this option, an rcs archive is created and initialized, but no versions are stored. If no path is specified, the rcs command creates the archive in the ./rcs directory or if the rcs archive already exists, an error message is displayed.

- -ausname(s)
  - Appends the user(s) username(s) to the access list. Several user names must be separated by commas.

- -Aold file
  - Copies the access list contained in the rcs archive old_file into the new rcs archive.

- -eusname(s)
  - Removes the user(s) username(s) from the access list. Several user names must be separated by commas.

- -b[version]
  - This option changes the default branching to version version.

- -comment
  - Sets the comment character to comment. This text is displayed in front of each log message line generated with $Log$. This is useful for programming languages that do not support multi-line comments.

# 344 TOOLS (NOT ONLY) FOR PROGRAMMERS

- -kmarker
  This option can be used to change the substitution of the res marker. The precise meaning of the individual options is documented in the man page for co.

- -1[version]
  - Locks a version with the number version. If no version number is specified, the last version is locked.

- -u[version]
  - Removes the lock from version version. If no version is specified, the last lock of the user is used. Normally, only the user who has set the lock is allowed to remove it. If another user removes the lock, a mail message is sent to the creator of the lock. The user trying to remove the lock is prompted for a reason. This text and the specification of the version is sent to the creator of the lock.

- -L
  - Sets locking to ‘mandatory.’ This means that the user must set locks for reading and writing. This is sensible if several users are working on one project.

- -U
  - Sets locking to ‘not mandatory.’ This means that a user can read and write without setting a lock. This option should not be used if the files can be used by several users. Normally, locking is set to ‘mandatory’.

- -nname:version
  - This option assigns the symbolic name to the version version. If the name is already assigned to another version, an error message is displayed. Omitting the version number removes the symbolic name.

- -Nname:version
  - This option works exactly as the option -n. However, if a name is already assigned to the version version, this name is overwritten.

- -orange
  - A range of versions is removed from the archive. The parameter version1-version2 stands for the revisions version1 to version2 in the current branch. The parameter -revision means all versions from the beginning of the branch to this version. the parameter -revision deletes all versions from this version to the end of the branch.

# THE REVISION CONTROL SYSTEM (rcs) 345

- This option activates the 'quiet mode.' This suppresses the display of error messages.

- By specifying this option, the user is interactively prompted, even if the standard input is not a terminal.

```
-sstatus[:version]
```

- This option sets the status of the version to status. If no version is specified, the last version stored in the archive is used. ci automatically uses the status Exp.

```
-t[file]
```

- This option replaces the description of the work file in the rcs archive with the contents of file. If no name is specified, the text is read from the standard input (keyboard). The input is terminated with a dot (full stop).

```
-t-text
```

- Replaces the description with the text text.

# Merging of several branches

When working with several branches, modifications to one branch must often be carried out on a second branch. Thus, for example, an error correction in the production version should also be incorporated into the developers' version, unless point has not already been modified in some other way. This stressful and time-consuming task can be largely automated by means of the rcsmerge program. All options of rcsmerge can be found in the main page.

For a better understanding of the functioning of rcsmerge, we will look at an example. After we have delivered the program hello.c with version 2.2, we have opened a new development branch with version 3.3. Now, a programmer suggests some improvements to version 2.2, which you would like to incorporate into your current development version. To do this, you store the external modifications to version 2.2 in the file hello.c and start the rcsmerge command (Listing 11.20).

# 346 TOOLS (NOT ONLY) FOR PROGRAMMERS

```
(Linux):> rcmerge -p -r2.2 -r3.3 hello.c
```

**Listing 11.20** The rcsmerge.

Subsequently, you will find all modifications, at least those that could be carried out automatically, in the file.merged.c. However, since it is possible that changes were made to both branches, you should check this file.

```
(Linux):> ci -r2.2 -r3.3 hello.c
```

**Listing 11.21** The rcmerge.

# ident - identifying files

The ident searches the specified file or the standard input for markers. These markers are usually set by co, but they can also be inserted by hand. The option -q deactivates the display of warning that no markers could be found. ident works with both text and binary files.

```
(Linux):> ident hello
hello: hello.c,v1 1985/01/15 16:01:00 Exp
```

**Listing 11.22** Creation of rcmerge.

# 11.5.4 Additional information and programs

| Additional Information and Sources |
| --- | --- |
| Man pages | ci(1), co(1), rcs(1), rcsdiff(1), ident(1), rsclean(1), rcsintro(1), rcsmerger(1), rlog(1), rcsfile(5) |
| Books | Bolinger and Bronson (1995). Applying RCS and SCCS |
| ftp server | ftp.gnu.org |
| ftp path | /pub/gnu |
| File name | rcs-5.7.tar.gz |
| Size | 280 Kbytes |
| File name | cvs-1.5.tar.gz |
| Size | 1.1 Mbytes |

# 11.6 Other versionment systems

RCS processes each file individually. If you work on a project that consists of many files and you have made changes to more than one file, you must check each file individually. Furthermore, RCS expects that only those files for a lock set were modified.

# 11.6.1 The Concurrent Versions System

In projects it is often sensible to read or write the whole source tree with one command. This function is implemented (besides many other useful things) in CVS, the Concurrent Versions System. The authors have noticed that in most cases only one programmer works on a special function, so CVS without locks.

If the system notes that modifications cannot be fitted in automatically, the programmer is prompted to remedy this conflict manually. This offers the advantage that programmers very seldom get in each other's way.
