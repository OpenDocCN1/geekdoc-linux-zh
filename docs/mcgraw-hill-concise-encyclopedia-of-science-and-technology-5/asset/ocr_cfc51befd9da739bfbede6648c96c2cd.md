# **616 Dasycladales**

raw stems (underground stems) are baked or boiled to eliminate an irritating substance present in the cells. **See** ARELES.  
[P.R.S.I.E.C.]

# **Dasycladales**

An order of green algae (Chlorophyceae) in which the plant body (thallus) is composed of a nonsepate axis, attached by rhizoids and bearing whorls of branches. The walls utilize a partially crystalline mannann (polymer of mannose and fucose) as the skeletal component and usually are impregnated with argonite, a form of calcim carbon carbonate, causing these algae to be easily fossilized. Among green algae, only the Dasycladales have a fossil record sufficient to permit meaningful phylogenetic speculation. About 140 extinct genera have been described from limestones as old as the Ordovic, with three parts of abundance and diversity: Carboniferous, Jurassic-Cretaceous, and Eocene. Only about 11 genera comprising 50 species are extant, with 3 of the genus extending from the Cretaceous. All are confined to warm marine waters except _Botoptera_, which occurs as a relinct in brackish sinkholes in New Mexico in addition to having a normal Caribbean distribution.

The extant Dasycladales are usually placed in a single family, Dasycladaceae, but those forms in which fertile and sterile whorls alternate or only one fertile whorl is produced may be segregated as the Acatarhidiaceae (or Polyphyllaceae).  
**See** ALGAE; CHLOROPHYCEAE.  
[P.C.S.I. R.I.MoE]

# **Data communications**

The conveyance of information from a source to a destination. Data means the symbolic representation of information, generally in a digital (that is, discrete) form. (Analog information may be represented according to a continuous physical parameter, such as the height or amplitude of a wavefront, while digital information is encoded into a discrete set of some magnitude.) Usually, this digital information is composed of a sequence of binary digits (ones and zeros), called bits. A binary system is used because its simplicity is universally recognizable and because digital data have greater immunity to so-called noise than analog information and allow flexible processing of the information. Groups of eight bits create a data byte or character. These characters make up the so-called alphabets (including alphabetic, numeric, and special symbols) which are used in data communications. The most common data sources and destinations are computers and computer peripherals, and the data represent groups of characters to form text (either text organized according to topic rather than linear sequence), or multimedia information, including audio, graphics, animation, and video information.  
**See** BIT; COMPUTER; COMPUTER GRAPHICS; COMPUTER PERIPHERAL DEVICE; DIGITAL COMPUTER; MULTIMEDIA TECHNOLOGY.

Data communications may be accomplished through two principal functions, data transmission and data switching.

Data transmission always involves at least three elements: a source of the information, a channel for the transmission of the information, and a destination for the information. In addition, sometimes the data are encoded. The codes can be used for error detection and correction, compression of the digital data, and so forth. **See** DATA COMPRESSION.

The communications channel is carried over a transmission medium. Such media can be wired, as in the cases of twisted-pair telephone wires, coaxial cables, or fiber-optic cables, or they can be wireless, where the transmission is not confined to any physical medium, such as in radio, satellite, or infrared optical transmission. Sometimes, even when the source of the information is digital, the transmission medium requires analog signaling, and modems (modulators-demodulators) are required to convert the digital signal to analog for the wire line. For example, data communication between personal computers transmitted over telephone lines normally uses modems.  
**See** COAXIAL CABLE; COMMUNICATIONS SATELLITE; MODEM; OPTICAL COMMUNICATIONS; OPTICAL FIBERS; RADIO; TELEPHONE SERVICE.

The directionality of the information can be either one-way (simplex communication) or two-way. Two-way communications can be either half-duplex (information goes both ways over the communications link, but not at the same time) or full-duplex (information goes both ways at the same time).

The data channel can be a serial channel, in which the bits are transmitted one after another across a single physical connection; or a parallel channel, in which many bits are transmitted simultaneously (for instance, over parallel wires). Generally, small channels are used for short-distance links (less than 300 ft or 100 m), whereas serial links are used for larger distances and high data rates.

At low data rates (less than a few hundred kilobits per second) communications channels are typically dedicated, whereas at higher data rates, because of the cost of high-speed transmitters and receivers, shared channels are used for multiplexing the data streams. For example, two independent data streams with constant data rates of 10 megabits per second (Mb/s) could use a shared channel having a data-rate capability of 20 Mb/s. The multiplexing system would select one bit from each of the two channels to time-multiplex the data together. **See** MULTIPLEXING AND MULTIPLE ACCESS.

In many cases, the source, the destination, and the path taken by the data may vary; thus, switching is required.

The two primary types of switching employed in data communications are circuit switching and packet switching. In circuit-switched data communications, an end-to-end connection is established prior to the actual transmission of the data and the communications channel is open (whether or not it is in use) until the connection is terminated.

A packet is a group of data bytes that represents a specific information unit with a known beginning and end. The packet can be formed from either a fixed or variable number of bytes. Some of these bytes represent the information payload, while the rest represent the header, which contains address information to be used in routing the packet. In packet switching, unlike circuit switching, the packets are sent only when information transmission is required. The channel is not used when there is no information to be sent. Sharing the channel capacity through multiplexing is natural for packet-switched systems. Furthermore, the packet switches allow for temporary loading of the network beyond the transmission capacity of the channel. This information (overflow) is stored (buffered) in the packet switches and sent on when the channel becomes available.

In order to transfer information from a sender to a receiver, a common physical transmission protocol must be used. Protocols can range from very simple to quite complex. The Open Systems Interconnection (OSI) model, developed by the International Standards Organization, reduces protocol complexity by breaking the protocol into smaller functional units which operate in conjunction with similar functional units at a peer-to-peer level. Each layer performs functions for the next higher layer by building on the functions provided by the layer below. The advantage of performing communications based on this model is that at the application layers (user processes) there is no concern with the communications mechanisms.  
**See** ELECTRICAL COMMUNICATIONS; INTEGRATED SERVICES DIGITAL NETWORK (ISDN); PACKET SWITCHING; SWITCHING SYSTEMS (COMMUNICATIONS); TELEPROCESSING.  
[M.S.G.I]

# **Data compression**

The process of transforming information from one representation to another, smaller representation from which the original, or a close approximation to it, can be recovered. The compression and decompression processes are often referred to as encoding and decoding. Data compression has important applications in the areas of data storage and data transmission. Besides compression savings, other parameters of concern include encoding and decoding speeds and workspace requirements, the ability to access and decode partial files, and error generation and propagation.