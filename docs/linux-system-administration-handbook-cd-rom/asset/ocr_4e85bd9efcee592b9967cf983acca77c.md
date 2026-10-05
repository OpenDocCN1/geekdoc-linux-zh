# 10.8 Common Error Messages and What They Mean (Taken from the INN FAQ)

sion. If the number of groups to be carried is reasonably large, the newsmaster can go out to a site like uu.net and obtain an active file and trim it down.

# Obtaining a Usenet Feed and Exchanging News

Once an active file has been created with the desired groups, the newsmaster must obtain a feed from some other machine. Newsfeeds are generally obtained from a service provider, or perhaps a friend. Once a feed is found, the feeding machine will need to access port 119 on the new news server to pass news, and the new news server will need to be access port 119 on the feeding machine to pass news back. Make sure that no firewalls are in place between the two machines, and then change the news machine's configuration files to allow the remote machine to have access.

To add news hosts, edit the newsfeeds, hosts.mntp, and nntpsend.ctl files as described above. If news is not being received by the remote machine, try opening a telnet session to the remote machine on port 119. If a denial message appears, the remote site probably does not have the local machine in its hosts.mntp file. If news cannot get from the remote site to the local site, check the local hosts.nntp file and all of the logs in the news directory for any errors.

# 10.8 Common Error Messages and What They Mean (Taken from the INN FAQ)

# When Innd Fails to Start

+   - inndstart: inndstart cant bind Address already in use

Another news daemon is already running or something else is using port 119. Try opening a telnet session to port 119 or using netstat to identify who or what is connected to the port. Also check in /etc/inetd.conf to see if there are entries there.

+   - SERVER cant dbminist <history> No such file or directory

The history file was never created. Run the BUILD script or run “makehistory” by hand.