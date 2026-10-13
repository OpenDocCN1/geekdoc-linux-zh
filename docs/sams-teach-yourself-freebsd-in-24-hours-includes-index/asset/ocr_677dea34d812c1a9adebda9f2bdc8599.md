# Quiz Answers

+   1. The correct answer is B. Laptops, however, typically use PCMCIA cards.
+   2. The correct answer is A. Unless you're buying a 3Com card, which is usually much more expensive for some reason.
+   3. The correct answer is A.
+   4. The correct answer is C.
+   5. The correct answer is B, though if the motherboard's built-in Ethernet chipset is also a 3Com 3c905, the second installed card would be `/dev/x12`.

# Exercises

+   1. After running `sysinstall`, look at your `/etc/rc.conf` file and examine the changes that have been made. Are they correct? How would you configure another Ethernet card that you choose to install—without using `sysinstall`? Remember that the only persistent configuration that `sysinstall` does is to write these settings into `/etc/rc.conf`. This means that you can do everything `sysinstall` does simply by manually adding lines to `rc.conf` and rebooting.
+   2. How can you change your network settings without rebooting? It's actually quite easy. After making your changes in `/etc/rc.conf`, use the `/etc/netstart` script to automatically read them in and apply them. Note, however, that `/etc/netstart` does not reset your default gateway router; the proper sequence is to first issue a `route delete default` command, and then run `/etc/netstart`.