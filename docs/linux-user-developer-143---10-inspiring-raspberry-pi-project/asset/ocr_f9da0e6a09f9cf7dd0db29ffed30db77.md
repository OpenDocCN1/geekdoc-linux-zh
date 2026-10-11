# # Banana Pi

First of the true Raspberry Pi clones – is it a successor?

# ## REVIEW

![](bbox=[0.06, 0.19, 0.55, 0.49])

Left The Banana Pi’s dual-core processor leaves the Model B+ standing in terms of performance

# ## Technical specs

| Category | Specification |
| :--- | :--- |
| Operating System | Linaro 14.04 (Raspbian, Android, Arch, openSuSE, Kali, OpenWRT also available) |
| Processor | AllWinner A20 ARM Cortex-A7 Dual-Core, 912MHz |
| Memory | 1GB DDR3 RAM |
| Dimensions | 65.7mm x 74mm x 19.5mm (including connectors) |
| Weight | 43g (excluding cables) |
| Storage | None on-board, maximum 64GB via SD Card and/or 2TB via SATA |
| Ports | 2x USB 2.0, USB OTG, gigabit Ethernet, HDMI, composite video, 3.5mm audio out, SATA 2 with 5V power |
| Extras | 26-pin GPIO header, infra-red receiver, microphone |

# ## Also consider

![](bbox=[0.8, 0.42, 0.95, 0.48])

**HummingBoard-12eX**
**£88**
It’s a considerable price bump from the sub-£30 price of the Banana Pi, but the SoloBuys HummingBoard (previously known as the Carriers One) boasts a more powerful Freescale i.MX6 processor, a similar Pi-inspired layout and on-board mSATA and mini-PCI Express connectivity for high-speed add-on boards. Cheaper versions without mSATA and mPCIe are also available. **newit.co.uk**

> “Positioned as an upgrade for users who have found the berry-flavoured variant lacking”

These annoyances aside, booting the Banana Pi up shows that there’s plenty to recommend the project, too. To speed its route to market, Lemaker has chosen to work on porting existing Linux distributions to its board rather than producing a distribution of its own. As a result, users can download SD card images for Linaro, openSuSE, Arch, and even Google’s Android, or complete the clone experience with a Raspbian port, which in its earliest releases even retained the Raspberry Pi logo as its wallpaper.

At launch, these ports had issues of their own, in particular in the use of the GPIO header. In the most recent releases, Lemaker has worked hard to overcome these issues to the extent that most projects based around Raspbian and the Wiring Pi or RPLGPIo libraries work absolutely fine on the Banana Pi.

In general use, the Banana Pi leaves the Raspberry Pi standing: the 95th percentile SysBench time for the Banana Pi stood at 29.72ms in testing, a considerable improvement over the Raspberry Pi’s 51.45ms. The dual-core processor also shines in multi-threaded applications, completing a 10MB gzip test in 2.39s compress and 0.21s decompress to the Raspberry Pi’s 8.64s compress and 3.08s decompress times.

The faster processor is also supported by more reliable USB ports, but it’s the SATA connectivity that will likely interest most. Using the angled port on the top side of the board, it’s easy to connect mass storage to the Banana Pi without tying up a USB port – something even the newest Raspberry Pi Model B+ can’t offer. Sadly, its usefulness as a compact single-drive NAS is limited by system bottlenecks limiting overall network throughput to around 233Mb/s. **Gareth Halfacree**

![](bbox=[0.78, 0.61, 0.95, 0.67])

**Raspberry Pi Model B+**
**£27.44**
The latest revision of the classic Raspberry Pi design, the single-core ARM6 processor can’t hold a candle to the Banana Pi despite the similar price. It’s a soloive ecosystem, however, is immanassuably more mature, while add-ons from biggest back-to- perfectly-fitting cases are easy to come by. **raspberrypi.org**

# ### Summary

While it’s easy to pour scorn on Lemaker for its blatant attempt to ride on the coattails of the Raspberry Pi, the Banana Pi brings some impressive improvements. The processor is considerably more powerful, and the SATA port provides access to high-speed storage. An altered layout, bottlenecked network and some software bugs prevent a perfect score, however.

![](bbox=[0.65, 0.83, 0.75, 0.85])

# More information

www.bananapi.org