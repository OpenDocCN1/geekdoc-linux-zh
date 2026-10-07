
If you want to let inetd handle the waisserver startup, you need to ensure the file /etc/services has an entry for WAIS. The line in the /etc/services file looks like this, where 210 is the port number WAIS uses, and tcp is the protocol:

```
z3955 210/tcp #WAIS
```

After modifying or verifying the entry in /etc/services, you need to add a WAIS entry to the inetd.conf file to start up waisserver whenever a request is received on port 210 (or whatever other port you are using). The entry looks like this, where the options are the same as for the command line startup mentioned above:

```
z3955 stream tcp nowait root /usr/local/bin/waisserver/waisserver.d -u username -d /usr/wais/wais_index
```

The daemon waisserver.d is used when starting up in inetd mode, instead of waisserver. Again you can use the -e option to log activity to a file.

## Building Your WAIS Indexes

After you have the freeWAIS server ready to run and everything seems to be working, it’s time to provide some content for your WAIS system. Usually, documents are the primary source of information for WAIS, although you can index any type of file. The key step to providing WAIS service is to build the WAIS index using the waisindex command. The waisindex command can be a bit obtuse at times, but a little practice and some trial-and-error fiddling will help you master its somewhat awkward behavior.

The waisindex program works by examining all the data in the files of which you want to create an index. From its examination, waisindex usually generates seven different index files (depending on the content and your commands). Each file holds a list of unique words in the documents. The different index files are then combined into one large database, often called the “source” (or “WAIS source”). Whenever a client WAIS package submits a search, the search strings are compared to the source, and the results displayed with accuracy analysis (the match score).

> The use of waisindex enables a client search to proceed much more quickly because the keywords in the data files have already been extracted. However, the mass of data in the index files can be sizable, so allow plenty of disk space for a WAIS server to work with. (For a typical WAIS site, assume at least double the amount of room needed for the source files.)

### WAIS Index Files

The freeWAIS index files are not usually readable by a system user (although one or two files can be read with some success). Usually, waisindex creates seven index files, although the number may vary depending on requirements. Each index file has a specific file extension to show its purpose, based on a root name (specified on the waisindex command line, or defaulting to index). The index files and their purposes are as follows:

- `index.doc` A document file that contains a table with the filename, a headline (title) from the file, the location of the first and last characters of an entry, the length of the document, the number of lines in the document, and the time and date the document was created.
- `index.dct` A dictionary file that contains a list of every unique word in the files cross-indexed to the inverted file.
- `index.fn` A filename file that contains a table with a list of the filenames, the date they were created in the index, and the type of file.
- `index.hl` A headline file that contains a table of all headlines (titles). The headline is displayed in the search output when a match occurs.
- `index.inv` Inverted files that contain a table associating every unique word in all the files with a pointer to the files themselves and the word's importance (determined by how close the word is to the start of the file, the number of times the word occurs in the document, and the percentage of times the word appears in the document).
- `index.src` A source description file that contains descriptions of the information indexed, including the host name and IP address, the port watched by WAIS, the source file name, any cost information for the service, the headline of the service, a description of the source, and the email address of the administrator. The source description file is editable by ASCII editors. We will look at this file in a little more detail shortly.
- `index.status` A status file containing user-defined information.

The source description file is a standard ASCII file that is read by waisindex at intervals to see whether information has changed. If the changes are significant, waisindex updates its internal information. A sample source file looks like this:

```lisp
(:source
 :version 2
 :ip-address "147.120.0.10"
 :ip-name "wizard.tpci.com"
 :tcp-port 210
 :database-name "Linux stuff"
 :cost 0.00
 :cost-unit "free"
 :maintainer "wais_help@tpci.com"
 :subjects "Everything you need to know about Linux"
 :description "If you need to know something about Linux, it's here."
)
```

You should edit this file when you set up freeWAIS because the default descriptions are rather sparse and useless.

### The waisindex Command

The waisindex command allows a number of options, some of which you have seen earlier in this chapter. The following list contains the primary waisindex options of interest to most users:

- `-a` Appends data to an existing index file (used to update index files instead of regenerating them each time a new document is added).
- `-contents` Indexes the file contents (default action).
- `-d` Gives the filename root for index files (for example, -d /usr/wais/foo named all index files as /usr/wais/foo.xxx).
- `-e` Gives the name of the log file for error information (default is stderr—usually the console—although you can specify -s for /dev/null).
- `-export` Adds the host name and TCP port to descriptions for easier Internet access.
- `-l` Gives the level of log messages. Valid values are as follows:
    - 0, no log
    - 1, log only high priority errors and warnings
    - 5, log medium priority errors and warnings, as well as index filename information
    - 10, log every event
- `-M` Links multiple types of files.
- `-mem` Limits memory usage during indexing (the higher the number specified, the faster the indexing process and the more memory used).
- `-nocontents` Prevents a file from being indexed (indexes only the document header and filename).
- `-nopairs` Instructs waisindex to ignore adjacent capitalized words from being indexed together.
- `-nopos` Ignores the location of keywords in a document when determining scores.
- `-pairs` Indexes adjacent capitalized words as a single entry.
- `-pos` Determines scores based on locations of keywords (proximity of keywords increases scores).
- `-r` Recursive subdirectory indexing.
- `-register` Registers your indexes with the WAIS Directory of Services.
- `-stdin` Uses a filename from the keyboard instead of a filename on the command line.
- `-stop` Indicates a file containing stopwords (words too common to be indexed), usually defined in `src/ir/stoplist.c`.
- `-t` Data file type indicator.
- `-T` Sets the type of data to whatever follows.

The waisindex program has to be told the type of information in a file; otherwise it may not be able to generate an index properly. Many file types are currently defined with freeWAIS, and you can display them by entering this command with no argument:

```
waisindex
```

Although many different types are supported by freeWAIS, only a few are really in common use. The most common file types supported by freeWAIS are the following:

- `filename` Same as text, except the filename is used as the headline.
- `first_line` Same as text, except the first line in the file is used as the headline.
- `ftp` Contains FTP code users can use to retrieve information from another machine.
- `GIF` GIF images, one image per file. The filename is used as the headline.
- `mail` or `rmail` Indexes the mbox mailbox contents as individual items.
- `mail_digest` Standard email, indexed as individual messages. The subject field is the headline.
- `netnews` Standard Usenet news, each article a separate item. The subject field is the headline.
- `one_line` Indexes each sentence in a document separately.
- `PICT` PICT image, one image per file. The filename is used as the headline.
- `ps` A PostScript file with one document per file.
- `text` Indexes the file as one document, the pathname as the heading.
- `TIFF` TIFF image, one image per file. The filename is used as the headline.

![](img/e8e6b47ac20475e23d48b4c476f5d891_846_0.png)
