# Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

**PostScript** This printout formatting language is designed to allow sophisticated page layout from various programs. GhostScript is an open source implementation of the PostScript language and is included as part of the CUPS distribution.

**print job name** This is the unique name assigned to a print job by the `lpr` or `lp` command.

**print queue** All print jobs are placed in a queue, or list, for processing by a specific printer.

# Exercises

+   1. Use the `lpinfo -a` command or the `printers` command to find out what printers are available on your system. Which command is easier to use? How many printers are available?

+   2. Is your `PRINTER` variable already set to a printer? Is it the printer you would choose?

+   3. Use `man -k` to see what commands you have on your system that work with the printers and print queues. Use `man` to peruse them.

+   4. Show three ways to print the file `dickens.note` with `lpr`.

+   5. Add a print job to the queue and then remove it with `lprm`. What happened?

+   6. How would you use `pr` to add A Tale of Two Cities as a running title across each printout page of the file `dickens.note`? How would you start the printout on the second page of the file?

# Preview of the Next Hour

In the next hour, you’ll learn about the various ways you can archive backups and otherwise work with your file system as a whole. You’ll also learn about how Unixes now work with package management systems to make the process of installing software considerably less work.