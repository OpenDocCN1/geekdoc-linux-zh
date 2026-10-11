# MakerSpace

# Flexible HiFiBerry replaces old audio amplifier

# Musical Pi

A **HiFiBerry HAT**, the matching system, and a **Raspberry Pi** combine with two old speakers to create a contemporary boombox. By Tim Schürmann

![](bbox=[0.05, 0.44, 0.32, 0.56])

When my trusty audio amplifier bit the dust with crackling, hissing, and sound dropouts, the speakers and CD player from the hi-fi system still worked perfectly. My idea was to replace the broken module with a Raspberry Pi at a reasonable price. If it could receive music on Bluetooth, then all of my family members could feed it from their smartphones without leaving the couch.

A piggyback board from the HiFiBerry series combined with the matching system on a Raspberry Pi replaced this legacy audio amplifier. The system can play music sent over Bluetooth or other ways, and you can control it conveniently in a browser. However, the build and setup come with a few pitfalls, along with a few minor quirks in operation.

A setup like this is also useful for corporate meeting rooms: The presenter streams the audio output from the Raspberry Pi to the speakers, without wiring or even leaving their seat.

# Hi-Fi Berries

Of course, the Raspberry Pi only has one analog audio output, and it is not renowned for particularly good musical quality. To the rescue comes the Swiss company Modul 9, which offers various amplifiers for the small-board computer

SMB) under the HiFiBerry brand. You simply connect the small boards to the Raspberry Pi GPIO ports and plug the speaker cables into the sockets provided – that's all it takes.

The company also provides its own operating system (OS), HiFiBerryOS, which promises easy hardware startup and acts as a small audio center immediately after launching. Among other things, it accepts signals over Bluetooth and AirPlay or from a connected storage

# Tricky Manual Steps

> Raspberry Pi OS comes with all the drivers required for the HiFiBerry products. Instead of HiFiBerryOS, then, you could use Raspberry Pi OS and manually install all the required services. However, even setting up Bluetooth could cause you to break a sweat and lose half a weekend. If you still want to try it, you will find instructions online [1].
> Although it makes sense to shut down Raspberry Pi OS gracefully, most people simply switch a boombox or hi-fi system on and off with the power switch. For this to work, you need to run the system completely in main memory. However, setting up this kind of configuration is time consuming and complex. Going for HiFiBerryOS will take you to your goal far faster and is easier on your nerves.