Although the Open Group managed development of the X Window System as public domain software, no version of X was freely available; it was included only as part of expensive UNIX systems from vendors such as IBM and Hewlett-Packard. These versions of X typically ran on expensive minicomputers such as the IBM RS/6000 and Hewlett-Packard PA-RISC-based systems.

The XFree86 Project was started as a nonprofit organization dedicated to creating a version of X for Intel-based versions of UNIX. The XFree86 Project software was welcomed by Linux developers because it provided the foundation for a graphical interface similar to that used by all other UNIX-like operating systems. X was soon incorporated into every mainstream Linux distribution. You can read more about the XFree86 Project at www.xfree86.org.

# How the X Window System Functions

The Macintosh and Microsoft Windows graphical environments are successful because they run on widely available computer hardware. In particular, the developers of Microsoft Windows worked to ensure that Windows could use any popular video card; likewise, as Windows itself became hugely popular, video card manufacturers scrambled to make sure they created software to help Microsoft Windows function with their hardware.

Coming from UNIX roots, the developers of X took a different approach. Instead of embedding video card specifications in a driver, they designed a text-based configuration file that lets the user basically write the driver for any video card that comes on the market. For all this potential technological power, the result was that X was very difficult to configure on Linux.

Fortunately, recent developments by the XFree86 Project and by Linux vendors mean that virtually all video cards are now automatically configured by the Linux installation program. Later in this chapter you learn about using configuration utilities to set up or refine the graphical configuration.

# Components of the X Window System

The developers of X used a clever design that has allowed X to continue as a viable technology more than 15 years after it was first released. This design separates control of the video card (sending signals to the computer hardware) from management of program information on the screen. The following list of components shows the modular nature of the X Window System design:

+   - An X server is the program that communicates with the video card, sending the most basic instructions on what images should appear on the screen. It is similar to a video card driver, but an X server also interacts with the keyboard and mouse used in a graphical environment. The X server relies on other components to tell it what to display and to process keyboard and mouse input.