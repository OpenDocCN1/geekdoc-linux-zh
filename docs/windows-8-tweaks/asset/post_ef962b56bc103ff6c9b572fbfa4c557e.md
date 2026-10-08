
![](img/ea75090cfee8ac890f64c8c4f62f7285_232_0.png)

Figure 13-2: The BIOS Setup screen displays the Quick Boot feature.

-   Use the Change Value keys to cycle through the options and select Enable for the Quick Boot feature or Disable if your system’s BIOS has the Memory Check feature.
-   After you have made the change to the setting, exit the system BIOS by pressing the Escape key. Make sure you save the changes upon exit.

Using the Quick Boot feature or disabling the Memory Check won’t do any harm to your system. In fact, some computer manufacturers even ship their computers with these settings already optimized for performance. The only downside to disabling the tests is in the rare situation in which your RAM self-destructs; the BIOS won’t catch it, and you might receive errors from the operating system or your system could become unstable. If you notice that your system becomes unstable and crashes frequently or won’t boot, go back into the BIOS and re-enable the tests to find out whether your system’s memory is causing the problems.

## Modifying the Operating System Boot

You can use several different tricks to shave a few more seconds off the boot time. For example, you can reduce Timeout values and slim down the system to get rid of all the extra features and services that you do not use or need. Check out the following ways to do so.

### Windows Boot Manager

If you have more than one operating system installed on your computer, you have to deal with the Windows Boot Manager installed by Windows 8. By default, the Windows Boot Manager gives you 30 seconds to select an operating system before it reverts to the default operating system. The only way not to wait 30 seconds is to select the operating system you want to use right away. If you use one operating system the majority of the time, you will definitely save time if you set that operating system as the default and lower the Timeout value to 1 or 2 seconds. That way, you won't have to select an operating system every time you turn on your system or wait 30 seconds before your computer actually starts to load the operating system.

> **TIP** Before you make any changes to the Windows Boot Manager (WBM), it is a good idea to back it up using the Boot Configuration Data Editor (bcdedit.exe) so that you can easily revert to an earlier version should you have any problems. At a command prompt run as the Administrator account, type `bcdedit /export "C:\Backup File"`. This saves the WBM to a file that you can use to import using the `/import` flag.

### Lowering OS Timeout Values

If you have multiple operating systems installed on your computer and the Windows Boot Manager is installed, the default selection timeout is often way too high. It is much better to set a lower timeout so that if you do not make a selection, it quickly reverts to the default OS, making your boot time much faster.

Changing the Timeout value is simple with the System Configuration utility. Follow the steps here to use the System Configuration utility to lower the OS Timeout value:

-   Open the Start screen, type **msconfig**, and press Enter.
-   When the System Configuration utility loads, click the Boot tab.
-   Locate the Timeout box and replace 30 with a much lower value, as shown in Figure 13-3. I recommend you use between 2 and 5. I use 2 because that gives me just the right amount of time to hit a key on my keyboard when the Windows Boot Manager is displayed on the screen.
-   After the value has been updated, click OK to exit.

Now that the Timeout value has been updated, the boot menu no longer increases your system startup time. Even though this is a simple tip, it really helps a lot on systems that have multiple operating systems installed. The default operating system on the Windows Boot Manager can be set in the next section.

![](img/ea75090cfee8ac890f64c8c4f62f7285_234_0.png)

**Figure 13-3**: Use the System Configuration utility to set the Boot menu Timeout value.

### Setting the Default OS

In the preceding section, you learned to set a new Timeout value that cuts down on the amount of time that is wasted before the operating system starts to load. That works great when your primary operating system is the default; but if it is not, you must remember to hit a key at the right moment every single boot. There is a much better way to handle the situation. Just make your primary operating system the default operating system in the Windows Boot Manager. This allows you to benefit from the lower Timeout value and speed up the overall boot time.

You can set the default operating system using the System Configuration utility or the command-line Boot Configuration Editor, bcdedit.exe. Follow these steps to use the System Configuration utility:

-   Open the Start screen, type msconfig, and hit Enter.
-   Click the Boot tab.
-   Select the operating system from the list you want to make the default and then click the Set As Default button.
-   When you are finished, click OK.

Using the System Configuration utility is the easiest way to set the default operating system, but you can also set it with the bcdedit.exe utility. Follow the next steps to use the Boot Configuration Editor to set the default operating system:

-   Open the Start screen, and type Command Prompt.
-   Right-click on the Command Prompt shortcut at the top right.
-   Select Run As Administrator from the charm application bar on the bottom of the screen.
-   When the command prompt has loaded, you are ready to use the bcdedit.exe command. First, you need to get the ID of the operating system that you want to set as the default. To do this, type bcdedit /enum all in the open Command Prompt window. Scroll through the list of entries and look for Windows 8.
-   After you have found the correct entry, note its identifier. You use this in the next step.
-   At the command prompt, type bcdedit /default (entry identifier). For example, I ran bcdedit /default {b2721d73-1db4-4c62-bf78-c548a880142d}.

The default operating system on the Windows Boot Manager is now set. The next time you reboot, your changes will be applied.

> **TIP** The Boot Configuration Editor is a powerful utility that you can also use to change many other settings of the Windows Boot Manager. Experiment with bcdedit.exe by running bcdedit /? from the command prompt. This shows you all the other available options and flags that you can use with the Boot Configuration Editor.

### USING EASYBCD TO EDIT THE WINDOWS BOOT MANAGER

EasyBCD is a cool and easy-to-use front end to the Boot Configuration Editor. Instead of using the command-line interface, you can use this free utility by NeoSmart Technologies. With EasyBCD, you can change the Timeout value, default selection, description, and even the boot order, as shown in Figure 13-4. Download a free copy of EasyBCD at http://tweaks.com/887200.

![](img/ea75090cfee8ac890f64c8c4f62f7285_236_0.png)

### Disabling the System Boot Screen

Windows 8 has a new high-resolution animated boot screen that looks much better than the previous Windows boot screens. The flag animation sure is a nice loading screen, but is it really worth an extra fraction of a second when your computer is loading? Disabling the boot screen can cut down on your boot time. Keep in mind that every fraction of a second counts.

This performance improvement works on a simple principle. It takes time for the computer to do anything. Taking away some work the hardware has to do, such as loading the boot screen, frees up time that it can spend loading your system files instead.

The process for disabling the system boot screen is similar to the process for modifying the default operating system timeout. For this change, you need to start up the System Configuration tool:

-   Open the Start screen, type **msconfig**, and press Enter.
-   When the System Configuration tool loads, click the **Boot** tab.
-   Locate the No GUI boot check box and check it, as shown in Figure 13-5.
-   Click **OK** to close the System Configuration tool.
-   A small window pops up and asks you whether you would like to reboot your computer now or later. Make sure you have any open documents closed, and click **Restart**.

![](img/ea75090cfee8ac890f64c8c4f62f7285_237_0.png)

**Figure 13-5:** Disable the boot screen with the System Configuration tool.

-   After your computer has restarted, the System Configuration tool may load automatically, notifying you of the change. Check the box that says Don't Show This Message Or Start System Configuration When Windows Starts and click **OK**.

After you close the System Configuration tool and reboot, the boot screen is gone. You have saved your computer from doing extra work while loading Windows 8 on your computer.
