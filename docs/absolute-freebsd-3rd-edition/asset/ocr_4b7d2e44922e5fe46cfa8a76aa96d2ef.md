FreeBSD manages device nodes through devfs(5), a virtual filesystem that dynamically provides device nodes as hardware boots, appears, and disappears. See Chapter 13 for more information.

# # /etc/dhclient.conf

Many operating systems give you very basic DHCP client configuration with no way to fine-tune or customize it; you either use it or you don't. In most cases, an empty /etc/dhclient.conf file gives you full DHCP client functionality, but it won't work correctly in all situations. Perhaps your network is having trouble or you're at a conference where some script kiddie thinks it's fun to set up a second DHCP server and route everyone's traffic through his machine so he can capture passwords.

Your server better not be configured via DHCP (unless it's diskless), so we won't go into any depth on this. You should be aware that you can configure FreeBSD's DHCP client functionality, however.

# # /etc/disktab

Once upon a time, hard disks were rare and exotic creatures that came in only a few varieties. In /etc/disktab, you'll find low-level descriptions of many different kinds of disks, from the 360KB floppy disk to a Panasonic 60MB laptop hard drive. (Yes, laptops came with 60MB hard drives, and we were durned happy to have them.)

Today, this file is mostly used for removable media, such as 1.44MB floppy disks and zip disks. While I described formatting flash drives in Chapter 13, this file contains the descriptions needed to format other removable media. If you want to put a filesystem on your LS 120 disk or zip drive, you'll find the necessary label here at the beginning of an entry.

Editing /etc/disktab is useful only if you have multiple identical hard drives that you want to partition and format in exactly the same way. If you need to make your own entries, read disktab(5).