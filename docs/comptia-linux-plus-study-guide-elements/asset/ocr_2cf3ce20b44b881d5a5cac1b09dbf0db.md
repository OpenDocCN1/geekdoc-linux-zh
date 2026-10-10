# **TABLE 9.3   lpr and lp Options and Effects (continued)**

| lpr Option | lp Option | Effect |
|---|---|---|
| `-C _jobname_`, `-J _jobname_`, or `-T _jobname_` | `-t '_jobname'` | Print jobs have names to help identify them, both while they're in the queue and once printed (if the queue is configured to print banner pages). The name is normally the name of the first file in the print job, but you can change it by including this option. |
| `-# _number_` | `-n _copies_` | You can specify the number of copies of a print job by including this option. |
| `-l` | None | This option causes CUPS to bypass its smart filter for the printer. |
| `-m` | `-m` | You can have CUPS send you an e-mail when the job has finished by using this option. |
| None | `-P _page-list_` | Sets a range of pages to be printed. Pages may be listed individually, separated by commas (as in `1,7,9`), be a range separated by a dash (as in `2-4`), or use both methods (as in `1,7-9,12`). |

Suppose you have a file called `report.txt` that you want to print to the printer attached to the `texmark` queue. This queue is often quite busy, so you want the system to send e-mail to your account when it's done so that you know when to pick up the printout. You could use the following command to accomplish this task:

```
$ lpr -Pltexmark -m report.txt
```

The equivalent command using `lp` is as follows:

```
$ lp -d texmark -m report.txt
```

The `lpr` and `lp` commands are accessible to ordinary users as well as to root, so anybody may print using these commands.

Many programs that need to print directly, such as graphics programs and word processors, call `lpr` or `lp`. Other programs interface more directly with CUPS. In either case, these programs typically give you some way to adjust the print command so that you can change parameters such as the printer name. For instance, Figure 9.4 shows Konquерor's Print dialog box. Konquерor features a pop-up list button that lets you select the print queue. This is the Name field in Figure 9.4, but some programs call it something else. Some programs also provide a text entry field in which you type some or all of an `lpr` or `lp` command, instead of selecting from a pop-up list of available queues. Consult the program's documentation if you're not sure how it works.