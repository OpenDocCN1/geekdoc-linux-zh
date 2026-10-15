# Viewing File Beginnings with head

Using head, as shown in Code Listing 6.3, you can find out in a jiffy what’s in a file by viewing the top few lines. This is particularly handy when you’re browsing file listings or trying to find a specific file among several others with similar content.

# To view file beginnings with head:

+   - head honeydo
+   At the shell prompt, type head followed by the filename. As Code Listing 6.3 shows, you’ll see the first ten lines on the screen. Notice that “lines” are defined by hard returns, so a line could, in some cases, wrap to many screen lines.

# To view a specified number of lines:

+   - head -20 honeydo
+   Add -20 (or whatever number of lines you want to view) to view a specific number of lines.

# To view the beginnings of multiple files:

+   - head honey* | more
+   You can view the tops of multiple files by piping head (plus the filenames) to more. Note that head conveniently tells you the filename of each file, as shown in Code Listing 6.4

```
[ejr@hobbes manipulate]$ head honeydo
Take garbage out
Clean litter box
Clean diaper pails
Clean litter box
Mow lawn
Edge lawn
Clean litter box
Polish swamp cooler
Buff garage floor
Clean litter box
[ejr@hobbes manipulate]$
```

# Code Listing 6.3 Use head to look at just the top of a file, which gives you a manageable view of the file.

```
[ejr@hobbes manipulate]$ head honey* | more
==> honeyconsider <==
Mother-in-law visits next week
Cat mess in hall to clean up
Cat mess in entry to clean up
Cat mess in living room to clean up
Toddler mess in family room to clean up
Cat and toddler mess in den to clean up
IRS called again today
Neighbors on both sides looking for donations for the annual fund drive
Boss called last Friday and said it’s urgent
==> honeydo <==
Take garbage out
Clean litter box
Clean diaper pails
Clean litter box
Mow lawn
Edge lawn
Clean litter box
Polish swamp cooler
Buff garage floor
```

# Code Listing 6.4 head, with the help of more, lets you see the beginnings of several files in sequence.