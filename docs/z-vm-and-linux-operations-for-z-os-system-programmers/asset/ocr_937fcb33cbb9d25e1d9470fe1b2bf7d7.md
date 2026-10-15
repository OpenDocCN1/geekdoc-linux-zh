```
SEND FILE
All Help Information
line 1 of 807

>>-- -SENDFile-...-! Choice A |-----------------><
`-SFIle-----' |!- Choice B |-
'-! Choice C |-

Choice A:
(1) -----------------
| (2) -----------------
| Options |---
'-! -----------------

Choice B:
PF1= Brief 2= Top 3= Quit 4= Return 6= ?
PF7= Backward 8= Forward 9= PFkeys 10= 11= Related 12= Cursor

=====> _

Figure 2-8 Output of the command help cms sendfile (detail)
```

RELATED

The help information entries for some commands allow you to select help entries for similar commands; this is known as related help.

For example, suppose you want to remove a file from your rdrlist. After reading HELP ERASE, you realize that ERASE is not the correct command. Instead, using the RELATED layer of the ERASE command lets you easily access the help file for the correct command, DISCARD.

When you request related help on the SET or QUERY commands, the window lists and briefly describes all the SET and QUERY operands available for the system component. You can directly access help information about any of the displayed operands from these menu windows by positioning the cursor on a particular operand and pressing Enter.

The following example requests related help for the ERASE command in the CMS environment:

help cms erase (related