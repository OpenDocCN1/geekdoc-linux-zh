forwarding, while the *sshd_config* option controls remote port forwarding.

GatewayPorts is set to no by default, meaning that clients cannot connect any port forwarding to any network-facing IP address. This is identical in both *ssh_config* and *sshd_config.*

When used in *ssh_config*, setting GatewayPorts to yes to allows ssh to request to listen to any IP on the client.

On the server side, setting GatewayPorts to yes in *sshd_config* means that no matter what the client requests, remote forwarding always listens to all addresses on the host. I have no idea why you’d enable global network access on all port forwardings, but it’s an option.

The server supports one additional GatewayPorts option in *sshd_config*, `clientspecified`, which tells sshd to let a client bind to whatever they request. Permitting the client fine-grained control on a forwarding-by-forwarding basis is usually the best choice.

# Allow Specific Ports and Addresses

If you want more specificity than GatewayPorts supports, you can restrict which TCP ports and addresses can be forwarded with the PermitOpen keyword in *sshd_config*. PermitOpen takes a space-delimited list of ports that may be forwarded in the form of hostname:port. For example, here I permit the server’s ports 25 and 110 to be forwarded back to the client, and only from the localhost address.

```
PermitOpen localhost:25 localhost:110
```

Anything not permitted is forbidden. The SSH session will open normally, but when you attempt to pass traffic over a forbidden forwarded port your SSH client displays an error.

# Requiring Port Forwarding

Perhaps the port forwarding is the only reason for this connection to exist. If setting up port forwarding fails, you don’t even want the connection to establish. The ExitOnForwardFailure *ssh_config* keyword tells ssh what to do in the event an attempt to forward a port fails. The default, no, means the connection should be set up even if port forwarding cannot be established. By setting ExitOnForwardFailure to yes, you tell SSH to immediately disconnect if the port forwarding doesn’t work.

Now that you know how to selectively forward ports to help glue your network together, let’s see how to keep an SSH session alive for hours or days at a time, without human intervention.

1 My HTML education ended about 1996, and I have no desire to resume it.

2 Yes, we're solving the wrong problem here. The real fix is to replace the boneheaded application.