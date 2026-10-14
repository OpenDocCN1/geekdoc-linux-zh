
**Note** With most UPS units, the power sockets will be divided between those that are powered in the event of an outage and those that aren’t. All sockets are generally protected against surges.

Given, say, four powered sockets, you have to decide what devices will use it. Naturally, your server should be a given. That’s followed by the home’s internal router switch so that a “shutting down” message can be sent and processed by the other machine on a UPS. (This is for the computer’s benefit only, since any human will have noticed the lights going out and will instantly panic knowing they haven’t hit the Save button on their application.) You may also want to keep the broadband router on the UPS also so that a warning message (via e-mail, for example) can be sent. This is usually a minor consideration, but if you work remotely with the machine, this will prompt you to ease up on any processor-heavy tasks so that the UPS can last for longer.

**Note** When the UPS is first installed, test it with the circuit breaker but not by pulling the plug out, which can introduce a floating ground that is dangerous to electronic equipment.

The discussion of multiple servers reappears here, as it can be beneficial to have a low-power master server on the UPS, with the media-transcoding machine on its own UPS, to preserve the longevity of the main server and even finish recording that vital episode of *Doctor Who* you might have normally missed during the power cut!

If both servers are fairly high power and you have only one UPS, then it is usually worth consolidating both into one box to limit the power drain on the unit.

You may also consider keeping one powered socket for a monitor, perhaps connected to the second media server UPS unit. If you keep it turned off, it’ll draw very little power from the UPS, but in the event of a problem, you are able to see the machine running through its shutdown procedure, and you can ensure that its closedown routine is working effectively. Without this, you will either have to trust the UPS software daemon is working or keep a laptop handy with a fully charged battery.

**Tip** You can ensure your laptop is fully charged by using the crontab to switch on an X10 module for at least an hour every night.

Once the hardware UPS is in place, you then need a way to detect that the power has gone and so begin the shutdown procedure.

Most UPS units come with a USB cable (sometimes with a proprietary connector on one end, so don’t lose it!) that allows a PC to query the state of the unit. Those that don’t have one are not generally worth buying. Granted, they are cheaper, and your data is probably safe with the journaling filesystem you’ve already installed, but the extra cost and peace of mind knowing you’ll get a clean shutdown is worth it.

**Note** It is possible to mimic the shutdown functionality of a UPS by using heyu to monitor the power lines and, if it sees two (or more) lights going off at the same time, trigger a shutdown. But this method is liable to false positives and doesn’t work during daylight hours.

Three primary packages are available to handle a UPS, all of which conflict if used together. They are apcupsd, nut-hal-drivers, and nut. I’ll cover the latter because it is the most recent, flexible, and actively developed.

First, perform a traditional installation:

```
apt-get install nut
```

The setup procedure then involves creating four configuration files in your /etc/nut directory:

```
# /etc/nut/ups.conf
[apc]
    driver = usbhid-ups
    port = auto
```

This references the appropriate driver for your UPS unit, which I have called apc here:

```
# /etc/nut/upsd.conf
ACL all 0.0.0.0/0
ACL localhost 127.0.0.1/32
ACCEPT localhost
REJECT all
```

This indicates that only the local machine should react to UPS messages, which eliminates hackers spoofing a UPS failure and causing your machine to switch off. Then set up a basic user that has access to daemon by doing this:

```
# /etc/nut/upsd.users
[local_mon]
    password = mypasswordhere
    allowfrom = localhost
    upsmon master
```

You can then configure the daemon by specifying its process commands:

```
# /etc/nut/upsmon.conf
MONITOR apc@localhost 1 local_mon mypasswordhere master
POWERDOWNFLAG /etc/killpower
SHUTDOWNCMD "/sbin/shutdown -h now"
```

You can set up multiple users if you will be monitoring the UPS from alternate machines, but it’s not necessary, as you’ll probably create a web page holding this information.

You can then fix the permissions for the files (as there’s a password in there you’d probably rather the world didn’t see):

```
sudo chown root:nut /etc/nut/*
sudo chmod 640 /etc/nut/*
```

and start the daemon running, like so:

```
upsdrvctl start
/etc/init.d/nut start
```

This can be made to start at every boot by editing the `/etc/default/nut` file. You can then query the state of a given UPS and check that it’s working by issuing the following command, where `apc` is the name given earlier:

```
upsc apc
```

The output is something like this:

```
battery.charge: 100
battery.charge.low: 10
battery.charge.warning: 50
battery.date: not set
battery.mfr.date: 2009/01/21
battery.runtime: 705
battery.runtime.low: 120
battery.type: PbAc
battery.voltage: 13.5
battery.voltage.nominal: 12.0
driver.name: usbhid-ups
driver.parameter.pollfreq: 30
driver.parameter.pollinterval: 2
driver.parameter.port: auto
driver.version: 2.2.2
driver.version.data: APC HID 0.92
driver.version.internal: 0.33
input.transfer.high: 266
input.transfer.low: 180
input.voltage: 242.0
input.voltage.nominal: 230
ups.beeper.status: enabled
ups.delay.shutdown: 20
ups.delay.start: 30
ups.firmware: 829.D2 .I
ups.firmware.aux: D2
ups.load: 49
ups.mfr: APC
ups.mfr.date: 2009/01/21
ups.model: Back-UPS ES 700
ups.productid: 0002
ups.serial: 5B0904T46000
ups.status: OL
ups.timer.reboot: 0
ups.timer.shutdown: -1
ups.vendorid: 051d
```

It is possible to have several UPS units controlled by a single server. This is usually beneficial because it allows your master server to handle all the system administration tasks, giving a single point of entry to the home network, which can be hardened as appropriate.

Having gotten the machine to shut down, you need a way of making it start up again once the power is back on full time. This becomes a hardware problem, and success is governed by whether there is an option in the BIOS to start up on power or similar. In the case of the NSLU2, you can physically hack the circuit board to perform the same task. It is also theoretically possible to hack the switch in a standard PC in a similar fashion, but it’s not recommended.

The WOL trick covered earlier generally doesn’t work across the Internet because it is a Wake on LAN feature. And even if your machine isn’t behind a router or modem that filters out such packets, something else generally will be. If it’s vital for your home machine to be powered for as long as possible and your machine cannot be made to boot when the power is connected, then you can employ an NSLU (hacked as shown in Chapter 2) as a bootstrap to issue WOL commands to your various server machines.

## Backups

There are only two important things to say about backups:

- Do them.
- Test them.

Everything else is mere details.

The first detail is whether these should be held on-site, that is, at home, or off-site in a remote location, such as a colocated server or hired virtual machine. In an ideal world, you would adopt both. Keeping them off-site helps minimize loss caused by local problems, while on-site backups are useful for data that you cannot possibly store elsewhere, such as configuration scripts and network plans that you’d need to rebuild the HA system should there be major failure.

The next detail is what data actually needs to be backed up. Again, in an ideal world, that would include everything on every machine in the house. In reality, you have to consider the cost of replacing the data and the time necessary to perform the backup. This usually boils down to anything that you’ve personally created, such as the following:

- Photographs
- Letters
- Program code
- Artwork
- Digital video
- Music

Each member of the family will have their own list that they will be responsible for. You, as the HA administrator, will also want to back up the server configurations.

From here you can decide on the technology needed to carry out this task. Programmers will already be aware of source control tools, such as Subversion ([http://subversion.tigris.org/](http://subversion.tigris.org/)) or Git ([http://www.git-scm.org/](http://www.git-scm.org/)), and will be adopting their use. For the uninitiated, these tools don’t just keep a copy of the latest version; they keep data to recreate copies of all the versions you’ve ever created, allowing you to go back in time to see what you wrote last week and what that does (or doesn’t) work! For the most part, it’s a good choice for code and system configurations because, as a developer, you have the mind-set necessary to perform the necessary update-merge-commit cycle at every juncture. However, with some coaxing, most family members will be able to work with it. Accessing the files requires a Subversion client, and there are several to choose from (such as TortoiseSVN or SmartSVN) that also have versions for Windows, eliminating that support headache. This also gives family members the ability to access their files from outside the home with no extra effort or software. On the downside, however, you will have to educate the family that word processing documents are usually stored in a binary format and, as such, are next-to-impossible to merge together if they change the same file at home and at school. Nor is it particularly efficient to use source control for large files that change often, such as raw Adobe Photoshop images.
