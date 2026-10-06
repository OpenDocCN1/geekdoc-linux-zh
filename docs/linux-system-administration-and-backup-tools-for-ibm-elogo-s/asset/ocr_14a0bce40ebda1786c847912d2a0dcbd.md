# Chapter 5. TurboLinux basic system administration

Linux follows the conventional UNIX method of storing configuration in plain text files under the directory /etc. Many of these files are human readable, and many others can be understood with a little experience with the system. However, it is quite time consuming and confusing to administering a Linux server by directly editing files in /etc, at least until you are more experienced. For this reason, we will emphasize the TurboLinux provides to make administration more convenient and understandable to novice and intermediate Linux users, while at the same time pointing to the actual files in /etc being modified.

# 5.1 Configuring X with Netfinity and XSeries servers

Current Netfinity and XSeries servers have several versions of S3 video cards that are not fully supported by the version of XFree86 (the X server) that ships with Turbo. Therefore you may encounter an issue of configuring X to work properly. In this section we will start with instructions to configure an X with generic SVGA server. We will then give instructions for using the VESA frame buffer server (see 5.1.2, "Installing the VESA frame buffer server" on page 127), a generic driver that will give basic support to any video card.

# 5.1.1 X-Windows configuration and startup

X-Windows configuration is a process that is still a work in progress. In Appendix B, "Working modes for IBM Netfinity servers" in the IBM redbook, TurboLinux Integration Guide for IBM @server XSeries and Netfinity, SG24-5862 are some of the monitor and video adapter settings you need to be concerned about when setting up your X-Windows system. In order to configure your XWindows you need to run a tool that will probe the system for information and build or modify a file to include the appropriate information. Two tools are available to perform the X-Windows configuration that can run from your Linux command prompt:

+   * turbcfg. This is also called Xconfigurator.
* XF86Setup. This program is a standard X-Windows tool and can sometimes provide information that is different from turbocfg.

In Figure 122 is an example of executing turbocfg.