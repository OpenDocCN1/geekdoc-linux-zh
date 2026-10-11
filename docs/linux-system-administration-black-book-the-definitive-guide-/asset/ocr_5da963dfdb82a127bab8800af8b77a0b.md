# The Partial Address Class

Today it is difficult to get an entire class C address unless you have a demonstrable need for one. You are most likely to be handed a group of addresses from within a class C that belongs to your upstream provider. This situation leads to the nightmare of trying to figure out netmasks and other items for just part of a class C.

Newer routing protocols were required to simplify this process. These protocols see Internet addressing in a whole new light. They throw the whole concept of address classes out the window and instead use *classless routing*. This type of data routing sends both the IP address and the mask that shows where its network bits end and where its host bits begin, instead of assuming that all machines beginning with specific ranges of numbers have their network and host bits in the same exact spots.

Classless routing allows for some interesting tricks. You can use it to divide a network into subnets of different sizes instead of having to have them all the same size. It also lets people create sub-subnets, sub-sub-subnets, and even deeper subnets if they need to. Although the details of this type of networking are beyond the scope of this book, you can learn more about it in *IP Fundamentals*, by Thomas A. Mauf er.

# The Centrally Managed Network

The larger your network gets, the more onerous it becomes to add each new machine. Adding a new machine to a network requires editing every /etc/hosts file, adding user accounts and passwords on the new machine, having users change their passwords, and more. Fortunately, various tools are available to make your life easier as a system administrator.

# IP Addresses On Demand

Maintaining lists of addressing information on large networks on every machine is time-consuming and fraught with problems. This issue is especially troublesome if the network has to be reconfigured, if machines have to be moved around regularly, or if the network has more machines than available addresses due to growth after initial address allocation. With the Dynamic Host Configuration Protocol (DHCP) service, you can either hand out random IP addresses to machines as they boot or assign them permanent IP addresses. Additionally, you can give out netmasks, assign names, and specify the addresses of the name servers that the machines should use. The **pump** program handles both DHCP and the older Bootstrap Protocol (BOOTP) service in Red Hat Linux.