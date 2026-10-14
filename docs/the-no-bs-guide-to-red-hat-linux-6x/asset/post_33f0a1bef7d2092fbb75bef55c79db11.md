
In this case, ls returns just the file names in columnar format, but with a few marks, thanks to the -F flag. The slash suffix on slugs indicates that it is a directory, and zippity is identified as an executable.

```
ls -al animals
-rw-r--r-- 1 hermie users 1758 Mar 17 23:17 .hoohah
-rw-r--r-- 1 hermie users 45090 Mar 23 23:17 cat_info
-rw-r--r-- 1 hermie users 64183 Feb 14 22:07 cow_info
-rw-r--r-- 1 hermie users 115032 Jan 06 11:14 dog_info
-rw-r--r-- 1 hermie users 248 Jan 16 09:18 pig_info
drwxr-xr-x 1 hermie users 1024 Feb 28 06:12 slugs
-rwxr-xr-x 1 hermie users 45198 Jan 23 11:14 zippity
```

Here, ls has displayed all files in the animals directory, including the hidden hoohah file. In addition to the file name, the file's permissions, owner, group, size in bytes, and date and time of last modification are displayed. (More on permissions later in this chapter.)

```
ls -lrt animals
-rw-r--r-- 1 hermie users 115032 Jan 06 11:14 dog_info
-rw-r--r-- 1 hermie users 248 Jan 16 09:18 pig_info
-rwxr-xr-x 1 hermie users 45198 Jan 23 11:14 zippity
-rw-r--r-- 1 hermie users 64183 Feb 14 22:07 cow_info
drwxr-xr-x 1 hermie users 1024 Feb 28 06:12 slugs
-rw-r--r-- 1 hermie users 45090 Mar 23 23:17 cat_info
```

This time, the files are sorted by time stamp, in reverse order. If you have lots of files in a directory, this is a handy way to find out which are the oldest and newest. Also notice that the -l, -r, and -t switches were combined into -lrt in the preceding command. We could just as well have issued the command ls -l -r -t animals.

## LISTING FILES WITH MIDNIGHT COMMANDER

Red Hat Linux comes with a handy utility called Midnight Commander (see Figure 5-1), which is a text-based utility that makes it easier to list and manipulate your files. To start Midnight Commander, enter the mc command. Midnight Commander shows you the file system tree in the left panel and the files from the selected directory in the right panel. Follow the prompts at the bottom of the screen to navigate directories, browse or edit a file, or perform other operations such as copy, move, and delete.

![](img/3137cdda7122042e86dbeafe9840d4ed_155_0.png)

Figure 5-1: The Midnight Commander program

## LISTING FILES WITH FILE MANAGER

If you're running X Windows with GNOME, the File Manager (Figure 5-2) is highly recommended over the shell prompt commands or Midnight Commander. File Manager, also known as GNOME Midnight Commander, is a graphical version of the text-based Midnight Commander

![](img/3137cdda7122042e86dbeafe9840d4ed_155_1.png)

Figure 5-2: The File Manager program

program. When you start X Windows, the File Manager is already active and minimized on your desktop. Double-click on the folder icon at the top left of your screen to see the File Manager window. (Refer to Chapter 2, “GNOME: The Linux GUI,” for more detailed usage information.)

## DISPLAYING FILES

You know how to get a list of files. But what if you want to take a peek at a file's contents? Several commands, including cat, more, and less, can be used to display files. Let's see how they work in this example:

```
cat pig_info
Pigs make great pets, but they are not dogs or cats. Maybe
somewhere in between. I tend to believe that they have more
personality. They do require significant amounts of attention,
love, and scratches. But they aren't always snuggly in return.
```

The cat command (short for concatenate) shown in this example is like the DOS type command. In response to the command cat pig_info, the system simply splatters the file on the screen. If there is more data in the file than will fit on one screen, the contents whiz by before you can see it. The more command solves this problem by displaying the file screen by screen:

```
more dog_info
Affectionately known as the “Toller,” the Nova Scotian Duck
Tolling Retriever was once called the Little River Duck Dog,
since it was developed in the Little River district of Yarmouth
County, Nova Scotia. This engaging dog is a specialist with
waterfowl. Tolling, or luring, is the practice of tricking ducks
into gunshot range. Hunters had long observed this behavior
--More--(0%)
```

The more command pauses when the screen fills up and waits for you to press the spacebar before it rolls out another screenful of text. A legend at the bottom of the screen tells you what percentage of the file has been displayed so far. You can press CTRL-C to quit more before reaching the end of the file.

The less command works like more except that it lets you move both forward and backward in the file while the command is running—use the B key on your keyboard to back up one screen and the spacebar to move forward and show the next screen.
