either directly or indirectly, can be specified directly using the `-s` (or `--server`) and `-q` (or `--queue`) options. They may also be specified indirectly by passing the path of a NetWare bindery queue, using the `-b` (or `--bindery`) option, or the path to a NetWare Directory Services queue or printer object, using the `-n` (or `--nds`) option. If you do not specify any queue or servers, the environment variables `NWCLIENT_PREFERRED_QUEUE` and `NWCLIENT_PREFERRED_SERVER` are used to determine the queue and server to print to. If no filename is specified on the command line, then `stdin` is printed instead.

To print a file if the NetWare environment variables are set, type:

```
nwprint filename
```

To print a directory list from the command line (if the environment variables are set), switch to the directory you want to list and type:

```
ls | nwprint
```

Note that with both commands, if the environment variables are not set, you must use the `-q` or `-s` switch to specify either a print queue or a specific server to use. The proper syntax for this is

```
nwprint -s server -q queue_file
```

One other option for the `nwprint` command is the `-b` switch: this is used to specify a bindery server at the time you print. The syntax is as follows:

```
nwprint -b bindery/path/to/print/queue_file
```

Here's an example:

```
nwprint -b /NetWare/bindery/hsimpson/objects/01 somefile.txt
```

Use the `-n` option to send the print job to an NDS server:

```
nwprint -n NDS/path/to/print/queue_file
```

Your command will resemble this example:

```
nwprint -n /NetWare/NDS/tree1/myorg/01 somefile.txt
```

When the printer doesn't automatically return to the beginning of the next line, your text shows what is known as a stair-stepping effect. Add the `-c` option to the `nwprint` command so the printer will automatically insert carriage returns after each line:

```
nwprint -c somefile.txt
```

When you change your mind about a print job, you might want to view the print queue and delete it. The NetWare client allows you to do this fairly easily. You use the `nwqstat` command to view the print requests in a queue. `nwqstat` displays the status of a specific