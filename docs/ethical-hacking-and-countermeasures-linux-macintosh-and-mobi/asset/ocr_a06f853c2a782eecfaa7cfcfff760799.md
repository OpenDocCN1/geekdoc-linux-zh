# Tag Readers

Tag readers can either be mounted on a fixed location or held in the hand. Depending on the radio frequency and power output used, they emit a broad range of radio waves. The *RFID tag antenna* is tuned to receive these waves. Thus, when an RFID tag passes through an electromagnetic zone, it detects the tag reader’s activation signal. The tag sends waves back to the reader. The reader decrypts the encrypted data present in the integrated circuit of the tag and sends the extracted data to the host computer for processing.

# RFID Tag Antenna

An RFID tag antenna is bundled with a transceiver and a decoder. Radio signals are emitted by the antenna to activate the tag. The tag then transmits the information on its microchip to the antenna. The antenna reads the data from the tag, and if the tag contains a read-write chip, the antenna can write data to the tag as well.

# RFID Controller

An RFID controller is used in a store or distribution center environment. It supports the following functions:

+   - Provides connectivity that is either synchronous or asynchronous
+   - Provides software deployment including device drivers, filters, aggregators, and dynamically loaded software modules
+   - Ensures security that authenticates the readers at the edge

# RFID Premises Server

An RFID premises server is used in a store or distribution center. It supports the following functions:

+   - Adds persistence for storing all incoming RFID events from controllers
+   - Ensures that commands and data are passed to the network using synchronous or asynchronous communication
+   - Provides limited support for process management
+   - Sends and receives commands and data from the server through synchronous or asynchronous methods, behaving like a gateway to the RFID integration server

# RFID Integration Server

It supports the following functions:

+   - Offers process integration with complex management
+   - Improves RFID data from existing sources, which provides the ability to clean and validate the data
+   - Integrates business-to-business processes and various graphical user interfaces
+   - Allows customers to select various software products to replace servers or to implement their own replacement solution

# RFID Collisions

# RFID Tag Collision

*RFID tag collision* occurs when an RFID tag reader energizes numerous tags and the tags’ respective signals are reflected back to the reader simultaneously. This tag collision confuses the reader and it cannot differentiate the signals. This usually happens when large volumes of tags are read together in the same RF field.

Various systems have been developed to isolate individual tags and prevent tag collision. Although these systems vary from vendor to vendor, one such system causes the reader to transmit a “gap pulse” to the tags whenever tag collision has occurred. When each tag receives this signal, it asks a random number counter to determine the amount of time to wait before sending its data. The tags wait for the interval of time to pass before sending the data, allowing the data to be sent separately.