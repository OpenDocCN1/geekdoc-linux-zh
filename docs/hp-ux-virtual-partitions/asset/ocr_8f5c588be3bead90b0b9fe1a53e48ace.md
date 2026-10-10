# ## CHAPTER 13

# # Networking

# ## Virutal Partitions and Networking

You should have a minimum of one networking card devoted to each Virtual Partition. vPars will communicate with other vPars and other systems over the networking card(s). Like all components, networking cards in different Virutal Partitions are managed independently of one another and from the Virutal Partition to which they are attached. In the upcoming sections we’ll perform some basic work on networking cards and the networks of Virutual Partitions in general. We’ll view the configuration of network cards and the way in which Virutal Partitions communicate with one another over the network - even when these vPars are running on the same system.

To perform basic tasks such as **telnet** or *file transfer protocol* between two Virutal Partitions running on the same system, you would use their network cards. There is no low-level vPar-specific functionality that allows communication over the backplane between vPars as opposed to through the respective network cards of the vPars.