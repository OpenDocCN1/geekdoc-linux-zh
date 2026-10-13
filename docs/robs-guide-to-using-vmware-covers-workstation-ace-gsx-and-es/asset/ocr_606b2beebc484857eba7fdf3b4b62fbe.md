# 15.3 The Low Cost Approach of P2V Conversion

During the last few years, I have performed many conversions to move physical machines into virtual machines. The actual technique is simple, but the complexity is in the operating system. Windows is especially not an operating system that can easily be transferred from one hardware platform to another.

# Imaging software

The software that I will introduce in this part for P2V conversion is regular imaging software that you may already own. I will also use tools and commands that are standard in all Linux distributions. The skills that you need for P2V, especially with Windows, are the skills that you would also need to have for normal imaging operations between different hardware platforms.

With imaging software, you copy a hard disk to another hard disk (mostly in another PC) directly via the network or via an image file to create a copy of a PC. This is a very common technology that is being used for deploying new PCs. The problem with imaging is mainly the difference in hardware on the source PC and the destination PC. Different network and video drivers, another hard disk type (IDE or SCSI), as well as many other differences in hardware can result in you not being able to load the imaged operating system on the destination PC. And not surprisingly, all available PCs contain other hardware than those on your virtual machines.

Whether you encounter problems with your P2V conversion depends on the operating system that you are converting. NetWare, for example, is a very imaging-friendly operating system. This is because it starts the kernel and if the configured hardware (storage adapter or ACPI support) is not found, it just does not load the driver. It stops at the server console, and allows you to copy the correct drivers to the server, and adds them to the server startup files. For Windows, the process is more complex, because if the Hardware Abstraction Layer is different, Windows generates a stop-error and ends with a blue screen. This is also something we can overcome. You will learn how to do this in chapter 21.

There are two methods to be used: P2V via an image file or P2V via the network. They both have their advantages and disadvantages.

# P2V via an image file

To use this method, you need to create an image file from your PC and store it somewhere. From that location, you should add the file into a virtual hard disk file and restore the image inside your virtual machine. The advantage is that it works with all imaging software because they all support image files. However, they do not all support imaging via the network. The disadvantage is that you may need a lot of disk space if your PC contains a lot of data. Storing a 50 GB image file, copying it into a virtual hard disk, and restoring it to another virtual destination hard disk requires 150 GB of available storage. This is three times the amount that you have available on your physical machine.