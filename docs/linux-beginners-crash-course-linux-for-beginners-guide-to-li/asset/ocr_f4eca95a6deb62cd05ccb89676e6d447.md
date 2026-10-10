# # Copying a file or directory

Sometimes you might want to make a copy of a directory or a file, for example if you’re about to make changes to it and you want a backup so that, if things do go wrong, all is not lost! The command for this is cp, which is short for copy:

```
cp [options] <source> <destination>
```

There are a number of options for this command, one of which I will demonstrate now:

```
ls

example1 foo
```

```
cp example1 barney

ls

barney example1 foo
```

Did you see that both the destination and the source are paths? These can be referred to using both relative and absolute paths, as per these examples:

```
cp /home/Simon/linuxtutorialwork/example2 example3

cp example2 ../../backups

cp example2 ../../backups/example4

cp /home/Simon/linuxtutorialwork/example2 /otherdir/foo/example5
```

When you use the cp command, it can be either a path to a file or a path to a directory. If it goes to a file, a copy of the source will be created and it will be named by the filename that is specified in the destination path. If the path goes to a directory, the file will be copied into that directory and be named the same as the source.

By default, cp only copies a file. If we use the option -r, which stands for Recursive, we can copy directories. Recursive means that you want to see a directory and you want to see all of the files and the directories contained in it. For the subdirectories, simply go into them and repeat the command, and so on: