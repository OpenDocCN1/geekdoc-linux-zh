Once you have the drone binaries built and installed, you can configure the `kismet_drone.conf` file with your source just as with the server configuration.

You may need to build and install `setuid root`, depending on how your PC drone is configured. If you don't install `setuid root`, make sure to add a normal user to the system that Kismet can drop privileges to. The added advantage to using a PC is that most compatible cards and drivers don't need external scripts to channel hop. Using compatible cards also means that the Kismet server can control channel hopping (locking and re-enabling hopping) and properly report what channel is currently in use. You also need to change your `allowed hosts` line in the `kismet_drone.conf` file to something like:

```
allowedhosts=127.0.0.1,192.168.0.0/24
```

By default, the drone only allows connection from the local system. You will need to add your network segment that you will connect your server from to the list with no spaces. It can be a single IP address, or a whole network using decimal notation and no spaces. If you don't change this, it is still possible to connect the server, however, no data will come through.

Set up the `Kismet.conf` file on your laptop/workstation to use `source=kismet_drone,<IP Address>:3501,drone`. You can run other sources at the same time (e.g., wi-fi cards, other drones) on separate `source=` lines.

The source line breaks down like this:

+   - **Kismet_drone** indicates this is a remote drone source, as opposed to a local card source.

+   - **<IP Address>:3501** is the TCP/IP address and port that the drone is running on. You can change the IP address to whatever you set up your router to. You shouldn't need to change the port.

+   - **drone** is just an arbitrary description that is shown in the bottom right corner of the Kismet window in the sources list. You can change this to whatever you want for organizational purposes, be it where the drone is or perhaps what channels it's monitoring.

As for running the drone on startup, it all depends on your distribution's method of starting programs at startup. There are too many to go over in detail, so just check with the documentation for your particular distribution.