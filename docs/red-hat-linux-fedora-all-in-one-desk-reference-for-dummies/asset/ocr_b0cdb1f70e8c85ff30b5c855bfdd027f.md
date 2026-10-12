Figure 1-7:
A modem bridges the digital world of PCs and the analog world of telephones.

![](bbox=[0.28, 0.2, 0.88, 0.38])

Before you can dial out using an external modem, you have to make sure that the modem is properly connected to one of the serial or USB ports of your PC.

If you have an external modem, make sure that your modem is properly connected to the power supply and that the modem is connected to the telephone line. Buy the right type of cable to connect the modem to the PC. You need a straight-through serial cable to connect the modem to the PC. The connectors at the ends of the cable depend on the type of serial connector on your PC. The modem end of the cable needs a male 25-pin connector. The PC end of the cable often is a female 9-pin connector. You can buy modem cables at most computer stores. Often you can find 9-pin-female-to-25-pin-male modem cables sold under the label "AT Modem Cable." Connect USB modems by using a USB cable.

![](bbox=[0.15, 0.7, 0.25, 0.8])

If your PC has an internal modem, all you have to do is connect the phone line to the phone jack that's at the back of the internal-modem card. If it's a winmodem, you still connect the phone line, but you also have to do a bit of research on the Internet and download a driver that makes the winmodem work in Red Hat Linux. After you install a working Linux driver for a winmodem, it works just like the older serialport modems.

# Learning the serial-device names

The PC typically has two serial ports, called COM1 and COM2 in MS-DOS parlance. Many new PCs with Universal Serial Bus (USB) have only one serial port. The PC also can support two more serial ports: COM3 and COM4. Because of these port names, we often refer to the serial ports as COM ports.

Like other devices, the serial-port devices are represented by device files in the /dev directory. The serial ports also need interrupt request (IRQ) numbers and I/O port addresses. Two IRQs — 3 and 4 — are shared among the four COM ports. Table 1-2 lists the serial-device names corresponding to the PC's COM ports, as well as the IRQs and I/O port addresses assigned to the four serial ports.