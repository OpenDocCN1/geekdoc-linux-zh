# OPEN STORY

Open RAN

# Reference Model

Figure 5 shows the reference model of the 5G network. The three main elements are the terminal, the gNodeB, and the core network. The terminal can be a smartphone, an IoT system, a laptop, or any similar device. The gNodeB is the equivalent of a switch in Ethernet, acting below the IP layer. The core network is the equivalent of the ISP network. From bottom to top, the layers of the reference model are:

+   • Physical layer (PHY): deals with all the radio aspects of the communications, such as modulation and demodulation. See the “Radio Aspects” box for a definition of these terms.
+   • Medium Access Control (MAC): defines logical channels over the PHY channels (which are defined by time and frequency). Also performs error correction.
+   • Radio Link Control (RLC): provides a data transfer service to upper layers over the MAC, with error recovery, segmentation and reassembly, and reestablishment of radio link when needed.
+   • Packet Data Convergence Protocol (PDCP): provides an interface to higher layers with one or several RLC entities. This allows multi-connectivity, the ability of connecting to more than one gNodeB at RLC layer. It also provides some throughput gains with header compression.
+   • Service Data Adaptation Protocol (SDAP): provides mechanisms to ensure certain quality of service (QoS) to different data and receive data over the air, and it is called “distributed” because it is normally deployed physically near the RUs to reduce latency.
+   • The Central Unit (CU): Contains the higher layers, that is, functions such as routing the user and control data (PDCP layer) and assigning network resources such as channels and carriers (RRc layer). It is usually in a centralized location (hence the name) and can even be physically running in the same computer as the core.
+   Another element shown in Figure 4 is the RAN Intelligent Controller (RIC), which contains functions that control the overall operations of the RAN elements. The RIC includes functions such as optimization of resources, monitoring, etc., and even end user services that must be very close to the terminals. The RIC is further divided into Real Time RIC, for some lower-layer functions that require quick reaction times, and Non-Real Time RIC, with functions with longer timeframes In 6G, this element will contain ML-based solutions

+   flows. For instance, for video streaming, a steady data flow with a relatively high bandwidth is required, while for web browsing, the QoS requirements can be relaxed. This sublayer is present in the user plane, the part of the protocol stack that is used to transmit user data.
+   • Radio Resource Control (RRC): this is a control plane sublayer, so the functions it contains do not deal with user data, but with the metadata required to keep the service working correctly. In this case, it contains all the required protocols to keep the radio connection open and stable. It deals with handovers (changes of serving gNodeB), changes to more robust or capable modulations, etc.
+   • PDU layer: only present in the user plane and only in the terminal and the core network. It contains the IP functionality and connects the terminal to the UPF, which acts as a router.
+   • Non Access Stratum (NAS): only present in the control plane and only in the terminal and core network. It contains the control functionality, such as the establishment of connection between the terminal and core in the user plane, authentication, and other services.
+   • Application: in the user layer, the Application layer contains the higher layers of the services that operate between processes in the terminal and the remote servers.
+   that continuously monitor the network, learn by reinforcement, and improve the quality of service.
+   Except the RU, all other components are software components that can run in any computer with the minimum CPU, memory, and storage requirements. This support for commodity hardware means a drastic cost reduction for RAN manufacturers and operators.
+   The RAN can then be thought of as a network containing cloud instances and off-the-shelf computers, some of them with SDR devices. Some of this infrastructure is centralized, in a

![](bbox=[0.25, 0.63, 0.92, 0.93])