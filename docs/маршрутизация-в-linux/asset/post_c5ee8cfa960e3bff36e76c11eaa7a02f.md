
Chapter 12, "Network Hardware Components, Technology, and Solutions," covers hardware types in detail and discusses how to deal with whatever connection type(s) you have.

## WANPIPE

One WAN package for Linux is the WANPIPE package. To utilize this package you'll need a supported card, and you'll also need to compile support for WAN Router and WAN Interfaces in the Linux kernel. (See Chapter 13, "Building a Routing Kernel," for a walk-through on kernel compilation.)

If you need the WANPIPE package, you can download it from the Sangoma FTP server ftp://ftp.sangoma.com/linux/current_wanpipe/. This directory also includes a README that might contain information newer than what we have as of this writing. Follow the instructions in the README.install, and you should be ready to go. If you're a Debian GNU/Linux user, it's even easier. Simply run:

```
apt-get update
apt-get install wanpipe
```

as root, and apt-get will download and install the package for you automatically, assuming that you have a valid download site in /etc/apt/sources.list for the packages. Note that packages in the Debian GNU/Linux "stable" release are usually not the most recent packages, so if there's a brand-new feature that you need, you might need to install the version from testing or unstable.

The wanpipe program calls the wanconfig program, which loads a configuration file with the proper options for your WAN card. The /etc/wanpipe/wanpipe1.conf configuration file is a symlink to the /etc/wanpipe/router.conf file, which contains all of the information about your WAN device or devices, the definitions for your WAN interfaces, and a hardware and physical interface section.

The usage of the wanpipe is very simple; the only difficult thing might be to get your configuration file set up correctly. Because there are so many options for the configuration file, we won't try to delve into them here. However, the Sangoma folks maintain a mailing list for WANPIPE, and the odds are if you pop into the list and detail your setup, someone on the list will be able to give you the information you need.

To start your WAN devices after you've gotten the configuration file set up, simply issue the command:

```
wanpipe start
```

which will start all of the devices that are listed in your configuration file. If you need to shut down the WAN interfaces then use:

```
wanpipe stop
```

As you might have guessed, it's also possible to stop or start individual devices, by using:

```
wanpipe start | stop wanpipe#
```

where the "#" is the number of the interface. The device numbering starts at 1, and you are allowed up to 16 devices, which should be more than enough under normal circumstances.

## VPN Routing Basics

Typically, VPNs are set up through a firewall rather than a router. However, because we're using Linux we've got the flexibility to combine the two. Alternatively, you could still use Linux for the router and firewall/VPN but build them on separate boxes for security purposes. Whatever you want to do, Linux is flexible enough for you to do it.

A VPN is an alternative to expensive leased lines that are closed to other network traffic. By making use of the Internet as a bridge between networks, companies can save a lot of money and still be secure by utilizing a VPN.

## A Little More About VPNs

As you probably already know, VPN stands for Virtual Private Network. Because the Internet is hideously insecure, you wouldn't want to transmit any important data over the Internet unencrypted. For folks doing commerce, we have HTTPS. For people who just want to run a shell or X sessions, there's SSH. But what if you want to join two far-flung networks together securely and share all the common resources across the Internet? That's where VPNs come in.

The metaphor most often used to describe the method of connecting two networks securely is a tunnel. You think of the communications taking place between the two networks as being inside a few layers of outer coating. You're still using TCP/IP to transmit your data, but instead of unencrypted data being transmitted, the data is encrypted so that even if a potential attacker can intercept your packets—something you have no control over on an unsecured shared network—they shouldn't be able to make any sense out of the packets themselves. Your data is (theoretically) safe from prying eyes, and your network is safe from intruders.

So it's considered a private network even though the transmissions take place over a public network. It's not always as convenient as a WAN, but VPNs can prove a very useful substitute where budget and resource constraints make WANs impractical or when time and mobility are factors. For instance, you might wish to implement a VPN to allow Linux-based Point-of-Sale terminals to operate over a dial-up to interact with a central credit-card processing machine for your company while doing sales at trade shows.
