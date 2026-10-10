channels more often. (See the Kismet server.conf chapter for more information on tweaking your channel hopping for maximum performance.)

You probably don't want to SSH into the router every time you want to start the drone. You probably want it as an appliance that starts the drone automatically.

To do this, use your favorite text editor to create the file `/etc/init.d/S60kismet_drone` on the router with the following in it:

```
#! /bin/sh
echo "Setting radio for kismet_drone"
mkdir /var/log

/sbin/ifconfig eth1 up
/usr/sbin/wl ap 0
/usr/sbin/wl disassoc
/usr/sbin/wl passive 1
/usr/sbin/wl promisc 1
/usr/sbin/wl monitor 1
echo "Running kismet_drone"
/usr/bin/. /kismet_drone -f /etc/kismet/kismet_drone.conf > /dev/null 2>&1 &
sleep 3
echo "kismet_drone now running"
```

# Now just make it executable with:

```
chmod 777 /etc/init.d/S60kismet_drone
```

This will start the drone on startup first, followed by the channel hopping script if you chose to use it.

If everything is working fine, you should see data coming in when you start your server and hopefully across all channels. If you don't see anything, check the following:

# Troubleshooting

If the server is failing to start:

+   - Is the source line for your drone correct and do you have source entries for all sources present?
+   - Can you ping the drone's IP address? Is the Kismet drone shown as running using the ps command?