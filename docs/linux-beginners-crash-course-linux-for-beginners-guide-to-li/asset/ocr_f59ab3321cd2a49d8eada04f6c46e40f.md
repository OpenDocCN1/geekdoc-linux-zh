```
ls
barney example1 foo
cp foo foo2
cp: omitting directory 'foo'
cp -r foo foo2
ls
barney example1 foo foo2
```

In this example, the files and the directories that are contained in the directory named foo are copied to foo2.

# Moving a file or directory

If you want to move a directory or a file, you can do so with the command mv, which stands for move. It works in pretty much the same way as cp, with one small advantage – we don’t need to use the -r option to move a directory:

```
mv [options] <source> <destination>
```

For example:

```
ls
barney example1 foo foo2
mkdir backups
mv foo2 backups/foo3
mv barney backups/
ls
backups example1 foo
```

Let’s break that down. In line 3, a new directory called backups is created. In line 4, the directory called foo2 is moved into the new backups directory and renamed foo3. Then the file called barney is moved to the directory called backups. It retains the same name because we didn’t give a new destination name.