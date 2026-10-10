
## 8-19 Multiple Print Managers

![](img/840007e8f98ea6653e5877e945c27dc6_342_0.png)

Eric activated it by loading the Print Manager software on the UASHOST server and updating the startup files. In the following activity, you use iManager to create a Print Manager for your version of the UAS network.

### Activity 8-10: Creating a Print Manager

**Time Required:** 10 minutes

**Objective:** Create and configure a Print Manager.

**Requirements:** A Windows XP or SUSE Linux 10 computer and your assigned administrative user name. If you're using a dedicated NetWare 6.5 server, you need to have loaded your NDDS Broker by completing Activity 8-7. If you're using a shared classroom server, your instructor should have already loaded the NDDS Broker.

**Description:** In this activity, you use iManager to create a Print Manager for your UAS container.

> Because the classroom server can have only one Print Manager loaded at a time, you must use the UAS_NDPS object set up by your instructor, rather than your own Print Manager object, to create printer agents.

- 1. If necessary, start your computer, and log on with your local user name and password. If you're using a Windows XP system, click to enable the **Workstation Only** check box, and enter your user name and password for logging on to the local Windows system.
- 2. If necessary, start iManager, and log on with your administrative user name and password.
- 3. Click to expand the **iPrint** heading, and then click the **Create Print Manager** link to open the Create Print Manager window shown in Figure 8-20.

![](img/840007e8f98ea6653e5877e945c27dc6_343_0.png)

**Figure 8-20 The Create Print Manager window**

- 4. Enter **UAS_PrtMgr##** (replacing **##** with your assigned student number) in the Print Manager name text box.
- 5. If your UAS container isn't displayed in the Container name text box, click the **Object Selector** button, and then click your **UAS** container.
- 6. Click the **Object Selector** button next to the Database volume text box, and click the **UASHOST_CORP** volume.
- 7. Click **OK** to create the Print Manager object, and then click **OK** to return to the iManager main window.
- 8. Click the **Exit** button on the toolbar to return to the iManager Login window.
- 9. Close your Web browser, and stay logged in for the next activity.

## Loading Print Manager Software

Before creating the other NDPS objects, both the NDPS Broker and Print Manager components need to be loaded on the NetWare server. In Activity 8-7, you learned how to use Remote Manager to load the UAS_BROKER software on the NetWare 6.5 server. In the following activity, you perform a similar process to load Print Manager software.

### **Activity 8-11: (Optional) Loading Print Manager Software**

**Time Required:** 10 minutes

**Objective:** Load Print Manager software in Remote Manager.

**Requirements:** Completion of Activity 8-7 and the Supervisor right to the NetWare 6.5 server; this activity is intended for a dedicated NetWare 6.5 server

**Description:** In this activity, you use Remote Manager to load the Print Manager you created in Activity 8-10 on the NetWare 6.5 OES server.

If you're using a shared classroom server, your instructor might demonstrate this process, as only one Print Manager can be loaded on a NetWare server.

- 1. If necessary, start your computer, and log on with your local user name and password. If you’re using a Windows XP system, click to enable the **Workstation Only** check box, and enter your user name and password for logging on to the local Windows system.
- 2. Start **Remote Manager**, and log on with your administrative user name and password.
- 3. Click the **Console Screens** link under the **Manage Server** heading to display the **Console Screens** window shown previously in Figure 8-13.
- 4. Click the **System Console** link under the **HTML Based Screen Pages** heading to display the **System Console** window.
- 5. Click in the text box above the **Execute Command Line** button and enter the **LOAD NDPSM_UAS_PrIMgr.UAS** command.
- 6. Click the **Execute Command Line** button.
- 7. Click the **Begin Refresh** button at the top left to refresh the console screen.
- 8. Close the System Console window, and click the **Exit** button to end your Remote Manager session. You can stay logged on for the next activity.

## Creating Printer Agents

As described previously, printer agents are software components that represent network printers, forming the core of the NDPS architecture; each physical printer on the network must be represented by a printer agent. Printer agents perform the following basic functions for a networked printer:

- Receive spooled output from applications running on client computers and store the output as a print job in a database on the NetWare® server
- Act as a print server by sending print jobs from the server database to the printer
- Provide printer status and control information to network clients through the **Broker**

For non-NDPS printers, such as the UAS printers, the printer agent is contained in the Print Manager software running on the NetWare 6.5 server. This software acts as a liaison between the physical network printer it represents and the client computer (see Figure 8-21).

![](img/840007e8f98ea6653e5877e945c27dc6_344_0.png)

When a user prints to a network printer, the output first goes to the printer agent representing that printer, which spools the output to a database file on the NetWare server until the printer is ready. When the printer is available, the printer agent takes a print job from the database file and then uses its assigned gateway to transmit the print job, along with any special configuration commands, to the network printer.

To spool printer output and work with other network services, a printer agent needs to be configured with basic printer information, including the physical printer’s name, make, and model and the gateway used by the printer attachment method. In addition, to access printers with IPP, printer agents need to be IPP enabled (which they are by default). When the first printer agent on a Print Manager is IPP enabled, NetWare automatically loads the IPPSRVR.NLM module to handle IPP-based printing functions. You can disable IPP printing by using the printer's Client Support option in iManager. Printer agents that aren't IPP enabled are accessible only to users who have Novell Client loaded.

Printer agents can be classified as public access or controlled access. As the name implies, **public access printers** are available to anyone with an attachment to the network. These printers are the easiest to set up because they don't require a corresponding eDirectory object. The disadvantage of public access printers is that they can't be managed from iManager and are limited to being accessed only from computers using the Novell NDPS client. **Controlled access printers** offer more security and administrative control, but for each controlled access printer, you need to create and configure an eDirectory object and then grant access to that object for users or groups. By default, the container in which a controlled access printer is located is made a user of the printer agent. For example, to allow only the IT Department to use a certain printer, Eric created a controlled access printer agent named IT_Opt_1 in the IT OU.

## Setting Up Gateways

Before creating the printer agent, you need to define a gateway for connecting the printer agent to the physical printer. As you can see in Figure 8-22, gateways are used to connect physical printers to their associated printer agents running on Print Manager.

![](img/840007e8f98ea6653e5877e945c27dc6_345_0.png)

Gateways ensure that printer agents can communicate with physical printers regardless of the attachment method or port. When you create a printer agent, in addition to selecting the Print Manager that hosts the agent, you need to identify the gateway and the physical printer's make, model, and connection information (port and address).

In addition to the local and remote attachment methods, the Novell LPR gateway supports direct (network) printer attachment. Today, most network printers are attached directly to the network cable with a special network card for the printer or a dedicated print server device, such as Hewlett-Packard's JetDirect products. Dedicated print server devices have a network port, one or more printer ports, and built-in software that enables them to receive print jobs from the network and print them on attached printers. Many high-speed laser printers have an option that includes a network card for attaching printers directly to the network cable. With the direct/network attachment method, the printer can become its own client and print jobs directly from a printer agent. Currently, only the Novell LPR gateway ships with Open Enterprise Server. This gateway handles most printers using IP. Third-party gateways are also available but must be installed from the server console before a printer agent can use them.
