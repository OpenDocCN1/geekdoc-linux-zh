While VirtualBox is free for personal use, make sure you or your organization meets the requirements for usage of the software, especially the free Extension Pack license. The only requirement for VirtualBox to function is a computer that supports virtualization. Any modern Windows host should work without any modification.

Most mid-range and high-end computers made within the past five years should have no problem, but may require you to enable virtualization support in the BIOS (Basic Input / Output System) during startup. Netbooks, older machines, and cheap low-end computers will likely give you problems. If you are in doubt about meeting this requirement, search for your model of computer followed by "virtualization" and you should find the answers. The rest of this section will assume that your Windows host computer meets this requirement and now possesses VirtualBox.

First, we need to download the Pop! OS ISO file as previously explained. This file behaves similarly to a physical CD which would install Windows or any other operating system. Save the file to your Desktop or anywhere else to which you have easy access. Expect an approximate file size of 3 GB. Next, open VirtualBox and click on the button labeled "New". The following creates a VM appropriate for our needs. These exact steps change often, but this should provide the general settings required.

+   - Provide a name of "Pop! OS" and choose your location to save the machine.
+   - Select "Linux" as type, "Ubuntu 22.04 (64-bit)" as version, and click "Next".
+   - Under Base Memory, move the slider to select 50% of your system memory.
+   - Under Processors, move the slider to select 50% of your resources.
+   - Click "Next" and then "Create".
+   - Leave the hard disk file type as "VDI" and click "Next".
+   - Select the default option of "Dynamically allocated" and click "Next".
+   - Choose the desired size of your virtual hard drive. If you have a large internal drive, 50 GB should be sufficient. If you are limited, you may need to decrease that number.
+   - Click "Create".

Your VM has been created, but it will do nothing upon launch. We need to tell it to boot from the ISO file which we previously downloaded. Select your new machine in the menu to the left and complete the following.

+   - Click the Settings icon then the Storage icon.
+   - Click the CD icon which displays "Empty" in the left menu.
+   - Click the small blue circle to the far right in the "Optical Drive" option.
+   - Select "Choose a disk file".
+   - Select the Pop! OS ISO previously downloaded then click "Open".
+   - Click "OK" and then "Start" in the main menu.
+   - If prompted, confirm your choice by clicking "Start".

Your Pop! OS installation process should now start within a new window. You should be booting to the ISO file previously downloaded, which is behaving as if you had placed a Pop! OS install CD into the virtual computer. This is your first virtual machine running on top of your host operating system. If the window is too small, click "View", "Virtual Screen", then "Scale to 200%" within the VirtualBox menu. Avoid this, if possible, as it may cause viewing issues later. Consider reversing this setting once you are finished if things appear large. We can now finish the installation of Pop! OS with the previous tutorials.