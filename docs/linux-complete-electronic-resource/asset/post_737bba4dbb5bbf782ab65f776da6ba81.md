
4. Under the Network Software and Adapter Cards section, highlight **TCP/IP Protocol** in the **Installed Network Software** selection box.

5. In **TCP/IP Configuration**, select the appropriate adapter, for example, `[1]Novell NE2000 Adapter`. Then set the IP Address to 192.168.1.x (1 < x < 255), then set **Subnet Mask** to 255.255.255.0 and **Default Gateway** to 192.168.1.1

6. Do not enable **Automatic DHCP Configuration** or put anything in those **WINS Server** input areas unless you’re in a Windows NT domain and you know what you’re doing.

7. Click **DNS**, fill in the appropriate information mentioned in step 6 of the “Configuring Windows 95” section, then click **OK** when you’re done.

8. Click **Advanced**, and check **Enable DNS for Windows Name Resolution** and **Enable LMHOSTS lookup** if you’re using a lookup host file, similar to the one mentioned in step 10 of the “Configuring Windows 95” section.

9. Click **OK** in all dialog boxes and restart your system.

10. Ping the Linux box to test the network connection: **File/Run**, type `ping 192.168.1.1`. (This is only a LAN connection testing; you can’t ping the outside world yet.)

## Configuring Unix Based Systems

1. If you haven’t installed your network card and recompiled your kernel with the appropriate adapter driver, do so now.

2. Install **TCP/IP** networking, such as the **nettools** package, if you don’t have it already.

3. Set **IPADDR** to 192.168.1.x (1 < x < 255), then, set **NETMASK** to 255.255.255.0, **GATEWAY** to 192.168.1.1, and **BROADCAST** to 192.168.1.255. For example, you can edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file on a Red Hat Linux system, or simply do it through the Control Panel. (It’s different in SunOS, BSDI, Slackware Linux, etc.)

4. Add your **domain name service (DNS)** and **domain search suffix** in `/etc/resolv.conf`.

5. You may want to update your `/etc/networks` file, depending on your settings.

6. Restart the appropriate services, or simply restart your system.

7. Issue a `ping` command (`ping 192.168.1.1`) to test the connection to your gateway machine. (This is only a LAN connection testing; you can't ping the outside world yet.)

## Configuring DOS Using the NCSA Telnet Package

1. If you haven't installed your network card, do so now.

2. Load the appropriate packet driver. For an NE2000 card, issue `nwpd 0x60 10 0x300`, with your network card set to IRQ 10 and hardware address at `0x300`

3. Make a new directory, and then unpack the NCSA Telnet package: `pkunzip tel2308B.zip`.

4. Use a text editor to open the `config.tel` file.

5. Set `myip=192.168.1.x` (1 < x < 255) and `netmask=255.255.255.0`

6. In this example, you should set `hardware=packet`, `interrupt=10`, and `ioaddr=60`.

7. You should have at least one individual machine specification set as the gateway, that is, the Linux host:
   - `name=default`
   - `host=yourlinuxhostname`
   - `hostip=192.168.1.1`
   - `gateway=1`

8. Have another specification for a domain name service:
   - `name=dns.domain.com ; hostip=123.123.123.123; nameserver=1`
   - Substitute the appropriate information about the DNS that your Linux host uses.

9. Save your `config.tel` file.

10. Telnet to the Linux box to test the network connection: `telnet 192.168.1.1`.

## Configuring a Macintosh Running MacTCP

1. If you haven't installed the appropriate driver software for your Ethernet adapter, now would be a very good time to do so.

2. Open the MacTCP Control Panel. Select the appropriate network driver (Ethernet, *not EtherTalk*) and click on the More... button.

3. Under **Obtain Address** click **Manually**.

4. Under **IP Address** select class **C** from the pop-up menu. Ignore the rest of this section of the dialog box.

5. Fill in the appropriate information under **Domain Name Server Information**.

6. Under **Gateway Address** enter **192.168.1.1**.

7. Click **OK** to save the settings. In the main window of the MacTCP control panel, enter the IP address of your Mac (192.168.1.x, 1 < x < 255) in the **IP Address:** box.

8. Close the MacTCP control panel. If a dialog box pops up notifying you to do so, restart the system.

9. You may optionally ping the Linux box to test the network connection. If you have the freeware program **MacTCP Watcher**, click the **Ping** button, and enter the address of your Linux box (192.168.1.1) in the dialog box that pops up. (This is only a LAN connection testing; you can't ping the outside world yet.)

10. You can optionally create a *Hosts* file in your **System Folder** so that you can use the hostnames of the machines on your LAN. The file should already exist in your **System Folder** and should contain some (commented-out) sample entries, which you can modify according to your needs.

## Configuring a Macintosh Running Open Transport

1. If you haven't installed the appropriate driver software for your Ethernet adapter, now would be a very good time to do so.

2. Open the TCP/IP Control Panel and choose **User Mode...** from the Edit menu. Make sure the user mode is set to at least **Advanced** and click the **OK** button.

3. Choose Configurations... from the File menu. Select your Default configuration and click the Duplicate... button. Enter **IP Masq** (or something to let you know that this is a special configuration) in the Duplicate Configuration dialog; it will probably say something like Default copy. Then click the OK button and the Make Active button.

4. Select Ethernet from the Connect via: pop-up.

5. Select the appropriate item from the Configure: pop-up. If you don't know which option to choose, you probably should re-select your Default configuration and quit. I use Manually.

6. Enter the IP address of your Mac (192.168.1.x, 1 < x < 255) in the IP Address: box.

7. Enter 255.255.255.0 in the Subnet mask box.

8. Enter 192.168.1.1 in the Router address box.

9. Enter the IP addresses of your domain name servers in the Name server addr. box.

10. Enter the name of your Internet domain (for example, microsoft.com) in the Starting domain name box under Implicit Search Path.

11. The following procedures are optional. Incorrect values may cause erratic behavior. If you're not sure, it's probably better to leave them blank, unchecked, and/or unselected. Remove any information from those fields, if necessary. As far as I know, there is no way in the TCP/IP dialogs to tell the system not to use a previously selected alternate Hosts file. If you know, I would be interested. Check the 802.3 if your network requires 802.3 frame types.

12. Click the Options... button to make sure that the TCP/IP is active. I use the Load only when needed option. If you run and quit TCP/IP applications many times without rebooting your machine, you may find that unchecking the Load only when needed option will prevent/reduce the effects on your machine's memory management. With the item unchecked, the TCP/IP protocol stacks are always loaded and available for use. If checked, the TCP/IP stacks are automatically loaded when needed and unloaded when not. It's the loading and unloading process that can cause your machine's memory to become fragmented.

13. You may ping the Linux box to test the network connection. If you have the freeware program MacTCP Watcher, click the Ping button, and enter the address of your Linux box (192.168.1.1) in the dialog box that pops up. (This is only a LAN connection testing; you can't ping the outside world yet.)

14. You can create a *Hosts* file in your System Folder so that you can use the hostnames of the machines on your LAN. The file may or may not already exist in your System Folder. If so, it should contain some (commented-out) sample entries, which you can modify according to your needs. If not, you can get a copy of the file from a system running MacTCP, or just create your own (it follows a subset of the Unix `/etc/hosts` file format, described on RFC952). Once you've created the file, open the TCP/IP Control Panel, click the Select Hosts File... button, and open the Hosts file.

15. Click the close box or choose Close or Quit from the File menu, and then click the Save button to save the changes you have made.

16. The changes take effect immediately, but rebooting the system won't hurt.

## Configuring a Novell Network Using DNS

1. If you haven't installed the appropriate driver software for your Ethernet adapter, now would be a very good time to do so.

2. Download `tcpipl6.exe` from `ftp.novell.com/pub/updates/unixconn/1wp5`.

3. Edit `c:\nwclient\startnet.bat`. (Here is a copy of mine.)
```
SET NWLANGUAGE=ENGLISH
LH LSL.COM
LH KTC2000.COM
LH IPXODI.COM
LH tcpi
LH VLM.EXE
F:
```
