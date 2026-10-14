# Determining the Best Room

Even the humblest of abodes has several locations suitable as Node0. Most people choose the closet under the stairs (as it’s central and therefore requires less wiring), but there’s more to it than that! In fact, while reading the next section, you are expected to mentally move the server from one room to another as each problem or solution presents itself. Furthermore, in some cases, it’s not physically possible to find one room that can solve all of the particular problems, in which case you may have to drop the offending feature or use a second server in a separate location.

# Lawful Considerations

Laws vary according to country and change over time, so it is important to take the necessary advice and acquire any permissions before work is begun. In reality, this affects very few people, such as those who are building new structures on their land (such as sun rooms) or amending buildings that have been granted “graded” or “listed” status.

# Necessary Considerations

The necessary considerations in this section cover the limits of particular pieces of hardware and their interconnects. Because the main server will need full unfettered access to all your equipment, these considerations are of primary importance.

X10 signals can dissipate and get swallowed whole by various devices placed around the house, as mentioned in Chapter 1. Moving the Computer-X10 gateway (CM11) to another socket can change its reach quite considerably, so a lot of testing is necessary. Alas, it might not be possible to place the device in any single location that allows the messages to make a complete circuit in both directions around the house. This would subsequently require two servers or two gateways.

Ethernet over Power (EoP; not to be confused with Power over Ethernet) is one way of adding two-way networking capabilities using the existing power lines, in the same way that X10 introduces appliance control. Like X10, it is at the mercy of other devices on the power line, so should parts of your home become inaccessible to WiFi, this approach should be tested also.

Broadband and cable modems can often enter the house only at a number of predetermined points, thereby limiting the rooms available. It is, however, rarely necessary to have your server connected locally to the modem unless your Linux machine is acting as the gateway to the rest of your home. In most cases, a good router can effectively separate the internal and external network traffic with enough control to make the use of a full-blown PC unnecessary.

WiFi signals, like X10, dissipate. Furthermore, because the frequency band used is common to many other protocols, this can cause the connection quality to worsen considerably or disappear altogether. These devices include some wireless access points (such as the United Kingdom’s BT Homehub), wireless phones, TV senders, and microwave ovens. Furthermore, because they travel through the air, they’re more susceptible to external influences outside of your control, such as neighbours. You can limit the effect of these other devices by doing the following:

+   - Switching the WiFi channel. Depending on the country, WiFi is split into either 14 (Japan) or 13 (everywhere else) distinct frequency bands with each channel occupying a group of 4 or 5 of these bands. This places channels at midpoints at channels 1, 6, and 11 (for the United States) and 1, 5, 9, and 13 in most other places.
+   - Adding more WiFi base stations to minimize the distance necessary for each signal to travel. When setting this up, set all units to the same SSID, and connect to the same section of wired Ethernet.
+   - Switching to wired versions of the offending devices. To determine the offending device, simply turn them off in sequence, and/or point a spectrum analyzer in each direction to determine the source of the transmissions.
+   - Jamming the signal of the offending device (particularly if it originates from someone else).
+   - Using directional transmitters.