+   5. Continue. When the welcome screen appears, click Release Notes to see information about this version of Fedora Core. Click Next when you're ready to continue.

+   6. Choose a language. When prompted, indicate the language that you would like to use during the installation procedure by moving the arrow keys and selecting Next. (Later, you will be able to add additional languages.) You are asked to choose a keyboard.

+   7. Choose a keyboard. Select the correct keyboard layout (U.S. English, with Generic 101-key PC keyboard by default). Some layouts enable dead keys (on by default). Dead keys let you use characters with special markings (such as circumflexes and umlauts).

+   8. Choose install type. Select either “Install Fedora Core” for a new install or “Upgrade an existing installation” to upgrade an existing version of Fedora.

# Choosing Different Install Modes

Although most computers will enable you to install Fedora in the default mode (graphical), there may be times when your video card does not support that mode. Also, though the install process will detect most computer hardware, there may be times when your hard disk, Ethernet card, or other critical piece of hardware cannot be detected and will require you to enter special information at boot time.

The following is a list of different installation modes you can use to start the Fedora install process. You would typically only try these modes if the default mode failed (that is, if the screen was garbled or installation failed at some point). For a list of other supported modes, refer to the /usr/share/doc/anacorn2/cmdline.txt file or press F2 to see short descriptions of some of these types.

+   - linux text: Type linux text to run installation in a text-based mode. Do this if installation doesn't seem to recognize your graphics card. The installation screens aren't as pretty, but they work just as well.

+   - linux lowres: Type linux lowres to run installation in 640x480 screen resolution for graphics cards that can't support the higher resolution.

+   - linux nofb: Type linux nofb to turn off frame buffer.

+   - linux noprobe: Normally, the installation process will try to determine what hardware you have on your computer. In noprobe mode, installation will not probe to determine your hardware; you will be asked to load any special drivers that might be needed to install it.

+   - linux mediacheck: Type linux mediacheck to check your DVD or CDs before installing. Because media checking is done next in the normal installation process, you should do this only to test the media on a computer you are not installing on.

+   - linux rescue: The linux rescue mode is not really an installation mode. This mode boots from DVD or CD, mounts your hard disk, and lets you