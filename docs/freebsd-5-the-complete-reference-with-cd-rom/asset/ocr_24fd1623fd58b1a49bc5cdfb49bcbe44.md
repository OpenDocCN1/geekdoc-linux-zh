Once you’ve modified your /etc/printcap file to use your new filters, restart lpd. You can then test printing by using lpr to print a variety of files. Try paging through your filter files to learn what file types your filter supports. When you try to print a file that’s not supported by magicfilter, the file should quietly disappear from the queue, preventing a possible spew of paper with gibberish. (The root user will receive an e-mail notification of this rejection, though.) If the file type is supported, it should be processed and you should receive reasonable output.

# # Controlling a Printer

If you’ve configured your system as you read this chapter, you should now have a functioning print queue on your FreeBSD system. This section describes how to use this print queue, both as an ordinary user and as the system administrator. Topics include submitting print jobs, checking on jobs in the queue, deleting jobs, reordering jobs, and changing the availability of print queues.

# ## Submitting Print Jobs

This chapter has already referred to the `lpr` utility, which is FreeBSD’s tool for submitting print jobs to the queue. This tool is important enough that it deserves an extended description. You should also know how applications interact with `lpr` to enable you to print directly from a program, rather than generate a PostScript file and then print it manually with `lpr`.

# ## Using lpr

The `lpr` program accepts a large number of options, some of which are fairly esoteric. Consult the `lpr` man page for details. A simplified syntax is

```
```
lpr [-P*printer*] [-*num*] [-U *user*] [-hnmrs] [*filename*...]```

The meanings of these options are
```

+   - -P*printer* This option sets the printer queue to be used. It may be the most-used `lpr` option on systems that support multiple printers. The default is the value of the *PRINTER* environment variable or `lp` if that variable doesn’t exist. Some versions of `lpr` require that there be no space between the `-P` and the queue name, but the BSD LPD included with FreeBSD can tolerate a space.

+   - -#*num* This option tells `lpr` to generate *num* copies of the printout. For instance, `lpr -#4 afile.ps` creates four copies of `afile.ps`.

+   - -U *user* FreeBSD tracks who submits print jobs. This option, which is accessible to *root* and *daemon* only, enables you to specify the user associated with a print job.