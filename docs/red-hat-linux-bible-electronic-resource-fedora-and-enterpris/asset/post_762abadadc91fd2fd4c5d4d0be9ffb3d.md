
- **Advanced Configuration and Power Interface (ACPI)** — Besides monitoring power features on your laptop, ACPI can also do thermal control, motherboard configuration, and change power states.

Many older laptops do not include support for ACPI in the BIOS, so you must use APM to monitor and manage your batteries. For some newer laptops, ACPI may be required. In general, ACPI offers a more complete feature set for power management, but APM has more user-level support today.

To check whether ACPI or APM are supported on your Red Hat Linux system, you can use the `dmesg` command after a reboot. For example, type:

```
# dmesg | less
```

Page through the output looking for lines beginning with ACPI or APM. On a computer where APM wasn't working, I saw the message "apm: BIOS not found." When ACPI wasn't working, I saw the message "ACPI: System description tables not found."

The following procedure was performed on a laptop that used APM to manage power events. It describes how to use the Battery Charge Monitor applet on the desktop to monitor your battery and the `apm` command to place your laptop in suspend mode.

> **NOTE:** If it seems that ACPI is interfering with the proper operation of your laptop, you can turn off ACPI when you boot your computer. Add `acpi=off` to the end of the kernel line (from the GRUB boot screen or the `/boot/grub/grub.conf` file) to turn off ACPI.

## Using the battery status applet

If you are using the GNOME desktop, you can add a Battery Status Monitor to your panel to keep track of the power levels of your battery. The following procedure steps you through adding the monitor to your panel and configuring it to behave as you like:

1. Right-click the GNOME panel; then select Add to Panel → Utility → Battery Charge Monitor. If the Battery Charge Monitor applet appears on the panel (which it should), you can stop here if you like. The applet will:
   - Include a battery icon that appears green (with the battery above a 40% charge), yellow (25%-40%), orange (15%-25%) or red (under 15%).
   - Show a power cord if the laptop is plugged in.
   - Notify you with a pop-up window when the battery charge is low.
   - Notify you with a pop-up window when the battery is fully charged.
   - Display the percent charged and whether the battery is currently charging when you move the mouse pointer over the applet icon.

Continue with the following steps if you want to change that behavior.

2. Right-click the Battery Charge monitor applet, then select Preferences. Figure 10-7 shows the Battery Charge Monitor Preferences window and the applet in the panel.

![](img/27a85d56d393921ced6412ae6e8336bf_403_0.png)

3. Change any of the following values related to your battery monitor:
   - **Battery color levels** — You can change the levels at which the battery icon changes from green, yellow, orange, and red.
   - **Warnings** — Select whether or not you want to be notified (with a pop-up) when the battery charge is low or fully charged. You can also select to have the laptop beep if either case is true.
   - **Suspend command** — Add a command to put the laptop in suspend mode. (Try the `apm -s` command as described in the next section.) With a Suspend command set, you can right-click the icon and choose Suspend Computer to suspend your laptop.
   - **Appearance** — Select the Appearance tab. From there, you can choose which icons appear on the applet (battery, power cord, and/or percent charged). You can also change whether the progress bar on the battery moves up or down as power empties.

> **NOTE:** If, when you try to add the Battery Charge Monitor icon to the panel, a pop-up window tells you that the operation fails, it may be that the apmd daemon isn't running. You can try starting the apmd service (as root user; type `service apmd start`). If, however, APM is shown as not supported in your dmesg file, you can try turning on APM support in your laptop’s BIOS.

## Using apm to enter suspend mode

The `apm` command lets you view information about your computer’s power management and put the computer in suspend mode (if it is supported on your laptop). Here are some examples of using the `apm` command:

```
# apm -m
```

Using the `-m` option, the `apm` command displays the number of minutes of battery life remaining (if that information is available). It may also give you information about the status of how the battery is charging and whether or not the laptop is currently plugged in.

```
# apm -s
```

The `-s` option of `apm` causes the laptop to enter suspend mode. You can start up the laptop again, in most cases, by pressing a key on the keyboard.

## Choosing Software Alternatives

Because several software packages are available for every major service available in Linux (such as mail, printing, and so on), there will be times when people using the system will prefer one service over another. Software packages that have been designed to work with the alternatives system can be configured in Red Hat Linux to let an administrator choose which of the alternatives to a particular service he or she wants to use by default.

### Selecting mail and printing alternatives

Beginning with Red Hat Linux 7.3, which was the first version to offer the alternatives feature, two major services were configured to use alternatives: mail transport and printing services. The alternatives facility lets users choose the following, related to mail transport and printing:

- **Mail Transport Agent (MTA)** — If both the sendmail and postfix mail transport agents are installed, as an administrator you can choose which of those two services is the default for sending e-mail.
- **Printing** — If both LPRng and CUPS printing services are installed, you can choose which service is the default for printing documents.

As an administrator, you still need to configure each alternative service to work. Descriptions for configuring sendmail and postfix mail-transport agents are contained in Chapter 19. Information on setting up the CUPS printing service is in Chapter 17. (LPRng is no longer delivered with Red Hat Linux, although it is still available from sites such as `rpmfind.net`.)

In terms of setting up the alternatives side of mail and printing services, much of the work of creating links so that the services can be chosen has already been done. Links relating to the default services are set up in the `/etc/alternatives` directory. Definitions that identify the alternative components of mail and printing are contained in the `/var/lib/alternatives` directory.

Because much of the configuration has been done in advance, the first step in switching between the different printing or mail services installed on your computer is only a couple of clicks away. To switch the default mail or printing services on your computer, do the following:

1. Select one of the following from the Red Hat menu, depending on whether you want to switch your mail or printing service:
   - To switch print service, select **System Settings → More System Settings → Printer System Switcher**.
   - To switch mail service, select **System Tools → More System Tools → Mail Transport Agent Switcher**.

   The switcher window for the service you requested appears.
2. Click on the service you want to switch to — LPRng or CUPS for printing, Sendmail or Postfix for mail. (If the one you want is already selected, you can just cancel.)

   If the switch is successful, a pop-up window tells you to restart the new service.
3. Close the pop-up window.

The next time your computer boots, your new printing or mail service takes over that service. All the links are in place and the start-up scripts are changed. However, your system is still running the old service. The start-up scripts for those four services are in the /etc/init.d directory. They are as follows:

- *lpd* For the LPRng printing service
- *cups* For the CUPS printing service
- *sendmail* For the Sendmail service
- *postfix* For the Postfix service

To stop the old service so that the new one can take over, type the following (replacing *service* with the name of the service you want to stop):

```
# /etc/init.d/service stop
```

To start the new service, type the following (replacing *service* with the name of the service you want to start):

```
# /etc/init.d/service start
```

Providing that the new service was configured properly, it should now be available to the users of your computer.

## Using mail and printing alternatives

The printing and mail-transport services that the alternatives facility allows you to change rely on many of the same command names. For example, both printing services use the lpr
