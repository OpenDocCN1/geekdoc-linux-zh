If your using a v2.0, make sure it's `eth1`.
`source=wrt54g,eth1,wrt54g`

If you are using a v3.0 router, change it to:
`source=wrt54g,eth1,priism0,wrt54g`

Most users using a v4.0 router, however, WRT54GL or others will use `priism0`
`source=wrt54g,priism0,wrt54g`

If you run into problems with the drone not caputuring data or not starting due to incorrect interfaces, try another interface name. Revisions to the driver and OpenWRT mean that it's possible for things to change between hardware revisions.

You also need to change your `allowedhosts` line in the `kismet_drone.conf` file to something like:
`allowedhosts=127.0.0.1,192.168.0.0/24`

By default, the drone only allows connections from the local system. You will need to add your network segment that you will connect your server from to the list with no spaces. It can be a single IP address, or a whole network using decimal notation and no spaces. If you don't change this, it is still possible to connect to the server, however, no data will come through.

At this point we should set up our server to talk to the drone.

# # Server Configuration

Set up the `Kismet.conf` file on your laptop/workstation to use `source=kismet_drone,<IP Address>:3501,drone`. You can run other sources at the same time (e.g., wi-fi cards, other drones) on separate `source=` lines.

The source line breaks down like this:

+   - **Kismet_drone** indicates this is a remote drone source, as opposed to a local card source.
+   - **<IP Address>:3501** is the Transmisionn Control Protocal (TCP)/IP address and port that the drone is running on. You can change the IP address to whatever you set your router to. You shouldn't need to change the port.
+   - **drone** is just an arbitray description that is shown in the bottom right corner of the Kismet window in the sources list. You can change this to whatever you want for organizational purposes, be it where the drone is or perhapse what channels it's monitoring.