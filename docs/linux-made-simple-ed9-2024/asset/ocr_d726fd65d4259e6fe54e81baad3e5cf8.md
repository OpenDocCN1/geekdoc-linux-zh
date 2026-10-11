# # Exploring the NVIDIA X Server interface

+   - **Display Configuration**
+   Select this to tweak the resolution settings for each monitor attached to your PC – click a screen to select that monitor.

+   - **OpenGL settings**
+   Access the 'Image Settings' slider from here, where you can try and strike a different balance between image quality and performance.

+   - **Antialiasing settings**
+   This section allows you to configure the card’s ability to smooth jagged edges and textures when rendering 3D objects using OpenGL.

![](bbox=[0.4, 0.13, 0.8, 0.33])

+   - **Thermal Settings**
+   This provides a temperature gauge for your graphics card – keep it open while you stress-test the card if you’re worried about heat problems.

+   - **Application Profiles**
+   Advanced users can fine-tune the various settings on offer for specific applications – typically games. Use the Help button to guide you.

+   - **PowerMizer**
+   Some cards support different performance states – use this tab to view current settings and see if you can push the envelope if required.

provide more than basic functionality, with pretty decent 2D and 3D acceleration. They also support most older chipsets stretching back more than a decade. There’s no need to install them either – if your card is correctly detected, the driver should already be in place. Visit https://nouveau. freedesktop.org/wiki/ and https://help.ubuntu.com/ community/RadeonDriver respectively for full details.

If you’re lucky enough to be able to use the proprietary driver, then not only do you gain performance enhancements for gaming and other high-end purposes, you’ll also be able to tweak your card using either the Catalyst Control Centre (AMD) or NVIDIA X Server utility – see the annotated screenshot for details of using the latter.

# ## Intel chipsets

If your PC has an Intel processor and utilises its onboard graphics chip, you may be able to install the open-source Intel driver, which is found at https://01.org/linuxgraphics. At time of writing, the latest available driver is 1.4.0, which is designed for Ubuntu 15.10 and supports the following Intel graphics chips: 2nd-6th generation Intel Core processors, Bay Trail, Braswell and Haswell Intel Celeron processors and the Intel Atom N450 (Pine Trail) chipset.

If your processor fits the bill, click the link under ‘Latest download’, then choose the 32-bit or 64-bit version depending on your Ubuntu build – if you don’t know that, open up System Settings and click Details, then check the ‘OS type’. Click the link to save the .deb file to your hard drive (or opt to open it in Software Centre if prompted). If necessary, double-click the file and click Install, then follow the prompts to install the utility. Once done, open the Dash and type ‘intel’ to locate the graphics installer. Again, follow the prompts and if your chipset is correctly identified, click Install to add the driver. Reboot when prompted, and you’re done. There’s no separate graphical configuration utility – instead, use Screen Display under System Settings to tweak your card’s settings.

# ## Troubleshooting

Sadly, not all driver updates are successful, and you can find yourself locked out of the Ubuntu desktop if one goes awry. If this happens with NVIDIA drivers, press [Ctrl] + [Alt] + [F3] to drop to the shell. Log in using your username and password, then enter the following command:

```
sudo ubuntu-drivers devices
```

This identifies which graphics drivers are installed. Assuming it reveals NVIDIA drivers, enter the following command next:

```
sudo apt-get autoremove --purge nvidia-"‍*
Now add the following command:
sudo apt-get install xserver-xorg-video-nouveau
```

Once done (don’t worry if it tells you it’s already present), type sudo reboot and you should hopefully regain access to your desktop.
AMD users should try the following lines instead:
sudo apt-get autoremove --purge fglrx-*
sudo apt-get install xserver-xorg-video-ati
While they’re the most likely solutions, we’re sorry to say that these may not work – if this is the case, you’ll need to Google your problem to try some of the other suggestions on offer.

![](bbox=[0.5, 0.75, 0.95, 0.89])

![](bbox=[0.75, 0.5, 0.95, 0.67])

Switching to proprietary graphics drivers is actually quite simple – assuming your card is supported, of course.

+   - **Quick tip**
+   To avoid any worry when considering installing new drivers, take a drive image following the before you install drivers, allowing you to roll back should the worst happen.