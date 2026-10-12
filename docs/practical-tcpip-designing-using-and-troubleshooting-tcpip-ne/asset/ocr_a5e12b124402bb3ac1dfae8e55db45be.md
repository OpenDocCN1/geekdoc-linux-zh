![](bbox=[0.18, 0.09, 0.69, 0.41])

What’s happening is that we’re trying to specify the main network as “the range .0-.255 except for .64-.79,” but you can’t specify this using a single netmask, and therefore it can’t work correctly.

There are three ways to get over this problem:

+   1. you can manually configure explicit routes on every PC on the main LAN to says that network 192.0.2.64/28 is accessible via Robert. As this is a more specific route than the default route to Rupert, it will work correctly

+   2. in certain circumstances, if the numbers are right, you could use DHCP (Chapter 16) to automatically configure the explicit routes in (1) above. However, at present, DHCP can only disseminate “class-ful” routes, i.e. it doesn’t include a netmask with the network address, so the usefulness of this is limited. (A proposal to modify DHCP to handle CIDR routes, i.e. with netmasks, is currently working its way through the Internet standards process.)

+   3. sub-net the network the correct way, as described in the next module.