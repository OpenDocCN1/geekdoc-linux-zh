336 Chapter Nine

# # Network Security

If you are linking your LAN to the Internet using PPP—or even just to a foreign LAN, you need to think about security issues. I strongly urge you to think about setting up a firewall!

You should also speak to the LAN administrator at your site *before* you start linking to foreign LANs or the Internet this way. Failure to do so could earn you anything from no reaction to really serious trouble.

# # After the Link Comes Up—THE /etc/ppp/ip-up Script

Once the PPP link is established, pppd looks for /etc/ppp/ip-up. If this script exists and is executable, the PPP daemon executes the script. This allows you to automate any special routing commands that may be necessary and any other actions that you want to occur every time the PPP link is activated.

This is just a shell script and can do anything that a shell script can do (i.e. virtually anything you want).

For example, you can get Sendmail to dispatch any waiting outbound messages in the mail queue.

Similarly, you can insert the commands into ip-up to collect (using pop) any e-mail waiting for you at your ISP.

There are restrictions on /etc/ppp/ip-up:

+   - It runs in a deliberately restricted environment to enhance security. This means you must give a full path to binaries, etc.

+   - Technically, /etc/ppp/ip-up is a *program* not a script. This means it can be directly executed—and hence it requires the standard file magic (#!/bin/bash) at the start of the first line and must be readable and executable by root.

# ## Special Routing

If you are linking two LANs, you will need to set up specific routes to the "foreign" LANs. This is easily done using the /etc/ppp/ip-up script. The only difficulty arises if your machine handles multiple PPP links.