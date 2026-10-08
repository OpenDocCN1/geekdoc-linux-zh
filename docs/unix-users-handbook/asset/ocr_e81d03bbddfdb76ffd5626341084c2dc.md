```
martyp $ L P D E S T=r o s 2 2 2 8
martyp $ export $ L P D E S T
martyp $ l p m b o x
Job number is: 4
martyp $
```

The **LPDEST** environment variable is normally associated with a user’s default printer. You can also specify the default printer in your startup file.

Print jobs are spooled to a printer so that you can proceed with other work. You don’t have to wait until a print job completes without a problem before you move on. You can receive an electronic mail message if there was any problem with your print job using the **-m** option as shown in the following example:

```
martyp $ l p - m t ^ { \ast }
Job number is: 5
martyp $
```

In this case, we have again sent the two files beginning with "t" to the default printer we earlier set up. You can assume this print job will complete without any problem unless you receive an electronic mail message informing you otherwise.

You would sometimes like to see the status of printers. The spooling functionality means that several files may be spooled to the printer, which means that you may have to wait for your file to print. There may only be one file ahead of yours in the print queue; however, it may be a very large file such as a report from an ERP system. To obtain the status of printers you use the **lpstat** command. I normally issue this with the **-t** option to obtain a long status listing, as shown in the following example: