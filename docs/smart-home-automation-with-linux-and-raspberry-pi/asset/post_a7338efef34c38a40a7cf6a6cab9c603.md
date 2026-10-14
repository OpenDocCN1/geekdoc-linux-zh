
For the geek, the primary difference is in the software because the protocol is closed, making Linux tools impossible. To reclaim this market, Clipsal has released an RPM containing a binary-only driver that is available for zero cost on its website.

**Note:** A Red Hat package manager (RPM) can be utilized on non–Red Hat platforms such as SUSE or converted using tools such as Alien. The biggest problem with drivers packaged in this way, however, is its level of compatibility with the Linux kernel. Any change in the driver API, or similar breakage between kernel version numbers, will render the driver (and therefore your C-Bus system) useless. In these situations, when there is no more open solution available, it is always best to keep a low-level legacy system available and be prepared to migrate other software away from the box when necessary.

Unlike X10, each C-Bus device contains a microprocessor that makes it possible to control other devices remotely, without a computer. This is provided by switching the device into one of its five modes, which break down roughly as follows:

- Normal, stand-alone, switch
- Basic peer-to-peer switch control
- Networked switch control
- Networked switch control, with remote
- Interfacing with a wired C-Bus install

The adscititious computer is of benefit to smaller HA installations and those concerned about complex lighting UI. But for those of us intending to control other devices, the inclusion of a PC is not an issue.

## Devices

Like X10 devices, C-Bus has the ability to dim lights and control appliances that are attached to it. Where they differ is the ability of a C-Bus light switch to control one or more other devices straight out of the box and with minimal on-device configuration.

**Note:** I’ll consider only the wireless devices here, for the reasons given previously.

## Controlling Lights

There are two designs of light switch, Neo and Saturn, which fall in the 5850 and 5880 product ranges, respectively, and differ by their decorative styles only, although within each group you have the choice of two-, four-, six-, and eight-button versions. They are always paired, with the first two buttons controlling the dim function of the connected lightbulb. Each subsequent pair is required to transmit the button press information (wireless) to another device (provided that they are configured in a networking mode) or devices. Because of the built-in microcontroller, these switches can be configured as a dimmer switch, an on/off pair, a remote trigger, or a scene trigger (the latter being the C-Bus term for macro programming, where several state changes can occur on several devices at the same time). Scene programming can also occur through the C-Bus Toolkit Software, although this is currently available only for Microsoft Windows.

There are several devices in each family, capable of various support loads and characteristics, but generally speaking a C-Bus dimmer will support incandescent and halogen lamps between 25W to 500W (up to 2A), along with fan motors (up to 2A).

These two series also provide basic switch units. These appear the same as their lamp-controlling counterparts, except that they lack the dim functionality. By way of compensation, they can support a much greater range of devices (up to 2KW, and 8A in places) including fluorescent lights.

> **Note:** There appear to be no in-wall units for sale, meaning you cannot use wireless C-Bus electronics with your own style of face plate.

## Controlling Appliances

Like X10, C-Bus provides an appliance module that plugs into the wall and controls the flow of current to its corresponding socket. These are known as the 5812 series plug-in adapters and look like their X10 counterparts, with the exception that they, too, support dimming and switch versions.

Because every C-Bus device includes a microcontroller and the C-Bus protocol supports the remote programming of other devices, any of the light switches mentioned earlier can also be used to control an appliance switch by programming an “association” on the switch, equivalent to a Linux symbolic link.

## Controllers

The Series Wireless remote control 5888 is the main device here. It is an RF transmitter (operating at 433.92 MHz) supporting ten devices up to 70 meters away (although 25 is more likely inside a building). Because of the unified design of all C-Bus modules, it is technically possible to control more than the allotted ten devices by using the remote to control one switch, which in turn controls another two through the use of a scene. Furthermore, no RF gateway is required to use this remote, since the C-Bus wireless network is already operating on RF. This also means that multiple remotes can control any individual device, and any individual button can control multiple devices.

Like X10, it also supports an “all off” message.

## Gateways

With so much emphasis on the wireless network, it is sometimes necessary to revert to wires. This is where the Wireless Gateway C-Bus 5800 Series comes in. This is a necessary feature and the only way that the wired and wireless versions of C-Bus can be connected together. Also, through the use of software such as C-Bus Toolkit, it can be connected to a computer for remote, sequenced, and intelligent control. Consequently, this device is also necessary for a wireless-only network that needs to feature PC control because the 802.11 wireless protocol used by commercial routers is not suitable as a C-Bus wireless gateway.

## Lighting Control

In addition to the general purpose appliance controls that I’ve discussed, there are also a number of specific controllers for lighting. This is a recent development, but not a great surprise, since lighting is one of the major contributing factors in uptake for home automation. Most of us start with a controller light switch, after all. Given that lights are a specific case, it is therefore possible to add extra functionality to the communication protocols which would make no sense if it were a traditional appliance, such as colour.

**Note:** Although many bulbs class themselves as WiFi, this is rarely the case because they communicate to a hub, which in turn talks to the network.

## Hue

Designed by electronics giant Philips, this is the most prominent lighting-only solution at present. The basic starter kits provide a control hub and three bulbs, although the unit can support up to 50. This hub connects to both a wired Ethernet port and a power socket. It then uses the ZigBee light link (wireless) protocol to talk directly to the bulbs.

Hue’s biggest selling point is the color; or, rather, its range of colors. Each screw bulb supports a dynamic range of colours, selectable from a color wheel on the app. These colors may be picked from a photo, and programmed into a scene, so that the three lights are able to reflect the color scheme of your room, maybe by enhancing the colors present in your mantelpiece photograph, for example.

Configuration is automatic (as you’d expect for a consumer device) and the hub acquires its IP from your DHCP server, which serves a web page that redirects to the Hue online service where you can register your device and make a connection between the (online) account and your bridge. Once this has happened you can operate it remotely through the web site. This works through a polling protocol whereby, every half second, the Hue bridge makes a call to the Hue server to request any new commands, and update the server of the bridge’s IP. You can verify that the Hue website can see your bridge by browsing to http://www.meethue.com/api/nupnp.

Alternatively, you can control Hue through your phone, with both iOS and Android devices currently supported. For those of us working with open source, the reliance on an app is an occasional bind, although Philips have just launched their API that allows you to talk directly to the hub to control the lights. This is available at http://developers.meethue.com/coreconcepts.html. After getting the IP of your bridge, you must set up a user by pressing the “link” button on top of the bridge and then, within 30 seconds, issue the command:

```sh
$ curl -H "Content-Type: application/json" -X POST -d '{"devicetype":"myhome"}' http://192.168.0.27/api/
```

that returns a JSON object with a username, such as d7ae8b2151d50df1e61f380289f33bf, which should be used in all future requests.

You can then ask the bridge to search for lights on the system with:

```sh
$ curl http://192.168.0.27/api/d7ae8b2151d50df1e61f380289f33bf/lights
```

It will take a few moments for the scan to happen, before you can re-issue the command to get those available, returned in the form:

```json
{"1":{"name": "Hue Lamp 1"}}
```

From here the fun begins as you can query the state:

```sh
$ curl http://192.168.0.27/api/d7ae8b2151d50df1e61f380289f33bf/lights/1
```

```json
{
  "state": {
    "on": true,
    "bri": 254,
    "hue": 14922,
```
