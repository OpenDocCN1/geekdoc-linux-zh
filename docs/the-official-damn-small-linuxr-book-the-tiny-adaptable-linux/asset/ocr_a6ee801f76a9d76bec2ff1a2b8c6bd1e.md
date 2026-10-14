```
#!/bin/bash
# put other system startup commands here
/opt/lampp/lampp start
/opt/rc.firewall
```

If you installed the XAMPP tarball and copied the rc.firewall script as described earlier, both those services are now set up to start automatically the next time DSL boots.

If you also want to add a static IP address for your server, instead of getting addresses assigned from a DHCP server, you can add commands for that to your bootlocal.sh script. For example, you could add the following lines to set your IP address for the eth0 interface to 192.168.0.10, set the default router (gateway) to 192.168.0.1, and identify your DNS servers as 192.168.0.5 and 192.168.0.6.

```
ifconfig eth0 192.168.0.10
route add default gw 192.168.0.1
echo nameserver 192.168.0.5 > /etc/resolv.conf
echo nameserver 192.168.0.6 >> /etc/resolv.conf
```

Note that the addresses used here are all private IP addresses. If you are configuring a public server, you either need to have public IP addresses assigned or use some sort of port forwarding from a public IP address to a machine behind a firewall/router.

# 2. Create DSL on USB flash drive—Insert your USB flash drive, that you are prepared to erase and use for your Web server, into your computer's USB port (don't mount it). Next, from the DSL menu on the desktop, select Apps, Tools, Install to USB Pendrive. Then, select either For USB-ZIP Pendrive (if you expect to run the server on an older PC) or For USB-HDD Pendrive (to run the server on newer PCs).

This procedure erases everything on your USB drive! So make sure you've removed everything you need from the drive. Answer the questions as prompted. (See Chapter 6, "Running a Native Pen Drive Install," for details on installing DSL to a pen drive.)

# 3. Select files/directories to back up—The files and directories that DSL backs up for you need to be listed in the /home/dsl/.filetool.lst file. Several entries are already in that file. Open that file using any text editor and add the last lines shown here in bold: