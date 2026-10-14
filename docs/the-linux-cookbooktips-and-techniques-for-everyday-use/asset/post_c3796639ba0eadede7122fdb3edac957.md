
## 32.5.1 Saving a URL to a File

To download a single file from the Web, give the URL of the file as an argument to wget.

- For example, to download ftp://ftp.neuron.net/pub/spiral/septembr.mp3 to a file, type:

```
$ wget ftp://ftp.neuron.net/pub/spiral/septembr.mp3
```

This command reads a given URL, writing its contents to a file with the same name as the original, `septembr.mp3`, in the current working directory.

If you interrupt a download before it's finished, the contents of the file you were retrieving will contain only the portion of the file wget retrieved until it was interrupted. Use wget with the `-c` option to resume the download from the point it left off.

- To resume download of the URL from the previous example, type:

```
$ wget -c ftp://ftp.neuron.net/pub/spiral/septembr.mp3
```

> NOTE: In order for the `-c` option to have the desired effect, you should run wget from the same directory as it was run previously, where that partially-retrieved file should still exist.

## 32.5.2 Archiving an Entire Web Site

To archive a single Web site, use the `-m` ("mirror") option, which saves files with the exact timestamp of the original, if possible, and sets the "recursive retrieval" option to download everything. To specify the number of retries to use when an error occurs in retrieval, use the `-t` option with a numeric argument---`-t 3` is usually good for safely retrieving across the net; use `-t 0` to specify an infinite number of retries, good for when a network connection is really bad but you really want to archive something, regardless of how long it takes. Finally, use the `-o` with a file name as an argument to write a progress log to the file---examining it can be useful in the event that something goes wrong during the archiving; once the archival process is complete and you've determined that it was successful, you can delete the log file.

- To mirror the Web site at http://www.bloofga.org/, giving up to three retries for retrieving files and putting error messages in a log file called `mirror.log`, type:

```
$ wget -m -t3 http://www.bloofga.org/ -o mirror.log
```

This command makes an archive of the Web site at `www.bloofga.org` in a subdirectory called `www.bloofga.org` in the current directory. Log messages are written to a file in the current directory called `mirror.log`.

To continue an archive that you’ve left off, use the `-nc` ("no clobber") option; it doesn’t retrieve files that have already been downloaded. For this option to work the way you want it to, be sure that you are in the same directory that you were in when you originally began archiving the site.

- To continue an interrupted mirror of the Web site at http://www.bloofga.org/ and make sure that existing files are not downloaded, giving up to three retries for retrieval of files and putting error messages in a log file called `mirror.log`, type:

```
$ wget -nc -m -t3 http://www.bloofga.org/ -o mirror.log
```

## 32.5.3 Archiving Part of a Web Site

To archive only part of a Web site—such as, say, a user’s home page—use the `-I` option followed by a list of the absolute path names of the directories to archive; all other directories on the site are ignored.

- To archive the Web site at http://dougal.bris.ac.uk/~mbt/, only archiving the `/~mbt` directory, and writing log messages to a file called `uk.log`, type:

```
$ wget -m -t3 -I /~mbt http://dougal.bris.ac.uk/~mbt/ -o uk.log
```

This command archives all files on the http://dougal.bris.ac.uk/~mbt/ Web site whose directory names begin with `/~mbt`.

To only get files in a given directory, use the `-r` and `-l1` options (the `-l` option specifies the number of levels to descend from the given level). To only download files in a given directory, combine these options with the `--no-parent` option, which specifies not to ascend to the parent directory.

Use the `-A` option to specify the exact file name extensions to accept—for example, use `-A txt, text, tex` to only download files whose names end with `.txt`, `.text`, and `.tex` extensions. The `-R` option works similarly, but specifies the file extensions to reject and not download.

- To download only the files ending in a `.gz` extension and only in the given directory `/~rj h/indiepop-1/download/` at `monash.edu.au`, type:
