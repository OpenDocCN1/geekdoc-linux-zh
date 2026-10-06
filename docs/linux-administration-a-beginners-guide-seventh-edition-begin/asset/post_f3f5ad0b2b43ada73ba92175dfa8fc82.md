
## Using Client-Side Printing Tools

When a client machine prints, the job is sent to the printer server and is spooled. Spooling is simply the act of putting a print job into the printer queue—this is also known as a print job. A print job can be in different states, such as in progress, paused (for example, where the administrator has paused printing to refill the paper tray), or cancelled (where the job has been manually cancelled for whatever reason). When something goes awry with the printer, print jobs can queue up and create a problem when the printer comes back.

In this section, we'll look at some commands that can be used to print and manage queues. We cover the end user's (client) view and interaction with the printing system.

## lpr

The lpr command is used to print documents. Most PostScript and text documents can be printed by directly using the lpr command. If you are using a stand-alone application (such as AbiWord, KOffice, LibreOffice, GIMP, OpenOffice, and so on), you might have to set those applications to print to the correct device.

Let's create a plain-text file that we will attempt to print. The file will contain the simple text "Hello Printer" and be named test-page.txt.

1. While logged into the system as an unprivileged user (for example, the user yangang), type the following:
```bash
yang@client ~$ echo "Hello Printer" >> test-page.txt
```
2. Find the name of the default printer configured on the system:
```bash
yang@client ~$ lpstat -d
system default destination: Imagine-printer
```
3. Send the test-page.txt file to the default printer:
```bash
yang@client ~$ lpr test-page.txt
```
This will print/send the document test-page.txt to the default printer, which is usually the first printer that was installed.
4. Now send the same document to the other imaginary printer that was installed earlier, the printer named Imagine-printer-2:
```bash
yang@client ~$ lpr -P Imagine-printer-number-2 test-page.txt
```

Once you have entered this command, the printer should start printing fairly quickly, unless you are printing a large file.
To see the status of your print job, use the lpq command (discussed next).

## lpq

After you have submitted the job, you can view what is on the print spooler by using the **lpq** command. If you've just printed a job and notice that it doesn't come out of the printer, use the **lpq** command to display the current list of jobs that are spooled on the printer. Typically, you'll see a bunch of jobs in queue, and upon further investigation, you may discover that the printer is out of paper. If you unspool the print job from the printer, you can use the **lprm** command, discussed in the next section.

For example, to see the status of the print request that was sent to the default printer, type this:

```bash
yyang@client -$ lpq -av
```

To view the status of the print job sent to the second printer, type this:

```bash
yyang@client -$ lpq -av -P Imagine-printer-number-2
```

It's either your fault or yours (because you didn't use your **imagination** well enough!), if both jobs are stuck in the imaginary queue or if you don't see any physical pages being printed. Regardless of whose fault it is, we'll remove the print jobs next.

## lprm

If you suddenly realize that you didn't mean to print the document you just printed, you might have a chance to delete it before it gets printed. To do this, use the **lprm** command. This will unspool the print job from the printer.

For example, to delete the print job that you created with an ID of 2 from the default printer, type this:

```bash
yyang@client -$ lprm 2
```

To remove a job from a specific printer, simply add the **-P** option. For example, to remove the job with an ID of 2 from the printer named Imagine-printer-number-2, type this:

```bash
yyang@client -$ lprm 2 -P Imagine-printer-number-2
```

If you are the root user, you can purge all print jobs from the printer **imagine-printer** by issuing the **lprm** command:

```bash
root@server -$ lprm -P imagine-printer
```

The dash (-) at the end of this command means "all jobs."

## CHAPTER 26 Printing

TIP Regular users can typically manage only their own print jobs—that is, user A cannot ordinarily go and delete a job submitted by user B from the print queue. The superuser, of course, control everybody's print jobs. Also, you should understand that the window of sending a job to the printer and being able to delete it is very narrow. Therefore, you may find that the lprm request fails because the command was issued too late. This will usually result in an error such as, "lprm: Unable to lprm job(s)". As root, you may, of course, use the dash (–) option to clear the print queue of all jobs at any time.

## Summary

This chapter discussed the Common UNIX Printing System (CUPS) and touched on simple printer management tasks, such as adding printers via the CUPS web interface and from the command line, managing printers.

Usage of common tools to Linux was discussed, with examples provided.

## CHAPTER 29 Dynamic Host Configuration Protocol (DHCP)

## Linux Administration: A Beginner's Guide

Manually configuring IP addresses for a handful of systems is a simple task. However, manually configuring IP addresses for an entire department can be daunting.

The DHCP (Dynamic Host Configuration Protocol) client and server assist with these tasks. The client machine is configured to obtain its address from the network. When the DHCP client software is started, it broadcasts a request onto the network for an address. If all goes well, a DHCP server on the network will respond, issuing an address and other information to the client.

Such dynamic is also useful for mobile or transient machines. Users who travel from office to office can plug their machines into the local network and obtain an address for their location.

This chapter covers the process of configuring a DHCP server and client. It includes obtaining and installing the necessary software and walking through the process of writing a configuration file for it. At the end of the chapter, we'll step through a complete configuration.

> NOTE DHCP is a standard. Thus, any operating system or device that conforms to this standard, theoretically, be operable with a Linux-based DHCP server or client. One common solution using a Linux-based DHCP server in office environments with a large number of Windows-based clients. The Windows systems can be configured to use DHCP and contact the Linux server to get their IP addresses. The Windows clients will not necessarily know or care that their IP information is being provided by a Linux server, because DHCP is a standards-based protocol.

## The Mechanics of DHCP

When a client is configured to obtain its address from the network, it asks for an address in the form of a DHCP request. A DHCP server listens for client requests. Once a request is received, it checks its local database and issues an appropriate response. The response can include any combination of an IP address, name servers, network mask, default gateway, and so on. The client accepts the response from the server and configures its settings accordingly.

The DHCP server maintains a list of addresses it can issue. Each address is issued with an associated lease, which dictates how long a client is allowed to use the address before it must contact the server to renew the lease. When the lease expires, the client is not expected to use the address any more. As such, the DHCP server assumes that the address has become available and can be put back in the server's pool of addresses.
