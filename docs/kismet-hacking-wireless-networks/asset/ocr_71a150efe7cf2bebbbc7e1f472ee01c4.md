To run the drone manually, just SSH into the router in another window or terminal and run the following commands:

+   - **wl ap 0** Put the router in Cilent mode, just to be sure. We don't want anyone associating while we drive by.

+   - **wl disassoc** To make sure it's not associated with anything that could screw up our detection.

+   - **wl passive 1** This throws the router scan engine into passive mode, and prevents any transmussions.

+   - **wl promisc 1** Why not put it in promisc mode too?

Run the drone, specifying where the config file is:

```
`/usr/bin/../kismet_drone -f /etc/kismet/kismet_drone.conf`
```

You should then see something like :

```
```
Suid priv-dropping disabled. This may not be secure.
No specific sources given to be enabled, all will be enabled.
Enabling channel hopping.
Disabling channel splitting.
Source 0 (wrt54g): Enabling monitor mode for wrt54g source interface eth2
channel 6...
Source 0 (wrt54g): Opening wrt54g source interface eth2...
Kismet Drone 2006-04-R1 (Kismet)
Listening on port 3501 (protocol 8).
Allowing connections from 192.168.0.0/255.255.0.0
```
```

If not, double check your steps.

The last line is the most important. It means that the drone will now accept connections from servers on the 192.168.0.0/24 network, where our server is hopefully set up.

You should then be able to fire up Kismet on your workstation and if everything lines up, you'll see “accepted streamer connection from” in the router SSH session, and Kismet will show a drone with channel “--” in the bottom right corner as a source (This doesn't mean it's not scanning channels, it's just a limitation of the server to know which channel the drone is on). If it's also your only source and you detect networks, you'll know it is working.

Kismet cannot control the channel of the WRT54G; this is a known limitation with the Kismet drone and server. If you want to monitor just one channel, you'll want to