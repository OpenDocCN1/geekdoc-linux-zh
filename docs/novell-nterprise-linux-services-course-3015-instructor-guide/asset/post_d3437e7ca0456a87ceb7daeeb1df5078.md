
## Locate iPrint Files

During a default installation, the following iPrint directories and files are created:

1. `/var/opt/novell/http/htdocs/ippdocs`
2. `/var/opt/novell/iprint`
3. `/var/opt/novell/log/ipsmd.log`
4. `/etc/opt/novell/iprint/ipsmd.conf`

The `/var/opt/novell/http/htdocs/ippdocs` directory holds items such as the list of available print drivers (`iprint.ini`) and printer maps.

The `ipsmd.log` and `ipsmd.conf` files are the log and configuration files for the iPrint daemon (`ipsmd`).

## Install the iPrint Client on a Windows Workstation

To install the iPrint client on a Windows workstation, do the following:

1. Enter the following URL in Internet Explorer:
   `http://server_ip_address/ipp`
2. Select **Install iPrint Client**.
3. Follow the steps to install the client.
4. Restart your Windows workstation.

## Create and Start a Driver Store

To create and start a driver store, do the following:

1. Open **iManager**:
   a. For the iManager URL, enter `https://server_ip_address/nps/iManager.html`. A Login page appears.
   b. Enter your username and password.
   c. Select **Login**.

   After a few moments, the Novell iManager home page appears.

2. On the left under **iPrint**, select **Create Driver Store**.
3. Enter a driver store name.
4. Enter, or browse to and select, a container for the driver store.
5. In the **Target Server** field, enter a DNS name or IP address for the server that will host the driver store.
6. In the **eDir Server** field, enter the context of your eDir server.
7. Make sure **Start Driver Store after Creation** is selected.
8. Select **OK**.

## Add Printer Drivers to Your Driver Store

**iPrint** allows you to upload drivers to your Driver Store by using the drivers from an .inf file or from the drivers that currently exist on your Windows workstation.

To add drivers to your driver store, do the following:

1. In **iManager** under **iPrint**, select **Manage Driver Store**.
2. Browse to and select the driver store you want to add print drivers to.
3. Select **OK**.
4. Select the **Drivers** tab.
5. Select the tab of the Platform you want to work with (**XP, 2000, NT 4, or 95/98/Me**).
6. Do one of the following:
   - Add drivers from a print driver .inf file by selecting **Add from File**.
   - Or add drivers from the Windows workstation client on which you are running iManager by selecting **Add from System**.

![](img/d63035f3fce0eaaf97203dde900affb7_146_0.png)

> If you choose **Add from System**, you can only upload drivers to the same platform as the workstation you are working from.
>
> For example, if you are on a Windows 2000 machine, you will only be able to upload the drivers that are on your Windows 2000 machine.

7. Select the printer driver you want to add.
8. Select the Printer Driver Language (PDL) for the driver.
9. Select **OK**.
10. Repeat steps 7 through 9 until you have added all of your printer drivers.
11. Select **OK**.

## Create and Start the iPrint Manager

To create and start the iPrint Manager, do the following:

1. In iManager under iPrint, select **Create Print Manager**.
2. Enter a Manager name.
3. Enter the *container* where you want the iPrint Manager's object to reside.
4. In the Target Server field, enter a *DNS name* or *IP address* for the server that will host the iPrint Manager.
5. In the eDir Server field, enter the *context* of your eDirectory server.
6. In the Driver Store field, browse to and select your Driver Store object.
7. Make sure **Start print manager after creation** is selected.
8. Select **OK**.

## Create Your Printer Objects

To create a printer object for your printer, do the following:

1. In iManager under iPrint, select **Create Printer**.
2. Enter the name you want to assign to the new printer.

![](img/d63035f3fce0eaaf97203dde900affb7_147_0.png)

3. In the Container name field, browse to and select the *container* where you want the printer to reside.
4. In the Manager name field, browse to and select the iPrint Manager you want to have assigned to this printer.
5. In the DNS name or IP address field, enter the *DNS name* or *IP address* of the printer.

Secure printing uses port 443 to send secure data from the client to the server.

Non-secure printing uses port 631 to send clear text from the client to the server.

![](img/d63035f3fce0eaaf97203dde900affb7_148_0.png)

All print data is non-secure between the server and the printer because iPrint sends its data from the server to the printer via LPR (Line Printer Remote). LPR does not handle authentication or security and, therefore, is clear text.

6. (Optional) Enter information describing the location of the printer.
7. (Optional) Enter a description of the printer.
8. Select Next.
9. Select the default print drivers to install for each Windows platform.
10. Select Next.
11. (Optional) To create additional Printer objects, select Repeat Task and repeat all the above steps to create a Printer object.
12. Select OK.

## Configure Your Network for Workstation and/or User Printers

Before you configure your network for workstation and/or user printers, you need to understand what each of them is:

- **Workstation Printer.** This is an installed printer on a Windows NT/2000/XP machine that is available to anyone who is logged on to that Windows machine. Workstation printers can be created on Windows NT/2000/XP machines only by users who have Administrator or Power User rights.
- **User Printer.** This is an installed printer that is available only to the person who installed it on a Windows NT/2000/XP machine. User printers can be created by any user in your network.

To determine which kinds of printers are created on your network, do the following:

1. Browse to the `iprint.ini` file located in the `/var/opt/novell/http/htdocs/ippdocs` folder on your Linux server.
2. Right-click the `iprint.ini` file; then select Open With > gedit.
3. Configure the AllowUserPrinters value to one of the following:
   - 0 (the default) means that only users with sufficient rights (Administrator rights or Power User rights) can install a printer to the desktop. When a printer is installed to the desktop, it will be a Workstation printer.
   - 1 means that if the current user doesn't have rights to add it as a Workstation printer, it will be added as a User printer.
   - 2 means that all printers added, regardless of the user's rights, will be User printers.
4. When you finish, select Save.
5. Select Exit.

![](img/d63035f3fce0eaaf97203dde900affb7_149_0.png)

Windows 9x ignores these values and only creates Workstation printers.

## Create Location-Based Printing Web Pages

Location-based printing lets users select printers based on location by using one of the following:

- List View
- Maps

### List View

The **iPrint Manager** creates a list of your printers at the default iPrint page (`http://server_IP_address/ipp`).

To create a custom web page with your own list, you must use an HTML editor and create links to the printer’s URL.

To view a printer’s URL, do the following:

1. In **iManager** under **iPrint**, select **Manage Printer**.
2. In the **iPrint Printer name** field, browse to and select the printer you want.
3. Select **OK**.
4. Select **Client Support > iPrint Support**.

The printer’s URL is displayed under **Accepted IPP URL**.

### Maps

You can create maps with printer icons representing the location of your printers within your workplace environment. This enables your users to easily select which printer they want to print from, and download the correct driver for that printer.

Novell has created an iPrint Map Designer tool that utilizes drag-and-drop technology to aid you in creating your own location-based maps.

To create and configure a location-based map using the iPrint Map Designer, you must have the following:

- Internet Explorer 5.5 or later
- Windows 95/98/Me or Windows NT/2000/XP
- iPrint client installed on the workstation
- Maps to place printers in
