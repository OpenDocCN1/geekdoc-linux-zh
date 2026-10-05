# GETTING HELP IN RED HAT ENTERPRISE LINUX

PERFORMANCE CHECKLIST
In this lab, you will look up information to help you complete tasks in man pages and GNU Info documents.

OUTCOMES
You should be able to:

+   - Locate relevant commands by searching man pages and Info nodes.
- Learn new options for commonly used documentation commands.
- Use appropriate tools to view and print documentation and other non-text formatted files.

BEFORE YOU BEGIN
Log in to workstation as student using student as the password.
On workstation, run the lab help-review start.

```
[student@workstation ~]$ lab help-review start
```

+   1. On workstation, determine how to prepare a man page for printing. Specifically, find what format or rendering language is used for printing.

+   2. Create a formatted output file of the password man page. Call the file password.ps. Determine the file content format. Inspect the contents of the password.ps file.

> NOTE
Created output of the password man page using the following command:

[student@workstation $] man -t password > password.ps

The symbol redirects the contents of the man page to the password.ps file. This command is taught in more detail in a following chapter.

+   3. Using man, learn the commands used for viewing and printing PostScript files.

+   4. Learn how to use the evince() viewer in preview mode. Also, determine how to open a document starting on a specific page.

+   5. View your PostScript file using the various evince options you researched. Close your document file when you are finished.