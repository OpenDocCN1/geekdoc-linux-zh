version. ipmasqcuseme.c normally resides in net/ipv4 off of the Linux source tree. You should compile and install this module.

Now, you should set up IP Autoforwarding for UDP ports 7648–7649 as follows:

```
ipautofw -A -r udp 7648 7649 -c udp 7648 -u
```
or
```
ipautofw -A -r udp 7648 7649 -h www.xxx.yyy.zzz
```

The first form will allow calls to/from the last workstation to use port 7648 (the primary CU-SeeMe port) . The second invocation of ipautofw will allow CU-SeeMe calls only to/from www.xxx.yyy.zzz. I prefer the former invocation, as it is more flexible because there is no need to specify a fixed workstation IP. However, this invocation also requires a workstation to have previously placed an outgoing call in order to receive incoming calls.

Note that both invocations leave UDP ports 7648–7649 on the client machines open to the outside world—and while this does not pose an enormous security hazard, you should use appropriate caution.

Finally, load up the new ipmasqcuseme module as follows:

```
modprobe ip_masq_cuseme
```

You should now be able to fire up CU-SeeMe from a masqueraded machine on your LAN and connect to a remote reflector or another CU-SeeMe user. You should also be able to get incoming calls. Note that outside callers should call using the IP of your Linux gateway, not the masqueraded workstation.

# Restrictions/Caveats

# Password Protected Reflectors

No way, no how. Un-uh. Negatory. White Pine uses the source IP (as computed by the client program) to encrypt the password prior to transmission. Since we have to rewrite this address, the reflector ends up using the wrong source IP to decrypt it, which yields an invalid password. This will only be fixed if White Pine changes their password encryption scheme (which I have suggested), or if they would be willing to make their password encryption routines public so I could add in a fix to ipmasqcuseme. While chances for the latter solution are vanishingly small, I would encourage anyone reading this to contact White Pine and suggest the former approach. On the traffic on this page is relatively high, I suspect we could generate enough e-mail to get this problem moved up on White Pine’s list of priorities.

Thanks to Thomas Grienwka for bringing this to my attention.

![](bbox=[0.93, 0.56, 0.98, 0.8])