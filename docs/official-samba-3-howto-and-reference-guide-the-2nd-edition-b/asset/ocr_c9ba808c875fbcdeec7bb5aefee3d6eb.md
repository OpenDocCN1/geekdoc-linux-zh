**NOTE**

Most of the following examples have been verified on Windows XP Professional clients. Where this document describes the responses to commands given, bear in mind that Windows 200x/XP clients are quite similar but may differ in minor details. Windows NT4 is somewhat different again.

# ## 20.2 Technical Introduction

Samba’s printing support always relies on the installed print subsystem of the UNIX OS it runs on. Samba is a **middleman**. It takes print files from Windows (or other SMB) clients and passes them to the real printing system for further processing; therefore, it needs to communicate with both sides: the Windows print clients and the UNIX printing system. Hence, we must differentiate between the various client OS types, each of which behave differently, as well as the various UNIX print subsystems, which themselves have different features and are accessed differently.

This chapter deals with the traditional way of UNIX printing. The next chapter covers in great detail the more modern CUPS.

**IMPORTANT**

CUPS users, be warned: do not just jump on to the next chapter. You might miss important information only found here!

It is apparent from postings on the Samba mailing list that print configuration is one of the most problematic aspects of Samba administration today. Many new Samba administrators have the impression that Samba performs some sort of print processing. Rest assured, Samba does not perform any type of print processing. It does not do any form of print filtering.

Samba obtains from its clients a data stream (print job) that it spools to a local spool area. When the entire print job has been received, Samba invokes a local UNIX/Linux print command and passes the spooled file to it. It is up to the local system printing subsystems to correctly process the print job and to submit it to the printer.