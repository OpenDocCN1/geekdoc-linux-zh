allow you to remove print jobs, these are stored in the print spool, which is separate from any application directory. Therefore, answer c is incorrect.

# Question 3

Which of the following is used to translate print jobs from text or graphical applications to a format that a printer can actually use?

+   - a. Input translator
+   - b. Printer filter
+   - c. Line printer daemon
+   - d. Stair-step manager

Answer b is correct. Printer filters, as configured in your /etc/printcap file, allow your applications to send print jobs in a language that your printer can use. Because there is no print-related purpose for an input translator, answer a is incorrect. Although the line printer daemon (lpd) uses printer filters, the daemon itself is not a printer filter; therefore, answer c is incorrect. Although stair-stepping is a problem for text, it is not an issue for graphical applications. Therefore, answer d is incorrect.

# Question 4

Which of the following steps do you need to take to delete a specific print job? The owner of the print job is named sam, and you don't know the print job number. It's his only current print job. Others also have print jobs in progress. The name of the printer is hp, and it is not your default printer. Select the option that works in the shortest number of steps.

+   - a. Use lpc -P to find the print job number, and then delete it by number with the lprm command.
+   - b. Use lpq -a to find the print job number, and then delete it by number with the lprm command.
+   - c. Use lprm -P hp sam to delete all of sam's current print jobs.
+   - d. Use lpc -P hp sam to delete all of sam's current print jobs.

Answer c is correct. The lprm command removes print jobs. The -P switch specifies the printer. And you can specify print jobs to remove by user. The lpc command helps you if you know the print job number. Because the printer isn't specified in answer a, that answer is incorrect. Because there is no -a switch for the lpq command, answer b is incorrect. You can use the lpc command to abort