graphics programs and word processors. These programs typically give you some way to adjust the print command so that you can enter parameters such as the printer name. Some programs provide point-and-click methods of adjusting print options, as described shortly, in “Using GUI Printing Tools.” Other programs provide a text entry field in which you type some or all of an `lpr` command instead of selecting from a pop-up list of available queues. Consult the program’s documentation if you’re not sure how it works.

# Displaying Print Queue Information with `lpq`

The `lpq` utility displays information on the print queue—how many files it contains, how large they are, who their owners are, and so on. By entering the user’s name as an argument, you can also use this command to check on any print jobs owned by a particular user. To use `lpq` to examine a queue, you might issue a command like the following:

```
$ `lpq -P`lexmark`
texamrk is ready and printing
Rank  Owner  Job    File(s)             Total  Size
active  rodsmit 1048   http://localhost:631/printers 123904 bytes
```

![](bbox=[0.14, 0.44, 0.25, 0.51])

This example shows the output of CUPS’s `lpq`. Systems that use the original BSD LPD and LPRng display different information, but the most important information (such as the job number, job owner, Job name, and Job size) are present in all cases.

Of particular interest is the job number—1048 in this example. You can use this number to delete a job from the queue or reorder it so that it prints before other jobs. Any user may use the `lpq` command.

![](bbox=[0.14, 0.62, 0.25, 0.7])

If you submit a single small print job with `lpr` or some other tool, it might vanish from the queue before you can see it appear with `lpq`. If you believe this is happening, you could try submitting several print jobs. Documents that print slowly, such as graphics files, are likely to stay in the queue longer. Alternatively, you can use `lpc` or the CUPS Web-based control system to stop the print queue, causing jobs to pile up as they’re submitted.

# Removing Print Jobs with `lprm`

The `lprm` command removes one or more jobs from the print queue. There are several ways to issue this command:

+   - If it’s issued with a number, that number is understood to be the job ID (as shown in `lpq`’s output) that’s to be deleted.
+   - If root runs `lprm` and passes a username to the program, it removes all the jobs belonging to that user.