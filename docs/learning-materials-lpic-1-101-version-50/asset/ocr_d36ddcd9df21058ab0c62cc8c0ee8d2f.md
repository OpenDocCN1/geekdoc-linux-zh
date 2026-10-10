In the example below, `find` locates all files in the hierarchy starting at the current directory then deletes all files that end with the characters `.bak`:

```
```
$ find . -name "*.bak" -delete
```
```

# # Archiving Files

# ## The tar Command (Archiving and Compression)

The `tar` command, short for “tape archive(r)”, is used to create tar archives by converting a group of files into an archive. Archives are created so as to easily move or backup a group of files. Think of `tar` as a tool that creates a glue onto which files can be attached, grouped and easily moved.

`tar` also has the ability to extract tar archives, display a list of the files included in the archive as well as add additional files to an existing archive.

The `tar` command syntax is as follows:

```
```tar [OPERATION_AND_OPTIONS] [ARCHIVE_NAME] [FILE_NAME(S)]```
```

# ### OPERATION

Only one operation argument is allowed and required. The most frequently used operations are:

+   - `--create (-c)`
+     Create a new tar archive.

+   - `--extract (-x)`
+     Extract the entire archive or one or more files from an archive.

+   - `--list (-t)`
+     Display a list of the files included in the archive.

# ### OPTIONS

The most frequently used options are:

+   - `--verbose (-v)`
+     Show the files being processed by the `tar` command.