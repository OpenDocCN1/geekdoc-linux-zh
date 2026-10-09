The advanced administrator may find that SMIT provides a faster interface to many management tasks than the command line. This is especially true for some configuration commands that have a multitude of switch options. When using SMIT, two files are created, the *smi t.script* and the *smi t.log* files. The SMIT script facility may be used to assist in creating complex administration scripts, and the logging facility keeps a log of the tasks that were performed on the system, as well as the date / time the commands were executed.

The choice is yours to use SMIT to manage AIX. As you gain experience with SMIT and the AIX environment, you may find that you prefer to use SMIT for some management activities and the command line for others. Whether you love it or hate it, SMIT is here to stay.

# USING SMIT

SMIT is started by executing the **smit** command for a Motif interface or the **smitty** command for an ANSI interface from the command line. By default, SMIT will enter the top-level system management menu. To enter SMIT at a particular task submenu, you can supply the SMIT FastPath name as an argument.

```
```
# smit
# smit user
```
```

SMIT allows you to take a test drive utilizing all of its features without making changes to the operating system. Invoke **smit** with the *-X* flag to kick the tires and get a feel for how it operates. SMIT will log the commands it would have executed in the *$HOME/smit.script* file.

```
```
# smit -X
```
```

You can also use the *F6* key within SMIT to display the actual AIX command and arguments it will invoke before committing the update. This ability to check out the commands that SMIT will execute gives new AIX System Administrators a leg up on the command syntax and structure.

# smit Versus smitty Displays

SMIT provides both ASCII and Motif-based user interfaces. The Motif interface is invoked by default on an X11 or CDE managed display and employs a point-and-click feel. The Motif display enhances the operating environment through the use of buttons, slider