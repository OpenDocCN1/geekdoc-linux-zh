
The capital X switch will disable the channel hopper, if it is not already disabled.

-f, --config-file <file>
Use alternate config file

If you need to specify an alternate location or an alternate filename for your config file, the -f switch will do that for you.

-c, --capture-source <src>
Packet capture source line (type,interface,name)

Sometimes you need to specify another capture source. Much like in the config file, it consists of the type (see the README for allowed types), the interface name, and a description with no spaces and all comma separated.

-C, --enable-capture-sources Comma separated list of named packet sources to use.

If you have multiple sources in your config file, you can fine tune which ones are enabled with the -C switch and listing the descriptions you included in the config file.

-p, --port <port>
TCPIP server port for stream connections

Due to firewalls or other restrictions, you may need to specify an alternate port to serve up connections from on the drone. If you do so, you'll have to adjust the source= line on your server system to connect to the new port.

-a, --allowed-hosts <hosts> Comma separated list of hosts allowed to connect

To add a host to allow connections from temporarily, use the -a switch and the IP address.

-b, --bind-address <address>
Bind to this address. Default: INADDR_ANY.

On multi-homed systems the drone defaults to accepting connections from any configured address. If you want to restrict connections to one address, use the -b switch.

-s, --silent
Don't send any output to console.

Particularly useful in testing is to suppress output from the drone when it runs.

-N, --server-name
Server name

For organizational purposes, you can change the server's name. This doesn't show up anywhere major with drones, so no need to worry about it.

-v, --version
Kismet version

-v outputs the version of the kismet_drone

-h, --help
What do you think you're reading?

If you find yourself without this book handy, the -h switch will show you the options available.

## Summary

Drones have limitations and some quirks. You want to be careful how you set up the backhaul to make sure you don’t interfere with normal operations. In most situations, you want to backhaul from your drone to the server over a wired network. Some people try to send the data from the sniffer back over a wireless, which can get you into a great deal of trouble. If you are monitoring the data you are backhauling, you’re then capturing it again and broadcasting it back to be sniffed again and getting into a very ugly loop that will likely saturate things very quickly. Also, if you are monitoring a heavily used wireless network and sending the captured data back over the same network, you are effectively doubling the amount of data going down the wire. This can be an issue if you are already near capacity.

For the headaches it saves and the extra data you have to deal with, it’s best to run the drones over a separate network from what you are monitoring. Be it through separate wires or Virtual Local Area Networks (VLANs), this will save you a great deal of time and effort.

Currently, drones are a pull-type connection. When the server starts, it connects to all the drones listed as *source*= lines and requests data to be sent, and if the drone is functional, it does so. The current architecture of Kismet does not support dynamically adding sources beyond the startup of the server. This means that if a drone goes down, you have to restart the whole server to bring it back up. This is being addressed in kismet-newcore but for now, if something downs a drone, it takes a server restart to bring it back online.

Drones can be a very cheap and efficient way of extending your view of the network into the RF layer and to see beyond just TCP/IP packets and see what is going on in the lower layers of the stack at remote locations. Drones can be nearly any type of system that runs Linux, has a backhaul method, and a compatible wireless device. Some devices have their own quirks and issues. A bit of research and development will save you some headaches and hopefully some money.

# Kismet and Mapping

Solutions in this Chapter:

- GPSMap/KisMap
- WiGLE
- WiGLE Google Map
- IGIGLE
- GpsDrive
- Alternatives
- Summary
- Solutions Fast Track

## Introduction

Kismet's data formats are well-suited to allow integration of this data into other tools and programs. In terms of Kismet, the tools that are often most helpful or useful are mapping programs. The focus of this chapter will be on the use of mapping programs (both native and third-party) to enhance Kismet's ability.

## GPSMap/KisMap

Kismet's native mapping tool is known as GPSMap. GPSMap is designed to download maps from online repositories and overlay Kismet networks onto them. GPSMap's features include:

- Travel path/track
- Approximate network circular range
- Approximate network center
- Convex hull of all network sample points
- Interpolated (weathermap-style) graphing of power and range
- Labeling of network centers
- Scatterplot of all detected packets
- Legend showing total sample networks, visible networks, colors, power ranges, network center, and so forth

> NOTE
> Unfortunately, the current incarnation of GPSMap is hobbled by the fact that most of the source data for the maps is no longer available. GPSMap has been patched to use Expedia data, but this is only available for Europe. To remedy this situation, you can patch GPSMap to work with Google Maps (see below).

### Patching GPSMap

You can patch GPSMap to work with Google Maps, but this also presumes that you have a place to display those maps (i.e., your own Web server).

First, download the patch (http://parknation.com/gmap/files/gpsmap-gmap-0.1.tgz). Then, uncompress and apply the patch to the source and compile the binary:

```
tar xzf gpsmap-gmap-0.1.tgz
cd /pentest/svn/kismet-devel
patch -p0 < /root/gpsmap-gmap-0.1/gpsmap-gmap-0.1.diff
./configure
make gpsmap
```

Next, copy gpsmap to your desired location. Then, copy index.html and the mapfiles folder from /root/gpsmap-gmap-0.1 (or wherever you uncomprsessed it) to your web server. Run gpsmap against one of your Kismet .GPS files:

```
gpsmap -j -o gpsdata.js -u -r Kismet.gps
```

Your output file, gpsdata.js, should be copied to your Web server. Finally, you'll require a Google Maps API (http://code.google.com/apis/maps/signup.html). When you get your key, paste it into the index.html file (conveniently, where it says “KEYHERE”). This process is a bit complicated, and it does require that you have a Web server, but the results speak for themselves.

## KisMap

Due partially to the lack of map sources and the limitations of the patches, GPSMap is currently being re-written from the ground up as a new python-based tool (currently known as KisMap). KisMap works with Google Maps (something that was not originally supported in GPSMap), with other formats likely to come in the future.

## WiGLE

As has been mentioned in the BackTrack chapter, WiGLE (Wireless Geographic Logging Engine) is an online database that includes in excess of 15 million recorded wireless networks, most with geographic coordinates. WiGLE gives you access to Service Set Identifier (SSID) and manufacturer statistics, octet and channel usage statistics, and a browsable Web map of the world (see Figure 9.1).

**Figure 9.1** WiGLE Web Maps Display of the Baltimore-Washington, DC Corridor

![](img/d6ac176c353d2b7687c1186a140180a1_230_0.png)

## WiGLE Google Map

WiGLE Google Map (http://wgle.rustyredwagon.com/) is a Web-based tool that displays WiGLE data on Google Maps. Simply enter an address, select the type of networks you’d like to see, and WiGLE Google Map will query the WiGLE database and display the appropriate network data on the map.
