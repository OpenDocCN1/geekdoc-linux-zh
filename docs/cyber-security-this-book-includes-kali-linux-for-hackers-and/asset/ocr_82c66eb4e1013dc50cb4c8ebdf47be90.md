find that its full name is windows / smb / ms08_067_netapi.

So we would type the following command: use windows / smb /
ms08_067_netapi

If everything goes well (we have written the name of the exploit
correctly) metasploit will show on the console the exploit you are
using in red, indicating that you have managed to load it.

Once this is done, we will proceed to use a payload to take
advantage of the exploit. To see a list of payloads compatible with
our exploit, we will use the show payloads operation.

```
msf exploit ( ms08_067_netapi )> show payloads
```

As we can see, metasploit tells us that you are ready to use the
payload. If we introduce show options below we will be shown the
options that we can use:

```
msf exploit ( ms08_067_netapi )> show options
```

# ### Automatic Targeting

We see that in this case, all the options are necessary (all have
the Required = yes field) as well as most of them already have a
default value, although we can adjust them to our convenience with
the command set [option] [parameters] as we will see next.

We indicate the IP of the target machine, as well as ours, by
means of the orders set RHOST [ target ip ] and set LHOST [our IP],
as we have seen in the table of options above.

After putting the corresponding IPs, we will use the meterpreter to
take advantage of the vulnerability. Once initialized meterpreter we
can fully exploit the vulnerability.

# ### How does it work?

Metasploit Framework has a modular architecture (which we can
see in more detail below) this means that each exploit is integrated
into the framework so that it can interact with it (and consequently