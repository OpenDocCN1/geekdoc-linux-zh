It’s then a simple matter of adding Samba shares for each directory:

```
```text
[media_tv]
    comment = Media (TV)
    path = /net/media/tv
    browseable = yes
    public = yes
    writable = no
    read only = yes
    guest ok = yes
```
```

As in Chapter 1, I create basic Samba shares that are read-only for the family and create separate ones for me that are password-protected and read-write.

Note also that I used my home’s subdomain (homenet) as a delimiter from the rest of the directory, instead of placing everything in /net. It allows me, as a software developer, to create my own subnet that isn’t part of the general home automation network in case I need to do something risky or experimental.

# Media Extenders

Once you have a file server providing access to your media, you then need some way of rendering the media, aurally or visually, to the world. This can involve stand-alone hardware, a Linux-based machine, or a combination of the two.

# Stand-Alone Hardware

To fit into this category, the hardware must connect the network, use DHCP to determine its IP address, and then stream the data from a file server to a physically connected TV or speakers. These devices invariably use Samba as a file server, because the installation of specific drivers (such as ZFS) is not a real-world possibility.

# Hauppauge MediaMVP

This device, despite dating from 2002, can stream music, standard-definition video, and pictures across the network and display them on a TV. The retail unit is fairly cheap, small, and silent, making it an ideal head unit. It comes with just three sockets: power, RJ-45 Ethernet, and SCART. (The U.S. version expands this last socket to S-Video, composite video, and stereo audio.)

To work, the MediaMVP needs three separate services:⁷ DHCP, TFTP for the bootup procedure, and Samba for data as it has no storage facilities of its own. Out of the box, these services are provided by a piece of Windows software, which has a number of limitations such as a slow menu system. The machine also prevents you from viewing any video that isn’t MPEG1 or MPEG2 encoded. This is because the video signal is decoded by a chip inside the MediaMVP that only supports these earlier codecs. Fortunately, the protocols used by the MediaMVP to boot up are standard, enabling you to use Linux as a server. You can then take this stage further by replacing the firmware that runs on the actual device, allowing it to connect to VLC to transcode your files to MPEG2 in real time.

⁷ The word *server* is used in this context to denote a physical piece of hardware, whereas a *service* is for elements of software that provide access to data or resources on a server. Confusingly, the most common name for these services are things such as *e-mail server*, *web server*, and so on.