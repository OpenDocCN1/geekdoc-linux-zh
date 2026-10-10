```
# GPS lock lost sound
# sound_gpslost=@sharedatadir9/klsmet/wav/bar.wav
# Alert sound
sound_alert=@sharedatadir9/klsmet/wav/alert.wav
```

Each event can have its own sound, and if you want, your own custom sound. Simply load your own WAV files onto your system and point each event at the sound you want to use. You can also enable only specific event sounds such as the new network or Global Positioning System (GPS) lock, lost by commenting out un-needed sounds lines.

```
# Do we automatically make a group for probed networks or do we show them
# amidst other networks?
autogroup_probe=true
```

The client can take and group all the probe networks (clients looking for networks) together. They will be listed under the `<probe networks>` group, and can be expanded by selecting the group and pressing **Enter** to show information about all the probe networks. If a probe is seen and then associated with a network, it will be moved to the client list for that network.

```
# Do we autogroup data-only networks?
autogroup_data=true
```

Like probe networks, the client can group *data-only networks* together in the same manner. Select the data networks group and press **Enter** to see the data networks.

```
# Do we autogroup adhoc networks?
autogroup_adhoc=true
```

Once again, we can group ad-hoc networks together just like probe and data networks. It is sometimes a good idea to set this as false, to see if anyone may be setting up ad-hoc networks that circumvent your security policies.

```
# Dsplay battery status?
apm=true
```

If your system has APM enabled, Kismet can report your battery status at the bottom left of the client. Useful if your running around on battery power and want to keep an eye on your time left before you have to plug in and charge up.

```
# Does the GUI talk to us with Festival?
speech=false
```