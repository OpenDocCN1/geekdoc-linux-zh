into an ore deposit can generally imply and rare. If those events placed the deposit sufficiently near the surface, open pit mining may be viable.

Material encountered during the mining process that has little or no economic value is called waste or overburden. One important economic criterion for open pit mining is the amount of overlying waste that must be removed to extract the ore. The ratio of the amount of waste to the amount of ore is referred to as the strip ratio. In general, the lower the strip ratio, the more likely an ore body is to be mined by open pit methods.

Modern open pit mining utilizes large mechanical equipment to remove the ore and waste from the open pit excavation. The amount of equipment and its type and size depend on the characteristics of the ore and waste and the required production capacity. In general, there are four basic unit operations common to most open pit mining operations. These are drilling, blasting, loading, and hauling.

Waste material that is generated during the course of mining at most mines must be discarded as economically as possible without jeopardizing future mining activities but while respecting environmental regulations. Two types of waste material are generated at most mining operations: waste rock and overburden from the mine, and tailings—the waste material from the processing plant after treatment of the ore. See LAND RECLAMATION.

Computer software is available to assist the mining engineer in ore reserve estimation with the application of geostatistics, mine planning and design, and production and maintenance monitoring and reporting. With the help of high-speed computers for the engineering and construction staff, all evaluation aspects of the mining activities, which allows a more efficient and economical extraction of the mineral commodity. See MINING; OPERATIONS RESEARCH; OPTIMIZATION. [H.W.e.; J.M.M.]

# **Operating system** The software component of a computer system that is responsible for the management and coordination of activities and the sharing of the resources of the computer. The operating system (OS) acts as a host for application programs that are run on the machine. As a host, one of the purposes of an operating system is to handle the details of the operation of the hardware. This relieves application programs from having to manage these details and makes it easier to write applications. Almost all computers, including hand-held computers, desktop computers, supercomputers, and even modern video game consoles, use an operating system of some type. See COMPUTER SYSTEMS ARCHITECTURE.

Operating systems offer a number of services to application programs and users. Applications access these services through application programming interfaces (APIs) or system calls. By invoking these interfaces, the application can request a service from the operating system, pass parameters, and receive the results of the operation. Users may also interact with the operating system by typing commands or using a graphical user interface (GUI, commonly pronounced "gooey"). For hand-held and desktop computers, the GUI is generally considered part of the operating system. For large multuser systems, the GUI is generally implemented as an application program that runs outside the operating system. See COMPUTER PROGRAMMING; HUMAN- COMPUTER INTERACTION.

Modern operating systems provide the capability of running multiple application programs simultaneously, which is referred to as multiprogramming. Each program running is represented by a process in the operating system. The operating system provides an execution environment for each process by sharing the hardware resources so that each application does not need to be aware of the execution of other processes. The central processing unit (CPU) of the computer can be used by only one program at a time. The operating system can share the CPU among the processes by using a technique known as time slicing. In this manner, the processes take turns using the CPU.

Single-user desktop personal computers (PCs) may simplify this further by granting the CPU to whichever application the user has currently selected and allowing the user to switch between applications at will.

The main memory of a computer (referred to as random access memory, or RAM) is a finite resource. The operating system is responsible for sharing the memory among the currently running processes. When a user initiates an application, the operating system decides where to place it in memory and may allocate additional memory to the application if it requests it. The operating system may use capabilities in the hardware to prevent one application from overwriting the memory of another. This provides security and prevents applications from interfering with one another. See COMPUTER STORAGE TECHNOLOGY.

The details of device management are left to the operating system. The operating system provides a set of APIs to the applications for accessing input/output (I/O) devices in a consistent and relatively simple manner regardless of the specifics of the underlying hardware. The operating system itself will generally use a software component called a device driver to control an I/O device. This allows the operating system to be upgraded to support new devices as they become available. In addition to a device driver for the network I/O device, the operating system includes software known as a network protocol and makes various network utilities available to the user. See COMPUTER PERIPHERAL DEVICES; LOCAL-AREA NETWORKS; WIDE-AREA NETWORKS.

Operating systems provide security by preventing unauthorized access to the computer's resources. Many operating systems also prevent users of a computer from accidentally or intentionally interfering with another. The security policies that an operating system enforces range from none in the case of a video game console, to simple password protection for hand-held and desktop computers, to very elaborate schemes for use in high-security environments. See COMPUTER SECURITY. [C.S.h.]

# **Operational amplifier** A voltage amplifier that amplifies the differential voltage between a pair of input nodes. For an ideal operational amplifier (also called an op amp), the amplification or gain is infinite.

Most existing operational amplifiers are produced on a single semiconductor substrate as an integrated circuit. These integrated circuits are used as building blocks in a wide variety of applications. See INTEGRATED CIRCUITS.

Although an operational amplifier is actually a differential-input voltage amplifier with a very high gain, it is almost never used directly as an open-loop voltage amplifier in linear applications for several reasons. First, the gain variation from one operational amplifier to another is quite high and may vary by ± 50% or more from the value specified by the manufacturer. Second, other nonidealities such as the offset voltage make it impractical to stabilize the dc operating point. Finally, performance characteristics such as linearity and bandwidth of the open-loop operational amplifier are poor. In linear applications, the operational amplifier is almost always used in a feedback mode.

A block diagram of a classical feedback circuit is shown in illus. A. The transfer characteristic, often termed the feedback gain $A_{f}$ of this circuit, is given by Eq. (1). In the limiting case,

```
$$A_{f}=\frac{X_{o}}{X_{i}}\frac{A}{1+A \beta} \tag{1}$$
```

A becomes very large, the feedback gain is approximated by Eq. (2).

```
$$A_{f} \simeq \frac{1}{\beta} \tag{2}$$
```

See FEEDBACK CIRCUIT.

An operational amplifier is often used for the amplifier designated $A$ in this block diagram. Since $A_{f}$ in the limiting case is independent of $A$, the exact gain characteristics of the operational amplifier become important provided the gain is large.