# CHAPTER 10

# HOST DRIVER FOR EMBEDDED CONTROLLER

In This Chapter

+   - Bootstrap Linux USB HCD
- Linux USB HCD
- Sample Implementation of USB HCD

This host controller hardware is compliant and implements universal serial bus (USB) host control interface (HCI) specifications defined by vendors such as Intel and Compaq. The software portion of the HCI acts as an interface to the system software. The host controller driver (HCD) is the lowermost layer of the USB host framework that directly interacts with the host controller hardware. On Linux, the HCD acts as an interface between the usbcore and the host controller hardware. It integrates the host controller hardware with the platform and allows the layers above it to manage and communicate with the connected USB device.

This chapter explores the Linux USB HCD framework that is essential for a developer to bring up his host controller hardware. It begins by discussing the essential data structures and interface functions of the Linux USB HCD. Then it explores the functional modules of the HCD and the sequence of activities that occurs inside the HCD. It concludes with a sample implementation of an HCD.