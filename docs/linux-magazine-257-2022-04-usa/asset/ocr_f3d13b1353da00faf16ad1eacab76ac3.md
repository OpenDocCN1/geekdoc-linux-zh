will get rid of dependencies and libraries so that when you try the next option you are starting from a clean slate. In the example above I listed a few of the packages that show up when I run the `l1st` command, but there are about 20 or 22 of them in total. Once that is done, you will finalize the uninstallation by running the same but with `purge` instead of `remove`, à la:

```
`$ apt purge nvidia-driver-390 nvidia-settings nvidia-prime nvidia-dkms ... etc.`
```

This gets rid of any settings and configurations that may still be lingering after removal of the packages themselves. You can also do a quick cleaning with the following command after all of that.

```
`$ apt autoremove`
```

just to be sure that you have gotten everything out of there that can be removed.

When this is complete, simply type **reboot** and hit Enter to reboot the system. At this point you should see that the *nouveau* drivers are loaded and running instead of the proprietary NVIDIA ones. You can now try a different driver package by listing and installing as you did before, and I would recommend going to the next available lower number. In my experience most of the problems that I have had with installing NVIDIA drivers stem from the fact that my old cards aren't well supported on newer drivers, even though those newer drivers will show up when queried. Going to older available packages one at a time ensures that I have the most up-to-date set of packages available for my card which will run without problems.

# Concluding Remarks

I cannot express the amount of frustration I felt as a beginner around installing one of these only to have a blank screen be the result upon reboot. At that time, my solution was a complete reinstall of the OS, at which point I would try to use the open source driver package with its faults or go to a different NVIDIA driver and cross my fingers and hope for better results. Yes, I have reinstalled Ubuntu more than four times simply trying to get a driver package that worked. That is exactly why I think it is important not only to be comfortable with the terminal and with using the recovery mode, but also simply to know a bit about what is happening under the hood. Now that I have a method for recovery upon failure and have some

![](bbox=[0.57, 0.08, 0.97, 0.34])

confidence that I can get my system back to a working desktop, I can say that I simply find it easier and faster to use the terminal for the entire process. The added benefit here in my opinion is that you can actually see what is happening in the terminal rather than waiting, guessing, and hoping with the GUI equivalent (Figure 4).

Hopefully one day we will see the NVIDIA gang team up with our beloved open source community to produce a non-proprietary solution with the performance and benefits of the closed driver offering that currently exists. Until then I am afraid we are stuck with some of this hassle. Following the advice given above, however, you at least won't have to be stuck at a blank screen for too long after installing their solution onto your machine. I guess it really is as they say: You win some and you lose some.

# Info

+   [1] NVIDIA: [https://www.nvidia.com/](https://www.nvidia.com/)
+   [2] AMD Radeon graphics cards: [https://www.amd.com/en-us/graphics/radeon-rx-graphics](https://www.amd.com/en-us/graphics/radeon-rx-graphics)
+   [3] Ubuntu: [https://ubuntu.com/](https://ubuntu.com/)
+   [4] Red Hat Enterprise Linux: [https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)
+   [5] Fedora Linux: [https://getfedora.org/](https://getfedora.org/)
+   [6] Nouveau Xorg driver: [https://launchpad.net/nouveau](https://launchpad.net/nouveau)
+   [7] SteamOS and Linux titles: [https://store.steampowered.com/linux](https://store.steampowered.com/linux)
+   [8] Pop!\_OS by system76: [https://pop.system76.com/](https://pop.system76.com/)
+   [9] YouTube: Gaming on Linux is NOT Rng: [https://www.youtube.com/watch?v=RY4K16ujFw](https://www.youtube.com/watch?v=RY4K16ujFw)
+   [10] NVIDIA Optimus technology: [https://www.nvidia.com/en-us/geforce/technologies/optimus-technology/](https://www.nvidia.com/en-us/geforce/technologies/optimus-technology/)
+   [11] Intel GPUs: [https://www.intel.com/content/www/us/en/products/discrete-gpus.html](https://www.intel.com/content/www/us/en/products/discrete-gpus.html)
+   [12] Supermicro X8STi: [https://www.supermicro.com/products/motherboard/Xeon3000/X58/X8STi.cf](https://www.supermicro.com/products/motherboard/Xeon3000/X58/X8STi.cf)
+   [13] Dell Latitude E-series laptops: [https://www.dell.com/](https://www.dell.com/)