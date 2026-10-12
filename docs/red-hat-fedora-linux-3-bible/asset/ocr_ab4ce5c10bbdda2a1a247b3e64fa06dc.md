**NOTES:** If browsing isn't working, check the nmbd log file (/var/log/samba/log.nmbd). To get more detail, increase the debugging level to 2 or 3 (described earlier in the “Logging options” section) and restart Samba. The log can tell you if your Samba server is the master browser and, if so, which computers are on its list.

+   os level — Set a value to control whether your Samba server (nmbd daemon) can become the local master browser for your workgroup. Raising this setting increases the Samba server’s chance to control the browser list for the workgroup in the local broadcast area.
+   If the value is 0, a Windows machine will probably be selected. A value of 65 will probably ensure that the Samba host is chosen over an NT server. The default is 20.

+   preferred master — Set this to Yes if you want to force selection of a master browser. By setting this to Yes, the Samba server also has a better chance of being selected. (Setting Domain Master to Yes along with this option should ensure that the Samba server will be selected.) This is set to Auto by default, which causes Samba to try to detect the current master browser before taking that responsibility.

+   local master — Set this to Yes if you want the Samba server to become the local browser master. (This is not a guarantee, but gives it a chance.) Set the value to No if you do not want your Samba server selected as the local master. Local Master is Auto by default.

+   domain master — Set this to Yes if you want the Samba server (nmbd daemon) to identify itself as the domain master browser for its workgroup. This list will then allow client computers assigned to the workgroup to use SMB-shared files and printers from subnetworks that are outside of their own subnetwork. This is set to No by default.

# WINS options

Use the WINS options if you want to have a particular WINS server provide the name-to-address translation of NetBIOS names used by SMB clients. As noted earlier, you probably don’t need to use a WINS server if all of the clients and servers in your SMB workgroup are on the same subnetwork. That’s because NetBIOS names can be obtained through addresses that are broadcast. It is possible to have your Samba server provide WINS services.

+   wins server — If there is a WINS server on your network that you want to use to resolve the NetBIOS names for your workgroup, you can enter the IP address of that server here. Again, you will probably want to use a WINS server if your workgroup extends outside of the local subnetwork.

+   wins support — Set this value to Yes if you want your Samba server to act as a WINS server. (It’s No by default.) Again, this is not needed if all the computers in your workgroup are on the same subnetwork. Only one computer on your network should be assigned as the WINS server.