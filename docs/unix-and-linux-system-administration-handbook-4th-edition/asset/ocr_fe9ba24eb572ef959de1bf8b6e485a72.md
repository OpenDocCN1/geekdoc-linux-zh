To see the value of a variable, use cat; to set it, use echo redirected to the proper filename. For example, the command

```
ubuntu$ cat icmp_echo_ignore_broadcasts
0
```

shows that this variable’s value is 0, meaning that broadcast pings are not ignored. To set it to 1 (and avoid falling prey to Smurf-type denial of service attacks), run

```
ubuntu$ sudo sh -c "echo 1 > icmp_echo_ignore_broadcasts"18
```

from the /proc/sys/net directory.

You are typically logged in over the same network you are tweaking as you adjust these variables, so be careful! You can mess things up badly enough to require a reboot from the console to recover, which might be inconvenient if the system happens to be in Point Barrow, Alaska, and it’s January. Test-tune these variables on your desktop system before you even think of tweaking a production machine.

To change any of these parameters permanently (or more accurately, to reset them every time the system boots), add the appropriate variables to /etc/sysctl.conf, which is read by the sysctl command at boot time. The format of the sysctl.conf file is variable=value rather than echo value > variable as you would run from the shell to change the variable by hand. Variable names are pathnames relative to /proc/sys; you can also use dots instead of slashes if you prefer. For example, either of the lines

```
net.ipv4.ip_forward=0
net/ipv4/ip_forward=0
```

in the /etc/sysctl.conf file would turn off IP forwarding on this host.

Some of the options under /proc are better documented than others. Your best bet is to look at the man page for the protocol in question in section 7 of the manuals. For example, man 7 icmp documents four of the six available options. (You must have man pages for the Linux kernel installed to see man pages about protocols.)

You can also take a look at the ip-sysctl.txt file in the kernel source distribution for some good comments. If you don’t have kernel source installed, just google for ip-sysctl-txt to reach the same document.

# Security-related kernel variables

Table 14.9 shows Linux’s default behavior with regard to various touchy network issues. For a brief description of the implications of these behaviors, see page 472. We recommend that you verify the values of these variables so that you do not answer broadcast pings, do not listen to routing redirects, and do not accept