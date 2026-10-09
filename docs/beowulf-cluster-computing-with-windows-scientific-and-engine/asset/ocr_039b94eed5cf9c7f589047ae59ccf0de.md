# # 2 An Overview of Cluster Computing

Thomas Sterling

Commodity cluster systems offer an alternative to the technical and commercial computing market for scalable computing systems for medium- and high-end computing capability. For many applications they replace previous-generation monolithic vector supercomputers and MPPs. By incorporating only components already developed for wider markets, they exploit the economy of scale not possible in the high-end computing market alone and circumvent significant development costs and lead times typical of earlier classes of high-end systems resulting in a price/performance advantage that may exceed an order of magnitude for many user workloads. In addition, users have greater flexibility of configuration, upgrade, and supplier, ensuring longevity of this class of distributed system and user confidence in their software investment. Beowulf-class systems exploit mass-market components such as PCs to deliver exceptional cost advantage with the widest space of choice for building systems. Beowulfs integrate widely available and easily accessible low-cost or no-cost system software to provide many of the capabilities required by a system environment. As a result of these attributes and the opportunities they imply, Beowulf-class clusters have penetrated almost every aspect of computing and are rapidly coming to dominate the medium to high end.

Computing with a Beowulf cluster engages four distinct but interrelated areas of consideration:

+   1. hardware system structure,
+   2. resource administration and management environment,
+   3. distributed programming libraries and tools, and
+   4. parallel algorithms.

Hardware system structure encompasses all aspects of the hardware node components and their capabilities, the dedicated network controllers and switches, and the interconnection topology that determines the system’s global organization. The resource management environment is the battery of system software and tools that govern all phases of system operation from installation, configuration, and initialization, through administration and task management, to system status monitoring, fault diagnosis, and maintenance. The distributed programming libraries and tools determine the paradigm by which the end user coordinates the distributed computing resources to execute simultaneously and cooperatively the many concurrent logical components constituting the parallel application program. Finally, the domain of parallel algorithms provides the models and approaches for organizing a