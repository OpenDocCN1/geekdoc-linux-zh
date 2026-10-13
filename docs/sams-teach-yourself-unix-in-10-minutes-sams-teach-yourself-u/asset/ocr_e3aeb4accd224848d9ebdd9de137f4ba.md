If you want to remove all the pending print jobs that you have sent, you can use the * character in place of the job ID. This cancels anything that you've sent to the printer.

![](bbox=[0.15, 0.3, 0.22, 0.42])

# Canceling a Print Job

The lp system uses the command cancel instead of lprm. To cancel a printer job, use the lpstat -t command to list the jobs, pick the job ID, and then issue the cancel command as follows: cancel <jobid>. Because lp keeps track of print job IDs with unique names rather than just numbers, there is no need for you to specify from which printer you want to remove the job.

# PRETTY PRINTING: ENSCRIPT

If you want to do some fancy printing, you can use the enscript command to convert your text files into postscript and add some flashy features. (This might not be installed on all systems—ask your system administrator to install this if you need it and can't find it.) For instance, if you want to print two pages of text on a single side of paper, enscript can format your document correctly. It can also print banner information with each page to help you identify what file has been printed and what page number you are looking at.

To use enscript in its most basic form, do the following:

+   1. Choose your printer.
+   2. Choose the file that you want to print.
+   3. Run enscript as follows: enscript -d <printer name> <filename> <filename> ...

For example, to use enscript to print the file samplefile.txt, you type the following:

```
>enscript -d hod samplefile.txt
```

```
[ 1 pages * 1 copy ] sent to printer
```