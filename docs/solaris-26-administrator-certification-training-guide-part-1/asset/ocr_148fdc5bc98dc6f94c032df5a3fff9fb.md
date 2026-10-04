you use the lpsched command. If a print request was printing when the print scheduler stopped running, that request will be printed in its entirety when you restart the print scheduler.

First, stop the scheduler by typing

```
/usr/lib/lp/lpshut
```

To restart the scheduler, type

```
/usr/lib/lp/lpsched
```

# Setting a User's Default Printer

When you added the printer, you were given the option of selecting that printer as the default printer for that particular system. You might want to set the default printer at the user level so that, on a particular system, users can specify their own default printer. If users don't provide a printer name when sending a print job, the print command searches for the default printer in the following order:

| Order | Item |
|---|---|
| First | LPDEST variable |
| Second | PRINTER variable |
| Third | System's default printer |

These variables can be set in the user's .profile file.

# Modifying the Printer with Admintool

The Solaris Admintool can be used to modify a printer after it was added to the system. Modifications that can be made to a printer via the Admintool include:

+   - Give the printer description.
- Indicate the printer port.
- List file contents.
- Provide fault notification.
- Select default printer.
- Print a banner.
- Accept and process print requests.
- Provide user access list.

To modify a printer via the Admintool, select Edit, Modify from the Printers window shown in Figure 9-7.