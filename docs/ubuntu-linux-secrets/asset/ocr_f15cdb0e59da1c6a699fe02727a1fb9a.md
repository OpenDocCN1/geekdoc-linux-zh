possible video card and monitor environment available. Instead, the X Windows software helps do that.

The X Windows software operates as an intermediary between the Ubuntu system and the input and output devices connected to the workstation. It’s responsible for controlling the graphical environment so that GNOME doesn’t have to support different types of video cards and monitors. Instead, the X Windows software handles all of that, and the GNOME software has to interact with just the X Windows software to display images on any type of video card and monitor combination.

Besides dealing with the video card and monitor, X Windows also handles any input devices attached to the workstation, such as the keyboard and mouse. It’s the main clearinghouse for all interaction for the desktop environment. Figure 16-1 shows a typical X Windows system.

![](bbox=[0.177, 0.316, 0.673, 0.576])

**Figure 16-1:** The X Windows system layout.

Because the X Windows software handles all of the input and output functions for the Ubuntu workstation, it’s important to ensure that the X Windows software is working properly. It must know the type of input and output devices it’s communicating with so that you can interact with your desktop.

The X Windows software is actually a specification of how to interact in a client/server methodology, serving the input and output devices to Ubuntu applications. Two popular X Windows implementations are currently available in the Linux world. The next section discusses them.

# Linux X Windows Software

Over the years, two X Windows software packages have emerged in the Linux world:

+   - XFree86
+   - X.Org

Let’s take a quick look at both of these packages.