# The Old Linux-PCMCIA Subsystem

The Linux-PCMCIA subsystem has recently undergone an overhaul. To get PCMCIA working with 2.6.13 and newer kernels, you need the *pcmciautils* package (http://kernel.org/pub/linux/utils/kernel/pcmcia/howto.html), which obsoletes the *pcmcia-cs* package (http://pcmcia-cs.sourceforge.net) used with earlier kernels. Internal kernel programming interfaces and data structures have also changed. Earlier kernels relied on a user space daemon called *cardmgr* to support hotplugging, but the new PCMCIA implementation handles hotplug using *udev*, just as other bus subsystems do. So with new setups, you don't need *cardmgr* and should make sure that it is not started. There is a migration guide at http://kernel.org/pub/linux/utils/kernel/pcmcia/cardmgr-to-pcmciautils.html.

Figure 9.3 contains the following components:

+   - Host controller device drivers that implement low-level routines for communicating with the PCMCIA host controller. Your handheld and laptop have different host controllers and, hence, use different host controller drivers. Each PCMCIA slot that the host controller supports is called a *socket*.
+   
+   - PCMCIA client drivers (*XX_cs* in **Figure 9.3**) that respond to socket events such as card insertion and ejection. This is the driver that you are most likely to implement when you attempt to Linux-enable a PCMCIA card. The *XX_cs* driver usually works in tandem with a generic driver (*XX* in **Figure 9.3**) that is not PCMCIA-specific. In relation to **Figure 9.3**, if your device is a PCMCIA IDE disk, *XX* is the IDE disk driver, *XX_cs* is the *ide_cs* driver, *XX*-dependent layers are filesystem layers, and *XX*-applications are programs that access data files. *XX_cs* configures the generic driver (*XX*) with resources such as IRQs, I/O base addresses, and memory windows.
+   
+   - The PCMCIA core that provides services to host controller drivers and client drivers. The core provides an infrastructure that makes driver implementations simpler and adds a level of indirection that renders client drivers independent of host controllers. Irrespective of whether you are using your Bluetooth CF card on an XScale-based handheld or an x86-based laptop, the same client drivers can be pressed into service.
+   
+   - A *driver services* module (*ds*) that offers registration interfaces and bus services to client drivers.
+   
+   - The *pcmciautils* package, which contains tools such as *pccardctl* that control the state of PCMCIA sockets and select between different card-configuration schemes.

Figure 9.4 glues kernel modules on top of Figure 9.1 to illustrate how the Linux-PCMCIA subsystem interacts with hardware on a PC-compatible system.

# **Figure 9.4. Relating PCMCIA driver components with PC hardware.**

![](bbox=[0.42, 0.81, 0.58, 0.83])