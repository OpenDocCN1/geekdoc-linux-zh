You don’t need to go to a directory in order to list it. If you provide a pathname to a file or a directory to ls, ls will list the file or directory requested:

```
[alberto@digital alberto]$ ls /opt
bin/        kde/        man/        netscape/
[alberto@digital alberto]$ pwd
/home/alberto
```

# ls in Technicolor

The version of ls shipped with Linux has the capability to display different file types in different colors. This capability is very useful, as it makes it easy to discern among files, directories, and programs.

To enable this behavior, you can type ls --color, and things will happen. The colors for the most popular file types are listed in the following table.

# Typical File Colors (ls --color)

| File Type | Color |
|---|---|
| Regular Files | White |
| Programs | Green |
| Directories | Blue |
| Links | Aqua |

Pretty nifty, eh? It’s so nice you might like to have the file types appear in color all the time. Fortunately, you can. Read on to learn how to change the default options of certain shell commands.