# Printing

do the opposite of what we've just described, namely, turning the Windows GUI into an X clientor display to the UNIX workstation. Such has required third-party software such as WinCenter
from Network Computing Devices.

The Open Group, through the XOrg Consortium, maintains the existing code base for
X Window System and promotes its development and standards. You can get a lot of good informa-
about X by consulting its Web site at www.x.org. You can also get information about X
at the Web site of XFree86 Project at www.free86.org. Whether obtained from these sources
or from vendors, X can help you achieve interoperability not for Windows and UNIX sys-
tems, for other platforms as well.

# 13.3 Printing

There are several permutations of configuration for printing in mixed HP-UX and Windows
2000 environments. For medium-to-large sites, network printing takes the form of using a
printer with an HP JetDirect card. For HP-UX systems, you must install the HP JetDirect soft-
wately in order to do this. For Windows 2000 systems, you either need to install the
Data Link Control (DLC) protocol (through Local Area Connection Properties) or use the
Standard TCP/IP Port Monitor (SPM). Windows 2000 print servers can contain the printer driv-
ers for Windows clients to print to JetDirect cards, but HP-UX systems must have the appropri-
ate interface model scripts installed locally. Printing to JetDirect printers is one simple way for
both Windows 2000 and HP-UX clients to share printers. Another way is to print with locally
attached printers using technology based on the old line printer daemon (LPD).

# 13.3.1 HP-UX Print Server with Locally Attached Printer

First, you must attach your printer to the HP-UX system and—if you're smart—use SAM to
configure your printer. You will also make your life easier if you attach an HP printer, since HP-
comes with interface model files for their printers. Start SAM, and then select Printers and
Plotters—>LP Spooler→Printers and Plotters→Actions→Add Local Printer/Plotter. After
selecting the appropriate interface (usually parallel), SAM will ask you for such things as the
printer name and model. As I have said, having an HP printer makes things simple, as you can
see it in the box that pops up after pressing the Printer Model/Interface button (see Figure 13–6).
Just make sure you pick the right script for your printer. Once you add your printer, SAM
will list it for you, and you can see it with the lpstat -a command.