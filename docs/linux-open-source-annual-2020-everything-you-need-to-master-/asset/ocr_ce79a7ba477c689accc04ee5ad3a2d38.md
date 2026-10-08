the specifications of the virtual video card. In order to display higher resolutions at higher colour depths, it’ll need more video memory. With the default settings, this uses system RAM rather than video RAM, so you can probably spare at least 64MB here. It’s actually possible to set this higher than the slider allows using the VBoxManage command line tool. More on that later...

Modern desktops, despite appearing on a two-dimensional surface, all use some kind of 3D acceleration (be it OpenGL, OpenGL ES, or latterly Vulkan) to move windows around and draw nice shadows beneath them. By clicking the **Enable 3D acceleration** box we let our VM pass these primitives more or less directly to the host’s video card, as well as access its video RAM directly. So if you’re using onboard graphics (or a very old and short of VRAM graphics card) make sure you don’t over-allocate here. It’s tempting to click the 2D acceleration box too, but that’s only for DirectDraw acceleration on Windows guests.

We can also accelerate the CPU side of things. The default settings allocate only a single thread to running the guest OS; this is pretty painful in a world that takes multitasking for granted. So select the **System** section on the left and choose the **Processor** tab. You can allocate as many virtual CPUs to the guest as threads the host machine is capable of running (so twice the number of cores if your processor supports HyperThreading or whatever AMD call it nowadays). Again, if you allocate too much CPU to the guest, then the host will suffer, which in turn will cause the guest to suffer. A reasonable rule of thumb is not to allocate more than half the available CPU resources. It’s also possible to set an execution cap, so that the VM can’t max out an entire core on the host, which can help for some misbehaving workloads.

Some operating systems require the **Enable PAE/NX box**, which would enable 32-bit VMs to access more than 4GB of memory. If you’re setting up an Ubuntu Server guest (and you admit as much in the **Machine Type** and

![](bbox=[0.45, 0.09, 0.93, 0.22])

![](bbox=[0.52, 0.22, 0.85, 0.27])

> Many Linux distros now include the guest additions, which enable the helpful features described here. But occasionally you’ll need to install them in the guest manually.

Version boxes), this gets ticked automatically. Moving to the **Acceleration tab** you should find that the **VT-x** and **Nested Paging** boxes are both checked. It’s not officially recommended to tick **Use Host I/O Cache** for our virtual hard disk. This turns off the dedicated **VirtualBox cache**

# ## SHARE OUT RESOURCES WISELY

> “If you allocate too much CPU to the guest, then the host will suffer, which in turn will cause the guest to suffer”

and uses the host OS one, but has been reported to speed up I/O intensive tasks, in particular OS installation and package updates. We won’t cover setting up a Windows VM here, but if you want to, you’ll probably have to experiment a little to get things running smoothly.

![](bbox=[0.07, 0.65, 0.33, 0.8])

![](bbox=[0.35, 0.65, 0.62, 0.8])

![](bbox=[0.65, 0.65, 0.93, 0.8])

# ### 4 Virtual hard disks

We’ll need some persistent storage for our VM. Modern Linux distros tend to be fussy about installing anywhere with less than 10GB of space, and if you can spare it then allocating more is a wise idea. Choose “Create a virtual hard disk now” to begin the process. If you have a spacious data partition it’s worth storing VMs there to avoid filling up your home folder.

# ### 5 Customise virtual storage

Choose the default VDI storage. These files can be fixed or dynamically sized (up to a given maximum). Dynamic storage is obviously much more flexible, and these days you’re unlikely to notice the increased I/O overhead, so go with that. You can specify the file’s location with the tiny icon to the right, otherwise it goes in `~/VirtualBox VMs/`

# ### 6 Boot your VM

You’ll need an ISO image to boot your machine. Download the Ubuntu flavour of your choosing and then go to **Settings>Storage** and select the optical drive **Now** click on the tiny disc drop-down on the right and select **Choose Virtual Optical Disk File (sic)**. Locate your ISO, click OK, then hit the green **Start** arrow. Chocks away!