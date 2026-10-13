Granting or modifying the rights that user jsmith has to the SYS:groups\acctg directory can be accomplished with the following command:

```
xnwborightsDD -o /NetWare/bindery/OPENLINUX/objects/JSMITH -p
/NetWare/bindery/OPENLINUX/volumes/SYS/groups/acctg
```

After the graphical utility comes up, you can modify the rights by clicking the appropriate radio buttons and clicking the Modify Rights button.

> > **Note**  
> > Treat the Change option as the Create right for both of the previously listed utilities.

# PROJECT: USING THE ncpfs PACKAGE

Of all the Linux flavors available today, Caldera’s OpenLinux is the first, and only, implementation that offers a commercial and fully licensed NetWare client and server that supports the latest Novell standards, including support for NDS—it is not too surprising since Caldera was founded by Ray Noorda, the former CEO of Novell. However, what can you do to access NetWare resources if you don’t have OpenLinux? The ncpfs package developed by Volker Lendecke is your answer! The ncpfs package allows Linux machines to mount volumes on network-connected NetWare file servers. ncpfs also include tools that allow printing to and from NetWare by Linux clients.

> > **Note**  
> > For the latest version of ncpfs, you must use kernel 1.3.71 or newer; this includes the 2.0.* kernels. If you are using a kernel that is version 1.3.71 or newer, then the ncpfs kernel code has been included in the standard kernel distribution. You need only answer Y to the prompt:
> >
> > ```text
> > Networking options  -->
> >     ...
> >     <*> The IPX protocol
> >     ...
> > Filesystems  -->
> >     ...
> >     <*> NCP filesystem support (to mount NetWare volumes)
> > ```
> >
> > and you can start at Step 5 below.

Use the following steps to use ncpmount to access your NetWare server:

+   1. Download Volker’s ncpfs package, which is available prepackaged in most modern Linux distributions or in source form from `ftp://ftp.gwdg.de/linux/misc/ncpfs/` or from `ftp://sunsite.unc.edu` or mirror sites. The version current at the time of writing is `ncpfs-2.0.11.tgz` or `ncpfs-2.2.0.tgz`, which adds the NDS support.