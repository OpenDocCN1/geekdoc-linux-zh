For example, if you wanted to remove job #15 from the queue in the
printer prl1, you can type

```
>lprm -Ppr1 15
```

To verify the results, you can use lpq to check the queue again:

```
>lpq -Ppr1
```

You should see the job you specified terminated and no longer active.

That's it for printing. As I have mentioned before, it is imperative that you
read more about this if you really want to master printing in Unix. Unix
printing is not difficult and can be learned simply by mastering the
concepts brought up in this lesson, and expanding on them. Make sure
you consult the Internet and man pages for more information on printing.

# Summary

In this, you learned the commands you need to print from the com-
mand line. The suite of lpr, lpq, and lprm commands make up the basis
for printing from Unix and most Unix computers. Here's a review of some
of what we covered in this lesson:

+   * lpr and lp1—The lpr and 1p commands are used to send a file
to the printer. If the file is a type other than plain text, it can be
processed by a filter that correctly formats the information for
your printer.

+   * lpq and lpstat—When a print request is sent to the printer,
ether from lpr or encript, it is added to the printer queue.
Use the lpq or lpstat -t program to display all pending printer
transactions, their corresponding job IDs, and their owners.

+   * lprm and cancel—If you want to remove a job from the print
queue, lprm and cancel will do the trick.