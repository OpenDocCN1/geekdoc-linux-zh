To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

# Searching for a Tool: apropos

Man is very useful if you know the name of the command you’re interested in. You can do a man commandname, and you are on your way. But what if you don’t know the name of the command you are looking for?

That is where the apropos command comes in: It allows you to search for keywords instead. As a result, it displays a list of documents that might be related to your question.

Great! There’s only one small hang-up: the database that apropos searches, called the whatis Database, does not exist until you create it. (You’ll learn how to do this in the section “Building the whatis Database: makewhatis.”) After you build it, you can query the database with the apropos command, for example, to find out about commands related to your tape drive:

```
[alberto@digital alberto]$ apropos tape
mt (1)              - control magnetic tape drive operation
smtbar (1)          - shell script for backing up SMB shares directly to UNIX tape drive
st (4)              - SCSI tape device
```

From this information, you know that there are at least three manual pages (use the man command) that relate to your tape drive. The numbers you see in parenthesis indicate a manual section.

The UNIX manual is organized into several sections. Each section is organized by topic. Table 15.1 provides a list of the sections.

# Table 15.1 Sections of the UNIX Man Pages Under Linux

| Section Number | Topic |
|---|---| 
| 1 | User commands, programs, and applications |
| 2 | System calls and kernel error codes |
| 3 | Library function calls |
| 4 | Special files (things in /dev directory) |
| 5 | Standard file formats |
| 6 | Games and other funny-type programs |
| 7 | Miscellaneous things that don’t fit elsewhere |