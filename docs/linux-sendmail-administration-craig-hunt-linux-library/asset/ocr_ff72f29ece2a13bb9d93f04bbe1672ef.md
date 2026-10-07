you actually want to serve. Linux distributions use two different access control mechanisms: tcpd and xinetd. Both of these access control mechanisms are covered in the following sections.

# Limit Login Access

For security reasons, you want to limit login access to the server. Deleting telnet and rlogind file described in the previous section eliminates the basic remote login services. Eliminating all remote logins would provide an ideal level of security, but it is usually impractical. Many users want to read e-mail directly on the server, which requires a login account and password on the server. As the system administrator, you need to provide secure remote login and controlled access.

If a user requires only POP or IMAP access, create the user's account without a valid login shell. The username and password from the account will provide IMAP or POP access, yet the user will not be granted login access without a valid shell. /bin/false is commonly used as the shell for this type of account. For users who require only POP or IMAP, but it does not work if the user also requires login access. In those cases, you may need to provide secure login software.

The secure shell (ssh) program is the most secure remote login software available. It supports secure login and even X Windows access. Linux systems includes openssh, a version of ssh that does not use any patented cryptographic techniques. If secure shell is not provided with your Linux distribution, it is available on the network. Go to www.ssh.org for more information about secure shell and to download the latest source code.

POP and IMAP services can run inside a secure connection using stunnel. stunnel is a program that uses Sockets Layer (SSL) to encrypt their traffic for daemons that do not encrypt their traffic. When run over stunnel, pop is called and assigned TCP port 995, and IMAP is called imaps and assigned TCP port 993. For example, the following command added to the start-up of a Caldera system would run POP inside an SSL tunnel:

```
stunnel -d 995 -1 /usr/sbin/ipop3 - ipop3d
```

That same system could run pops inside stunnel from inetd using the following entry in inetd.conf file:

```
pops stream tcp nowait root /usr/sbin/stunnel -1 /usr/sbin/ipop3 -- ipop3d
```

Listing 12.1 shows the xinetd.conf entry for imaps on a Red Hat 7 system.