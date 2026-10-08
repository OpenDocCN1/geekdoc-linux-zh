
# HummingBoard-i2eX
Can Carrier–One dethrone the bestselling Pi single-board computer?

## Technical specs

| Operating System | Android KitKat 4.4 (Debian, GeeXBox, Ubuntu also available) |
| :--- | :--- |
| Processor | Freescale i.MX6 Dual 1 GHz ARMv7 (as computer-on-module) |
| Memory | 1GB DDR3 RAM (as computer-on-module) |
| Dimensions | 66.6mm x 93.1mm x 23mm including connectors |
| Weight | 71g excluding cables |
| Storage | None on-board, maximum 128GB via micro SD Card plus mSATA support |
| Ports | 2x USB 2.0, gigabit Ethernet, HDMI, co-axial audio/PDIF digital out, 3.5mm analogue audio out, MIPI CSI-2, LVDS, mini-PCI Express, mSATA |
| Extras | 26-pin GPIO header, 8-in FlexCAN header, infrared receiver |
| Price | £89 |

![](img/c7d3278283754436651c50a2e9c72912_80_0.png)

**Left** The HummingBoard has a computer-on-module plus carrier board design

### Also consider

![](img/c7d3278283754436651c50a2e9c72912_80_1.png)

**CuBox-i4Pro**
*£124*
If you don't need Raspberry Pi-style GPIO capabilities and have a little room in your budget, the CuBox-i4Pro boasts full software compatibility with the HummingBoard but with a more powerful quad-core processor and 2GB of RAM. Packed into a tiny cube, additional extras include optical audio output, eSATA and integrated Wi-Fi and Bluetooth radios.

![](img/c7d3278283754436651c50a2e9c72912_80_2.png)

> The presence of a heatsink seems odd: rival boards do with no cooling at all

across all three available models of HummingBoard. This opens the door to the HummingBoard's real selling point: the potential. Should SolidRun choose to exploit it, the user can cheaply upgrade to a next-generation processor release simply by retaining their carrier board and replacing the CoM. If SolidRun travels that route, it will be a feather in its cap; if not, it's a wasted opportunity to bring some of the flexibility of traditional PC architecture to the hobbyist embedded space.

This upgradability would tie in well with the eX carrier board's mSATA and mPCIe ports, unique at this end of the market. The mSATA connectivity allows for a compact yet high-capacity solid-state drive (SSD) to be fitted to the underside of the board. The mPCIe slot meanwhile allows for a myriad of high-speed add-on hardware, including wireless radio modules, providing drivers compiled for ARMv7 are available. The HummingBoard-i2eX was tested with two operating systems: Android KitKat 4.4 and Debian Jessie. The former was responsive and pleasing, with full access to the Google Play application store, but the latter really does unlock the HummingBoard's true potential.

A SysBench 95th percentile time of 22.94ms demonstrates the HummingBoard's capabilities, blazing past the Raspberry Pi's sedate 51.45ms and the 29.72ms of its AllWinner A20-based rival, the Banana Pi. The multithreading results are even more impressive, with 1.296s and 0.136s compress and decompress times for a 10MB test file, compared to 8.64s and 3.08s on the Raspberry Pi. But there is still a bottleneck present in the design: raw network throughput was limited to 371MB/s as measured on a gigabit network – below even the 470MB/s it SolidRun warns customers of in the manual.

*Gareth Halfacree*

## Summary

The HummingBoard is an undeniably impressive design and its computer-on-module layout suggests that upgrades will be possible in the future. The processor is fast, the mPCIe and mSATA ports useful, and the GPIO header familiar to anyone who has used the Raspberry Pi. The large heatsink makes the HummingBoard bulkier than its competitors, however, while also preventing easy use of add-on boards.

![](img/c7d3278283754436651c50a2e9c72912_80_3.png)

**Raspberry Pi Model B+**
*£27.44*
The latest revision of the classic Raspberry Pi design, the single-core ARMv6 processor can't hold a candle to the Banana Pi despite the similar price. Its software ecosystem, however, is immeasurably more mature, while add-ons from pickybird boards to perfectly-fitting cases are easy to come by.
raspberrypi.org

![](img/c7d3278283754436651c50a2e9c72912_80_4.png)

**More information**

www.bananaPi.org

# Review

![](img/c7d3278283754436651c50a2e9c72912_81_0.png)

The browser can be customised to hide the URL and search bars and go full-screen

Blacklists and whitelists can be set up to control the web pages that users can access

You can set the browser into Neon mode, which is geared around digital signage

DISTRO

Best for: Old computers

# Webconverger 26

**Minimum Specs:** CPU x86 RAM 1GB STORAGE 1GB

Can this distro help you to transform your old computers and laptops into web kiosks and digital signs for safe use in public places?

- **Pros**
  Lots of features, easy to customise and flow-in resources. Efficient way to run info terminals
- **Cons**
  Configuration interface is easy to access from other browsers. Need to pay $200 to use configured setups

Webconverger is a browser-based OS (running on Firefox) that can transform computers into web kiosks or digital signage, such as the ones you'll see playing news channels or corporate slideshow in lobbies, or offering search, index tools and web-based apps in public places such as libraries or city centres. One of the key advantages of Webconverger over the myriad of other Linux tools and distros offering this same functionality is that it has a very small footprint, working with almost any standard x86 hardware with 1GB of RAM. This means it's an excellent way to repurpose old PCs and laptops to use in the spaces you want to get set up with a custom kiosk/signage network. Even better, it's incredibly simple to create a bootable USB stick with Webconverger so that you can transform computers on an ad hoc basis. When you run the distro, you'll see a blank desktop appear followed by a browser window – this is your web kiosk. Once it's running in a public place and accessible by passers-by, the only thing they'll be able to do is use the browser (with your customised configuration). Even if you've given them the ability to close it down, there's nothing else for them to interact with at all. This makes Webconverger ideal for situations such as a computer to provide free internet access in a café.

Customising the configuration is very easy. In previous versions the settings had to be made at the boot screen, which proved cumbersome, but since we last reviewed Webconverger this has been changed so that you can now customise all these settings through a web interface, and this also means that your configuration is stored between boots. Running Webconverger for the first time, the browser will take you straight to the interface, where you can add your email address (and then

## Webconverger 26
### Can this distro safely transform your old computers for public use?

**New features:** Firefox 32 • Proxy authentication • Security updates • Cron scheduler and printing fixed

![](img/c7d3278283754436651c50a2e9c72912_82_0.png)

![](img/c7d3278283754436651c50a2e9c72912_82_1.png)

You can edit the configuration from the web browser

Here’s our LUD campus terminal running in debug mode

> Ideal for situations such as a computer to provide free internet access in a café

confirm it) in order to create your configuration profile. From there, you add the machine identities of each computer you’re running Webconverger on, nicknaming them as desired, and you can then manage multiple kiosks from this one interface.

Changing the configuration is straightforward as well, though there’s a little reading to do on the developer’s website about the API (http://webconverger.org/API). The documentation is pretty good but not well organised, so expect to go rifling through lots of different pages to round up all the various commands you’ll want to use. You simply add API commands onto new lines in your configuration, hit submit and then enter your password to commit the changes, which are enacted on the kiosks on reboot.

The API commands themselves are very useful and wholly geared towards improving the kiosk experience. You can set multiple homepage tabs, filter websites through whitelists and blacklists, set up print servers and add a print button to the browser bar. You can use cron to schedule Firefox resets and even system shutdowns, and you can also change the browser interface to remove the URL and search bars, or display at fullscreen either by removing the chrome structure or turning it into digital signage via Neon. Neon used to be a separate digital signage service but is now based on the Webconverger platform, and you can access Neon Live separately via the boot menu as well as use it in this way through the API command.

A slight concern is the fact that, if you have a URL bar, you can access the configuration web page from the kiosk browser – as well as any other computer in the world, for that matter – and

then view all of the configuration details; all you need to know is the email address used to create the profile. You can even try to change the configuration, though you won’t get far without the password. However, because of the way that Webconverger is designed, with all of the browsing data being reset after each session or on a more regular, scheduled basis, this isn’t a real security concern. Still, it’s not exactly ideal.

All told, though, this does look like the complete package and it’s far better than a lot of the competition, both paid-for and free. You can’t really fault Webconverger for usability and speed, and all the features work just as you’d hope they would. We managed to get a cron schedule up to power our ‘University of Linux’ info terminal, sort out a basic proxy authentication, customise the desktop wallpaper to our own design and create a locked-in, browser-based experience around a few select web resources before digging further into the documentation. There are many advanced options available too, like the hidden terminal (if you’re in debug mode), the ability to create screensavers and to get homepage video plays starting automatically after a set period of inactivity. All of which left us with the impression that this is a genuinely useful tool to help you to create controlled public terminals to access the web. It’s not something everyone will need, but for those that do then this is definitely your answer.

*Gavin Thomas*

## Summary

Offers the customisation you need to create safe web kiosks and digital signs, and the configuration interface means simple management. But you’re stuck with unconfigured setups unless you’re willing to spend a cool $200 (£123 approx).

Download now
webconverger.com
