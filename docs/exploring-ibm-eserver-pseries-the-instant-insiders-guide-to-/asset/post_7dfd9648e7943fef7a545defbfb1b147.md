
secure Internet transactions. The adapter is enclosed in a tamper-proof enclosure that meets the FIPS 140-Level 4 standard. Its functions include support for 56-bit and 40-bit Data Encryption Standard (DES), message authentication and financial PIN processing, secure data storage and retrieval. In addition to its functional capabilities, this adapter offers several physical security features. The following events will cause an adapter shutdown and zeroing of secure data:

- Shipping or storage temperature less than 15° or greater than 95°
- Dead battery
- Supply voltage greater than 3.3 volts/12 volts maximum
- Mesh sensor opens or shorts detection
- X-ray exposure

Due to the restrictive nature of shipping requirements for this adapter, the IBM Cryptographic Coprocessor (FIPS-4) (#4963) is field-installable.

## Network Processors

As many brands of personal computers and UNIX-based workstations proliferated, so did different types of networks (e.g., Token-Ring, Ethernet, and SNA) used to interconnect the various computer systems. Some of the protocols are Transmission Control Protocol/Internet Protocol (TCP/IP), Xerox Internet Services Transport (XNS), Internet Packet Exchange (IPX), and Digital Equipment Corporation Network (DCNet). All these communications environments were developed to satisfy specific applications and network requirements, and also with the best intentions of providing interfaces that would allow future growth. Nonetheless, the result has been many incompatible networks of computers found their way into many enterprises. This necessitated the development of products called routers and bridges that allow different networks to communicate freely with one another.

## Options and Peripherals

Although bridges and routers use different approaches, devices are used to connect two or more independent (and dissimilar) communications networks together so that the users on one network can communicate with the users over the other. Network processors building and routing functions allow you to directly link two local LANs together, link a LAN and a WAN, or link two LANs together over a WAN. Network processors are commercially available from a number of sources.

The rapid development of the Internet and the e-business have made it more than ever—in fact, almost mandatory—that computer suppliers provide complete hardware and software solutions that adhere to industry standards and allow businesses to integrate heterogeneous computer systems and to communicate with their customers, suppliers, and employees. These communications interfaces include high-speed Internet, industry-standard fast (gigabit) Ethernet, wireless LANs, and IP telephony capacity. Fundamental of all this is TCP/IP communications and Web-enabled user interfaces.

Recently, IBM and Cisco Systems announced an alliance to integrate IBM's products and services with Cisco's leadership networking products for the Internet. pSeries systems and the AIX 5L operating systems, historically designed to “open-system” standards, are well positioned to play a key role in this alliance. They provide the industry-standard communications hardware and software capabilities needed to allow integration with third-party networking products, as those from Cisco, to form high-performance scalable e-business solutions.

## Displays

Displays used with pSeries systems are essentially the same as those used on PCs. They are placed on a desktop near the server and attached to the pSeries systems by a cable to a graphics adapter in one of the PCI slots. Graphics adapter options will be discussed in the next section.

The color used with pSeries systems provide high-resolution, full-color images. The IBM displays currently available, with their maximum viewable screen size when measured diagonally and maximum flicker-free resolution, are listed next.

- P260/P275 Color Monitor (19.8 inches/503 mm) (21-inch) Maximum resolution: 1600 × 1200 at 85 Hz
- L200p Flat Panel Monitor (20.1 inch/510 mm) Maximum resolution: 1600 × 1200 at 75 Hz analog and 60 Hz digital
- T541 15-inch TFT Color Monitor (15.0 inches/381 mm) Maximum resolution: 1024 × 768 at 75 Hz analog and 60 Hz digital

The P260/P275 display (#3628) (don't confuse this “P-series” display terminology with the pSeries family of UNIX servers) features Trinitron flat CRT and easy-to-use digital controls. It is available in sleek black.

The P260/P275 provides a front panel with controls such as the on/off switch, brightness, mode selection, and centering. A tilt/swivel stand is standard and allows the user to position the display for comfortable viewing. Antiglare coating helps reduce any reflections on the face of the display. IBM’s displays are designed to meet energy and ergonomic guidelines. In particular, these displays do:

- Incorporate a power management function that reduces energy consumption and increases product life.
- Meet the Environmental Protection Agency’s requirements for the “Energy Star” program.
- Emit virtually no static—meeting MPR-II standards.
- Meet International Organization for Standardization (ISO) ergonomics and Federal Communication Commission (FCC) Class B requirements.

The L200p Flat Panel Monitor (#3636) is a thin-film technology (TFT) display using liquid crystal display (LCD) technology with a pitch of 0.25 mm for a maximum resolution of 1600 × 1200. For applications in which high-definition 3D imaging is required, this display is supported by the POWER GXT4500P and POWER GXT500P 3D graphics accelerators using the digital interface. The L200p can also be used with the POWER GXT135P 2D accelerator #2848 (analog) or #2849 (digital). The L200p Flat Panel Monitor is available only in black.

The T541H (#3637) is also a TFT display, but in a smaller size with lower resolution than the L200p. The T541H has a 15.0-inch diagonal viewing area with pitch of 0.27 mm and a maximum resolution of 1024 × 768 at 75 Hz to the analog interface or at 60 Hz with the digital interface. It is supported by the POWER GXT135P 2D graphics accelerator (#2848 or #2849) and cannot be used for 3D graphics.

## Graphics Adapters

To support these displays, pSeries or RS/6000 systems must be equipped with a graphics adapter which translates the information stored in the system into the electronic signals necessary to create images on the displays. Those unfamiliar with computer-generated graphics may want to refer to the section “Graphics” in Chapter 1 before reading about the graphics accelerator.

For several reasons, pSeries systems except for p630 and p640 support only 2D graphics, in which case the systems administrator needs a native graphics interface and display for use as the system console. In addition, many pSeries servers are managed in server farms and are controlled over a LAN from a PC. Finally, even pSeries systems used by one person often run applications that require only 2D support, such as scientific and technical computing, complex financial analysis, or software development. All pSeries use GXT135P graphics accelerator.

## Two-Dimensional Graphics Accelerators

The GXT135P graphics accelerator (#2848) is a versatile, low-cost 2D graphics option for pSeries systems. It can be configured to operate in either 8-bit or 24-bit modes. Its 24-bit true color images provide 16.7 million colors, and it supports display resolution up to 1600 × 1200 on multisync monitors or TFT displays. It satisfies the ISO 9241 standard of visual quality, refreshing the screen at 60 Hz to 85 Hz for all resolutions. The GXT135P (#2848) is supported on AIX 5L v5.1 and v5.2, as well as on AIX 4.3.

### POWER GXT135P with Digital Support

The GXT135P with Digital Support (#2849) is essentially the same as #2848, with the additions of providing both an analog and digital interface and supporting an analog resolution up to 2048 × 1536. It is the latest generation of low-cost 2D graphics options for pSeries systems. Maximum resolution at the digital interface is 1600 × 1200. This adapter also satisfies the ISO 9241 standard of visual quality. The GXT135P with Digital Support is supported on AIX 5L v5.1 and v5.2, as well as on AIX 4.3. However, the digital interface is supported only by AIX 5L v5.1 and v5.2.

## Three-Dimensional Graphics Accelerators

Although 2D graphics support is adequate for the applications run on pSeries servers, workstations used for automotive and aircraft design require high-performance three-dimensional graphics accelerators. The following 3D graphics adapters support the application programming interfaces (APIs) for three-dimensional graphics: OpenGL and DirectGL. Each API tends to be used in its own specialized set of applications. Since all of them support both OpenGL and DirectGL, selecting the right graphics adapter depends on what performance the application requires. In words, the traditional price/performance criteria should be used in selecting a 3D graphics adapter. The more expensive (and better performing) adapters implement more graphics features within the adapter hardware, whereas the lower-priced adapters will leave more of the processing to the host system's processor.

## POWER GXT4500P

The POWER GXT4500P 3D Graphics Accelerator is a single-card adapter supported on pSeries 630, pSeries 640, and RS/6000 Models.
