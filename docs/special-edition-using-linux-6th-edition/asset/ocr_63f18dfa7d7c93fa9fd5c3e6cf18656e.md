The ipsec.secrets file will contain pairs of IP addresses with a shared secret. The lines will look like this:

```
192.168.0.2 192.168.0.1: PSK "0xb9e7371_74116d27_bd83734a_4e247ec9_221a9826_d78475ec"
```

Each system, in this case 192.168.0.1 and 192.168.0.2, must have this line in its individual ipsec.secrets file. Now these two systems will be able to authenticate each other and set up an encrypted tunnel. You can add as many lines as you need encrypted tunnels. Let’s assume you have three gateways that will tunnel traffic: California (192.168.1.1), New York (192.168.2.1), and Florida (192.168.3.1). You will need lines like this:

```
192.168.1.1 192.168.2.1: PSK "0xb0ad0fef_fecead4_cb19d474_2386a7fe_4a4f3106_6346855a"
192.168.1.1 192.168.3.1: PSK "0x23070df_7b54495e_dc22177_edf7fa4b_aacf5fa3_946b4a0a"
192.168.2.1 192.168.3.1: PSK "0x0fde3304_20722cf5_c62c68c1_c9502b5a_47952a0d_6d42387"
```

California should have the two lines containing 192.168.1.1 in its ipsec.secrets file; New York, the two lines containing 192.168.2.1; and Florida, the two lines containing 192.168.3.1. Although it won’t hurt for California to have the line that does not pertain to it (the shared secret between New York and Florida), one reason for not including it is increased security. Should the California host be compromised, the attacker will also be able to read traffic between New York and Florida because she has the key.

> > **Note**
> > Fully qualified domain names can be used, but a DNS outage would prevent a connection. For this reason, IP addresses are preferred.

If you want to simplify things just a little, you could have all three share the same secret. You can do this with the following lines:

```
192.168.1.1 192.168.2.1 192.168.3.1: PSK
"0x22d7faed_6357520f_a870f87f_926f6526_7efa4ff9_239d6a8e"
```

You can split the single line after any particular element in the parameter, but you must indent successive lines. The tradeoff with using one key for multiple tunnels is that one broken host exposes all encrypted tunnels.

As for where to get the key, you use the /usr/local/sbin/ipsec ranbits <bits> command to generate the shared secret. The preceding secrets were generated with a bits value of 192. You can make this value anything you want. But remember, the number of bits is directly related to the time it takes to encrypt or decrypt the message and also to the security of the message. That is, more bits take more time but are more secure (will take longer to “break”).

# ipsec.conf

The ipsec.conf file is the heart of the ipsec configuration and is broken down into two major parts: the config section and the conn section.

The config section contains general settings for the ipsec implementation on the system. The only valid config as of this writing is setup. Listing 20.1 shows a sample config section from an ipsec.conf file.