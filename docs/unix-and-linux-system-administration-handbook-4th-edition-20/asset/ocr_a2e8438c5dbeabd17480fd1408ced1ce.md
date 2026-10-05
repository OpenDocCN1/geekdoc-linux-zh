# 1.9 MAN PAGES AND OTHER ON-LINE DOCUMENTATION

The manual pages, usually called "man pages" because they are read with the man command, constitute the traditional "on-line" documentation. (Of course, these days all the documentation is on-line in some form or another.) Man pages are typically installed with the system. Program-specific man pages come along the ride when you install new software packages.

Man pages are concise descriptions of individual commands, drivers, file formats, or library routines. They do not address more general topics as "How do I install a new device?" or "Why is this system so damn slow?" For those questions, consult your vendor's administration guides (see page 18) or for Linux systems, the documents available from the Linux Documentation Project.

# Organization of the man pages

All systems divide the man pages into sections, but there are minor variations in the way sections are defined. The basic schema used by our example systems is shown in Table 1.3.

# Table 1.3 Sections of the man pages Contents

| Linux | Solaris | HP-UX | AIX | Contents |
|---|---|---|---||
| 1 | 1 | 1 | 1 | User-level commands and applications |
| 2 | 2 | 2 | 2 | System calls and kernel error codes |
| 3 | 3 | 3 | 3 | Library calls |
| 4 | 7 | 7 | 4 | Device drivers and network protocols |
| 5 | 4 | 4 | 5 | Standard format files |
| 6 | 6 | 6 | 6 | Games and demonstrations |
| 7 | 5 | 5 | 7 | Miscellaneous files and documents |
| 8 | 1m | 1m | 8 | System administration commands |
| 9 | 9 | 9 | - | Obscure kernel spaces and interfaces |
| - | - | 9 | - | HP-UX general information |

Some sections may be further subdivided. Solaris's 3c contains man pages about the system's standard C library. There is also considerable variation in the exact distribution of pages; some systems leave section 8 empty and lump system administration commands into section 1. A lot of systems have discontinued games and demos, leaving nothing in section 6. Many systems have a section of the manuals "I" (lowercase L) for local man pages.

The exact structure of the sections is not important for most topics because man finds the appropriate page wherever it is stored. You only need to be aware of the section definitions when a topic with the same name appears in multiple sections. For example, `passwd` is both a command and a configuration file, so it has entries in both section 1 and section 4 or 5.