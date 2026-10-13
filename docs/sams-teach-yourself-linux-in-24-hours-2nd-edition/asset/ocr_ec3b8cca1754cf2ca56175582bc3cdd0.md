# Reading Your System Log

If you want to read in detail about what is going on while your scripts are executing, take a look through your system log for a file called messages under the /var/log directory.

Try the following (as the root operator):

```
# less /var/log/messages
```

Look for the start of the pppd daemon in the ppp-on script. Notice that your dialer script uses the chat program, which does most of the work and then quits, followed by pppd getting and setting the network IP addresses, as follows:

```
...
Nov 5 16:29:49 localhost pppd[370]: pppd 2.2.0 started by root, uid 0
Nov 5 16:29:51 localhost chat[371]: timeout set to 3 seconds
Nov 5 16:29:51 localhost chat[371]: abort on (\nBUSY\r)
Nov 5 16:29:51 localhost chat[371]: abort on (\nNO ANSWER\r)
Nov 5 16:29:51 localhost chat[371]: abort on (\nRINGING\r)
→(\nRINGING\r)
Nov 5 16:29:51 localhost chat[371]: send (AT M)
Nov 5 16:29:51 localhost chat[371]: expect (OK)
Nov 5 16:29:51 localhost chat[371]: AT M
Nov 5 16:29:51 localhost chat[371]: OK -- got it
Nov 5 16:29:51 localhost chat[371]: send (ATH0 M)
Nov 5 16:29:51 localhost chat[371]: timeout set to 30 seconds
Nov 5 16:29:51 localhost chat[371]: expect (OK)
Nov 5 16:29:51 localhost chat[371]: M
Nov 5 16:29:51 localhost chat[371]: ATH0 M
Nov 5 16:29:51 localhost chat[371]: OK -- got it
Nov 5 16:29:51 localhost chat[371]: send (ATDT659-9041 M)
Nov 5 16:29:51 localhost chat[371]: expect (CONNECT)
Nov 5 16:30:10 localhost chat[371]: ATDT659-9041 M
Nov 5 16:30:10 localhost chat[371]: CONNECT -- got it
Nov 5 16:30:10 localhost chat[371]: send ( M)
Nov 5 16:30:10 localhost chat[371]: expect (ogin:)
Nov 5 16:30:10 localhost chat[371]: 57600 M
Nov 5 16:30:12 localhost chat[371]: M
Nov 5 16:30:12 localhost chat[371]: M
Nov 5 16:30:12 localhost chat[371]: Staffnet PMO login: -- got it
Nov 5 16:30:12 localhost chat[371]: send (username M)
Nov 5 16:30:12 localhost chat[371]: expect (assword:)
Nov 5 16:30:12 localhost chat[371]: username M
Nov 5 16:30:12 localhost chat[371]: Password: -- got it
Nov 5 16:30:12 localhost chat[371]: send (password M)
Nov 5 16:30:12 localhost pppd[370]: Serial connection established.
Nov 5 16:30:13 localhost pppd[370]: Using interface ppp0
Nov 5 16:30:13 localhost pppd[370]: Connect: ppp0 <-> /dev/modem
Nov 5 16:30:16 localhost pppd[370]: local IP address 207.226.80.171
Nov 5 16:30:16 localhost pppd[370]: remote IP address 207.226.80.214
...
```