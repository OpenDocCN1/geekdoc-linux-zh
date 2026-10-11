# cd

When you first log on to your computer, you are placed in your home directory. To change to other directories, you use the command **cd** (change directory) followed by the name of the new directory. The new directory then becomes your working directory. The syntax for cd is

```
```
cd [dir]
```

```

When designating a new directory, you can use either a *relative or absolute* path. The absolute path begins at the root or top of the filesystem and defines the complete route to your destination. For example

```
```
cd /home/hadden/letters
```

```

would locate the destination by starting at the root (/), then the home directory, then the hadden directory, and finally the letters directory. A relative path starts looking at the working directory and traverses down the path. So if your working directory is /home/hadden you could type

```
```
cd letters
or
cd letters/Aug
```

```

which would change to the letters subdirectory of /home/hadden. However, if the working directory is /home/hadden/memos you would receive an error message that the directory letters does not exist.

If you use a relative path with cd and the command fails, check to see that you are really where you think you are. To do this, use the command pwd (present working directory), which does not take any arguments. The pwd command outputs the absolute path to the working directory to your screen.

If you want to return to your home directory, you have several options. You can use the cd command followed by the absolute path to your home directory. A better way, however, is to use the cd command without any arguments. For example

```
```
$ pwd
/home/hadden/letters/Aug
$ cd
$ pwd
/home/hadden
```

```