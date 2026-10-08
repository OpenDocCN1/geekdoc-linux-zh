# The l1pr Command

Because Unix is a multiuser environment, it would only make sense that more than one person would be printing to a printer at any single time. When you print in Unix, your print job is sent with a job number. This number is assigned to the job by Unix to track and complete the job. Canceling a print job after you start one is canceled based on that job number. The job is removed from the print queue and you no longer have a print job pending.

Now that you understand the fundamentals of printing in Unix, let's take a look at how to actually get it done.

With the lpd (line printer daemon and its protocol) system available on your machine, you can use the l1pr suite of commands to send print jobs to your printer. The lpr (line printer) command is the primary method for sending data to the printer and is available on, if not, all Unix systems unless disabled or removed. lpr essentially dumps all data directly to the printer that you specify. To use l1pr, follow these steps:

+   1. Determine the name of the printer you want to use. In some cases, your Unix system administrator will give you the name.
2. Choose the file you want to print as a text file. If you do not have the one to print, make one with emacs or vi.
3. Send the print job by using the following command: lpr -P<printer name> <filename> <filename>.... (There is no space between -P and the printer name.)
4. If there is only one printer configured on your computer, chances are you simply type lpr <filename> <filename>...

Let's look at an example of how to print out a print job. As an example, type the following:

```
>lpr -Ppr anyfile.txt
```