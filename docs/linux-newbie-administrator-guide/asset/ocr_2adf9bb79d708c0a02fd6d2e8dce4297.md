# 4.5.3 I have problems configuring the ppp dial out

GUL. If I were you, I would install kde and use kppp. (If you don't have kde installed, look here [p 72] for information on how to install it.) kppp is really easy to configure and run. To set up your ppp dial out, run kppp (it is the "K" menu "Internet", or you can run it from the term by calling kppp), press the "setup" button, create an account, and fill out the information required: telephone number, authentication protocol, and your Internet Service Provider’s (ISP) domain name and the Domain Name Server (DNS) number of your ISP. All this information has been provided to you by your ISP.

Next, create a device called /dev/modem, by symbolically linking it to the device /dev/ttyS1 (as root)

```
ln -s /dev/tty1 /dev/modem
```

ttyS1 should work if your modem is on the port that DOS calls COM2. Use ttyS0 for COM1 and ttyS2 for COM3. The modem will not dial if all a wrong is chosen.

Finally, I tried to run the kppp but got an error message complaining about a "lock". So, I made the file /etc/ppp/options empty by deleting it (as root):

```
pico /etc/ppp/options
```

and deleting the word "lock", then saving the file.

After these steps, the kppp could connect to my ISP with no problems on RedHat 5.2.
RedHat 6.0 required one additional step: setting the "said" (substitute user id) so that "kppp" runs with the effective user id of root (it needs to access hardware directly). Without it, kppp complains that "it was not properly set up" and "can't create lock file.\. This has to be done as root:

```
cd /usr/bin/
chmod a+s kppp
```

Troubleshooting. If your modem refuses to dial on the port that you are positive is chosen properly, maybe the modem is not set properly (or it is a "winmodem") Then try it away and use a proper modem. In one instance, I had to run kppp setup, edit the "modem commands" and input ATZ1 as the initialization string (instead of the default ATZ for a standard Hayes-compatible modem).

If your line requires pulsing (instead of the default tone-tone dialing), you may need to change the dial command "ATDT" ("=ATAntion Dial Tonectone") to "ADDP" ("=ATAntion Dial Pulse"). These commands work with any standard Hayes-compatible modem.

If your modem dials correctly and you are able to connect, but your authentication fails, perhaps your Internet Service Provider (ISP) uses a different authentication protocol. Call them and ask them Or Try pay, terminal-based or chap (in your kppp setup) until you