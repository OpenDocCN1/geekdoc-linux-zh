To switch circuits, a WAN uses a method in which a dedicated physical circuit is established and maintained. It is also terminated through a carrier network for each communication session. Circuit switching accommodates two types of transmissions:

+   - Datagram transmissions
+   - Data-stream transmissions

Circuit switching operates very much like a normal telephone call operates and is used extensively in telephone company networks.

A WAN virtual circuit is a logical circuit that ensures reliable communication between two network devices. There are two types of virtual circuits:

+   - Switched virtual circuits (SVCs)
+   - Permanent virtual circuits (PVCs)

SVCs are dynamically established on demand and terminated when the transmission is complete. Communication over an SVC consists of three phases:

+   - Circuit establishment
+   - Data transfer
+   - Circuit termination

The first phase involves creating the virtual circuit between the source and destination devices. Data transfer involves transmitting data between the devices over the virtual circuit. The circuit termination phase involves tearing down the virtual circuit between the source and destination devices. SVCs are usually used when data transmission between devices is sporadic. SVCs increase bandwidth used due to the circuit establishment and termination phases but decrease the cost associated with constant virtual availability. (Both LANs and WANs are discussed further in Chapter 14.)

PVCs are predefined, logical connections through a switched network between two points. They are not flexible as SVCs are. Their primary benefit is the elimination of a call setup period. Typically, they are used to support communications between network devices that communicate on a routine basis. The PVC's endpoints are defined by data link connection identifiers and are given a committed information rate through the Frame Relay network. The data link connection identifiers are given a minimum available quantity of bandwidth with the option to temporarily burst beyond that limit under certain circumstances.

# ## The SNIA Shared Storage Model

Storage networking builds on many of the principles of traditional networking but adds additional functionality and emphasizes different services. Several groups in the storage industry have begun to build shared storage models and to publish and