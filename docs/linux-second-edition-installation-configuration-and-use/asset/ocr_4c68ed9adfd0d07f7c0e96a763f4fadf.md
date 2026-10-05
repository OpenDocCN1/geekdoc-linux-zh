# SLIP CONFIGURATION 323

F10 takes you back to the main dialog, where you activate the network device with F4. Subsequently you leave this dial too with F10. The result is two new files in /etc/sppp usually generic.chat and generic.options. (If your provider was on the list provided by SUSE, the name of the provider is specified instead of generic.)

Now you can start and stop PPP with the following two commands:

```
root# /etc/sppp/scripts/ppp-up generic debug
root# /etc/sppp/scripts/ppp-down
```

If one exists, you must specify the provider's name instead of generic. Once this works, you can choose also without the debug option. It causes additional logging information in /var/log/messages.

If everything is working, and you want PPP to be started automatically without prompts for confirmation at each Internet access (for example, if you want to read an Internet page with Netscape), you activate the AUTOMATIC DIAL option in the PPP dialog. Subsequently, you first have to execute init 1 and then init 2 in a text console for the setting to become valid.(Restarting the computer is, of course, another possibility.)

From now on, dial monitors starts PPP for each inquiry, and stops when there has not any Internet traffic for some time. You can set the timeout intervals in /etc/sppp/dial/generic.diald.

# 9.4 SLIP configuration

SLIP (Serial Line IP) allows TCP/IP communication via a serial interface, as does PPP. CSLIP is a variation of SLIP in which the protocol information is compressed (but not the data). SLIP/CSIP is so-to-speak, the predecessor of PPP. However, because of its limited security mechanisms it is losing significance.

To automate establishing connections, you need the dip program, which is usually located in the /usr/sbin directory. You might have to install the appropriate package.

Unfortunately, I did not have a chance to try out SLIP, so the information given here must be taken with some reservation. It is mainly based on available documentation: the HOWTO text on NET-2, the files in /usr/doc/dip, the man texts for slattach and dial, and finally on the Linux Network Administration Guide.

# Establishing the connection

With PPP, a connection is established manually by using a terminal emulator to make a connection with your Internet provider and to log in. Subsequently, you can connect without interrupting the line. Now you can take over the serial interface with slattach for exclusive use with SLIP. If you want to work with SLIP (and not CSLIP), you must specify the option -p slip.

```
root# /usr/sbin/slattach /dev/tty1 &
```

After SLIP has taken over the serial interface, this new Internet connection must be registered. This is done with the commands ifconfig and route: