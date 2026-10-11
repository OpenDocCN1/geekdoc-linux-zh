
**NOTE** If your remote SMB server is a Windows NT server, domain mode access control is always preferable to server mode because server mode consumes a license on the Windows NT server for the duration of the client-server connection. Domain mode authentication, on the other hand, releases the connection (and the Windows NT license instance) as soon as the authentication is performed. This is important because Microsoft's licensing strategy revolves around concurrent server connections.

## Other Access Control Features

In addition to these four access control methods, you may choose to take advantage of a trust relationship between your local NT domain and a second, trusted NT domain. As of Samba 2.0.4, the `smb.conf` directive `allow trusted domain = yes` can be used to gain authentication from an NT domain controller that, although it is not primary to your domain, is trusted by your PDC.

Another recent addition to the access control feature set of Samba is the `add user script` directive. This can be used in both `user` and `domain` access control modes to automatically add a user in the event that the user/password is authenticated by the password server but the user is not present locally. For example, you may want Samba to automatically add a user locally using the following `smb.conf` directive:

```text
add user script = sudo /usr/sbin/useradd %u
```

Conversely, a `delete user script` directive can be specified to delete a user that exists locally but is no longer valid on the PDC. An example of this usage is as follows:

```text
delete user script = sudo /usr/sbin/userdel %u
```

While adding and deleting local users in this fashion may be convenient, I urge you to implement it carefully because you are allowing the unattended creation and deletion of users in the same `/etc/passwd` or `/etc/shadow` files that you use for regular Linux server authentication.

## The [homes] Directive

A common approach to allowing all Linux server users access to their home directories is the special `[homes]` directive in the `smb.conf` file. Consider the following example:

```text
[homes]
comment = Home Directories
browseable = no
writable = yes
```

This directive specifies that any user in `/etc/passwd` can gain access to their home directory by pointing their SMB client to `\\server\\username`. This is not always desirable because this file includes system-related accounts such as root, operator, uucp, and bin. To ensure that these users are not granted access, use the `invalid users` directive to exclude these usernames, as in the following example:

```text
[global]
   invalid users = root, operator, uucp, bin
```

### Privacy of Samba Communications

Samba uses the TCP/IP layer to carry NetBIOS traffic from client to server. This allows you to share drives over the Internet, a convenient but often insecure practice because the contents of your files are exposed to potential eavesdroppers. If you are going to be exchanging SMB traffic over a public (untrusted) network like the Internet, your security policy needs to include a provision to ensure the privacy and authentication of this type of traffic.

There is a way to secure the contents of the SMB traffic by using the ever-popular OpenSSL implementation you used to tunnel SWAT traffic that was described in the previous section. Since Windows SMB clients don't support SSL directly, you have to set up a proxying SSL station at the edge of your local (trusted) network, which encrypts traffic and forwards it to the destination SSL-enabled Samba server on the client's behalf. This process is illustrated in Figure 8.5.

**Figure 8.5** Using SSL protection with Samba

![](img/3258bbaf790525f8c4eb25fabff7844a_248_0.png)

The figure shows two corporate sites (Site A and Site B) connected to the Internet by an access router. Behind Site A's access router, a Linux server has been set up as an SSL proxy. A typical Windows SMB client in Site A's LAN directs its SMB request to the local SSL proxy, which then relays the connection to Site B's Samba server inside an OpenSSL tunnel. While Site B's server also replies with an encrypted response, Site A's SSL proxy relays it in the clear back to the Windows client. This ensures that the SMB traffic is protected, at least while traveling over the public Internet. Be aware, however, that the SMB traffic travels in the clear within Site A's local network.

**Creating a Certificate Authority for Samba-SSL** The first step in setting up any SSL application is to create a certificate authority (CA) to issue the necessary digital certificates for the mutual authentication of the two endpoints. Start by making sure that OpenSSL is installed on your system:

```text
[ramon]$ rpm -q openssl
openssl-0.9.5a-14
```

Then you need to create a new directory for the CA using the following commands. Start by creating the directory that will hold Samba's CA:

```text
[ramon]$ sudo mkdir /etc/samba/CA
[ramon]$ cd /etc/samba/CA
```

Each certificate issued by this CA will carry a serial number. By adding the text "01" to the file `/etc/samba/CA/serial`, you are seeding the file that the CA will use for assigning serial numbers:

```text
[ramon]$ sudo echo "01" > serial
```

The `index.txt` file is used by the CA to maintain the database of certificates and must simply be created empty:

```text
[ramon]$ sudo cp /dev/null index.txt
```

Next, you need to create an appropriate OpenSSL configuration file that will suit your needs. Start by copying the original `/usr/share/ssl/openssl.cnf` file to the `/etc/samba/CA` directory:

```text
[ramon]$ sudo cp /usr/share/ssl/openssl.cnf openssl.cnf
```

Now edit the newly created `openssl.cnf` file to include these new settings:

```text
dir             = /etc/samba/CA                  # Where everything is kept
new_certs_dir   = $dir                            # default place for new certs.
certificate     = $dir/ca-cert.pem                # The CA certificate
private_key     = $dir/ca-key.pem                 # The private key
```

Note that you're simply changing the default base CA directory to be the one you created for Samba previously (`/etc/samba/CA`). You're also defining the CA's certificate and key to reside in `/etc/samba/CA/ca-cert.pem` and `/etc/samba/CA/ca-key.pem`, respectively.

![](img/3258bbaf790525f8c4eb25fabff7844a_249_0.png)

![](img/3258bbaf790525f8c4eb25fabff7844a_249_1.png)

Next, issue an `openssl` command to generate the CA’s private key (`ca-key.pem`) and its X.509 certificate (`ca-cert.pem`):

```bash
[ramon]$ sudo openssl req -new -x509 -keyout ca-key.pem -out ca-cert.pem -days 365 -config openssl.cnf
```

Now you’re ready to create a new certificate for the Samba server itself and sign it with the CA’s secret key. Enter the following commands:

```bash
[ramon]$ sudo openssl req -nodes -new -x509 -keyout server-key.pem -out newreq.pem -days 365 -config openssl.cnf
[ramon]$ sudo openssl x509 -x509toreq -in newreq.pem -signkey server-key.pem -out tmp.pem
[ramon]$ sudo openssl ca -config openssl.cnf -policy policy_anything -out server-cert.pem -infiles tmp.pem
```

The first command creates a private key for the Samba server (`server-key.pem`) and a certificate-signing request (`newreq.pem`). The second and third commands take the certificate-signing request and use the CA’s private key to sign the certificate. The resulting Samba certificate file is saved as the file `server-cert.pem`.

You also need to create a certificate for the client (the SSL proxy) because both the client and the server will need to authenticate each other. Create this certificate using the following commands:

```bash
[ramon]$ sudo openssl req -nodes -new -x509 -keyout proxy-key.pem -out newreq.pem -days 365 -config openssl.cnf
[ramon]$ sudo openssl x509 -x509toreq -in newreq.pem -signkey proxy-key.pem -out tmp.pem
[ramon]$ sudo openssl ca -config openssl.cnf -policy policy_anything -out proxy-cert.pem -infiles tmp.pem
```

You now have client and server certificates called `proxy-cert.pem` and `server-cert.pem` respectively, as well as corresponding private key files `proxy-key.pem` and `server-key.pem`. Note that you need to copy the `proxy-cert.pem` and `proxy-key.pem` files to the proxy machine. You’ll learn more about the placement of these files in the section “Downloading and Installing SSL Proxy” later in this chapter.

Congratulations! You have now completed the OpenSSL configuration necessary to tunnel SMB requests over SSL. Next, you need to inform Samba of the existence of this configuration, by entering the appropriate directives in the `/etc/samba/smb.conf` file. This is the topic of the next section.

**Configuring Samba for SSL support** Table 8.1 lists the syntax of the directives necessary to make Samba SSL-aware, along with their meaning.
