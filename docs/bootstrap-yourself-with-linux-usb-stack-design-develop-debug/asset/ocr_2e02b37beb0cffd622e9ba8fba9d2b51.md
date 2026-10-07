# Chapter 1 = USB and Linux: Introduction

![](bbox=[0.085, 0.095, 0.915, 0.313])

Figure 1.2
USB hardware configuration at a broad level.

which enables faster time to market. Figure 1.2 illustrates different configurations of USB controllers available in the industry.

The USB controllers can be standalone or integrated with an application processor. A standalone controller provides easy integration using simple interfaces available in the host processor. It provides an easy solution for fixing hardware errors by replacing the USB controller with the new corrected one. However, in an integrated solution, fixing any bug involves a high cost. On the other hand, USB in an integrated Internet Protocol (IP) means a single-point powerful solution that helps build complex systems.

In general, USB controller chips available on the market can be USB transceivers, standalone USB controllers, or application processors with USB controllers as part of them. The following section offers a brief overview of these hardware configurations and can help you when you implement a low-level driver.

# USB Transceiver

A transceiver is a simple mechanism that sends and receives signals from the same circuitry. A USB transceiver enables processors to have a digital USB core integrated on-chip, without the analog circuitry. The USB transceiver thus supports connection detection functionality and provides the analog electrical signalling requirement defined by the USB specification. Figure 1.3 illustrates a USB system block diagram, demonstrating how a USB transceiver fits in a USB system.