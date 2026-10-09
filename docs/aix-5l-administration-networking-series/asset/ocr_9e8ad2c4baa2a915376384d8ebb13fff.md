The terminfo database describes the characteristics for each different printer type. This database information is used by the **lpsech** daemon in the job screening process. Then the printer is initialized using the same information in the terminfo database.

If the job is not rejected in the job screening process, the job is given a unique ID by the **lpsech** daemon. Each a *request file* describing the print job is created in the print spooler directory. Each print job ID consists of two parts: the printer’s name and the unique ID number. Printers are sometimes grouped into *classes* of printers. Using printer classes, a user can submit a print job to a class of printers, and the job will be queued to the first printer in the class that is capable of printing the job. This is more efficient if you have a pool of printers in a centralized location.

The System V printer subsystem uses two types of filters to perform three separate functions. The first filter function is used in converting file content, which may include adding carriage returns and line feeds or character mapping. The second filter function is used to decipher special user-requested printer modes, such as reversing the page order or changing between landscape and portrait modes. The third filter is used to detect printer faults. The two types of filters are *slow* and *fast* filters. The slow filters are run directly by the **lpsech** daemon in the background for file conversion. The slow filters are run in the background because of the high overhead they produce converting files. The fast filters act on the printer directly. The fast filters directly control the printer and in some cases run file conversions as slow filters do. Fast filters are executed by the interface program, but the interface program is controlled by the **lpsech** daemon. The **lpsech** daemon may use a combination of several different filters to get the desired result.

As a print job reaches the head of the print queue, the **lpsech** daemon passes control of the print job over to the interface program defined for the specific printer. The interface program, which is just a shell script, then takes direct control of the printer. The interface program then initializes the printer using the terminfo database information, then uses a fast filter to print the banner page (if a banner page has been defined), and finally uses a fast filter to print the specified number of copies of the file.

# ## System V Printing Lingo

The System V print subsystem is confusing to the AX specialists because of the terminology. For example, there are at least three different *types*. There are the *printer type*, the *interface type*, and the *content type*. Please refer to Table 12-5. The *printer type* points the printer to an entry in the terminfo database. The **lpadmin** command is used to set the printer type. There are two default printer types, postscript (PS) and standard. The syntax to specify a printer type is

```
# lpadmin -T (PS, standard) .
```

The *interface type* is just a pointer to the interface program used for a particular printer.