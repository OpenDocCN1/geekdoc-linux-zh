```
)
    boot() {
        echo boot
        # commands to run at boot
        # continue with the start() section
        start
    }
```

What happens here is that on startup, the USB script runs and mounts the USB memory stick in /mnt/usbdive. The GPS script comes next and starts GPSD on the other USB port. After that, the Kismet server starts up, waits 3 seconds for the other scripts to settle, then switches to the newly mounted /mnt/usbdive and then launches the server, saving the data to the memory stick.

Once all this is done and saved, you can restart the router. Log back in and verify that GPSD, the Kismet server, and the hotplug daemon are all running with the ps command.

# Monitor Installation

This assumes that you are using something like a stripped down PC or a WRT54GL as drones, since they are the cheapest and easiest way to get data into a monitor system.

Planning out your monitoring system is essential. If you are covering one access point, that’s as easy as putting the sensor right beside the access point, but multiple access points need a bit more planning as to coverage. As well, you probably want to answer some essential questions about what you want to monitor.

In a typical network, threats come from all around. Monitoring your network is a good idea, but if you don’t plan, you’ll find yourself buried in data and missing a great deal of information.