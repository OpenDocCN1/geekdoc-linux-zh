# The CUPS Print Server

The Samba server software also allows you to share any system printers you have configured on the Ubuntu server on your Windows network. As discussed earlier in the “Creating a Samba Server” section, it’s easier to utilize the common UNIX printing system [CUPS] software on your Ubuntu server to interface between your system printers and Samba.

This section walks through the CUPS software and demonstrates how to use CUPS to define the printers on your system for Samba.

# Printing in Linux

One of the reasons printing in the Linux world is complicated is that, like everything else in Linux, there is more than one way of doing it. But before tackling how to use CUPS, let’s first look at how printing works in Ubuntu.

# Direct Printing

The most basic type of printing involves an application sending information directly to a printer that’s connected to the PC. This is called direct printing. With direct printing, printer data are sent from an application to a printer handler then directly to the printer. No data formatting or manipulation is performed by the Ubuntu system. In Ubuntu there are two printer applications you can use for direct printing: System V and Berkeley LPD.

Both of these systems have their roots in the old UNIX days, so you know they are complicated. In the past, you had to know exactly which print system your particular Linux distribution used and had to manually edit configuration files to get a printer to work. That was a painful process to go through to get a printer to work.

First, you had to know what port on the PC your printer was connected to. Second, you had to know what data format your printer used to accept data for printing.

In the Windows world you usually don’t have to know these things, because the operating system usually figures them out automatically for you. But with direct printing in Linux we are not so lucky.

There are several ways to connect printers to a PC, such as through the standard printer ports LPT1 and LPT2 and through standard USB ports. Also, to make life more interesting, in Linux, parallel printers are called lp0, lp1, and so forth (note that the first printer starts at 0, not 1, as in Windows). When a Linux application uses direct printing, it needs to know exactly where the printer is connected. Of course, if you move the printer, you must also configure the application accordingly.

With the thousands of different types of printers available, it’s hard to know the data format a specific one uses. In fact, most use proprietary languages to format print data. Therefore, each application on your PC needs to know what format to use when sending data to a specific printer. Fortunately, Linux geeks developed a solution to this problem.

# Filtered Printing

The geeks’ solution to direct printing problems in Linux was to create an intermediary between printers and applications. It’s called a filter. The job of the filter is to convert raw data sent from an application into data that a printer can use.

Each type of printer requires a unique filter configuration. So, in order to work, filter configurations have to contain information about the connected printer. Linux systems often include many different filter configurations for various types of printers.