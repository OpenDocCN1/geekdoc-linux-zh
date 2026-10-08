```
(Linux):> updatedb --localpaths=/home/jochen \\
? --output=update.db
(Linux):> locate -d update.db:/var/lib/locateddb passwdtab
```

**Listing 10.7** Creation of a user's locate database.

The updatedb command should be entered into (for an example, see Listing 10.32), so that the database is periodically updated. Usually, the database is located in the /var/lib directory. The name of the database (locateddb), which is normally created by updatedb, can be overwritten by setting the variable LOCATION_DB. Thus, for example, a database can be created for each CD-ROM. With the -d parameter, you can also specify colon-separated database names to be searched by locate.

In the following example (Listing 10.8) a database that contains the contents of the CD is created under the name cd_linux2_1.codes in the directory ~/locate. Once the database has been created, the locate command with the option -d~/locate/cd_linux2_1.codes can be used to search this database.

```
(Linux):# export LOCATE_DB="/locate/cd_linux2_1.codes
(Linux):# export SEARCHPATHS='CD'
(Linux):# export PRUNEREGEX=' '
(Linux):# updatedb
(Linux):# locate -d cd_linux2_1.codes ftape
```

**Listing 10.8** Creation of a search database for a CD.

The disadvantage of this system is that the UNIX database must be updated as often as possible, otherwise more recent files cannot be found or deleted files are still shown. The search itself is also not as flexible as that of the find command. You cannot search for data, owner, or the like, but only for file names. Furthermore, a run of updatedb is relatively costly because a find is carried out across the entire hard disk.

In all, the use of locate is always worthwhile if you have many users on your system, and the computer enjoys enough 'quiet' periods during which the database can be updated. If you notice that on your system you frequently search for files by name, using locate is sensible on a private system; on my own system, updatedb is called every four hours.