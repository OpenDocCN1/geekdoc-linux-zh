```
LOCAL_IP=0.0.0.0        # Local IP address if known. Dynamic = 0.0.0.0
REMOTE_IP=0.0.0.0       # Remote IP address if desired. Normally 0.0.0.0
NETMASK=255.255.255.0  # The proper netmask if needed
#
...
```

In this example, the script has been edited to add the telephone number of the remote ISP, along with the username and password assigned by the ISP. The only other change that you might want to make is the default modem speed, detailed later on in the file. This portion of the script looks like this:

```
exec /usr/sbin/pppd lock modem crtscts /dev/modem 115200 \
asyncmap 20a0000 escape FF $LOCAL_IP:$REMOTE_IP \
noipdefault netmask $NETMASK defaultroute connect \
$DIALER_SCRIPT &
```

In this example, the default speed for the modem (located on /dev/modem) is set to 115200. Make any desired change and save the file. You can then create a PPP connection (as root) to your remote ISP by using the ppp-on script, like this:

```
# /etc/ppp/ppp-on
```

# ## Configuring the kppp Client

If you use the K Desktop Environment for your X sessions, you will want to set up the *kppp* client to do the dialing for you. This section includes instructions on how to set up a simple PPP connection. In only a few steps you will be able to configure your system to dial out and connect to your ISP. The *kppp* client is a mature, stable, and robust dialer that has been in use for several years by KDE fans. If you use KDE, you will certainly love *kppp*!

Start the client from the desktop panel menu or the command line of an X terminal, like this:

```
$ kppp &
```

After you press Enter, you will see a small dialog box. To set up your connection, click the Setup button. You will then see an Account setup dialog box. Click the New button to begin, and you will be asked if you want to use *kppp*'s Wizard setup. Do not choose the Wizard setup unless you live outside the United States, as the configuration is for foreign countries. Instead, click the Dial Setup button, and you will see a dialog box as shown in Figure 9.2.

Click in the Connection field and give the account a name. Next, click the Add button and type in a phone number that will connect you to your remote ISP.