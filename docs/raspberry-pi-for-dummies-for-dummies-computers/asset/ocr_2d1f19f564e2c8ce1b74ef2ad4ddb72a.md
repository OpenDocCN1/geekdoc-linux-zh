The Raspberry Pi automatically connects to the Internet when used with a router that supports the Dynamic Host Configuration Protocol (DHCP), which means it works with most domestic routers. For advice on troubleshooting your Internet connection, see Appendix A.

If you have a Wi-Fi adapter, you can plug it into a USB socket so that it's ready for when you switch on your Raspberry Pi.

# # Connecting the Power and Turning on the Raspberry Pi

The last thing you do is not connect the power. The Micro USB power socket is indicated in Figures 3-1, Figure 3-2, and 3-3.

![](bbox=[0.153, 0.406, 0.226, 0.477])

The Raspberry Pi Foundation warns against using battery power unless you know what you're doing, because it's easy to damage your Pi unless you provide a steady 5 volts (5v) of power. Some cellphone emergency chargers can be used to provide steady power, but you should proceed with caution.

The Raspberry Pi has no on/off switch, so when you connect the power, it starts working. To turn it off again, disconnect the power. To avoid losing data, you should shut down first (see Chapters 4 and 5) and wait for that process to finish. Sean plugs his USB hub and Raspberry Pi into power sockets on an extension lead, so he can switch them simultaneously by switching on the power to extension lead. It's less clumsy than removing or inserting the plug in the wall socket or the power lead in the Raspberry all the time. It can also help prevent backpowering, where the USB hub feeds power back into the Raspberry Pi with the possible risk of causing damage to your Pi if there is a power surge.

![](bbox=[0.143, 0.683, 0.236, 0.754])

If you're using the Lite version of NOOBS, you need a network connection to download the operating system you wish to install. You can plug a network cable into the Ethernet port on the Pi, configure the onboard Wi-Fi on the Raspberry Pi 3 Model B or Pi Zero, or plug a Wi-Fi dongle into a USB port. You will be prompted to set this when NOOBS runs, but you can get back to the settings by clicking Wi-Fi networks or pressing W on the keyboard.

When you switch your Raspberry Pi, the screen shows a rainbow of color briefly and starts to run the NOOBS software on the SD or MicroSD card, as shown in Figure 13-2. The software gives you a choice of operating systems to install, and language and keyboard options at the choice of the screen.