# Listing 9-9: Sample /var/adm/file

```
Jul 20 15:20:02 tigerden chat[16501]: abort on (NO DIALTONE)
Jul 20 15:20:02 tigerden chat[16501]: send (AT&FHO^M)
Jul 20 15:20:02 tigerden chat[16501]: expect (OK)
Jul 20 15:20:02 tigerden chat[16501]: OK -- got it
Jul 20 15:20:02 tigerden chat[16501]: send (atdt9640240^M)
Jul 20 15:20:03 tigerden chat[16501]: timeout on 75 seconds
Jul 20 15:20:03 tigerden chat[16501]: expect (CONNECT)
Jul 20 15:20:03 tigerden chat[16501]: ^M
Jul 20 15:20:20 tigerden chat[16501]: atdt9640240^M^M
Jul 20 15:20:20 tigerden chat[16501]: CONNECT -- got it
Jul 20 15:20:20 tigerden pppd[16498]: Serial connection established.
Jul 20 15:20:21 tigerden su[16512]: + tty4 bob-root
Jul 20 15:20:21 tigerden pppd[16498]: Using interface ppp0
Jul 20 15:20:21 tigerden pppd[16498]: Connect: ppp0 <>- > /dev/cua0
Jul 20 15:20:24 tigerden pppd[16498]: Remote message: Login Succeeded
Jul 20 15:20:25 tigerden pppd[16498]: local IP address 209.24.241.60
Jul 20 15:20:25 tigerden pppd[16498]: remote IP address 204.156.128.1
```

Listing 9-10 is a PPP login. What's happening is the modem is getting initialized, and the connection is getting established between the PPP client and server. By looking at the file, it looks like the PPP connection is being created with a serial modem.

Listing 9-11 shows Secure Shell traffic to and from the ISP. Looks like all the connections are from bob, who we know is OK.

# Listing 9-11: Secure Shell traffic to and from the ISP

```
Jul 20 15:21:52 tigerden sshd[16529]: log: Connection from 1.2.3.4 port 995
Jul 20 15:22:00 tigerden sshd[16529]: log: Password authentication for bob accepted.
Jul 20 15:22:00 tigerden sshd[16529]: log: executing remote command as user bob
Jul 20 15:22:00 tigerden sshd[16529]: log: Closing connection to 1.2.3.4
Jul 20 15:22:24 tigerden sshd[16533]: log: Connection from 1.2.3.4 port 994
Jul 20 15:22:27 tigerden sshd[16533]: log: Password authentication for bob accepted.
Jul 20 15:22:30 tigerden sshd[16533]: log: executing remote command as user bob
Jul 20 15:22:30 tigerden sshd[16533]: log: Closing connection to 1.2.3.4
Jul 20 15:25:32 tigerden sshd[16542]: log: Connection from 1.2.3.4 port 993
Jul 20 15:25:35 tigerden sshd[16542]: log: Password authentication for bob accepted.
Jul 20 15:25:36 tigerden sshd[16542]: log: executing remote command as user bob
Jul 20 15:25:36 tigerden sshd[16542]: log: Closing connection to 1.2.3.4
Jul 20 15:25:48 tigerden sshd[16546]: log: Connection from 1.2.3.4 port 992
Jul 20 15:25:52 tigerden sshd[16546]: log: Password authentication for bob accepted.
Jul 20 15:25:52 tigerden sshd[16548]: log: executing remote command as user bob
Jul 20 15:25:53 tigerden sshd[16546]: log: Closing connection to 1.2.3.4
```