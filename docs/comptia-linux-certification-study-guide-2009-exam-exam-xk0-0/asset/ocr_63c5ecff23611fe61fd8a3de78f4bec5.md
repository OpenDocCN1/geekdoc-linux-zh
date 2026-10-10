Linux networking utilizing Transmission Control Protocol/Internet Protocol (TCP/IP) and how to manage this within Linux.

User management is one of the fundamental tasks that needs to be understood for day-to-day management of a Linux system, and to be able to achieve this in an effective manner is necessary for all Linux administrators. This is equally important whether the system is used by yourself, your whole family, or a large corporation. Users should have the correct rights and environment setup to ensure that their experience in using the system is favorable and that the support overhead is kept to a minimum.

As part of the system setup, the user will need and want to access the various devices installed on the system. The correct setup of these devices needs to be accomplished prior to deployment to ensure that the system is functioning correctly. This will typically need to be undertaken at the super-user level, a level of privilege that is typically not bestowed onto a normal user. In addition, the user interaction at this level can often cause system instabilities, which may be hard to diagnose.

The networking of the computer system, whether via wired or wireless connection, is usually a given necessity in today’s world. There will be very few systems deployed without this capability, and often, the user will require both options, particularly in any form of portable device. The computer will also typically use TCP/IP as the transport mechanism for the network connections, and the different options available to set up this will be discussed. The basics in connecting to name servers and Dynamic Host Configuration Protocol (DHCP) servers are also discussed, and the majority of parameters are explained.

# USER PROFILES

Any installation of Linux will include the creation of a number of different user accounts: the superuser, a normal day-to-day user, and a system user. Each of these accounts is important in their own right, and a user needs to understand the differences.

All users need to have an account on the system, which should be unique to them to ensure that there is a basic level of security built in. A normal user can add, delete, and modify their files and those that have the appropriate attributes set. These users cannot make system wide changes nor can they manage other users on the system. Standard users can also make changes that are specific to them, such as desktop wallpaper and addition of printers.

Users who are specified as being a superuser [also referred to as a system administrator] have global privileges, can create and delete users, and can