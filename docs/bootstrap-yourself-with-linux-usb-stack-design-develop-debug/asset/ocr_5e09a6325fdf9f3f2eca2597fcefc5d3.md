# USB Transfers

maximum transfer size of 512 bytes, is nonperiodic, and uses any available bus bandwidth. Because bulk transfers occur only on the basis of the bandwidth available, the transfers are faster when there are large amounts of free bandwidth.

A bulk pipe happens on a stream pipe, and the communication flow is either into or out of the host for a given pipe. A bulk transfer provides guaranteed data with no guaranteed delivery time. A bulk transfer does retry a transfer to ensure a guaranteed delivery of data in the case of occasional delivery failure due to errors on the bus.

The data in the bulk transfer is specific to the functional driver. It is not defined by a USB format.

# Interrupt Transfer

An interrupt transfer is used for nonperiodic, small data and supports a maximum packet size of 1,024 bytes. It is generally used to report status information (such as a cursor point) or a small amount of data (such as characters from a keyboard). This data is delivered in a limited latency; most of the application lacks explicit timing requirements.

An interrupt transfer is transferred in a stream pipe, and the data transferred is not USB specific. An interrupt transfer provides guaranteed delivery of data, in which the protocol does retry in case of any errors on the bus.

# Isochronous Transfer

An isochronous transfer is used for applications such as Web camera or audio transfers, which require periodic transfer of data from the device to the host. Because isochronous data is continuous and real time, on-time delivery is important. The isochronous transfer supports a maximum packet size of 1,024 bytes, and the on-time delivery is ensured by allocating a dedicated portion of USB bandwidth. However, the timely delivery comes at the expense of potential losses in the data stream

An isochronous transfer is transferred in a stream pipe, and the data transferred is not USB specific. Because isochronous data is bound by time, no retrying attempt to deliver the data is made for bus errors.