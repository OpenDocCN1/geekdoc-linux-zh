# How do I remove all the files in a directory matching a particular name?

Some editors and programs create large numbers of temporary files. Often you need to clean up after these programs, to prevent your hard drive from filling up. The simplest method to remove a set of files that matches a particular name is to use the find and xargs commands as follows:

```
find dir -type f -name 'name' .print | xargs rm
```

Here dir is the pathname of a directory and name is the filename that you want to remove. For example, the following command removes all of the files that end with - from the directory /home/cvs:

```
find /home/cvs -type f -name '*~' .print | xargs rm
```

The only limitation in using find and xargs is that xargs cannot properly deal with pathnames that contain spaces. If you need to delete files whose pathnames contain spaces you will need to use the -exec option of find rather than xargs:

```
find dir -type f -name 'name' -exec rm '{}' \; -print
```

# What command can I use to rename all the *.aaa files to *.bbb files?

In DOS and Windows, you can rename all the *.aaa files in a directory to *.bbb by using the rename command as follows:

```
rename *.aaa *.bbb
```

In UNIX you can use the mv command to rename files, but you cannot use it to rename more than one file at the same time. To do this, you need to use a for loop:

```
OLDSUFFIX=aaa
NEWSUFFIX=bbb
for FILE in "*.$OLDSUFFIX"
do
NEWNAME=`echo "$FILE" | sed -e 's/\.$OLDSUFFIX/\.$NEWSUFFIX/'`
mv "$FILE" "$NEWNAME"
done
```

Here you generate a list of all the files in the current directory that end with the value of the variable OLDSUFFIX. Then you use sed to modify the name of each file by removing the value of OLDSUFFIX from the filename and replacing it with the value of NEWSUFFIX. You use the $ character in our sed expression to anchor the suffix in OLDSUFFIX to the end of the line; this ensures that the pattern is really a filename suffix. After you have the new name, you rename the file from its original name, stored in FILE, to the new name stored in NEWNAME.