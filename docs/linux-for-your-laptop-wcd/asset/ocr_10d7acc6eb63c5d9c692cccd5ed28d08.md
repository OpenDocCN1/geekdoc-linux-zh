Linux IrDA development is a moving target, and specific procedures for enabling and using IrDA can (and most certainly will) change with each new Linux kernel. For the latest information and set of IrDA utilities, browse to

http://www.cs.ui/no/linux-irda/

A number of printers are also equipped with an IrDA port. This is a handy feature, especially for mobile Linux users, because you can print without the hassle of hooking up a print cable or logging in to a network. Several portable and desktop printers are reported to work well with Linux and the IrDA utilities. These printers include the following:

+   - Canon BJC-50, BJC-80
+   - HP 5M, 5N, 5P, 5MP, 6P, 6MP
+   - HP LaserJet 2100

# What If I Can’t Find a Printer?

If you don’t have a printer while on the road, but you need hard copy output, there are some alternatives. First, you can always pop into a local print or copy center and put your documents on diskette for reproduction or pay for access to a printer. Another alternative, albeit one that doesn’t provide the best resolution, is to fax your document to a fax machine. Linux supports sending and receiving of faxes using a number of software packages, such as efax, mgotty+sendfax, or (for SuSE Linux users) HylaFax.

> **iBook Support**
> 
> In order to use the iBook’s internal modem, you must boot Yellow Dog Linux using Apple’s OpenFirmware boot prompt and the Yaboot boot utility. You can then use the modem to send or receive faxes using Linux fax software.

If you have dial-up access to the Internet, you can try Internet worldwide fax service. Browse to http://linux.codema.com/tc/csmtp.html and read the details about how to send a fax. Using this service, you can e-mail fax documents to nearly any fax machine anywhere in the world. Sending a fax is as easy as this:

```
remote-printer.recipients_name@faxnumber.odd.tpc.int
```

In this example, the recipient’s name is the name of the person you want to receive the fax. The fax number must be a full 10-digit number. Not all U.S. area codes are