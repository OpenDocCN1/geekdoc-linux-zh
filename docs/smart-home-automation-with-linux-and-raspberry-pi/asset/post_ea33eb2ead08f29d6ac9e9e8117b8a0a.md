
When considering the low-level hardware implications, be aware that the full documentation for the Broadcom BCM2835 chip (which does all the main work) is unavailable without an NDA. Most people will be happy using it at a higher level, even programming the GPIO, or working from the kernel source. But if you’re hoping to be educated on the internal workings of a SoC, or wanting to investigate the drivers, then you’re out of luck and should look to the fully open options out there.³

³ A partial list of these alternatives can be found at http://www.bigboardlist.com.

From an interfacing point of view, the lack of VGA port is the one with which most people will be concerned. Although the Raspberry Pi Foundation considers VGA to be an antiquated technology, the reality is that there are many good value monitors available that don’t support HDMI and so requiring you to buy a separate converter. This problem is compounded when looking for small monitors, as there are very few of the smaller incarnations of HDMI available and (as yet) no definitive compatibility list. (HDMI on Raspberry Pi seems to have a worse issue of compatibility than HDMI on desktop PCs.) Consequently, you may be forced into using the composite video to make use of a small display, at which point you’re using an even older technology than VGA, and worse visual quality to boot. Other visual hook-ups include the Kindle (needs a jailbreak and a terminal emulator, as covered at http://www.punuku.net/2012/09/kindleberry-pi), iPad (just use a standard terminal emulator), or even an existing digital photo frame (http://www.cjbj.com/2012/06/raspberry-pi-wireless-display-using.html).

**Caution** If your HDMI device is not correctly detected you will need to edit the `/boot/config.txt` file to include parameters to explicitly define it. This appears as two lines, such as `hdmi_group=1` and `hdmi_mode=2`, with the parameters indicating the type of HDMI (CEA or DMT) and the resolution. Both are described at http://www.raspberrypi.org/phpBB3/viewtopic.php?f=26&t=5851.

The biggest single problem with the Raspberry Pi appears to be the implementation of the USB stack, with issues in both hardware and software. Although the situation is improving, anything that needs USB to be of a “mission-critical” nature might need to be redesigned. This, unfortunately, includes Ethernet as that is provided through USB. (This is also why you can’t have gigabit Ethernet on the Raspberry Pi–you’re limited by the speed of the basic USB port.)

At the time of writing, the USB issues haven’t been entirely solved, but the crux is thus. The hardware component inside the Broadcom chip, which handles the USB port, isn’t particularly good and the driver (dwc_otg) that attempts to tame it has some issues whereby if a NAK packet is received, the processor gets interrupted. At this time (but only some of the time, it seems) the hardware portion of the USB stack resends an IN packet . . . that generates another NAK packet... that causes another interrupt on the processor. And so on. This very quickly leads to an interrupt cascade problem that can render the Raspberry Pi unusable for 20 seconds or so. For an interesting discussion on this topic, and why the Raspberry Pi has 8000 interrupts per second when idle, the thread is still open at http://www.raspberrypi.org/phpBB3/viewtopic.php?f=28&t=7866&start=111.

One fix to this problem is to disable the USB entirely:

```
echo 1 > /sys/devices/platform/bcm2708_usb/bususpend
```

Naturally, this prevents the keyboard from working. And with Ethernet being controlled through USB also, this means that you can’t remotely control it to make it communicate with the outside world. It is possible to connect a keyboard or similar device through the GPIO, but such circuitry is outside the scope for this book. There is also some online discussion on whether the Raspberry Pi (Model A) avoids this problem, or whether it hasn’t been witnessed as often. A thread, more detailed than the official one, can be found at http://www.element14.com/community/thread/18568.

## Typical Projects

The Internet is awash with uses for the Raspberry Pi; so much so, that many might think that it is a solution looking for a problem! This is a standard behavior. With any new technology, there is always a cry of “could I do X on the Pi,” where X equates to any task they wanted to do on another machine. We shall now consider some of these projects, and how they can be realized but, more importantly, cover many more that are only possible because the Raspberry Pi is cheap enough, or small enough, to allow such ideas to come to fruition.

### The Telephone

The widespread use of mobile phones and the Internet have changed many businesses. Some, like the postal service, continue to argue for an “e-mail tax” to supplement their dying business model. Others, like the telecoms, are looking for new ways to sell their existing services in a world where the Internet providers can undercut them in most areas. One obvious area is in voice over IP, where traditional telephone calls can be made for virtually nothing on the Internet, instead of land lines. Indeed, you can even use an “all you can use” data package to run Skype on a mobile phone and bypass the phone charges of your mobile provider!

For those interested in VOIP solutions, you can leverage the Raspberry Pi’s small size by including it inside the drawer of the telephone table (for those that still have such things!). This can then be loaded with Asterisk, or other PBX software, to provide an internal phone system that may be as effective as another VOIP-based intercom systems. A Raspberry Pi placed in this location also provides a suitable excuse to use it as a charging and sync station for your mobile phone. As you return home, your phone can be placed in the Raspberry Pi-connected cradle, and the day’s photographs can be copied (i.e., backed up) to your home network server automatically.

### Child Minding

The Raspberry Pi’s size also gives you the opportunity to mount one inside a teddy bear to provide a comforting story telling device for the kids, while doubling up as a child safety monitor once they’ve gone to bed, by using a basic webcam and microphone combination. This can work both ways to include VOIP functionality, with all data streamed through Ethernet or a separate WiFi board. There is a Raspberry Pi-approved camera module in development, which should be ready by the time you read this.

Construction of such a model is simple. A “bedtime bear” is best, as they are largely devoid of stuffing, as the child is intended to place their nightclothes inside them. Instead of nightclothes, however, you can stuff the bear with a Raspberry Pi! This is one of those projects that is only possible because the Raspberry Pi is small enough. So much so, in fact, that you will need to add some stuffing back, as most bears are large enough to take a cased Raspberry Pi, a battery pack, and assorted peripherals!

As it is made of fabric, there is no easy way to screw a Raspberry Pi board into the bear, so sew a small pocket into the inside of the bear, and slot the Raspberry Pi (in either a case or an antistatic bag) into it and pierce holes for the cables to enter and leave the bag.

The UK TV children’s series Teletubbies had teddy bears who had television displays in their stomachs. You could replicate this, too. Or include a pico projector to show the child cartoons on the ceiling of their room. Maybe a different cartoon depending on where the bear is sat in the room, as detected by either QR codes, or with RFID or NFC sensors.

ToyTalk (http://www.toytalk.com) have recently begun work on the modern day Teddy Ruxpin that can interact with your child through stories and songs so, along with Kinetimals, you should be able to find a slew of good ideas for your virtual child minder.

If your child is older, then maybe it’d be better to build such child minding facilities into an arcade games cabinet, rather than a teddy bear!
