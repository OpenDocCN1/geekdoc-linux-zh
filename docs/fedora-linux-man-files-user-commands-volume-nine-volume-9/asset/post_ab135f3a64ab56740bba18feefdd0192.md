
## ESCAPE CHARACTERS

When a pseudo-terminal has been requested, ssh supports a number of functions through the use of an escape character.

A single tilde character can be sent as `~~` or by following the tilde by a character other than those described below. The escape character must always follow a newline to be interpreted as special. The escape character can be changed in configuration files using the `EscapeChar` configuration directive or on the command line by the `-e` option.

The supported escapes (assuming the default `~`) are:

- `~.`
  - Disconnect.
- `~/`
  - Background.
- `~#`
  - List forwarded connections.
- `~&`
  - Background ssh at logout when waiting for forwarded connection / X11 sessions to terminate.
- `~?`
  - Display a list of escape characters.
- `~B`
  - Send a BREAK to the remote system (only useful for SSH protocol version 2 and if the peer supports it).
- `~C`
  - Open command line. Currently this allows the addition of port forwardings using the `-L`, `-R` and `-D` options (see above). It also allows the cancellation of existing port-forwardings with `-KL [bind_address : port]` for local, `-KR [bind_address : port]` for remote and `-KD [bind_address : port]` for dynamic port-forwardings. `!` command allows the user to execute a local command if the `PermitLocalCommand` option is enabled in `ssh_config 5`. Basic help is available, using the `-h` option.
- `~R`
  - Request rekeying of the connection (only useful for SSH protocol version 2 and if the peer supports it).
- `~V`
  - Decrease the verbosity (`LogLevel`) when errors are being written to `stderr`.
- `~v`
  - Increase the verbosity (`LogLevel`) when errors are being written to `stderr`.

## TCP FORWARDING

Forwarding of arbitrary TCP connections over the secure channel can be specified either on the command line or in a configuration file. One possible application of TCP forwarding is a secure connection to a mail server; another is going through firewalls.

In the example below, we look at encrypting communication between an IRC client and server, even though the IRC server does not directly support encrypted communications. This works as follows: the user connects to the remote host using `ssh`, specifying a port to be used to forward connections to the remote server. After that it is possible to start the service which is to be encrypted on the client machine, connecting to the same local port, and **ssh** will encrypt and forward the connection.

The following example tunnels an IRC session from client machine “127.0.0.1” (localhost) to remote server “server.example.com”:
`$ ssh -f -L 1234:localhost:6667 server.example.com sleep 10 $ irc -c '#users' -p 1234 pinky 127.0.0.1`

This tunnels a connection to IRC server “server.example.com” joining channel “#users” nickname “pinky” using port 1234. It doesn’t matter which port is used, as long as it’s greater than 1023 (remember, only root can open sockets on privileged ports) and doesn’t conflict with any ports already in use. The connection is forwarded to port 6667 on the remote server, since that’s the standard port for IRC services.

The **-f** option backgrounds **ssh** and the remote command “sleep 10” is specified to allow an amount of time (10 seconds, in the example) to start the service which is to be tunnelled. If no connections are made within the time specified, **ssh** will exit.

## X11 FORWARDING

If the **ForwardX11** variable is set to “yes” (or see the description of the `-X -x` and `-Y` options above) and the user is using X11 (the **DISPLAY** environment variable is set), the connection to the X11 display is automatically forwarded to the remote side in such a way that any X11 programs started from the shell (or command) will go through the encrypted channel, and the connection to the real X server will be made from the local machine. The user should not manually set **DISPLAY**. Forwarding of X11 connections can be configured on the command line or in configuration files.

The **DISPLAY** value set by **ssh** will point to the server machine, but with a display number greater than zero. This is normal, and happens because **ssh** creates a “proxy” X server on the server machine for forwarding the connections over the encrypted channel.

**ssh** will also automatically set up Xauthority data on the server machine. For this purpose, it will generate a random authorization cookie, store it in Xauthority on the server, and verify that any forwarded connections carry this cookie and replace it by the real cookie when the connection is opened. The real authentication cookie is never sent to the server machine (and no cookies are sent in the plain).

If the **ForwardAgent** variable is set to “yes” (or see the description of the `-A` and `-a` options above) and the user is using an authentication agent, the connection to the agent is automatically forwarded to the remote side.

## VERIFYING HOST KEYS

When connecting to a server for the first time, a fingerprint of the server’s public key is presented to the user (unless the option **StrictHostKeyChecking** has been disabled). Fingerprints can be determined using ssh-keygen1:

```
$ ssh-keygen -l -f /etc/ssh/ssh_host_rsa_key
```

If the fingerprint is already known, it can be matched and the key can be accepted or rejected. If only legacy (MD5) fingerprints for the server are available, the ssh-keygen1 -E option may be used to downgrade the fingerprint algorithm to match.

Because of the difficulty of comparing host keys just by looking at fingerprint strings, there is also support to compare host keys visually, using *random art*. By setting the **VisualHostKey** option to “yes” a small ASCII graphic gets displayed on every login to a server, no matter if the session itself is interactive or not. By learning the pattern a known server produces, a user can easily find out that the host key has changed when a completely different pattern is displayed. Because these patterns are not unambiguous however, a pattern that looks similar to the pattern referred to only gives a good probability that the host key is the same, not guaranteed proof.

To get a listing of the fingerprints along with their random art for all known hosts, the following command line can be used:

```
$ ssh-keygen -lV -f ~/.ssh/known_hosts
```

If the fingerprint is unknown, an alternative method of verification is available: SSH fingerprints verified by DNS. An additional resource record (RR), SSHFP, is added to a zonefile and the connecting client is able to match the fingerprint with that of the key presented.

In this example, we are connecting a client to a server, “host.example.com”. The SSHFP resource records should first be added to the zonefile for host.example.com:

```
$ ssh-keygen -r host.example.com.
```

The output lines will have to be added to the zonefile. To check that the zone is answering fingerprint queries:

```
$ dig -t SSHFP host.example.com
```

Finally the client connects:

```
$ ssh -o "VerifyHostKeyDNS ask" host.example.com [...J Matching host key fingerprint found in DNS. Are you sure you want to continue connecting (yes/no)?
```

See the **VerifyHostKeyDNS** option in ssh_config5 for more information.

## SSH-BASED VIRTUAL PRIVATE NETWORKS

**ssh** contains support for Virtual Private Network (VPN) tunnelling using the (4) network pseudo-device, allowing two networks to be joined securely. The *sshd_config*5 configuration option **PermitTunnel** controls whether the server supports this, and at what level (layer 2 or 3 traffic).

The following example would connect client network 10.0.50.0/24 with remote network 10.0.99.0/24 using a point-to-point connection from 10.1.1.1 to 10.1.1.2, provided that the SSH server running on the gateway to the remote network, at 192.168.1.15, allows it.

On the client:

```
# ssh -f -W 0:1 192.168.1.15 true # ifconfig tun0 10.1.1.1 10.1.1.2 netmask 255.255.255.252 # route add 10.0.99.0/24 10.1.1.2
```

On the server:

```
# ifconfig tun1 10.1.1.2 10.1.1.1 netmask 255.255.255.252 # route add 10.0.50.0/24 10.1.1.1
```

Client access may be more finely tuned via the /root/ssh/authorized_keys file (see below) and the **PermitRootLogin** server option. The following entry would permit connections on (4) device 1 from user “jane” and on tun device 2 from user “john” if **PermitRootLogin** is set to “forced-commands-only”:

```
tunnel=1,command="sh /etc/netstart tun1" ssh-rsa... jane
tunnel=2,command="sh /etc/netstart tun2" ssh-rsa... john
```

Since an SSH-based setup entails a fair amount of overhead, it may be more suited to temporary setups, such as for wireless VPNs. More permanent VPNs are better provided by tools such as (8) and (8).
