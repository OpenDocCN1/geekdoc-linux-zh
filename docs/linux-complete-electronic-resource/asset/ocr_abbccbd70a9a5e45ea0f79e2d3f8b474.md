# # Assigning a Private Network IP Addresses

Since all other machines do not have official assigned addresses, there must be a right way to allocate addresses to those machines.

The following information is from the IP Masquerade FAQ. There is an RFC (1597, probably obsolete by now) on which IP addresses are to be used on a non-connected network. There are three blocks of numbers set aside specifically for this purpose. One which I use is 255 Class C subnets at 192.168.1.n to 192.168.255.n.

The following is from RCF 1597:

> Section 3: Private Address Space
> 
> The Internet Assigned Numbers Authority (IANA) has reserved the following three blocks of the IP address space for private networks:
> 
>     10.0.0.0        -    10.255.255.255
>     172.16.0.0      -    172.31.255.255
>     192.168.0.0     -    192.168.255.255
> 
> We will refer to the first block as "24-bit block", the second as "20-bit block", and to the third as "16-bit" block". Note that the first block is nothing but a single class A network number, while the second block is a set of 16 contiguous class B network numbers, and the third block is a set of 255 contiguous class C network numbers.
> 
> So, if you're using a class C network, you should name your machines as 192.168.1.1, 192.168.1.2, 192.168.1.3, ..., 192.168.1.x.

192.168.1.1 is usually the gateway machine, which is your Linux host connecting to the Internet. Notice that 192.168.1.0 and 192.168.1.255 are the Network and Broadcast address respectively, which are reserved. Avoid using these addresses on your machines.

# # Configuring the Other Machines

Besides setting the appropriate IP address for each machine, you should also set the appropriate gateway. In general, it is rather straightforward. You simply enter the address of your Linux host (usually 192.168.1.1) as the gateway address.