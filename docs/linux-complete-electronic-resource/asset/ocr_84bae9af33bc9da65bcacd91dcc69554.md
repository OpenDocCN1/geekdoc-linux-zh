More information about FiberTel can be found at `http://www.fibertel.com.ar`.

# # Videotron, Canada

I don't have much information about Videotron except the fact that they use DHCP for the assignment of IP addresses and other networking information. Just read the DHCP mini-HOWTO (see Chapter 11) and configure your system appropriately. There is no other necessary configuration.

Here is additional information from Mihai Petre `<mihai@videotron.ca>`:

> Yes, they are using DHCP for the TCP settings. They have also included DHCPd on their FTP server at `ftp://ftp.videotron.ca/pub/linux/`. Of course, the tech support cannot help you with the Linux-related stuff.
> They don't allow setup of any kind of servers on your machine (on ports 80, 21, 110, 25) so the only thing is to use some exotic ports.

Information about Videotron can be found at `http://www.videotron.ca`.

# ## Telekom (Teleweb), Austria

The following information is from Andreas Kostyrka.

> The Austrian Telekom (Teleweb) ISP works with Linux. It seems quite similar to MediaOne Express (`3c509+dhcp`, etc.).
> 
> There are 3COM configuration utilities for Linux (but don't fool around with them on a busy system; `3c509` may lock the bus if touched the wrong way):
> 
> * `ftp://ftp.redhat.com/pub/contrib/hurricane/SRPM/3c5x9utils-1.0-3.src.rpm`
> * `ftp://ftp.redhat.com/pub/contrib/readmes/3c5x9utils-1.0-1.READMIE`
> 
> Information about Telekom can be found at `http://www.telekom.at/`.