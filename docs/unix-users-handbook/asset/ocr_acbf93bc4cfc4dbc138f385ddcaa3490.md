# *Link Layer*

In order to connect to other systems local to your system, you use the link layer that is able to establish a connection to all the other systems on your local segment. This is the layer where you have either IEEE 802.3 or Ethernet. These are "encapsulation" methods, named so because your data is put in one of these two forms (either IEEE 802.3 or Ethernet). Data is transferred at the link layer in frames (just another name for data), with the source and destination addresses and some other information attached. You might think that because there are two different encapsulation methods they must be much different. This conclusion, however, is not the case. IEEE 802.3 and Ethernet are nearly identical. So with the bottom two layers, you have a physical connection between your systems and data that is encapsulated into one of two formats with a source and destination address attached. Figure 16-2 lists the components of an Ethernet encapsulation and includes comments about IEEE802.3 encapsulation where appropriate.

| destination address | | 6 bytes | | address to which data is sent |
| :--- | :--- | :--- | :--- | :--- |
| source address | | 6 bytes | | address from which data is sent |
| type | | 2 bytes | | the "length count" in 802.3 |
| data | | 46-1500 bytes | | 38-1492 bytes for 802.3 |
| crc | | 4 bytes | | checksum to detect errors |


**Figure 16-2 Ethernet Encapsulation**

One interesting item to note is the difference in the maximum data size between IEEE 802.3 and Ethernet of 1492 and 1500 bytes, respectively. This is the Maximum Transfer Unit (MTU). The data in