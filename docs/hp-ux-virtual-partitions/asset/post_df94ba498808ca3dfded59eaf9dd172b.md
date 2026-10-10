
see their contents. These files contain the information about all of the software you have loaded as part of your Ignite-UX depot.

The `manage_index` command is required to manage the index file used by Ignite-UX, as shown in the following example:

```
# /opt/Ignite/bin/manage_index -a -f /var/opt/Ignite/data/Rel_B.11.00/app.cfg
```

We have now set up the core operating system depot using the Ignite-UX graphical interface and the application depot using the three Ignite-UX commands at the command line. You now also have an entry for your release of the operating system in `/var/opt/Ignite/INDEX`. This is a file you will want to view so that you can see the entry made for your release of the operating system.

Let's now get back to using the Ignite-UX graphical interface on the server. We can get information about a specific client through the Ignite-UX interface on the server. The window that appears on the server is shown in Figure 10-10 for the client we'll be booting through Ignite-UX:

![](img/eff8b9287a5f38c5adf538f24aacf29e_597_0.png)

*Figure 10-10* Information about Client

Now that we've created both a core operating system and applications depot, we can boot and load one of our clients through Ignite-UX on the server.

In addition to controlling the client as we have done using the Ignite-UX graphical interface in “push” fashion from the server, you can also work from the client in “pull” fashion. In order to boot the client from the server while sitting at the server, you would issue the following command from PDC (Processor Dependent Code; see Chapter 1) after interrupting the boot process:

```
BOOT ADMIN> boot lan 15.32.163.26 install
```

The IP address specified is that of the server, where we set up the software depot. While sitting at the client, you would see the Ignite-UX interface in character mode and proceed with the installation while sitting at the client using the software depot we set up on the server.

Getting back to the GUI, we select the software we wish to load through the familiar Ignite-UX interface that is part of any initial operating system load as shown in Figure 10-11:

![](img/eff8b9287a5f38c5adf538f24aacf29e_598_0.png)

Figure 10-11 Selecting Software to Load on Client

Notice in Figure 10-11 that we are in the Software tab at the top of the screen. We'll progress through the System and File System tabs in two upcoming figures. Remember, all of this work is being done on the Ignite-UX server we set up.

We have selected a Java product that was part of the applications depot we created in Figure 10-11. The core operating system and other software selections were also made in the Software window.

In addition to the software load, we can also perform additional configuration on the server for the client we are loading, such as providing the system name under the System tab as shown in Figure 10-12:

![](img/eff8b9287a5f38c5adf538f24aacf29e_599_0.png)

Figure 10-12 Set Up the Client System

Next we can perform file-system-related configuration under the File System tab as shown in Figure 10-13:

![](img/eff8b9287a5f38c5adf538f24aacf29e_600_0.png)

After we have completed all of our initial work in the Ignite-UX for the client while working on the server, we can proceed with the client load. Figure 10-14 shows two Ignite-UX windows that appear on the server when we begin configuring and loading the client:

![](img/eff8b9287a5f38c5adf538f24aacf29e_601_0.png)

Figure 10-14 Status of Client Load

The leftmost window in Figure 10-14 shows the icon for the system we are working on and the rightmost window provides the status of the client load. Since we are working on only one system, only one icon appears in the leftmost window. The status of the software load in the rightmost window indicates that *Load the software* is an **ACTIVE** process. Several processes have been **COMPLETE**, and several others are **PENDING**.

*Although you can't see the colors in the original screen shot, the status messages are color-coded.*

There is substantially more that you can accomplish with Ignite-UX, such as grouping the configuration files into sets that you can select when loading clients, installing patch depots, and many other useful tasks. The *Ignite-UX Administrator Guide* at www.docs.hp.com covers many additional topics.

From the procedure we performed in this section, however, you can see how easy it is to create software depots and manage clients.

## System Recovery with Ignite-UX

Ignite-UX is a product bundled with HP-UX 11i that provides a process to create a bootable system recovery tape. The tape contains a boot area and an operating system archive. Should your root disk fail or corruption of the root disk take place, you can recover using the bootable system recovery tape.

**make_recovery** is the Ignite-UX tool that is used to create the bootable system recovery tape. **make_recovery** is being replaced by **make_net_recovery** at the time of this writing but **make_recovery** will be used throughout this section because the **check_recovery** function covered in this section was not yet implemented with **make_net_recovery**. You could boot and restore from the system recovery tape and then use your system backup to fully restore the system. If your root disk were to fail, in a non-mirrored environment, you would perform the following steps to recover from the failure:

- Replace the defective root disk.
- Boot from the recovery tape by selecting the tape device.
- Monitor the restoration of the operating system archive from the recovery tape.
- Restore the balance of data on the system with backup information.

The bootable system recovery tape consists of both a Logical Interchange Format (LIF) volume as well as the operating system archive. The LIF volume contains all the components necessary to boot from the tape. The operating system archive contains only the core operating system by default.

You can include additional files in the operating system archive, if you wish, using two different techniques. The first is to edit the file /var/opt/ignite/recovery/makrec.append and add to it the file name, directory name, or software distributor product name you wish to include in the operating system archive. The second technique is to run **make_recovery** in preview mode with the -p option, manually add files to include and/or exclude from the archive, and resume **make_recovery** with the -r option. The manual pages for /opt/ignite/bin/make_recovery and /opt/ignite/bin/ignite are online on your HP-UX system.

You can also determine whether your recovery tape is up-to-date by using the **check_recovery** command. Running **make_recovery** with the -C option produces a system recovery status file. **check_recovery** compares the system recovery status file to the current state of the system and produces a list of discrepancies. From this list you can determine whether or not you should produce another system recovery tape. The manual page for **/opt/ignite/bin/check_recovery** is online on your HP-UX system.

The recovery feature is only one component of the Ignite-UX product. Ignite-UX provides a means to install systems over the network by either pushing the installation to a client from an Ignite server or pulling the installation from the Ignite server to the client. With Ignite-UX, “golden images” of your standard installation setup can be created and systems can be set up in a matter of minutes by “igniting” them from this image over the network. More information about Ignite-UX can be viewed on the Internet at *http://www.software.hp.com/products/IUX* and read about in the “Configuring an Ignite-UX Server” and “Installing from the Ignite-UX Server” chapters as well as Appendix C: “Ignite-UX System Administration” of the *Installing HP-UX 11.0 and Upgrading 10.x to 11.0* manual from Hewlett-Packard. The “HP-UX System Recovery” chapter of the same manual gives additional information about the **make_recovery** feature of Ignite-UX.

## An Example of Creating a Bootable System Recovery Tape

Now that we have covered the basic components and capabilities of the Ignite-UX recovery process, let's look at an example of creating a bootable system recovery tape.

Let's first run **make_recovery** with the *-p* option so that we can see the way Ignite-UX reports the information it is including on the tape. I'll also use the *-A* option, which specifies that the entire root volume group is to be included. I sometimes use **make_recovery** to clone identical systems by producing a recovery tape with the *-A* option and then loading the tape on systems that I want to be identical to the original system. You would not use the *-A* option if you have a large root volume group or if you perform normal backups and don't need to include all root volume group information on the recovery tape. In addition to *-p* for preview and *-A* for all, I'll also use the *-v* for the verbose option and *-C* to create the system status file in the following preview command example:
