+   • one_line Index each line of a document so a match can show the exact line the match occurred in.
• text Index so a match shows the entire document with no indication of the exact line the match occurred in. This is the default option.

The waisindex command takes arguments for the name of the destination index file (-d followed by the filename), and the directory or files to be indexed. For example, to index a directory called /usr/sales/sales_lit into a destination index file called sales, using the one_line indexing approach, you would issue the command:

```
waisindex -d sales -t one_line /usr/sales/sales_lit
```

Because there is no path provided for the sales index file in this example, it would be stored in the current directory.

After your WAIS server is running (see the section entitled “Starting freeWAIS”), you can test the indexes by using the waissearch command. For example, to look for the word “WAIS” in the index files, issue the command:

```
waissearch -p 210 -d index_file WAIS
```

Where -p gives the port number (default value is 210), and -d is the path to the index file. If the search is successful (and you have something that matches) you will see messages about the number of records returned and the scores of each match. If you see error messages or nothing, check the configuration information and the index files.

A final step you can take if you want your freeWAIS system to be accessible by Internet users is to issue this command, where Filenames is the name of the index:

```
waisindex -export -register Filenames
```

This is registered with the Directory of Servers at cndir.org and quake.think.com. These addresses are reached automatically with the -register option. Only do this step if you want all Internet users to access your WAIS service. (We will look at the waisindex command in much more detail shortly.)

If you want to enable clients to connect to your freeWAIS system with a WWW browser (such as Mosaic or Netscape), you must issue this command:

```
waisindex -d WWW -T HTML -contents -export /usr/resources/*html
```

Replace the /usr/resources path with the path to your HTML files. This line allows WAIS clients to perform keyword searches on HTML documents, as well.

If you want, you can set WAIS to only allow certain domains to connect to it. This is done in the ir.h file, which has a line like this:

```
#define SERVSECURITYFILE "SERV_SEC"
```