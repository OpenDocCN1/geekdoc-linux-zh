As with so many UNIX commands, this is of the strong silent type, and unless you made some error in typing it in, it prints nothing and just returns you to the command prompt. If you want to check that it has done what you expected (always a good idea with **route** commands, even when you’ve had years of experience), run `**route –n**` to print the new settings.

The various parts of this command are:

+   add we’re adding a new route, not just displaying the settings, or deleting an existing route

+   default we’re defining the default gateway. In fact **default** is just a shorthand for `“-net 0.0.0.0”` so you could instead have entered the command as

```
route add -net 0.0.0.0 gw 192.0.2.1
```

(We’ll explain the `“-net”` in Chapter 5. Don’t worry about it for now.)

+   gw this keyword indicates that the following argument is the IP address of the router. The **route** command uses keywords like this to introduce values because, as you can see if you print the help message, you can set lots of different values for routes. Note that the words `“default gw,”` which occur together in the command are **not** the phrase ‘default gateway,’ even though it looks that way. This will be even clearer in Chapter 5 where you’ll see commands like

```
route add -net 10.5.0.0 netmask 255.255.0.0 gw 192.168.13.28
```

# ## Common errors

# ### network is unreachable

The router you’ve specified as the default gateway isn’t in the range of IP addresses specified by this machine’s IP address and netmask. For example, if your IP address is 192.0.2.34 with netmask 255.255.255.0 and you enter the command

```
route add default gw 1.2.3.4
```

you’ll get the “network is unreachable” error.

# ### SIOCGADDR: Operation not supported by device

You get this error if you omit the **gw** keyword before the IP address, as in

```
route add default 192.0.2.29
```

This is very easy to do if you’re used to other UNIX systems where the syntax of the **route** command is slightly different.

# ## Making your settings permanent

Just like the *ifconfig* settings that we covered in Module 2.11, your Linux default gateway setting defined with **route add** is lost when you reboot the system, so you must store them in a configuration file. See Appendix 6.