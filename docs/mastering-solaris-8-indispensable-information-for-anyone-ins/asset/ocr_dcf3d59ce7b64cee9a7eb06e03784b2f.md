# **FIGURE 10.7**

*The Admintool’s Add Access to Printer dialog box*

![](bbox=[0.29, 0.14, 0.81, 0.47])

Follow these steps to add a new attached printer to a print server:

+   1.  Start the Solaris Print Manager (see “Adding Printer Access”).
+   2.  Select the New Attached Printer command from the Printer menu. The New Attached Printer dialog box appears.
+   3.  Enter the printer name and select the printer port, printer type, file contents, and fault notification options. Set the Default Printer and Always Print Banner options.
+   4.  In the User Access List list box, enter the name of users or groups or enter **all** for all users.
+   5.  Click the Apply button to continue adding additional attached printers. Or click the OK button to return to the main Print Manager window.

You will see the attached printer added to the Print Manager, and the printer’s information will be added to the appropriate configuration files.

Finally, test that the network printer was correctly attached by using the `lp -d <printname> <filename>` command to print a test file.

You can enter the following sequence of commands at the command line to attach a printer and set its attributes for a print server:

```
```bash
# chown lp /dev/term/b
# chmod 600 /dev/term/b
# lpadmin -p flash -v /dev/term/b
# lpadmin -p flash -T PS
```
```