After you have enabled dial-on-demand, you can create a startup script to automatically start the `pppd` daemon each time your system boots. There are several ways to do this; but, as you have seen in Chapter 11, “System Configuration and Startup Scripts,” the best way is to create a startup script in `/usr/local/etc/rc.d` with the single line `pppd` in it. This file can be called anything you want, but it’s a good idea to name it `ppp` or something else that makes sense and tells you what it does.

> **TIP**
> 
> If you have dial-on-demand enabled and your Internet connection seems to be starting periodically for no reason, a program is probably trying to do a DNS lookup. More often than not, Sendmail is the program causing problems. You can fix this by enabling the `SMART_HOST` relay definition or the `rondns` feature in the `freebsd.nc` configuration file, or by adding the IP address and hostname of your ISP’s mail server to your `/etc/hosts` file. See Chapter 24, “Configuring E-mail Services,” for information on how to configure Sendmail using the Master Config file.

> **TIP**
> 
> If you have dial-on-demand enabled and you are running Fetchmail in daemon mode so that it periodically polls your mail server, this might keep the connection open all the time in addition to causing `pppd` to dial on a regular basis. See the “E-mail for Standalone Workstations” section in Chapter 24 for ways to stop this from happening.

# Persistent Connections

You can also tell `pppd` to always keep the connection up. This is done by adding the `persist` statement to `/etc/ppp/options`. If this statement is present, `pppd` automatically tells the modem to re-establish the connection if it is lost.

> **CAUTION**
> 
> Even if your ISP tells you that you have unlimited access, make sure you read the fine print. There might be a “within reason” clause or something. If you are using the `persist` option to keep your Internet connection open 24 hours a day, 365 days a year, your ISP may terminate your account or ask you to purchase a dedicated line. The moral of this is that unlimited access does not always truly mean “unlimited access.”

# Running Commands on Connect and Disconnect

When `pppd` establishes a connection, it checks for the existence of a file called `ip-up` in `/etc/ppp`. Likewise, when the PPP connection goes down, `pppd` checks for the existence of a file called `ip-down` in `/etc/ppp`. If these files exist, whatever commands are listed in them are executed.

![](bbox=[0.94, 0.31, 0.99, 0.34])