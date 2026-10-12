# # Restoring access

If access was cut off to a computer that you wanted to have access, there are several things you can check to correct that problem:

+   - **/etc/hosts.deny:** See if the computer's IP address was mistakenly added to this file. This would cause network services to be denied to the host at that IP address.
+   - **/var/portsentry/portsentry.blocked:** Check that an entry for the computer's IP address wasn't added to the portsentry.blocked.udp or portsentry.blocked.tcp files.
+   - **route:** Run the /sbin/route command to see if messages from the computer are being rerouted to a dead host (probably the localhost).
+   - **ipchains:** Run the ipchains -L command to see if a new firewall was created to block access from the computer. (If you had created an iptables rule instead, type iptables -L to see the new firewall entry.)

> TIP: To make sure that access isn't cut off again, you can add the IP address of the remote computer to the /etc/portsentry/portsentry.ignore file. Future improper scans or requests for services won't cause the remote computer to be blocked.

# # Summary

With the rise of the Internet, security has become a critical issue for nearly all computer users. Properly using passwords, securely configuring network services, and monitoring log files are critical ways of keeping your computer secure.

Using encryption keys you can help verify the authenticity of those you communicate with, as well as make the data you transmit more secure. With tools such as LogSentry and PortSentry, you can protect your Red Hat Linux system from intrusions.