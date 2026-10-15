
# Task 2

Install traceroute: `sudo apt install traceroute`

Now run a few more commands to verify that you have end-to-end connectivity with 101labs.net, and trace the routes in between.

* `ping 101labs.net`
* `traceroute 101labs.net`
* `sudo traceroute -I 101labs.net`
* `tracepath -b 101labs.net`

The first `traceroute` and `tracepath` commands here are using UDP, while the second `traceroute` is using ICMP. Sometimes the methods will yield different results; sometimes not.

If you have IPv6 connectivity, you can also experiment with those versions of the tools. (At the time of this writing, 101labs.net does not have an IPv6 address.)

* `ping6 example.com`
* `traceroute6 example.com`
* `tracepath6 -b example.com`

# Notes

For any kind of non-trivial network troubleshooting, `netcat` is a useful tool to know. It can act as an arbitrary client or server for TCP, UDP, or UNIX-domain sockets, and supports IPv4 and IPv6.
