# Linux Administration: A Beginner's Guide

+   4. Use the lpstat command to list all the printers that are present:

```
[root@fedora-server ~]# lpstat -a
Imagine-printer accepting requests since Sun 31 ... 8 PM EDT
Imagine-printer-number-2 accepting requests since Sun 31 ... 6 PM EDT
```

+   5. You can also view the printer you just added the CUPS web interface. Point your web browser to this:

```
http://localhost:631/printers
```

# Routine CUPS Administration

Setting up the printer(s) is half of the battle in managing a printing environment. The preceding section gives you enough information to get going in that regard. This section will discuss some printer administration tasks, such as deleting printers, managing the printer queue, and viewing print job statuses. We will use both the command-line tools and the web interface to manage some of these tasks.

# Setting the Default Printer

On a system with multiple print queues set, you may find it desirable to set up a particular printer (queue) as the default printer for clients to use. The default printer is the printer that is used when a printer name is not specified explicitly for printing by clients.

For example, to set up the printer named Imagine-printer-number-2 as the default printer on the system, you'd type the following:

```
[root@server ~]# lpadmin -d imagine-printer-number-2
```

# Enabling, Disabling, and Deleting Printers

Disabling a printer is like taking the printer temporarily offline. In this state, the printer queue can still accept print jobs, but it will not actually print them. The jobs are queued until the printer is put in an enabled state or restarted. This is useful, for example, when the physical print device is not working properly and the system administrator does not want to interrupt users' printing.

To disable a printer named imagine-printer-number-2, type the following:

```
[root@server ~]# cupsdisable imagine-printer-number-2
```

To enable the printer named imagine-printer-number-2, type the following:

```
[root@server ~]# cupsenable imagine-printer-number-2
```