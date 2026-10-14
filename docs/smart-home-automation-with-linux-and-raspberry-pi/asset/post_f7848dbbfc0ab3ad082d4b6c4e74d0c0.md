
## Your Own Powered Devices

Even some hardened geeks balk at the idea of creating hacks with mains electricity.¹⁰ But with a little care and attention, you can add control to any mains-powered device, such as water heaters, heaters, garage door motors, and so on. To do so requires a controllable relay system, accepting a control signal and closing, or opening, a set of contacts that allows current to flow from the plug to your unit. You can even wire them directly to standard consumer equipment (like modems and printers) to reboot or power cycle them. There are a few options in this area.

### X10 Control

Building an entire X10 unit to control a motor, for example, is so far beyond the scope of this book that it wouldn’t be fair to try. Instead, I will show an inline appliance module, such as the AM12W, which handles the dirty work of processing the X10 protocol and results in a set of closed contacts between two of its connections. It works in the same way as the AM12 you saw in Chapter 1 (although slightly cheaper), but instead of controlling the flow of current to a plug socket, it controls the flow between the mains and the X10 unit and between the unit and the device. Figure 2-8 shows this wiring.

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_99_0.png)

This works for any unit that is remotely controlled only through X10. To support a local switch (either the on/off variety or a momentary push button), a better choice of module is the AD10. This also supports a manual override on the device, shown as the blue button in Figure 2-9.

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_100_0.png)

*Figure 2-9. The AD10 module*

Figure 2-10 shows the wiring; although both types of button are featured here, only one would be used in practice.

![](img/cbcdf34138bb96edef7aa6057d0d0d0e_100_1.png)

*Figure 2-10. Wiring an AD10 to a mains-powered device*

The main advantage of this module over the AM12W is that the switches used are standard electrical ones and not the (more expensive) X10 variety.

> **Note:** All devices should be grounded accordingly, not as shown in the figures for clarity.

### WiFi Control

With suitable electronics, you can connect a Raspberry Pi or Arduino to a WiFi board, and add some relays to control external devices. However, such hacking is not always necessary as some prebuilt devices already exist, which eliminate the need and worry of working with mains power.

One such device is the DIN Relay III (from [http://www.digital-loggers.com/din.html](http://www.digital-loggers.com/din.html)), which is WiFi enabled and allows you to control up to eight devices, powered by either AC or DC, at once. This has natural benefits of scale if you have several devices located in a cupboard under the stairs, for example. Even if your current house wiring isn’t home run (to a single location), this device makes such a task more tempting, because it provides a centralized control system with very little expense.

Although it has a scripting language (which is wholly ignorable!), it does have scheduling and a built-in status LCD that is controllable, and need not display information about the status of the unit.

### Low Voltage Control

For many applications, having control over a 115/240V power line isn’t necessary. This is because virtually all household devices work on much lower voltage, usually 24V or less. This includes a number of more modern 24V light bulbs. Therefore, instead of controlling the device at the plug, you can bypass it, and switch the current flow between the exit of the power supply and the entrance to the circuit board.

> **Note:** Some devices have dual power lines, such as a 3.3V and a 5V rail. In this case you will need a “double throw” relay so that both power circuits can be opened, or closed, at the same time.

This switching action can happen with any suitable relay. What determines a “suitable” relay is governed by the “contact ratings.” This is how much current, at a specific voltage, a relay is capable of safely switching. If this is exceeded, the relay could remain permanently on, or off, without any warning that it is doing so. These are always specified on the relays, or the switching units that use them. The National Electrical Manufacturers Association, or NEMA, have introduced a series of designations for both AC and DC, which indicate the type of current flow, and the maximum voltage.

You can build your own WiFi Relay Switch using an Arduino, a relay, and the guidelines above for digital output control of an Arduino. For those looking for a prebuilt solution, [http://www.relaypros.com/Relay/Relay-Wi-Fi_Relay](http://www.relaypros.com/Relay/Relay-Wi-Fi_Relay), and [http://www.relaycontrollers.com](http://www.relaycontrollers.com) (along with many others) both provide suitable functionality.

Of course, it needn’t be an Arduino controlling the relay, as a Raspberry Pi, or any form of microcontroller, can handle the task equally well. One famous case of this was “Feed Toby,” by Nat Morris ([http://natmorris.co.uk/feedtoby](http://natmorris.co.uk/feedtoby)) who used a microcontroller to release food pellets to his pet dog, via Twitter. In this case a motor was used instead of a relay.

### Conclusion

In the same way that you can build complex and evocative systems using a couple of well-chosen pieces of hardware, so can you build smart automation tools with a minimum of effort. By using alternate input devices, such as pressure mats and joysticks, you can change the way that you interact with your home. By adding alternate output devices, perhaps powered by old game consoles, you supply visuals to areas previously inaccessible to full-scale desktop PCs. And the introduction of robots and computerized welcome mats adds a level of previously unknown coolness to your home.

## CHAPTER 3: Media Systems: Incorporating the TV and the HiFi

The most visible part in any home environment is the media system. Ever since real fireplaces fell out of fashion, the TV or stereo system has become the focal point of most living rooms. The TV and stereo system are also the devices with which we spend the most time interacting. It is therefore essential that you understand the possibilities of these devices.

As with all consumer electronics, the feature sets and prices change on a daily basis. Therefore, I’ll concentrate primarily on the necessary features and inner workings of the machines without detailing specific makes and models because by the time you read this, other machines will already be available.

### The Data Chain

The simple act of “playing an album” changes significantly in the home automation field. Not only is the location of the media itself unconstrained, but it’s also the place where you can listen to it. This has been exemplified recently with iTunes, which allows you to play music on several different computers, and with Spotify, which provides a music-streaming service allowing access to various music tracks from your home PC or mobile.¹ If your interest in music is casual, or chart-based, then these services are often enough. But many people have albums in their collection that are either rare or obscure enough to not appear on any commercial-led web site. Some people might prefer to have their music data stored on their own computers, lest the company go out of business, change the terms of service, or lose connectivity in some other fashion. When this is the case, we need to provide a way of getting the music from a hard disk to the human ear. This is the *data chain*.

There are four steps in this chain. The first step is the data itself. This is the directory structure of WAVs, MP3s, or OGGs that represent the music (or other media) in your collection. This data is then read by a server (which is the second step) before being distributed (the third step) to one or more speakers in the house. The fourth and final step is when the human gets to hear (or see) the media. This model still applies when playing music on a portable music player or desktop PC, although for a desktop PC all of the logical units are held within one physical box.

### Extracting the Data

Often known as *ripping*, this is the process by which the media, usually stored on DVD or CD, is converted into a computer-friendly data format, ready for playback. Many pieces of software are available, so I’ll cover these with an example only.

¹ Access through a mobile phone requires the paid-for premium service.
