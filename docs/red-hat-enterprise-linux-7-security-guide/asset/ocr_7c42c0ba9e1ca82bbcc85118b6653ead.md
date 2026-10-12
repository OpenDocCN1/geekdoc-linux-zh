![](bbox=[0.19, 0.07, 0.25, 0.12])

# WARNING

Always use certificates signed by a Certificate Authority for servers running in a production environment. Self-signed certificates are only appropriate for testing purposes or private networks.

See *Section 4.7.2.1, “Creating a Certificate Signing Request”* for more information about certificates granted by a Certificate Authority. On the other hand, to create a self-signed certificate for stunnel, enter the `/etc/pki/tls/certs/` directory and type the following command as *root*:

```
certs]# make stunnel.pem
```

Answer all of the questions to complete the process.

+   2. When you have a certificate, create a configuration file for stunnel. It is a text file in which every line specifies an option or the beginning of a service definition. You can also keep comments and empty lines in the file to improve its legibility, where comments start with a semicolon.

The stunnel RPM package contains the `/etc/stunnel/` directory, in which you can store the configuration file. Although stunnel does not require any special format of the file name or its extension, use `/etc/stunnel/stunnel.conf`. The following content configures *stunnel* as a TLS wrapper:

```
cert = /etc/pki/tls/certs/stunnel.pem
; Allow only TLS, thus avoiding SSL
sslVersion = TLSv1
chroot = /var/run/stunnel
setuid = nobody
setgid = nobody
pid = /stunnel.pid
socket = l:TCP_NODELAY=1
socket = r:TCP_NODELAY=1

[service_name]
accept = port
connect = port
TIMEOUTclose = 0
```

Alternatively, you can avoid SSL by replacing the line containing `sslVersion = TLSv1` with the following lines:

```
options = NO_SSLv2
options = NO_SSLv3
```

The purpose of the options is as follows:

+   - cert – the path to your certificate