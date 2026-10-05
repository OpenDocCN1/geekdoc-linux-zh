# 144 TCP/IP and Linux Protocol Implementation

| 13 * | Alan Cox | verify_area() fixes |
| 14 * | Alan Cox | Removed DDI |
| 15 * | Jonathan Kamens | SOCK_DGRAM reconnect bug |
| 16 * | Alan Cox | Moved a load of checks to the very top level. |
| 17 * | | Move address structures to/user |
| 18 * | Alan Cox | mode above the protocol layers. |
| 19 * | Rob Janssen | Allow 0 length sends. |
| 20 * | Alan Cox | Asynchronous I/O (cribbed from the tty drivers). |
| 21 * | | Asynchronous I/O for writes (4.4BSD style) |
| 22 * | Nibe Yutaka | Made max number of sockets command-line |
| 23 * | Jeff Uphoff | configurable. |
| 24 * | Matti Aarnio | Made the number of sockets dynamic, to be allocated when needed, and mr. |
| 25 * | | Uphoff's max is used as max to be allowed. |
| 26 * | Linus | Argh. removed all the socket allocation altogether: it's in the inode now. |
| 27 * | Alan Cox | sock_alloc()(socket_release()) public for Network and kernel nfs type stuff. |
| 28 * | | sendmsg/recv basics. |
| 29 * | | Export net symbols. |
| 30 * | Marcincki | Fixed problems with CONFIG_NET="m". |
| 31 * | Alan Cox | Added thread locking to sys.c calls for sockets. May have errors at the moment. |
| 32 * | | |
| 33 * | Kevin Burin | Fixed the dumb errors in the above. |
| 34 * | Andi Keelen | Some small cleanups, optimizations, and fixed a copy_from_user() bug. |
| 35 * | Tigran Aiavaz | sys_send(args) calls sys_sendto(args, NULL, 0) |
| 36 * | Tigran Aiavaz | Made listen(2) backlog sanity checks protocol-independent |

There is a copy of the GNU General Public License here, too.

**Figure 5** Socket interface—main copyright, and so on: linux/net/socket.c.

| 48 * | | This program is free software; you can redistribute it and/or |
| 49 * | | modify it under the terms of the GNU General Public License |
| 50 * | | as published by the Free Software Foundation; either version |
| 51 * | | 2 of the License, or (at your option) any later version. |
| 52 * | | |
| 53 * | | |
| 54 * | | |
| 55 * | | This module is effectively the top level interface to the BSD socket |
| 56 * | | paradigms. |
| 57 * | | |
| 58 * | /*/ |