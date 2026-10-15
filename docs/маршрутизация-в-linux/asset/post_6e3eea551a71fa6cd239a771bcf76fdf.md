
The second chance for dividing your network is into four pieces because those first two x’s can be 00, 01, 10, or 11. So now your network bytes are nnnnnnnn.nnnnnnnn.nnnnnnnn.nnhhhhhh. Once again, TCP/IP keeps track of this through your netmask. The last byte of your netmask is equal to the position values of the n’s within it. So the netmask for a two-subnet network is 255.255.255.128. It follows that the netmask for four subnets is 255.255.255.192. Table 4.4 outlines the possible IP v4 subnets for a class C address and their pertinent values.

## Table 4.4 Pertinent Facts About the Possible IP v4 class C Subnets, Where n Stands for Network Bit, h Stands for Host Bit, and x Stands for Network Byte

| Number | Network Bits | Binary Netmask | Decimal Netmask |
|---|---|---|---|
| 2 | nhhhhhhhh | .10000000 | 255.255.255.128 |
| 4 | nnhhhhhhh | .11000000 | 255.255.255.192 |
| 8 | nnnhhhhhh | .11100000 | 255.255.255.224 |
| 16 | nnnnhhhh | .11110000 | 255.255.255.240 |
| 32 | nnnnnnhh | .11111000 | 255.255.255.248 |
| 64 | nnnnnnnh | .11111100 | 255.255.255.252 |
| 128 | nnnnnnnh | .11111110 | 255.255.255.254 |

Now, some of these subnet sizes are pretty unrealistic. We’ll illustrate why by getting into the internals of the subnetwork addresses, host address ranges, and more. Let’s take the two-subnet case to start with you. You can use the remaining host bits to help you determine the range of host numbers that goes toward each subnetwork. In the case of the two-subnet breakdown, the h’s (host bits) in n hhhhhhhh add up to 127. So subnet 1 is from x.x.x.0 through x.x.x.127, and subnet 2 is from x.x.x.128 through x.x.x.255.

It’s not that simple though. The first and last host bits are always reserved, even in a subnetted network, so you really only get x.x.x.1 through x.x.x.126 and x.x.x.128 through x.x.x.254 for your subnets. Now we have to pull out the network addresses. For subnet 1 this is x.x.x.1 and for subnet 2 this is x.x.x.128—for the entire network it’s x.x.x.0, and that’s all the rest of the Internet sees. So your available host IP addresses are now x.x.x.2 through x.x.x.126 and x.x.x.129 through x.x.x.254. We now need the subnet broadcast addresses, as opposed to the x.x.x.255, which broadcasts to the entire network. Those would be the last address in each subnet, x.x.x.127 and x.x.x.254. Now our hosts can be x.x.x.2 through x.x.x.126 and x.x.x.129 through x.x.x.253. As you can see, for the convenience of turning our class C network into two subnetworks, we’ve given up the use of four host IP addresses.

Things of course get more complex as we create four subnets. The host bits in nnhhhhhh add up to 63, so we end up with the following four subnet ranges: x.x.x.0 through x.x.x.63, x.x.x.64 through x.x.x.127, x.x.x.128 through x.x.x.191, and x.x.x.192 through x.x.x.255. Once again, we lose x.x.x.0 and x.x.x.255 to the overall network address and broadcast address. We also lose x.x.x.1, x.x.x.64, x.x.x.128, and x.x.x.192 to network addresses; x.x.x.63, x.x.x.127, x.x.x.191, and x.x.x.254 to broadcast addresses. Table 4.5 lays out the address ranges for each subnetting possibility and the address lost as well.

## Table 4.5 Host and Special Addresses Among IP v4 Class C Subnets Two Through Thirty-Two, Assuming That x.x.x.0 and x.x.x.255 Are Always Lost for Network and Broadcast Addresses

| Number of Networks | Network Numbers | Broadcast Addresses | Host Addresses |
|---|---|---|---|
| 2 | x.x.x.1, x.x.x.128 | x.x.x.127, x.x.x.254 | x.x.x.2 – x.x.x.126, x.x.x.129 – x.x.x.253 |
| 4 | x.x.x.1, x.x.x.64, x.x.x.128, x.x.x.192 | x.x.x.63, x.x.x.127, x.x.x.191, x.x.x.254 | x.x.x.2 – x.x.x.62, x.x.x.65 – x.x.x.126, x.x.x.129 – x.x.x.190, x.x.x.193 – x.x.x.253 |
| 8 | x.x.x.1, x.x.x.32, x.x.x.64, x.x.x.96, x.x.x.128, x.x.x.160, x.x.x.192, x.x.x.224 | x.x.x.31, x.x.x.63, x.x.x.95, x.x.x.127, x.x.x.159, x.x.x.191, x.x.x.223, x.x.x.254 | x.x.x.2 – x.x.x.30, x.x.x.33 – x.x.x.62, x.x.x.65 – x.x.x.94, x.x.x.97 – x.x.x.126, x.x.x.129 – x.x.x.158, x.x.x.161 – x.x.x.190, x.x.x.193 – x.x.x.222, x.x.x.225 – x.x.x.253 |
| 16 | x.x.x.1, x.x.x.16, x.x.x.32, x.x.x.48, x.x.x.64, x.x.x.80, x.x.x.96, x.x.x.112, x.x.x.128, x.x.x.144, x.x.x.160, x.x.x.176, x.x.x.192, x.x.x.208, x.x.x.224, x.x.x.240 | x.x.x.15, x.x.x.31, x.x.x.47, x.x.x.63, x.x.x.79, x.x.x.95, x.x.x.111, x.x.x.127, x.x.x.143, x.x.x.159, x.x.x.175, x.x.x.191, x.x.x.207, x.x.x.223, x.x.x.239, x.x.x.254 | x.x.x.2 – x.x.x.14, x.x.x.17 – x.x.x.30, x.x.x.33 – x.x.x.46, x.x.x.49 – x.x.x.62, x.x.x.65 – x.x.x.78, x.x.x.81 – x.x.x.94, x.x.x.97 – x.x.x.110, x.x.x.113 – x.x.x.126, x.x.x.129 – x.x.x.142, x.x.x.145 – x.x.x.158, x.x.x.161 – x.x.x.174, x.x.x.177 – x.x.x.190, x.x.x.193 – x.x.x.206, x.x.x.209 – x.x.x.222, x.x.x.225 – x.x.x.238, x.x.x.241 – x.x.x.253 |

continues
