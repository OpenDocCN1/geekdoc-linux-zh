# LISTING 21.2 continued

```
TIMEOUT 30 \
OK ATDTSTELEPHONE \
CONNECT \
ogin:--ogin: $ACCOUNT \
assword: $PASSWORD
```

6. Make the file executable. Type chmod 755 /etc/ppp/ppp-on-dialer and press Enter.

7. Configure the DNS address numbers used by your ISP. Type vi /etc/resolv.conf and press Enter. A sample of this file appears in Listing 21.3.

# LISTING 21.3 Edit Search and Nameserver Information in the /etc/resolv.conf File

```
search myisp.net
nameserver 255.255.255.244
nameserver 255.255.255.245
```

On the first line, enter the domain name for your ISP. On the second line, enter the primary DNS number. On the third line, enter the secondary DNS number. When you are done, save and close the file.

8. Dial up your ISP. Type /etc/ppp/ppp-on and press Enter. You should hear the modem dial.

9. When you are ready to disconnect from the Internet, type /etc/ppp/ppp-off. You'll see a message that says

```
PPP link to ppp0 terminated.
```

# Summary

You're connected to the Internet and ready to go. During the past hour, you learned several ways in which you could create a dialup connection to your Internet service provider. If a single user account will be cruising the Internet, you might want to use either the GNOME or KDE dialup utility. You also saw how easy it is to create a shell script to tell the modem when to connect to the Internet and when to disconnect. If you want to make one Internet connection available to all users, you might want to create the shell script. That way, you only have to set up the account one time.