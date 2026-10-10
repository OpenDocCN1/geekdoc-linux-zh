# ## SSH

While `telnet` is still available on modern Linux systems, the preferred method for accessing a command shell on a remote system is with SSH, the Secure Shell. It is nearly as easy to use for basic shell access, is very secure, and offers several very cool extra features. There are two parts to `ssh`: the `ssh` client you use to connect to a remote system and the `sshd` "daemon" that runs on the remote side.

The syntax for `ssh` are as follows:

```
```
ssh [OPTIONS] [username@]hostname [command]
```
```

The list of options is truly bewildering, but for basic connectivity, all that is required to connect to server1 is to type

```
```
ssh server1
```
```

This abbreviated format assumes you want to use the same username on the remote system as you are using on the local one. The passwords don't have to match. To login to the remote system with a different username, you can either use the `-l username` option or type the username in front of the hostname, with an `@` between them, like this

```
```
ssh bob@server1
```
```

The first time `ssh` is used to connect to a remote host, the new hosts signature is shown, and `ssh` asks if you'd like to add the signature to your list of known hosts.

# ### Secure tunnels

One of the more interesting capabilities of `ssh` is to catch traffic going to a local TCP port, pass it through its own encrypted connection, and hand it off to a TCP port on the remote side. With this feature, it is possible to protect normally unencrypted network traffic. This is called forwarding or tunneling.

To create a tunnel, you need to know the TCP port of the service on the remote server that you want to tunnel to and pick a random unused TCP port on your local service. The syntax looks like this

```
```
ssh -Llocal_tcp_port:localhost:remote_tcp_port remote_host_name
```
```

An example of this is shown in the book *Next Generation SSH2 Implementation: Securing Data in Motion*, ISBN: 978-1-59749-283-6, Snyress,\[note]\[note] to forward SMTP traffic between your local e-mail client and your Simple Mail Transfer Protocol (SMTP) mail server http://my_mail_server.com using a randomly chosen local TCP port of 4444, and for the standard SMTP TCP port of 25, you would do this