# TCP/IP COMPONENTS

Just as a language has certain components, such as words, grammar, and syntax, the TCP/IP protocol contains components that enable each computer on a TCP/IP network to function and communicate on the network. You must configure three major TCP/IP components on TCP/IP computers: the IP address, subnet mask, and default gateway.

Binary numbers are calculated by counting from the right to the left of a series of binary digits. Each bit counts twice as much as the previous bit. In other words, the first bit equals 1, the second bit equals 2, the third bit equals 4, and so forth. In an IP address, there are 8 bits, so the eighth bit is equal to 128:

```
128 64 32 16 8 4 2 1
```

# IP Address

Each computer on a TCP/IP network must have a unique IP address. The IP address identifies that computer on the network and the address must be unique (no two computers can have the same IP address. You can think of an IP address as being similar to a postal address, which is uniquely identified by city, state, zip code, then by street address, then by the person’s name. These address qualities enable the postal system to deliver a piece of mail to a particular person at a particular address. A computer’s IP address enables the network to deliver communication to that particular computer.

In binary math, the bits are added together to determine the numerical value. For example, if all bits in the octet are turned "on," then the numerical value is 255. In other words, 11111111 in binary is equal to 128+64+32+16+8+4+2+1, which equals 255.

Each IP address is 32 bits long, and is divided into 4 bytes. Each byte is referred to as an octet. A typical IP address looks like this: 131.107.2.200. In order to understand IP addressing, you have to start thinking in binary math. Computers see data in terms of ones and zeroes. In essence, a stream of network data is simply made up of ones and zeroes that the computer interprets. One (1) represents "on" and zero (0) represents "off."

If all the bits are "off," then the binary representation is 00000000 which is equal to 0+0+0+0+0+0+0+0, which equals 0. Using this scheme, you can represent any number between 0 and 255.

For example, what is binary value of 10? Remember that the bits in the octet must be turned on or off to equal the number ten. In the binary octet, the number 10 is represented as 00001010, which equals 0+0+0+0+0+8+0+2+0, which equals 10.

An IP address is made up of four octets that are separated by periods. A typical IP address you may assign to a computer would be 10.2.0.4. In binary, the computers see this address as:

```
00001010 00000010 00000000 00000100
```