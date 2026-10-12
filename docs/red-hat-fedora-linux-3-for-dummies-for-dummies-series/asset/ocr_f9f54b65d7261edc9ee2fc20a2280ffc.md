newer systems, Fedora Core detects all the basic hardware. Then the Fedora Core installation process starts and the Welcome to Fedora Core window opens.

![](bbox=[0.14, 0.16, 0.24, 0.25])

If the installation process crashes at this point, reboot your computer and add the `nofb` option after the boot: prompt (for example: boot: nofb). If that fails, reboot and use the text installation mode: boot: linux text. Also, Sony Vaio notebook users may need to enter the option `pci=off` `ide1=0x180,0x386` at the boot: prompt to make their CD-ROM drive work correctly.

+   3. If prompted with the CD Found screen, you can select to verify that your DVD or CD-ROMs are error-free. (Refer to the sidebar “Checking your discs.”) Otherwise, press Tab to select the Skip option and then press Enter.

+   4. Click the **Next** button.

The Language Selection window opens.

![](bbox=[0.14, 0.44, 0.24, 0.53])

You can view information about Fedora Core by clicking the **Release Notes** button, in the lower-left corner of the screen. Additional information about where to find more information is displayed on the informational sidebar on the left side of the information window.

+   5. Select a language (if you don’t want the default of English) and click **Next**.

Choose the language you speak — or, if you’re feeling adventurous, one you don’t (not recommended).

The Keyboard Configuration window appears.

+   6. Select your **keyboard configuration** and then click **Next**.

Usually Fedora Core detects and configures your mouse, but if it doesn’t, the Mouse Configuration window opens.

+   7. If prompted (unlikely), select your mouse (squeak!) and click **Next**.

+   - If you have a PS/2 mouse, all you have to do is select the manufacturer and the number of buttons.

+   - If you have the older style of mouse that connects via a serial port, you have to select the manufacturer, number of buttons, and serial port to which it’s connected: you can either only four serial ports to select from (in many cases, only two: either `ttyS0` or `ttyS1`).

+   - If you have a two-button mouse (either serial or PS/2), you can choose to have it emulate three buttons by selecting the **Emulate 3 Buttons** option. You emulate the third (middle) button by pressing both mouse buttons at one time.

+   8. In the **Installation Type** window, select the **Workstation** option and click the **Next** button.