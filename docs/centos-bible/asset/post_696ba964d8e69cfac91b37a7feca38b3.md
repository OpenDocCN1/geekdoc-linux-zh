
# Part IV

## Networking

In this chapter, descriptions of how Internet domains are organized built on the coverage of IP addresses in the previous chapter. Creating dial-up connections to the Internet focused on descriptions of PPP. This chapter also discussed several different techniques for connecting your LAN to the Internet. You can set up your Linux computer as a router or as a Squid proxy server.

To use your Internet connection to transport sensitive data to another location in your company's private network, you can configure a VPN. This chapter describes how to use IPsec in CentOS to create a VPN connection between two locations.

# Chapter 16

## Setting Up Printers and Printing

Sharing printers is a good way to save money and make your printing more efficient. Very few people need to print all the time, but when they do want to print something, they usually need it quickly. Setting up a print server can save money by eliminating the need for a printer at every workstation. Some of those savings can be used to buy printers that can output more pages per minute or have higher-quality output.

You can attach printers to your CentOS system to make them available to users of that system or to other computers on the network. You can configure your CentOS printer as a remote CUPS printer or Samba printer. With Samba, you are emulating a Windows print server.

This chapter describes configuring and using printers in CentOS. It focuses on Common UNIX Printing Service (CUPS), which is the recommended print service for the current versions of CentOS. To configure CUPS printers, this chapter focuses on the Printer Configuration window (`system-config-printer` command).

When a local printer is configured, print commands (such as `lpr`) are available for carrying out the actual printing. Commands also exist for querying print queues (`lpq`), manipulating print queues (`lpc`), and removing print jobs (`lprm`). A local printer can also be shared as a print server to users on other computers on your network.

### IN THIS CHAPTER

- Understanding printing in Linux
- Setting up printers
- Using printing commands
- Managing document printing
- Sharing printers

## Common UNIX Printing Service

CUPS has become the standard for printing from Linux and other UNIX-like operating systems. Instead of being based on older, text-based line printing technology, CUPS was designed to meet today's needs for standardized printer definitions and sharing on IP-based networks (as most computer networks are today). Here are some features of CUPS:

- **IPP** — At its heart, CUPS is based on the Internet Printing Protocol (IPP) (www.pwg.org/ipp), a standard that was created to simplify how printers can be shared over IP networks. In the IPP model, printer servers and clients who want to print can exchange information about the model and features of a printer using the HTTP protocol. A server can also broadcast the availability of a printer, so a printing client can easily find a list of locally available printers.
- **Drivers** — CUPS also standardized how printer drivers are created. The idea was to have a common format that could be used by printer manufacturers that could work across all different types of UNIX systems. That way, a manufacturer had to create the driver only once to work for Linux, Mac OS X, and a variety of UNIX derivatives.
- **Printer Classes** — Using printer classes, you can create multiple print server entries that point to the same printer or one print server entry that points to multiple printers. In the first case, multiple entries could each allow different options (such as pointing to a particular paper tray or printing with certain printer sizes or margins). In the second case, you could have a pool of printers so that printing is distributed. This would decrease the occurrence of congested print jobs, caused by a malfunctioning printer or a printer that is dealing with very large documents.
- **UNIX Print Commands** — To integrate into Linux and other UNIX environments, CUPS offers versions of standard commands for printing and managing printers that have been traditionally offered by UNIX systems.

The Printer Configuration window (`system-config-printer` command) lets you configure printers in CentOS that use the CUPS facility. However, CUPS also offers a Web-based interface for adding and managing printers. Configuration files for CUPS are contained in the `/etc/cups` directory. In particular, you might be interested in the `cupsd.conf` file (which identifies permission, authentication, and other information for the print daemon) and `printers.conf` (which identifies addresses and options for configured printers).

## Setting Up Printers

Most parallel printers and USB printers can be detected and set up using the Printer Configuration window. However, the Printer Configuration window also lets you configure CentOS so that you can use printers that are available on your LAN as a Windows printer (Samba), Apple-Socket or HP JetDirect, Internet Printing Protocol (IPP) printer, or UNIX printer (LPD or LPD daemons).

### Choosing a Printer

If you are choosing a new printer to use with your CentOS system, look for one that is PostScript-compatible. The PostScript language is the preferred format for Linux and UNIX printing and has been for many years. Every major word and image processing application that runs on Linux and UNIX systems supports PostScript printing.

If you get a PostScript printer and it is not explicitly shown in the list of supported printers, simply select the PostScript filter when you install the printer locally. No special drivers are needed.

Your next best choice is to choose a printer that supports PCL (Hewlett Packard’s Printer Control Language). In either case, make sure that the PostScript or PCL is implemented in the printer hardware and not in the Windows driver.

When selecting a printer, avoid those that are referred to as Winprinters. These printers use nonstandard printing interfaces (those other than PostScript or PCL). Support for these low-end printers is hit-or-miss. For example, some low-end HP Deskjet printers use the `pnm2ppa` driver to print documents in Printing Performance Architecture (PPA) format. Some Lexmark printers use the `pbm2ilk` driver to print. Although drivers are available for many of these Winprinters, many of them are not fully supported.

Ghostscript may also support your printer; if it does, you can use that tool to do your printing. Ghostscript (www.ghostscript.com) is a free PostScript and PDF file interpreter program. It can convert that content to output that can be interpreted by a variety of printers. With the ghostscript package installed, type `gs -h` to see a list of available output device formats.

You’ll find an excellent list of printers supported in Linux at the Free Standards Group OpenPrinting site (www.linux-foundation.org/en/OpenPrinting). I strongly recommend that you visit that site before you purchase a printer to work with Linux. The site offers a Printer Compatibility database, so you can find out if your printer is supported and, if so, what print driver is needed to get your printer working in Linux. For useful information on purchasing a printer that will work in Linux, refer to the “Supported Printers” section of the Printing HOWTO (www.tldp.org/HOWTO/Printing-HOWTO/printers.html).

### Using the Printer Configuration Window

To install a printer from your desktop, use the Printer Configuration window (`system-config-printer` command). This tool enables you to add printers, delete printers, and edit printer properties. It also lets you send test pages to those printers to make sure that they are working properly.

The key here is that you are configuring printers that are managed by your print daemon (`cupsd` for the CUPS service). After a printer is configured, users on your local system can use it. Following that, you can refer to the “Configuring Print Servers” section to learn how to make the server available to users from other computers on your network.
