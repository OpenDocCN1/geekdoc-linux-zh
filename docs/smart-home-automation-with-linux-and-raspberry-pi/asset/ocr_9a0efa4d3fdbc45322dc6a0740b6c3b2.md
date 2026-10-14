# Motion Sensors

Most sensors on the market are passive infrared sensors (PIRs) and exist in both indoor and outdoor varieties, with the latter being commonly used as security lights that are mounted in the same area as the sensor. PIRs, like the EagleEye Motion Sensor (MS14), send an “on” message to specific but user-selectable X10 modules whenever motion is detected. Most models can also be configured to send “on” and “off” messages at dusk and dawn, respectively. Although some devices can send the message to more than one device (the PR511 and PSH01 spring to mind, both of which contain built-in floodlights), most only communicate to a single device, requiring a computer in your X10 setup to relay this message to other devices if required. You’ll discover how later!

# Gateways and Other Exotic Devices

A *gateway* is any device that allows communication data to flow through it, despite each side of the conversation having different protocols. In most technologies, a gateway performs a two-way function, converting the protocols in either direction. In an X10 gateway, there is generally only one direction, that is, *into* X10.

The primary device in this category is the TM13U, the RF-to-X10 gateway that I’ve touched upon already. One of these devices, shown in Figure 1-12, allows a wireless RF remote control to place messages onto the power lines for an X10 device to process. It never does the reverse. This device will listen for all RF messages coming from the same house code as is set on its front dial and retransmit them (using the same house code) to the mains line (provided that the socket is switched on). If the dial is set to P, however, it will respond to RF signals for all house codes but retransmit them on the original house code. This device generally has a hardwired address of 1.

![](bbox=[0.1, 0.448, 0.251, 0.887])