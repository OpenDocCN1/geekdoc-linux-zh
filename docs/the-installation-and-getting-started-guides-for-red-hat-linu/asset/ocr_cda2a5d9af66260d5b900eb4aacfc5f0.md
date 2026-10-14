# Appendix C: Package List

# rwho — (Version 0.10, 25K)

[W][S]

The rwho command displays output similar to the output of the who command (it shows who is logged in) for all machines on the local network running the rwho daemon. Install the rwho command if you need to keep track of the users who are logged in to your local network.

# samba — (Version 2.0.3, 6,498K)

[S]

Samba provides an SMB server which can be used to provide network services to SMB (sometimes called "Lan Manager") clients, including various versions of MS Windows, OS/2, and other Linux machines. Samba also provides some SMB clients, which complement the built-in SMB filesystem in Linux. Samba uses NetBIOS over TCP/IP (NetBT) protocols and does NOT need NetBEUI (Microsoft Raw NetBIOS frame) protocol. Samba-2 features an almost working NT Domain Control capability and includes the new SWAT (Samba Web Administration Tool) that allows samba's smb.conf file to be remotely managed using your favourite web browser. For the time being this is being enabled on TCP port 901 via inetd. Please refer to the WHATSNEW.txt document for fixup information. This binary release includes encrypted password support. Please read the smb.conf file and ENCRYPTION.txt in the docs directory for implementation details. NOTE: Red Hat Linux 5.X Uses PAM which has integrated support for Shadow passwords. Do NOT recompile with the SHADOW_PWD option enabled. Red Hat Linux has built in support for quotas in PAM.

# sendmail — (Version 8.9.3, 526K)

[B]

The Sendmail program is a very widely used Mail Transport Agent (MTA). MTAs send mail from one machine to another. Sendmail is not a client program, which you use to read your email. Sendmail is a behind-the-scenes program which actually moves your email over networks or the Internet to where you want it to go. If you ever need to reconfigure Sendmail, you'll also need to have the sendmail.cf package installed. If you need documentation on Sendmail, you can install the sendmail-doc package.

# sendmail-cf — (Version 8.9.3, 503K)