
The RSA keys are stored in the following files:

- /etc/ssh/ssh_host_key (private half)
- /etc/ssh/ssh_host_key.pub (public half)

The DSA keys are located in the following files:

- /etc/ssh/ssh_host_dsa_key (private half)
- /etc/ssh/ssh_host_dsa_key.pub (public half)

You are now ready to accept SSH connections over port 22. Make sure that any perimeter security devices that may be in front of the OpenSSH server allow incoming connections to TCP port 22.

The SSH client takes a number of command-line options. Table 12.3 lists the most important ones.

**Table 12.3:** ssh Client Command-line Options

| Option | Meaning |
|:-----------|:-----------|
| -l user | Log on as username user. |
| -i file | Identity file for RSA authentication (other than $HOME/.ssh/identity). |
| -v | Display verbose output (useful for debugging). |
| -V | Display version number. |
| -q | Don't display any messages (quiet). |
| -c [3des | blowfish] | Select an encryption algorithm. |
| -C | Enable compression. |
| -o option | Specify an option (using the same format as /etc/ssh/ssh_config) for this session only. |

For example, to connect to remote SSH server `remote.example.com` as root using the Blowfish encryption algorithm, use the following command:

```bash
[ramon]$ ssh -l root -c 'blowfish' remote.example.com
root@remote.example.com's password:
Last login: Wed Feb 7 16:55:33 2001 from redhat.example.com
remote:~ #
```

Or, to connect to the same server with the `StrictHostKeyChecking` option (listed in Table 12.2) turned off, use the following command:

```bash
[ramon]$ ssh -l root -c 'blowfish' -o StrictHostKeyChecking=no \
remote.example.com
Warning: Permanently added 'remote.example.com,209.207.155.67' (DSA)
to the list of known hosts.
root@remote.example.com's password:
Last login: Wed Feb 7 17:03:37 2001 from redhat.example.com
remote:~ #
```

Note that the local SSH client has warned you that you have received a DSA host key from the remote end. If you ever need to disable the `StrictHostKeyChecking` option, I encourage you to check the validity of the resulting host key with the server's administrator (ideally, offline).

## In Sum

This chapter introduced the concept of virtual private networking and the increasingly prevalent role that this technology is going to play in your Linux network, especially if your company has several branch offices that need to be interconnected. The IPsec specification has been universally accepted as the leading candidate for implementing VPN endpoints, and the FreeS/WAN Linux implementation includes all the features necessary for you to roll it out as a production solution.

For remote access to protected internal resources, the PPTP protocol allows you to leverage a potentially large installed base of PPTP-compliant Windows remote users. This is a tremendous advantage over VPN technologies that would force you to roll out a proprietary client. Although Windows 2000 now ships with IPsec capabilities, the older Windows versions (95, 98, and NT) lack an established IPsec client. The PopTop Linux PPTP package is now in version 1.1 and offers a good alternative to a Windows NT or 2000-based PPTP server.

Secure Shell (SSH) is an essential addition to your Linux server, especially if you need to log on interactively using password authentication. Although SSH encrypts the username/password exchange, using RSA authentication further ensures that you do not expose password information on the wire.

The next chapter wraps up this book by visiting the issue of strong authentication using secret key technology, one-time passwords, and how Linux can provide seamless support for heterogeneous authentication mechanisms.

# Strong User Authentication

A significant number of security breaches are due to the theft of authentication credentials (passwords or other secret keys) via both eavesdropping and brute-force guessing attacks. This chapter addresses both of these concerns by introducing two strong authentication facilities: the Kerberos secret-key authentication system and the S/Key one-time password system.

By definition, strong authentication differs from conventional username/password authentication in the types of credentials used and in the exposure of these credentials. The Kerberos system enhances the security of your Linux server by eliminating the exchange of passwords in the clear. Kerberos users obtain encrypted tickets locally and use the ticket to authenticate themselves to other network resources. This eliminates the need to provide cleartext passwords every time a network service is requested. The S/Key system still relies on regular username/password exchanges but it uses a different password with every access request, thereby eliminating the risk of eavesdropping.

In addition, this chapter introduces the Pluggable Authentication Modules (PAM) facility. PAM is a framework for providing a single point of configuration where system and security administrators can request authentication mechanisms from all network applications running on the Linux server.

Let’s get started by taking a closer look at the Kerberos authentication system.

## Kerberos

Originally designed by R.M. Needham and M.D. Schroeder at MIT, Kerberos gets its name from the three-headed dog that, according to Greek mythology, guarded the entrance to the underworld. In real life, Kerberos is a service based on secret keys that is used for strong authentication of users and services. Instead of providing separate authentication credentials to each server on your network, Kerberos allows users to request their credentials once in the form of a Kerberos *ticket* and then use this ticket to authenticate themselves to any Kerberos-enabled server on your network. Both users and servers rely on a central Key Distribution Center (KDC) to obtain and authenticate tickets.

The main advantage of Kerberos over standard username/password authentication is that passwords are never exposed on the network. This is accomplished using shared keys between Kerberos participants (including humans, servers, and the Kerberos central authority). Before authentication credentials are exchanged, they are always encrypted to ensure their privacy.

Figure 13.1 gives you an idea of what’s available on the Kerberos home page at `http://web.mit.edu/kerberos/www/`.

**Figure 13.1** Kerberos home page

![](img/3258bbaf790525f8c4eb25fabff7844a_398_0.png)

Kerberos, like many technical systems, has its own language for describing its components and functions. Before digging into the operation of the Kerberos protocol, let’s define some key terminology that will be used throughout this chapter:

**Principal** A *principal* is a user or server program (service) that will be using Kerberos authentication.

**Key Distribution Center (KDC)** The KDC is a physically secure server that contains a database that includes all principals in the system as well as their master keys.

**Master Key** The *master key* is a secret key that is shared between the KDC and each principal in the system.

**Credentials** *Credentials* are encrypted authentication evidence presented by a principal to a service or to the KDC for authentication.

**Ticket** A *ticket* is a special type of credential that allows a principal to log on to a specific service.

**Ticket-Granting Ticket** A *ticket-granting ticket* (*TGT*) is a special type of credential used by a service on behalf of a user to request a service-specific ticket (e.g., to log on to a given server).

**Realm** A *realm* is a set of Kerberos principals, servers, services, and KDCs under a common administrative domain. (A realm is similar in concept to a DNS domain.)

The Linux Kerberos system consist of three parts:

**Key Distribution Center** The KDC is the centerpiece of the Kerberos authentication. As described earlier in this section, it contains the database of all Kerberos participants (principals). The KDC is typically also used to host the administration daemon (*kadm*) that allows authorized principals to manage the Kerberos database remotely using Kerberos authentication.

**Kerberized Services** Kerberized services are direct replacements for popular Linux server daemons such as Telnet, FTP, remote login, and remote shell. Kerberized services have been modified to use Kerberos authentication, but they provide all the other functionality that you are used to.

**Kerberized Clients** Kerberized clients are the companion clients to the Kerberized services described in the previous paragraph. They too are equivalent in functionality to the traditional Telnet, FTP, and remote login clients and can be used to connect to non-Kerberized services.
