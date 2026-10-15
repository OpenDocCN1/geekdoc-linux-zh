
Using a Linux computer running Samba can be an excellent way to share printers on a network of DOS, Windows, or OS/2 computers. As described in Chapter 14, “Preparing to Share a Printer,” you can share a printer either “raw,” by using Windows drivers for the specific model you’re using, or by using Ghostscript to make the printer look like a PostScript printer to Windows. Of course, if the printer has PostScript built in, the two options produce very similar results in practice.

Printer sharing requires that you have Samba installed and running. Basic Samba configuration is covered in Chapter 11, “Samba: Sharing Files with DOS, Windows, and OS/2,” particularly in the section titled “Setting Samba Options.” This chapter helps you configure your Linux/Samba print server.

## Setting Samba Printer Options

Just as with Samba file sharing, you can configure Samba printer shares either using a GUI utility or by directly editing the /etc/smb.conf file. Unfortunately, the version of linuxconf included with Red Hat Linux 6.0 is rather fussy about the form of the printer share information in /etc/smb.conf, and the Samba printer configuration section of linuxconf doesn’t work with many configurations. You might therefore need to use the Samba Web Administration Tool (SWAT; see the sidebar on p. 262) for a GUI configuration tool for Samba. Figure 16.1 shows SWAT displaying a Samba printer share configuration.

![](img/5d4d3092919d1d16884788127447cc6d_411_0.png)

Because the GUI printer configuration options are so similar to those in the text-mode /etc/smb.conf file, I focus on the latter. If you're using a GUI configuration tool, you need only locate appropriately named options in that tool to adapt the information presented in this chapter.

## Sharing Some or All Printers

One of the most important decisions concerning printer sharing is whether you want to share some or all of your printers. Samba can extract information from the /etc/printcap file to share all your printers, much as lpd does for UNIX-style printer sharing. Alternatively, you can create separate share definitions for each printer you want to share.

To create a default share for all printers, create a share named [printers]. Samba reads the /etc/printcap file and creates a share under the first name of every printer it finds, using the options set for the [printers] share.

> NOTE
> 
> You should omit the square braces ({ }) from the share name when creating a share with a GUI tool such as linuxconf or SWAT.

> NOTE
> 
> If you use SWAT to manage a Samba configuration that includes a [printers] share, SWAT displays the names of all the printers that are included from that share. SWAT marks these autoloaded printers with asterisks (*). You can't delete them from the configuration, but you can edit them. When you do so, SWAT creates a separate share for the modified configuration, and this modified configuration overrides that of the [printers] share for that one printer.

For instance, here's a sample configuration for a default printer share:

```
[printers]
    path = /var/spool/samba
    print ok = Yes
```

The meanings of the various options are described shortly. Alternatively, suppose the server has three printers defined in /etc/printcap, but you only want to share two of them. You could create entries such as these:

```
[canon]
path = /var/spool/samba
print ok = Yes
```

```
[lexmark]
path = /var/spool/samba
print ok = Yes
```

Collectively, these two entries result in the sharing of the printers canon and lexmark. You can also use the individualized listing to set different options for the different printers. For instance, you can use the hosts allow option (p. 268) to specify which hosts can share a particular printer.

## Setting Printer Names

If you elect to use a [printers] share definition, Samba uses the first /etc/printcap name for a printer as that printer's Samba share name. Otherwise, Samba normally uses the name you place in square braces both to search for a matching /etc/printcap entry and as the share name. If you want the Samba export to be available under a name other than the Linux queue name, you can use the printer option to do so, as in the following:

```
[lexmark]
path = /var/spool/samba
printer = lp0
print ok = Yes
```

This share definition makes the Linux lp0 printer available under the name lexmark.

## Making Printers Browsable

If you want a printer to appear in the Windows Network Neighborhood, as shown in Figure 16.2, you must ensure that the share is browsable (p. 270), just as you do for file shares. There are two ways to accomplish this task:

- Place the load printers = yes option in the [global] section of your /etc/smb.conf file. Actually, yes is the default value for this parameter, so it shouldn't be necessary to specify it if you want all your printers to appear.
- Place the browsable = yes option in the individual share entries. As with load printers, the default value is yes, so you shouldn't need to adjust this parameter in most cases.
