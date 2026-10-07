# CHAPTER 2

# USB: AN OVERVIEW

In This Chapter

+   - USB System Architecture
- Enumeration
- USB Transfers
- Terms to Remember

The universal serial bus (USB) technology works in the master-slave communication model. The USB host controls complete communication (playing the master's role), and the USB device responds to the USB host's request (playing the slave role). The devices are connected to the USB host in a tiered-fashion, with a maximum of 127 devices connected to the host. Figure 2.1 from the USB 2.0 specification illustrates the star-tier topology of a USB setup.

To an end user working on a USB host or a device, these topological layers are invisible. The USB device looks as if it's connected directly to the USB host, as shown in Figure 2.2. This is done through the system software, which hides all these topological information and presents direct access to a device.

Because this book focuses mainly on the software aspect of a USB system, this chapter explores some key points from software development's perspective, extracted from the USB specification. This chapter begins with the system architecture of USB, which gives you an idea of the functional blocks of a USB system and how information