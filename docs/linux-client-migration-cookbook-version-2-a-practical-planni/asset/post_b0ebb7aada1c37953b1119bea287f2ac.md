
[content]

- Configuration management that can combine with kickstart actions to enable a complex provisioning action.
- Provision applications based on RPMs.
- Kickstart configuration writer.

All options are available in the Hosted architecture. The Proxy and Satellite architectures add extras such as custom channels, integrated network installs, and much more.

Using RHN, it is possible to remote manage the Red Hat Desktop clients. For the Hosted architecture, the management is limited to the operating system and applications included in the distribution. Using the other architectures, it is possible to create channels for third-party applications.

More information about RHN is available at:

```
http://www.redhat.com/software/rhn
```

> Note: More information is also in "Red Hat satellite server and Red Hat Network (RHN)" page 257.

# Administration of Novell Linux Desktop

The preferred method to update the Novell Linux Desktop is through the use of Novell ZENworks Management. ZENworks Linux Management is based on Red Carpet Enterprise.

ZENworks offers a central system where client systems can be configured and where updates and patches can be pushed to the client. The central system resides inside the firewalls of the organization and get its content (packages) from a variety of sources including Red Carpet servers, YaST Online Update, and even Red Hat Network.

The clients connect to the server to update and patch using the rig or red-carpet programs. This connection uses the HTTP protocol. Administration is done on the ZENworks server using either a Web interface or command line commands.

The activation key that is used to activate the client actually specifies which administrators have access, which channels are available, and to which groups the client belongs.

Some of the features included in the ZENworks Linux Management are:

- Enhanced ACL - Closely related to Activation keys. Administrators, groups, or machine notifications can be associated with an activation key.
- Check pending updates - Administrators can see which clients have updates pending and the importance of these.
- Package sets - Software packages can be grouped to a set. The sets behave as packages and can have a version and dependencies.
- Ad-hoc groups - Groups can be created whenever an Administrator needs one; for example, for all machines with a certain update pending.
- Enhanced transaction - Immediate or future execution scripts can be added or rolled back.
- Set permissions - Client configuration files can be controlled from the server.
- Server-side dry run - A transaction can be tested on the server to check dependency information without taxing the client.
- Machine comparisons - Tool lists the differences between two or more clients.
- Choice of database back-end - PostgreSQL or Oracle.
- Caching server - Server that caches software on different submits.
- Enhanced mirroring tool - Tool generates package sets from product descriptions provided by mirrored servers.

The client has the following additional features:

- Multiple server support - The client can access multiple ZENWorks Management servers.
- Time-based rollback - Can be invoked locally and from the server.
- Expanded system information - The client can send hardware, software, and system information to the server.

More information about ZENWorks Linux Management can be found at:

```
http://www.novell.com/products/zenworks/linuxmanagement/
```

> Note: More information can also be found in "Novell ZENWorks Management" on page 264.

# 4.6 Desktop versus notebook considerations

While looking at differences between desktops and notebooks, not only the included hardware pieces differ, but the way of working might be different, too. Users of notebooks often work offline and therefore need to be able to synchronize their data once they are back online. Another topic in this relationship is remote connectivity through wired or wireless networks.

Not only should hardware support working in disconnected mode; the software should also have mechanisms necessary to adapt to the current connection type if necessary.

> **Planning tip:** Notebook computer users are extremely likely to fall into the advanced end of the client functional segmentation shown in Figure 3-1 on page 50. Because of this, migrating notebook users will always require an extra level of technical planning, both for hardware compatibility issues as well as application migration.

## 4.6.1 Hardware considerations

When discussing hardware support in Linux, it is important to first state that support has improved significantly in the last few years. More manufacturers see the rising demand and use of Linux both in private and corporate environments, and therefore have started to focus more resources toward delivering compatible device drivers for Linux. Unfortunately, there is still a lot to be done, especially in areas such as wireless LAN device support, or specialties as Winmodems or G-printers. Also, the open source community runs projects that develop device drivers, such as the Wlan driver for the Centrino chipset. A problem in this context is the firmware files, which are mostly closed source and so open source developers have to achieve some level of functionality for native Linux drivers.

Developments such as this have even led to ideas such as the ndiswrapper project, which enables the loading of Windows ndis drivers to run network cards under NDIS. NDIS is the Windows network driver API, and ndiswrapper allows use of this API as kernel modules in Linux. The URL of project is:

```
http://ndiswrapper.sourceforge.net
```

It is very important that the hardware types are determined during the planning stage of a client migration (see 4.1.1, "Assessing the client hardware" on page 63). Existing hardware needs more effort to get it running properly on Linux than the hardware is currently worth.

This rule applies especially for the selection of PC models. Almost every PC vendor provides a model type that is suitable for Linux. IBM provides a Web site about supported models, which can be found at:

```
http://www.ibm.com/pc/support/site.wss/MIGR-48NT8D.html
```

Regarding desktop computers, it is quite easy to determine if Linux will run without problems; all the components, such as the graphics, are known and can be checked for Linux support. Onboard components need special consideration because they likely cause problems; but even if this happens, it is possible to work around this problem, such as inserting a separate AGP card with a supported graphics chipset.

When considering notebook computers, such an exchange cannot be made, because the components cannot be removed from the motherboard. Thus, it is necessary to check Linux support for notebook models before purchasing them.

Of special concern for mobile Linux-based computers is support for power management functions. The support of the standards APM and ACPI in Linux is still lacking in some areas. ACPI has been supported in the kernel since Version 2.6; but the implementation in hardware drivers varies, resulting in problems for some users. For example, it is frequently more reliable to use APM for systems than it is to use ACPI.

> Note: One method to test hardware compatibility is to use a bootable CD-ROM image of the Linux distribution that you are considering to. These live CDs are designed for this purpose. See 3.4.5 "Hands-on Linux prior to migration" on page 59 for more details. We highly recommend that you use this method to verify existing laptop system support.

In conclusion, it is very important to pay special attention to the hardware that will be in after the migration. Additional work might be required to have a customized version of a distribution that supports all components, if it is even possible to support every component.

## 4.6.2 Peripheral extensions

When you look into the client landscape, you will recognize that many users not only have a desktop computer, but also different kinds of peripherals. Examples include:

- Locally connected printers
- Scanners
- Plotters
- Card readers
- Digital cameras

While planning the migration, it is important to assess peripheral hardware in the same way that you assess the client hardware. Considerations about that are given in 4.1.1, "Assessing the client hardware" on page 63.

Especially in cases of cheap peripherals, we recommend building a list of approved and standardized devices, and aligning this with your inventory.
