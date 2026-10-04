# Attacking and Defending Unix • Chapter 14

to meet security expectations. Doing so closes a potential window of compromise that exists between the time of system installation and the time when the user gains access to the system to make the necessary modifications to the host configuration.

![](bbox=[0.125, 0.223, 0.875, 0.483])

# Dangerous Default Configurations

Many operating systems start an uncomfortable amount of services by default, and many of these services have or had security issues in the past. Installing a system with network connectivity can create a window in time that allows the attack and compromise of the host before staff have even had the chance to secure the host!

To eliminate this window, it is safest to install a system without network connectivity. This gives administrators a fighting chance.

As previously mentioned, some operating systems require, or at least provide, a facility that allows the user to install the entire operating system via the network. While this is convenient, and also provides network bandwidth conservation by preventing the downloading of unwanted or unneeded packages, there are some realistic expectations that one should ensure are fulfilled before using such a facility. It is not unreasonable to expect end-to-end security in such scenario, with multiple integrity checks such as the download of a cryptographic key from a trusted source, signed packages, and transfer via SSL. Figure 14.7 shows a checklist of items the user should expect when using such a service.

You can see there is a level of trust required when installing via the Internet. As previously mentioned, most vendors providing this facility have taken many of the listed factors into account, and have taken the necessary steps to ensure user security. However, if the choice is made to forego the conservative installation process, it is always safer to perform due diligence on the security of the vendor's delivery model rather than making an assumption.

![](bbox=[0.708, 0.943, 0.927, 0.968])