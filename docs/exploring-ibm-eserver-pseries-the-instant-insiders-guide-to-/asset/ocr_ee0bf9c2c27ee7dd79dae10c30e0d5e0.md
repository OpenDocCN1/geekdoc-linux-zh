tions from SuSE are supported on most pSeries servers, including LPARs.
Distributions from Red Hat and Turbo Linux are available for selected
pSeries and RS/6000 systems. This chapter includes a section on Linux
support for pSeries servers. For links to additional information about
Linux, see the companion Web site for this book (www.maxpress.com).

# Device Drivers

The third and final layer of software in our software model is the device
driver layer (highlighted in Figure 3.4). “Device driver” is a fancy term
for a set of highly specialized programs, usually written by the manuf-
turer of hardware. These specialized programs reside in pSeries
main memory or in memory provided right on the adapters they control.

Unlike application programs or operating systems, device drivers
are only used by the users and exist only to help application programs and
the operating system elements under their tasks. They interact directly with
computer hardware elements under the control of the operating system

![](bbox=[0.3668, 0.5465, 0.7152999999999999, 0.8065])

**Figure 3.4.** The device driver software layer of the software model. Device
drivers directly control the hardware elements of pSeries systems and shield
application programs and operating systems from hardware details.