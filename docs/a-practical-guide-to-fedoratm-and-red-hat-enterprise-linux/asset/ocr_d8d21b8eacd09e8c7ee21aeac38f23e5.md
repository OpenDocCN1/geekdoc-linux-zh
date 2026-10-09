![](bbox=[0.35, 0.1, 0.65, 0.38])

Figure 17-10  Virtual Machine Settings window, Hardware tab, CD/DVD selection

On the next screen you can customize the hardware or you can wait until the following screen to do so. Click **Finish**. If the next screen holds information about installing the guest operating system and VMware Tools, click **Close**.

Player displays the VMware Player window again, this time with a tab for the VM you just created under the tab labeled **Home** on the left. In the example the tab is labeled **F19a**; click that tab to select the VM. On the right side of this window is a picture of the state of the VM; because it has not been started, the picture is blank. The two buttons on the bottom of the right side are labeled **Play virtual machine** and **Edit virtual machine settings**.

# # INSTALLING THE OPERATING SYSTEM

You have created a VM without an operating system. The next step is to install Fedora (or another operating system) on the VM. To do so you must tell the VM which medium to boot from. It is as though you had a new physical computer: You have to put the installation medium (e.g., DVD or flash drive) with Fedora on it in the system before you boot the system.

Click **Edit virtual machine settings**; Player displays the Hardware tab of the Virtual Machine Settings window. On the left side, click **CD/DVD (IDE)**; Player displays information about the virtual DVD drive on the right side of the window. Click the radio button labeled **Use ISO image** and then the button labeled **Browse**. Highlight the ISO image file (Fedora-Live-Desktop-i686-19-1.iso in the example) and click the button labeled **Open**. The window should look similar to the one shown in Figure 17-10. Click **OK** or **Save**; Player redisplays the VMware Player window.

In the VMware Player window, click **Play virtual machine**. Player will boot the operating system you selected. Run the live system or install Fedora as explained in Chapter 3. Player might display a window asking whether you want to download