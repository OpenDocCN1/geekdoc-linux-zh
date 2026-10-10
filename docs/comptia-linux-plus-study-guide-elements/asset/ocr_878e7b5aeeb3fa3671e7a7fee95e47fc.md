do to get the job done. Actual configuration can be done using either the automatic DHCP tool or static IP addresses. Linux’s underlying network configuration mechanisms rely on startup scripts and their configuration files, but you may be able to use GUI tools to do the job instead.

# Network Hardware Configuration

The most fundamental part of network configuration is getting the network hardware up and running. In most cases, this task is fairly automatic—most distributions ship with system startup scripts that autodetect the network card and load the correct driver module. If you recompile your kernel, building the correct driver into the main kernel file will also ensure that it’s loaded at system startup.

If your network hardware isn’t correctly detected, though, subsequent configuration (as described in the upcoming sections “DHCP Configuration” and “Static IP Address Configuration”) won’t work. To correct this problem, you must load your network hardware driver. You can do this with the mdprobe command:

```
# mdprobe tulip
```

You must know the name of your network hardware’s kernel module, though (tulip in this example). This name may not be immediately obvious, because it varies greatly depending on your hardware, and the name is usually based on the chipset used in the network card, rather than on the name of the network card or its manufacturer. Chapter 1 includes information on identifying hardware, so consult it if you have problems with this task.

Once Linux has recognized the network hardware, you should be able to continue with network configuration, as described in the next couple of sections. To make Linux recognize your hardware at every boot, though, you may need to add the mdprobe command to a startup script. This task can be tricky; most distributions use very convoluted startup scripts. These scripts should already be detecting and loading the network driver. If they don’t, the best approach may be to recompile the kernel and build the driver into the main kernel file. Alternatively, you can try adding a call to mdprobe to an appropriate network startup script; however, placing this call in a good location can be a difficult task. Chapter 4, “Managing System Services,” includes information on system startup scripts.

# Setting Wireless Options

If you’re using a wireless (Wi-Fi) device, you must use the iwconfig command to set wireless-specific options before you use DHCP or manual tools to bring up the network interface. This is necessary because wireless networks have their own unique features, such as network names, broadcast frequencies, and encryption keys, that are not applicable to wired networks. As with other network configuration tools, your distribution’s startup scripts may launch iwxonfig as part of a general network startup routine, so you may not need to do this manually; however, at the very least you’ll need to enter the relevant information in a GUI or text-based tool, perhaps when you install Linux.