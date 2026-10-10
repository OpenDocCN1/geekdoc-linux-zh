enumdosers

Enumerate domain users

enumdomgroups

Enumerate domain groups

enumalsgroups

Enumerate alias groups

createdoser

Create domain user

saookupnas

Look up nas

saookuprids

Look up nas

deletedoser

Delete domain user

samquerysecojb

Qyery SAMR security object

getdompwinfo

Retrieve domain password info

lookupdomain

Look up domain

# **SPOOLSS**

adddriver <arch> <config> [<version>]

Execute an AddPrinterDriver() RPC to install the printer driver information on the server. Note that the driver files should already exist in the directory returned by getdriverdir. Possible values for *arch* are the sa as those for the getdriverdir command. The *config* parater is defined as follows: