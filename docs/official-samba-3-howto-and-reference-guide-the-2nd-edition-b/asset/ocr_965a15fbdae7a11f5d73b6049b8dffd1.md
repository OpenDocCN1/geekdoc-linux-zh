out in this section are inspired by this article, which describes a command-line method that can be applied to install network and local printers and their drivers. This is most useful if integrated in Logon Scripts. You can see what options are available by typing in the command prompt (DOS box):

```
rundll32 printui.dll,PrintUIEntry /?
```

A window pops up that shows you all of the command-line switches available. An extensive list of examples is also provided. This is only for Windows 200x/XP; it does not work on Windows NT. Windows NT probably has some other tools in the respective Resource Kit. Here is a suggestion about what a client logon script might contain, with a short explanation of what the lines actually do (it works if 200x/XP Windows clients access printers via Samba, and works for Windows-based print servers too):

```
rundll32 printui.dll,PrintUIEntry /dn /n "\\cupserver\\infotec2105-IPDS" /q
rundll32 printui.dll,PrintUIEntry /in /n "\\cupserver\\infotec2105-PS"
rundll32 printui.dll,PrintUIEntry /y /n "\\cupserver\\infotec2105-PS"
```

Here is a list of the used command-line parameters:

+   * /dn deletes a network printer.
+   * /q quiet mode.
+   * /n names a printer.
+   * /in adds a network printer connection.
+   * /y sets printer as default printer.

+   * Line 1 deletes a possibly existing previous network printer *infotec2105-IPDS* (which had used native Windows drivers with LPRng that were removed from the server that was converted to CUPS). The /q at the end prevents confirm or error dialog boxes from popping up. They should not be presented to the user logging on.
+   * Line 2 adds the new printer *infotec2105-PS* (which actually is the same physical device but is now run by the new CUPS printing system and associated with the CUP S/Adobe PS drivers). The printer and its driver must have been added to Samba prior to the user logging in (e.g., by a procedure as discussed earlier in this chapter or by running **cupssaddlsmb**). The driver is now auto-downloaded to the client PC where the user is about to log in.
+   * Line 3 sets the default printer to this new network printer (there might be several other printers installed with this same method, and some may be local as well, so we decide for a default printer). The default printer selection may, of course, be different for different users.