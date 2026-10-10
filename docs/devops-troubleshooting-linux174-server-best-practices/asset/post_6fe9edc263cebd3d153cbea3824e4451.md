
## Network Card Failures

When a network card starts to fail, it can be rather unnerving as you try all sorts of network troubleshooting steps to no real avail. Often when a network card or some other network component to which your host is connected starts to fail, you can see it in packet errors on your system. The `ifconfig` command you may have used for network troubleshooting before can also tell you about TX (transmit) or RX (receive) errors for a card. Here's an example from a healthy card:

```bash
$ sudo ifconfig eth0
eth0 Link:encap:Ethernet HWaddr 00:17:42:f1:18:be
in64 addr:10.1.1.7 Bcast:10.1.1.255 Mask:255.255.255.0
inet6 addr: fe80::217:42ff:fe1f:18be/64 Scope:Link
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:1 errors:0 dropped:0 overruns:0 frame:0
collisions:0 txqueuelen:1000
RX bytes:229 (229.0 B) TX bytes:2178 (2.1 KB)
Interrupt:10
```

The lines you are most interested in are

```bash
RX packets:1 errors:0 dropped:0 overruns:0 frame:0
TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
```

These lines will tell you about any errors on the device. If you start to see a lot of errors here, then it's worth troubleshooting your physical network components. It's possible a network card, cable, or switch port is going bad. Start with the easiest-to-test component by swapping out the network cable with a new or known good cable, and if you continue to get errors, then move the cable to a new, hopefully known, good switch port. Finally, if neither of those solutions help, try swapping out the network card (or switching to a different port if your server has multiple Ethernet ports).

## The Server Is Too Hot

Servers, especially busy servers, generate a lot of heat. Although ideally your server is collocated in a facility with good active cooling, it might also just be shoved under someone's desk, or it may sit at the top of a rack in a poorly cooled datacenter. A poorly cooled server can cause premature hard drive failure and premature failure in the rest of the server components as well. If that's not enough, modern motherboards often throttle the CPU down when it detects it is getting close to overheating, so even if your server doesn't fail completely, it may slow down to the point of being unusable. Other times, overheated components may cause processes to randomly crash.

If you suspect your datacenter may be running a bit too hot, one solution may be to purchase a rackmount thermometer that can monitor temperature for you. Rackmount thermometers work, but even if the ambient air is cool enough, a thermometer may not help you if your server is still too hot. Linux provides tools that allow you to probe CPU and motherboard temperatures, and, in some cases, the temperatures of PCI devices and even fan speeds. All of this support is provided by the `lm-sensors` package, which should be available for just about any distribution.

Once the `lm-sensors` package is installed, run the `sensors-detect` program as root:

```bash
$ sudo sensors-detect
```

This interactive script will probe the hardware on your system so it knows how to query for temperature. If you don't know how to respond to some of the questions it asks, just hit Enter to accept the default. Once the `sensors-detect` script is completed, you can pull data about your server by running the command `sensors`:

```bash
$ sensors
k8temp-pci-00c3
Adapter: PCI adapter
Core0 Temp: +34.0°C
Core1 Temp: +38.0°C

k8temp-pci-00cb
Adapter: PCI adapter
Core0 Temp: +32.0°C
Core1 Temp: +36.0°C
```

Different hardware will display different temperature readings. For instance, the previous code is from an HP ProLiant server whereas the following output is from a ThinkPad laptop:

```bash
$ sensors -f
acpitz-virtual-0
Adapter: Virtual device
temp1: +134.6°F (crit = +260.6°F)
temp2: +132.8°F (crit = +219.2°F)
thinkpad-isa-0000
Adapter: ISA adapter
fan1: 3756 RPM
temp1: +134.6°F
temp2: +122.0°F
```

As you can see in the second output, we not only got a fan speed, we also were able to see what temperatures were considered critical for a device. This example added the -f option as well, which will convert temperatures into Fahrenheit for you.

So, what do you do if your server is running too hot? For starters, examine the airflow around the server and make sure the vents in and out of the server aren’t clogged with dust. If the servers are in a datacenter that forces cool air from the bottom of the rack, you may want to consider moving particularly hot servers down closer to the floor (even if the servers aren’t in such a datacenter, the air is likely to be cooler closer to the floor). If you have room in your rack, also consider spacing your servers out more so none are stacked on top of each other. If you have the bad habit of not rack mounting your servers but instead installing a shelf and stacking servers one on top of the other, that will also contribute to poor airflow and overheating.

## Power Supply Failures

The final hardware failure this chapter will briefly cover is the power supply failure. Most modern server hardware has the option of having redundant power supplies so that if a power supply fails, the server stays up. Although complete power supply failures can be a problem, there really isn’t that much to troubleshoot there—the power supply shuts off and stops working. The power supply failure briefly mentioned in this section is one in which the power supply still technically works but can’t supply enough power.

When a power supply can’t supply adequate power either due to being underpowered or because it is going to fail soon, it can cause strange problems on the server. In fact, the symptoms are much like RAM errors, in that programs can randomly crash, but bad power supplies can also cause temporary failures in hard drives. In your syslog, you may see either SMART errors or possibly you may experience a file system error that causes your system to remount in read-only mode (Chapter 4 covers this type of error in more detail), yet when you do a RAM check or a follow-up SMART check, things come up clean. Many administrators, when faced with this kind of issue, just assume the motherboard or some other core component is starting to fail, and they will toss out the whole server!

So how do you tell when problems like this are caused by a bad power supply and not by bad RAM or failing drives? Generally, when a power supply starts to fail and can’t supply sufficient power, you’ll notice problems are more common when a system is under heavy load. For instance, you may notice you start getting more frequent file system errors when your build server is in the middle of a big build (although this may also point to a cooling issue as well). The simplest way to diagnose this kind of problem is basic troubleshooting: Swap out the power supply with a new one (or one from a known good system) and see if you can re-create the issue.
