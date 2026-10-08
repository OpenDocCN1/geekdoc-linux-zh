To search by size, use the following steps:

+   Select a target file size, and find will locate all files of the selected size and larger.

+   Choose a starting directory.

+   Start the find program using the -size option: find <starting directory> -size <k> -print.

For example:

```
find -size 1024k -print /home/rob/updates/testgraphic.jpg
```

The find command you see here has located a graphics file that is larger than 1,024k.

> What Else Can You Find? The find command is powerful. As you can see, using the find command with the -name, -ctime, and -size options can be helpful, but believe it or not, there is more.

Remember, Unix, the power is at the command line. Use the man pages (as discussed in Lesson 2, “Getting Help”) to learn other helpful options.

# Finding Data with Other Unix Commands

In the previous section of this lesson we learned about the find command. When used, it can be powerful. Other commands you can use are whereis and which, and these commands may bring you results as well.

# The whereis command

The whereis command can be used to run a quick search on a specific number of directories for whatever you specify. For example, if you wanted to run a search on a file named “test”, then you would get all