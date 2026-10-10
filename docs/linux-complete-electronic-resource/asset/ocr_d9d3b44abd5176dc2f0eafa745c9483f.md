3. Choose Configurations... from the File menu. Select your Default configuration and click the Duplicate... button. Enter **IP Masq** (or something to let you know that this is a special configuration) in the Duplicate Configuration dialog; it will probably say something like Default copy. Then click the OK button and the Make Active button.

4. Select Ethernet from the Connect via: pop-up.

5. Select the appropriate item from the Configure: pop-up. If you don't know which option to choose, you probably should re-select your Default configuration and quit. I use Manually.

6. Enter the IP address of your Mac (192.168.1.x, 1 < x < 255) in the IP Address: box.

7. Enter 255.255.255.0 in the Subnet mask box.

8. Enter 192.168.1.1 in the Router address box.

9. Enter the IP addresses of your domain name servers in the Name server addr. box.

10. Enter the name of your Internet domain (for example, m i c r o s o f t . c o m) in the Starting domain name box under Implicit Search Path.

11. The following procedures are optional. Incorrect values may cause erratic behavior. If you're not sure, it's probably better to leave them blank, unchecked, and/or unselected. Remove any information from those fields, if necessary. As far as I know, there is no way in the TCP/IP dialogs to tell the system not to use a previously selected alternate Hosts file. If you know, I would be interested. Check the 802.3 if your network requires 802.3 frame types.

12. Click the Options... button to make sure that the TCP/IP is active. I use the Load only when needed option. If you run and quit TCP/IP applications many times without rebooting your machine, you may find that unchecking the Load only when needed option will prevent/reduce the effects on your machine's memory management. With the item unchecked, the TCP/IP protocol stacks are always loaded and available for use. If checked, the TCP/IP stacks are automatically loaded when needed and unloaded when not. It's the loading