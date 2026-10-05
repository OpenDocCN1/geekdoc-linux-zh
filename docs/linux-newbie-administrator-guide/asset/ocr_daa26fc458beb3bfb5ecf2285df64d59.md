# GATWAYDEV=
GATEWAY=

[You don't want a gateway on your ethernet interface on this machine if it does not lead to the outside world. The ppp interface on this first machine will be set up as a default gateway once you connect through your modem, e.g. using kpppp.]

The name of a computer is entirely arbitrary--the main user normally chooses a short word s/h likes. The domain name of the home network is entirely arbitrary, unless you have a permanent connection in which a dense name is registered to you. Try to invent something that does not exist--it will make your life easier you have a permanent connection.

As for the DNS server (also called "named") RedHat 5.2 and 6.0 comes with DNS preinstalled as "caching-only" it is so easy to choose. You may also choose not to use DNS at all-if DNS is up a server and can find it, it can be a real-stopper (the machine can appear to be hung up for a few minutes). To use the "named" service must be enabled-- check this by running setup. To set up the caching-only DNS, fill up the appropriate boxes in `netconf`. E.g., I filled `nameserver 1` to my first machine on all computers (I entered the loopback address 127.0.0.1 on the machine xxx.xxx.xxx.1, and the proper xxx.xxx.xxx.1 address on all machines).

No routes to other networks and were required in my network, since I don't have other local networks. So I left this field blank.

Other than setting up the hardware correctly and filling up the info under netconf on each computer, as described above, I do not have to do anything on the standard RedHat to get my network working.

Reboot all computers one by one in order (this is not necessary, but won't hurt you) and watch the boot messages (if they scroll too fast off, use Shift+PgUp to scroll up, or use dmesg from the command line to view them). Did your cards configure correctly? Use the command route (as root) to see if the eth0 interface is running. Use the ping command to test the connections between machines. Try to telnet your local machine to see if the loopback works:

telnet name_of_the_machine_you_are_sitting_at

After a successful login, you can exit the telnet session by

exit

Finally, to telnet a machine on your network:

telnet name_of_a_remote_machine

If this works on all machines, your eth0 network interface is set up.

After setting up your ppp and connecting to your Internet Service Provider (ISP), you will have another network interface (ppp0) and then will be able to telnet any machine in the world.