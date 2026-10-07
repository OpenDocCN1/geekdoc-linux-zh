# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

dc3dd has also incorporated the hashing, splitting and logging of an acquisition into a single command. All of this can be done with regular dd and external tools (with pipes, redirection or scripting), but there is no doubt practitioners prefer an integrated approach. The standard options available to the regular dc3dd (bs, skip, etc).

More than just incorporating the other steps into a single command, dc3dd extends the functionality. For example, using a regular split with dd as we do in a previous exercise, we can either allow the default alphabetic naming of split, or pass the -d option to use with decimal extensions on or. In contrast, dc3dd allows us to only define the size of each split as to the imaging command (using ofsz) without need for a piped command, but it also allows more granular control over the format of the extensions each split will have as part of it. So, to split a 40 GB disk into 2 GB images, I would simply use:

```
ofs-BASENAME.FMT ofsz=2G
```

The ofs parameter is essentially "output file split". The extension following the output files is directly formatted in the command itself. According to the dc3dd man page:

+   4. FMT is a pattern for a sequence of file extensions that can be numerical starting at zero, one, or alphabetical. Specify FMT by using a series of zeros, ones, or a's, respectively. The number of characters used indicates the desired length of the extensions. For example, a FMT specifier of 0000 indicates four character numerical extensions starting with 0000.

If I issue the base command as something like this:

```
dc3dd if=/dev/sdd ofsz=32M ofs=filename.FMT
```

I can adjust the values for FMT, and my split extensions would change accordingly:

| FMT=aa | *aa, *ab, *ac | (two alphabetic chars) |
| FMT=aaa | *aaa, *aab, *aac | (three alphabetic chars) |
| FMT=aaaa | *aaaa, *aaab, *aaac | (four alphabetic chars) |