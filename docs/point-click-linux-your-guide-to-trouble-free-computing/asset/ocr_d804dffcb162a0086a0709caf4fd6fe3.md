Unfortunately, the process for using Samba to get Windows to access Linux network shares is much more complicated to set up and configure in both Linux and Windows, so in this chapter we're only going to deal with accessing Windows shares. For this example we're going to assume you have a Windows machine that has already been set up for a work-group-based network.

# The smb4k Utility

In the lower right-hand corner of your screen you'll notice a green and blue icon. That's your Samba client already running, scanning for Windows networks to connect to. Left-click on the icon to bring up the Share Browser.

![](bbox=[0.78, 0.27, 0.93, 0.33])

As you can see, all your Windows workgroups are listed in the left-hand portion of the window. In this example the name of our workgroup is, appropriately, **workgroup**. This is the default name for most versions of Windows; Windows XP's default workgroup name is **mshome**. Aside from defaults, you may have chosen your own workgroup name when you set up your network, or you might have multiple workgroups for different purposes throughout your home or office.

![](bbox=[0.35, 0.37, 0.91, 0.75])