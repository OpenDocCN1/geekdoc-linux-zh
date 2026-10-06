In the web interface, you can add a class (you will be prompted for its name, location and description, which can all be arbitrary). You then add printers to the class from the list of printers that CUPS already knows about. Figure 19-10 shows adding a class in the CUPS interface.

![](bbox=[0.181, 0.226, 0.692, 0.535])

**Figure 19-10:** Adding a class in the CUPS web interface

After the class is set up, the CUPS server offers the class as a print queue. From a client you can then select that queue to print in the YaST printer module (see Figure 19-11).

For example, if you are configuring a Windows system to print to the class queue called *sales*, you would choose `http://hatter:631/printers/sales`.

# Allow Remote Access to the CUPS Web Interface

As we mentioned earlier in the chapter, by default, CUPS does not allow you to log into its web interface from a remote location. If you want to change this, you have to edit the file `/etc/cups/cupsd.conf`. In the section starting

```
<Location /adminn
```

add a line

Allow from @LOCAL