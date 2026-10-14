
first, you have to add the applet to your taskbar. Choose Gnome Foot • Panel • Add Applet • Utility • Print. From the File Manager window, drag a plain text file and drop it on the “Printer Applet” icon. (See Figure 6-9.) The file should begin to print.

![](img/3137cdda7122042e86dbeafe9840d4ed_181_0.png)

Figure 6-9: GNOME Printer Applet

## USE CAT TO JOIN FILES

The cat command's primary function is to concatenate, or join, files, but you can also use it to display a file on the screen. The cat command takes one or more files that you specify, smashes them together, and then sends the resulting file to the standard output device (without changing any of the original files).

The standard output device is your screen, but by using the greater-than (>) operator, you can redirect cat's output to another file. Here are some examples:

| Command | Description |
|---|---|
| cat food | Display the food file on the screen. |
| cat scratch fever | Join the files scratch and fever and then display the result on the screen. |
| cat eats bird > DetailsAt11 | Join the files eats and bird and save them in the file DetailsAt11. |

Note that the original files that cat joins are not modified. For example, say the file eats contained these lines:

```
The Owl and the Pussy-Cat went to sea
In a beautiful pea-green boat.
```

Also say the file bird contained these lines:

```
They took some honey, and plenty of money
wrapped up in a five-pound note.
```

After the preceding command, neither file would change, but a new file called `DetailsAt11` would be created, containing all four lines:

```
The Owl and the Pussy-Cat went to sea
In a beautiful pea-green boat.
They took some honey, and plenty of money
Wrapped up in a five-pound note.
```

## SEARCH FOR FILES WITH FIND

Linux’s tree-structured file system is great for organizing your files, but a plethora of directories and subdirectories can make it easy to lose track of specific files. To search for a file named cookie, you can use the find command, like this:

```
find / -name "cookie" -print
```

This command tells find to start looking in the root directory of the file system (/) for files named (-name) cookie and then to print (-print) the full name of each file it finds.

Actually, you don’t need the -print flag on Red Hat Linux, but on most Unix systems, if you leave off the -print flag, find will merrily search and then throw the results in the bit bucket. (This is a fictitious device attached to all computers. When the operating system deletes a file or discards data, it is said to be thrown in the bit bucket.)

This is a departure from the rule of thumb that Linux commands will print their output on the screen unless you specify otherwise.

Starting from the root directory may take a long time, since find will search every single directory on the system. You can shorten the search time by telling find where to start searching if you know that the file you want lies along a certain path. Here are a few examples:

| Command | Description |
|---|---|
| `find . -name "cookie" -print` | Start looking in the current directory. |
| `find ~sigmund -name "cookie" -print` | Start looking in sigmund’s home directory. |
| `find /etc -name "cookie" -print` | Start looking in the /etc directory. |

## USING THE GRAPHICAL FILE FINDER

If you're running X Windows with GNOME, you can search for files with the GNOME Search Tool. Choose Gnome Foot • Utilities • Gnome Search Tool to launch the Search tool (see Figure 6-10). Enter a start directory and a file name (with optional wildcards) and click "Start" to view the results.

![](img/3137cdda7122042e86dbeafe9840d4ed_184_0.png)

![](img/3137cdda7122042e86dbeafe9840d4ed_184_1.png)

Figure 6-10: The GNOME Search tool

## WHAT'S THE DIFFERENCE BETWEEN TWO FILES?

If, when you use find, you discover two files with suspiciously similar names, you might want to know whether they really contain the same information. The diff command will compare two files and give you the lowdown on just how different they are. Here's an example of how you would use the diff command and the output you might get from it:

```
diff cookies.old cookies.new
5c5
< One cup vanilla extract
---
> One teaspoon vanilla extract
7d6
< Six ounces chopped liver
21a22
Note: The previous version of this recipe had a few errors!
```
