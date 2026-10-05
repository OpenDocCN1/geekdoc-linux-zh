# Kernel Management
CHAPTER 23

Most frequently, mishaps in configuring sound cards are due to IRQ or DMA and port conflicts from configuring a clone card as “Soundblaster-compatible”(most clones claim this mean “SBPro-compatible”) but may also run in MSS mode, or due to plug-and-play problems. Detailed information on compatibility issues and tips on troubleshooting support can be found in Documentation/sound/README.OSS.

# Tip

Most modern plug-and-play (PnP) sound cards have very little trouble with Linux, and some modern machines will assign PNP values through the PC BIOS when the system boots, but in some situations you may need to experiment with using pnpump and isapnp to generate and load acceptable settings into the card before you can use the sound system. In this situation, the sound card must be compiled as a module to allow using isapnp to set the device before the module is loaded.

To configure PnP devices, you first need to obtain the possible settings using the pnpump utility:

```
pnpump > /etc/isapnp.conf
```

This will create a long text file of configuration options for all PNP devices on your system. You must then edit this file to uncomment the settings that will work with your configuration:

```
vi /etc/isapnp.conf
```

If you have a Windows partition or access to a Windows machine where you can test the card, you can obtain the correct (or likely) settings by using the ControlPanel:System:Devices reports. Once you have set this configuration file to be compatible with your system, you can then add the lines to your boot scripts to first load the configuration and the driver:

```
isapnp -c /etc/isapnp.conf
insmod sound.o
```

In rare circumstances, this technique will not work because the card needs to be initialized by Windows before it can accept any service requests. The only way around this, outside of lobbying the manufacturer to be more friendly, is to boot your system under Windows and then use the DOS-based loadlin.exe boot loader to switch to Linux.

![](bbox=[0.87, 0.455, 0.943, 0.583])