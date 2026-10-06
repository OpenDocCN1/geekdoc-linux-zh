# Chapter 26: Integrating Fedora with Apple Macs 995

# Open firewall ports

If you enabled iptables service to protect your computer with a firewall, you need to open several ports in your firewall before someone from a remote computer can access your netatalk server. The easiest way to do that is to open the Security Level and Firewall window (System $ightarrow$ Administration $ightarrow$ Security Level and Firewall).

With the firewall set to Enabled, Select Other ports $ightarrow$ Add. Add each port number (for the tcp protocol) to open the netatalk server. Port numbers could include: 201, 202, 204, 206, and 548. (See the `/etc/services` file for descriptions of those port numbers). Click OK and the new ports will be opened.

# Defining general Apple server settings

Settings in the `/etc/stalk/netatalk.conf` define information related to the general operation of your netatalk server. Step 2 of “Setting up the netatalk server” describes the default settings in this file. The following code lines illustrate a few things you might want to change (as root user).

```
AFPD_MAX_CLIENTS=100
```

Instead of limiting the number of Mac clients who can simultaneously use your netatalk server to 50, you can use any number (I used 100 in the first example). To change the zone and server name, you could change the following settings:

```
ATALK_ZONE=GSTREET
ATALK_NAME="History101"
```

This example sets the zone name to GSTREET and the server name to History 101. To change how authentication is performed, you could use one of the two examples:

```
AFPD_UAMLIST=-U guests.so
AFPD_UAMLIST=-U users clrtxt.so
```

The first example makes netatalk a guest-only server. The second line allows valid users from the Linux system using clear-text passwords. The following line enables you to change the guest user account:

```
AFPD_GUEST=nobody
```

You could change nobody to any valid user account on Linux, and that account will be used as your guest user.

Other settings in the netatalk.conf file let you set which daemons run and export MAC and UNIX character sets to use with netatalk.