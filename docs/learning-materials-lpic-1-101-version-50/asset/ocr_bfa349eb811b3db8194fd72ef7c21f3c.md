# # Answers to Explorational Exercises

+   1. In your home directory, create the files called dog and cat.

```
$ touch dog cat
```

+   2. Still in your home directory, create the directory called animal. Move dog and cat into animal.

```
$ mkdir animal
$ mv dog cat -t animal/
```

+   3. Go to the Documents folder found in your home directory and inside, create the directory backup.

```
$ cd ~/Documents
$ mkdir backup
```

+   4. Copy animal and its contents into backup.

```
$ cp -r animal ~/Documents/backup
```

+   5. Rename animal in backup to animal.bkup.

```
$ mv animal/ animal.bkup
```

+   6. The /home/lpi/databases directory contains many files which includes: db-1.tar.gz, db-2.tar.gz and db-3.tar.gz. Which single command can you use to list only the files mention above?

```
$ ls db-[1-3].tar.gz
```

+   7. Consider the listing:

```
$ ls
cne122223.pdf cne12349.txt cne1234.pdf
```