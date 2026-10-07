# TABLE 4-1 Classes of IP Addresses

| Class of IP Address | Range of the First Number of the Address | Number of Network Nodes Available | Assignment Rules |
| --- | --- | --- | --- |
| A | 0-127 | hundreds of thousands | The first number is assigned; you assign the last three numbers to computers on your network. |
| B | 128-191 | tens of thousands | The first two numbers are assigned; you assign the last two numbers to computers on your network. |
| C | 192-223 | 256 | The first three numbers are assigned; you assign the last 253 numbers to computers on your network. |

This table tells you how to determine what class of address you're looking at. For example, the address 207.34.12.1 is a Class C address because the first number, 207, is in the range for C addresses. You are assigned certain numbers in an address, and choose other ones. So for example, when you receive a Class A address, you're assigned only the first number. You decide the last three numbers for every computer on your network. If you receive a Class C address, you're assigned the first three numbers (207.34.12 in the last example), and you assign the last number, with a range of 0 to 255, to various computers within your network.

It's interesting to note that because of the popularity explosion of the Web, the Class A addresses are long gone places like MIT, it's pretty hard to get a full Class C address. In fact, the Internet is running out of IP addresses. A new standard called IPv6, which provides plenty of space for the foreseeable future, is now in testing and will soon be available generally. Linux is one of the top testing platforms, and will likely be the most advanced platform for IPv6.

The Internet Protocol (IP) is the base that all Internet communication is built on. In the next section, you'll learn about some other protocols that are built on top of IP and communicate at a higher level.