# ## Starting Ethereal

To start Ethereal, choose Programs \u003e Internet \u003e ethereal, or type the following (as root user) from a Terminal window:

```
```bash
# ethereal &
```
```

The Ethereal window appears, as shown in Figure 15-13. (If the `ethereal` command is not found, the package is probably not installed. You can install the ethereal package from the Red Hat Linux installation CD-3.)

![](bbox=[0.06, 0.25, 0.81, 0.65])

The primary function of Ethereal is to take a snapshot of the packets coming across your network interfaces and display that data in the Ethereal window. You can filter the data based on a variety of filter primitives. When the capture is done, you can step through and sort the data based on the values in different columns. Optionally, you can save the captured data to a file to study the data at a later time.

> **TIP:** If you can’t use Ethereal because you don’t have a GUI available, you can use the `tcpdump` command from the shell. It is not as friendly as Ethereal, but it supports the same filtering syntax. Because `tcpdump` can produce a lot of output, you will probably want to use some form of filtering and/or direct the output of the command to a file. (Type `man tcpdump` for information on filter options.)