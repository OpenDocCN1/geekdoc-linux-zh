
clients ask the server to suspend, cancel, or reprioritize jobs. They can also move jobs from one queue to another.

Most changes require jobs be identified by their job number, which you can get from lpq. For example, to remove a print job, just run lprm jobid.

lpstat -t summarizes the print server's overall status.

## Multiple printers and queues

The CUPS server maintains a separate queue for each printer. Command-line clients accept an option (typically -P printer or -p printer) to specify which queue you want to address. You can also set a default printer for yourself by setting the PRINTER environment variable

```
$ export PRINTER=printer_name
```

or by telling CUPS to use a particular default for your account.

```
$ lpoptions -dprinter_name
```

When run as root, lpoptions sets system-wide defaults in /etc/cups/lpoptions, but it's more typically used by individual, nonroot users. lpoptions lets each user define personal printer instances and defaults, which it stores in ~/.lpoptions. lpoptions -l lists the current settings.

## Printer instances

If you have only one printer but want to use it in several ways—say, both for quick drafts and for final production work—CUPS lets you set up different "printer instances" for these different uses.

For example, if you already have a printer named Phaser_6120, the command

```
$ lpoptions -p Phaser_6120/2up -o number-up=2 -o job-sheets=standard
```

creates an instance named Phaser_6120/2up that performs 2-up printing and adds banner pages. Once the instance has been created, the command

```
$ lpr -P Phaser_6120/2up biglisting.ps
```

prints the PostScript file biglisting.ps as a 2-up job with a banner page.

## Network printing

From CUPS' perspective, a network of machines isn't very different from an isolated machine. Every computer runs a cupsd, and all the CUPS daemons talk to one another.

If you're working on the command line, you configure a CUPS daemon to accept print jobs from remote systems by editing the /etc/cups/cupsd.conf file (see Network print server setup on page 1039). By default, servers that are set up this way broadcast information every 30 seconds about the printers they serve. As a result, computers on the local network automatically learn about the printers that are available to them. You can effect the same configuration by clicking a check box in the CUPS GUI in your browser.

If someone has plugged in a new printer, if you’ve brought your laptop into work, or if you’ve just installed a new workstation, you can tell cupsd to look and see what’s out there by clicking on the Find New Printers button in the Administration tab of the CUPS GUI.

Because broadcast packets do not cross subnet boundaries, it’s a bit trickier to make printers available to multiple subnets. One solution is to designate a slave server on each subnet that polls the other subnets’ servers for information and then relays that information to machines on the local subnet.

For example, suppose the print servers allie (192.168.1.5) and jj (192.168.2.14) live on different subnets and we want both of them to be accessible to users on a third subnet, 192.168.3. We designate a slave server (say, copeland, 192.168.3.10) and add these lines to its cupsd.conf file:

```
BrowsePoll allie
BrowsePoll jj
BrowseRelay 127.0.0.1 192.168.3.255
```

The first two lines tell the slave’s cupsd to poll the cupsd s on allie and jj for information about the printers they serve. The third line tells copeland to relay the information it learns to its own subnet. Simple!

Need a more sophisticated setup? Multiple queues for one printer, each with different defaults? A single server that load-balances by parceling out jobs to several printers? Multiple servers that each handle interchangeable instances of the same kind of printer? lpd or Windows clients? There’s too much variation to go through here, but CUPS handles all these situations, and the documentation can walk you through the details. (See the section on documentation, starting on page 1083.)

## Filters

Rather than using a specialized printing tool for every printer, CUPS uses a chain of filters to convert each printed file into something the printer can understand.

The CUPS filter scheme is elegant. Given a document and a target printer, CUPS uses its .types files to figure out the document’s MIME type. It consults the printer’s PPD file to figure out what MIME types the printer can handle. It then uses the .convs files to deduce what filter chains could convert one format to the other, and what each prospective chain would cost. Finally, it picks a chain and passes the document through those filters. The final filter in the chain passes the printable format to a back end, which transmits the data to the printer through whatever hardware or protocol the printer understands.

Let’s flesh out that process a bit. CUPS uses rules in /etc/cups/mime.types to suss out the incoming data type. For example, the rule

```
application/pdf pdf string (0.%PDF)
```
