
Please Note: If you need to use a username and password for an SMB (LAN Manager) or NCP (NetWare) print queue, they are stored unencrypted in a local script. Thus, it is possible for another person to learn the username and password. It is therefore recommended that the username and password for use of the printer to be different than that for a user account on the local Red Hat Linux system, so that the only possible security compromise would be unauthorized use of the printer. If there are file shares from the SMB server, it is recommended that they also use a different password than the one for the print queue.

After you have added your print queue, you may need to restart the printer daemon (lpd). To do so, choose Restart lpd from the lpd menu.

You may print a test page for any print queue you have configured. Select the type of test page you would like to print from the Tests menu.

![](img/46f4935125ba89e12897afbe9d77a097_229_0.png)

Figure 8-35: Printing a Test Page

## Kernel Daemon Configuration

Red Hat Linux includes kerneld, the Kernel Daemon, which automatically loads some software and hardware support into memory as it is needed, and unloads it when it is no longer being used. The tool shown in Figure 8-36 manages the configuration file for kerneld. While kerneld can load some things, such as filesystems, without explicit configuration, it needs to be told what hardware support to load when it is presented with a generic hardware request.

![](img/46f4935125ba89e12897afbe9d77a097_230_0.png)

### Figure 8-36: Kernel Module Management

For instance, when the kernel wants to load support for ethernet, kerneld needs to know which ethernet card you have, and if your ethernet card requires special configuration, it needs to know about that, too.

## Changing Module Options

To change the options being given to a module when it is loaded, click on the line to select it, then click the Edit button. kernelcfg will bring up a window which looks like Figure 8-37. The options kernelcfg knows about (normally all available options) will each have their own field. Normally, you will want to ignore the Other arguments field. Some modules normally take no arguments; just in case, they have an Arguments field which allows you to enter configuration information.

![](img/46f4935125ba89e12897afbe9d77a097_231_0.png)

### Figure 8-37: Editing Module Options

## Changing Modules

To change which module gets invoked to provide a generic service, such as an ethernet card or SCSI host adapter module, you need to delete the old one and add a new one. To delete a module, select it by clicking on it, then click on Remove. Then click on Add to add the new module, as explained in the following section. If you have changed your SCSI controller (scsi_hostadapter), remember to make a new initial ramdisk with the /sbin/mkinitrd command as documented in Making an initrd image in Chapter 11.

## Adding Modules

To add a module of any type, click on the Add button. You will be presented with a dialog box (Figure 8-38) asking you to choose a module type. Ethernet is eth, Token Ring is tr, SCSI controllers are scsi_hostadapter, and so on. Click Ok to continue to the next dialog box.

![](img/46f4935125ba89e12897afbe9d77a097_232_0.png)

Figure 8-38: Adding a module

If there is more than one module which can be used for the module type you have chosen, you will be presented with a dialog box (Figure 8-39) which asks which module you want to use, and may also ask for specifics about the type of module; for ethernet, for example, you need to choose from eth0, eth1, etc. When you are done, click Ok again to continue to specify any module options in the next dialog box (Figure 8-39), which is the same as the dialog for editing a module.

![](img/46f4935125ba89e12897afbe9d77a097_232_1.png)

Figure 8-39: Selecting From Available Modules

## Restarting Kernel

The changes that you make with the Kernel Daemon Configuration tool will be made in the /etc/conf.modules file, which kerneld reads whenever it is started. Once you have made changes, you can restart kerneld by clicking on the Restart kerneld button. This will not cause any modules which are currently in use to be reloaded, it will only notify kerneld to use the configuration when it loads more modules in the future.
