
install the drivers directly from www.nvidia.com, but this is not recommended as then your distro’s package manager cannot track and update them. The situation with AMD graphic cards is similar, the potential hassles of running a binary driver versus the lower performance of the open source drivers. The choice between AMD and Nvidia is almost as religious as the Intel vs AMD CPU choice. Unless you need top notch 3D performance, either will work well for you, and if you need that performance you will have to use the binary drivers whichever way you choose. Currently, Nvidia’s proprietary drivers are considered better and more reliable, but that could easily change.

## Power supply
One of the most overlooked components is the power supply (PSU). Avoid the cheap PSUs that are included with cases (in fact, avoid cases that are cheap enough to include a PSU). A PSU must be reliable and good quality. That may seem an obvious statement that applies to all components, but when a PSU fails it can do so in a way that takes out other components. Having a £100 motherboard or hard drive, or both components, wrecked by a £15 PSU is not a good way of saving money.

Other aspects to consider when choosing a PSU are: that it must supply sufficient power for your needs, now and in the future, that it is efficient (any PSU worth its salt is rated 80 Plus, but look for Gold, Platinum and Titanium models) and that it’s quiet (particularly for a living room computer). There are several websites where you can list the components you are using and get a recommendation of the power supply you need, for example http://support.asus.com/PowerSupply.aspx?SLanguage=en. Check that the PSU you choose has connectors you need, most motherboards take a 24+4-pin ATX connector and a separate CPU power lead. Also ensure you have enough drive power connectors of the right type, some PSUs still come with more of the old Molex connectors than the useful SATA power plugs. If you are using a large case with a bottom mounted PSU, check that the leads are long enough to reach the drives at the top, although you can buy SATA power extender leads cheaply enough that deal with the last two points. You’ll be pleased to know there are no special considerations to be taken regarding Linux compatibility!

## Case
The computer’s case is often left as an afterthought, but a larger, well made case makes life so much easier. A Cheap case will make cable routing harder and will often have sharp edges that will mean bleeding knuckles and blood stains on your nice new motherboard (you can probably sense the first-hand experience in that statement).

A larger case also provides better airflow for improved cooling. If you are building a media centre that goes in the living room, a high WAF (See Terminology, p34) is a major consideration, but pay attention to noise levels. What initially seemed like a whisper can become annoying while watching TV. If you choose to go for a case with a window in the side, bear in mind that you will have to be extra careful when routing cables. A rat’s nest of cables is never a good idea, but it’s even worse when it is on show.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_51_0.png)

## Specialised systems
So far we have looked mainly at a general purpose desktop system, but there are some specialist users to consider, such as a home server or a high-performance gaming systems. If you want to build a home server, your requirements will be very different from a desktop or gaming system.

As all data is transferred over the network, a fast SSD is pointless. You could use one for the operating system, but servers are rarely rebooted, so you wouldn’t even benefit from the fast boot speed they offer, and they only run a limited number of programs, so loading time is not that important either. Servers generally run headless, so a fancy graphics card isn’t needed either, you only need a monitor for the installation process and the onboard graphics of most motherboards are more than suitable for that job. What you do need is a decent amount of memory and plenty of storage space. If you are building a file or media server, pick a motherboard with plenty of SATA ports and a case with a similar number of drive bays. However, much storage you add, at some time you will want more. If you are building a web or mail server, storage space is not such an issue, unless you want to serve media files over an internet connection, but plenty of memory helps, especially with Apache.

Another type of home server is a media server. This could simply be a repository for your video files or you could be doing the recording on the server too, using MythTV’s

> > “Many of the higher performance graphics cards take up two PCI-e slots.”

backend server software or something like Tvheadend. Either way, you will need plenty of space. If you have a server that transcodes video too, maybe something like Plex that reformats video to suit the device playing it and the speed of its connection to the server, you will need a decent amount of RAM and a reasonably fast CPU – not a gaming monster but something that’s not budget.

As everything works over the network, it goes without saying that it should have a fast network interface, especially if more than one client will be using it at the same time, so make sure it has a gigabit interface, or budget for a decent PCI-e network card.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_51_1.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_52_0.png)

### 3 Memory slots
Insert the memory DIMMS into the sockets on the motherboard. Make sure they are the right way round; slots in the DIMMS should line up with protrusions in the socket and they only go in one way. If you are not using all the slots, consult your motherboard manual for the optimum slots to use and to ensure you take advantage of any dual-channel abilities.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_51_2.png)

### 4 Motherboard backplate
Fit the motherboard’s I/O plate to the opening in the back of the case and then place the motherboard in the case. There are small posts that it should stand on, you may need to screw them into the case before going ahead and fitting the motherboard. Then secure the motherboard to the posts with the supplied screws – do not overtighten them.

## High-performance gaming
Gaming, and we mean the graphically intense kind and not gambling, places specific requirements on a computer. Performance is the obvious factor, but not just the performance of the CPU. The GPU on the graphics card plays a more important role than the CPU with some games. Clearly you want a fast CPU and graphics card. Many of the higher performance graphics cards take up the space of two PCI-e slots so you need to make sure both your computer’s case and motherboard have room for it and that your PSU is capable of powering it in terms of raw power and physical connectors it can offer. Memory is also important, you want plenty of it and the fastest available. Disk storage space is less important than speed, so an SSD is the preferred choice for storage. Gamers always want more performance and one of the ways of getting it is by overclocking their systems. This is where you run your processor and memory at higher than its rated speed. For general purpose use, opinions on

If you are building a media server, like this media server, your needs are different. You need plenty of disk space and a fast network connection (or two). You may also need some CPU horsepower for media transcoding.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_52_1.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_52_2.png)

### 5 Connectors
Fit the power supply and connect the power and CPU cables to the motherboard. This is a good time to connect all fan cables. Add your hard drives or SSDs and your optical drive. They may either screw to the case or in some cases they have screwless fittings. Connect the SATA cables from the drives to the motherboard. Connect their power cables for the PSU.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_52_3.png)

### 6 Case LEDs
Connect the cables from the case switches and LEDs to the motherboard. These are fiddly connectors but make sure you get them right, the motherboard manual will tell you what goes where. Some of the cables come with a block connector to make the job easier. This is also the time to connect the case’s USB ports to the relevant points on the motherboard.
