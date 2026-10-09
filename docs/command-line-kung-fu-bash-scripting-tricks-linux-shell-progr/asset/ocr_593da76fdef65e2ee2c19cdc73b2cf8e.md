```
$ mv jazz{.,.mp3}
$ ls jazzz*
jazz.mp3
$
```

# ## Create Backups of Files by Date with Ease

```
$ alias d='date +%F'
```

By using the date format of YYYY-MM-DD for file or directory names, you make ls output more human friendly. You can quickly tell the date order of the files when using this format.

```
$ ls -l file*
file.2013-04-08
file.2013-12-21
file.2014-04-08
$ ls -l other-file.*
other-file.04-08-2013
other-file.04-08-2014
other-file.12-21-2013
```

Before making a change to a file I like to make a backup copy of it. I also like to know when I made the backup. By creating an alias of "d" which is short for the date in YYYY-MM-DD format, I can quickly create these types of backups.

```
$ echo "alias d='date +%F'" >> ~/.bash_profile
$ ./.bash_profile
$ d
```