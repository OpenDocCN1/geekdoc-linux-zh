![](bbox=[0.28, 0.14, 0.62, 0.38])

# FIGURE 16.2

Browsable printers show up in Network Neighborhood, so you can easily locate them when setting up drivers or configuring the printer.

In practice, load printers isn't of much use because the browsable value takes precedence, and it's yes by default.

Even if you set a printer to not be browsable, you can print to it from a client system; the client simply has to know the name of the share. You could use this feature to hide seldom-used variants of printers from a cluttered listing of printers—but if the printer is seldom used, hiding it might be unwise because a user might then have a hard time locating the share.

# NOTE

> After you configure a queue for a printer on the client system, there's little need to browse the printer share because the client system's queue contains the share name, and the user interacts with the local queue.

# Additional Printer Options

Setting a printer name and making the share browsable are only part of the task of sharing a printer. There are many additional options, including the following:

+   - print ok or printable—These synonymous options identify the share as a printer share, rather than a file share. One of these parameters is mandatory for printer shares. The default value is no, so Samba treats a share without this option as a file share.

+   - path—Just as with file shares, Samba needs a location associated with the share. In fact, from the client's point of view, printer sharing is just like file sharing, except that the client uses printer shares almost exclusively for saving the output from printer drivers. The standard Samba installation for Red Hat 6.0 creates an appropriate directory called