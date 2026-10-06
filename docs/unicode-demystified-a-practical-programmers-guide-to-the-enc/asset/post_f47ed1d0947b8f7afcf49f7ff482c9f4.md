
# Configuring Network Services

do not click any of the Set Default buttons. Make sure to click Commit after you finishing your changes in a window before you click a button at the top of the window; otherwise, swat will not keep your changes.

First, click GLOBALS at the top of the Samba/swat home page (Figure 17-11). Leave everything at its default setting except as indicated in Table 17-16.

## Changes to Samba GLOBALS || table 17-16

| Base Options | |
|---|---|
| workgroup | Change to the name of your workgroup on the MS Windows system. |
| Security Options | hosts allow | Enter the hostname or IP address of the MS Windows machine. |

Click Commit Changes when you are done with the GLOBALS window.
A share (or window share) is a directory and its children that you share with another system using Samba. Next, click the SHARES button. Three buttons and two text boxes appear. In the box adjacent to the Create Share button, enter the name you want to assign to this share. This name can be anything you want; it does not specify the directory that you are sharing. Click Create Share. When you want to modify an existing share, bring up the name of the share in the combo box, and click Share. Either of these actions displays the complete Share Parameters window. Leave everything at its default setting except as indicated in Table 17-17.

## Changes to Samba Shares || table 17-17

| Base Options | |
|---|---|
| comment | An optional comment about the purpose of this share and its location on the GNU/Linux system can be helpful. |
| path | Change this to the absolute pathname of the share (directory) on the GNU/Linux system. |
| Security Options | hosts allow | Put the hostname or IP address of the MS Windows system. |

Click Commit Changes when you are done with the SHARES window. If you want to see how many options there are really, click Advanced View.

When everything is set up correctly, you should be able to open an explorer window on the Windows machine, click Tools on the menubar, and select Map Network, which opens the Map Network drive. Select an unused drive letter from the Drive combo box, and enter the (MS Windows) path to share you created. When you want to share /home/jenny on the machine named bravo and have named the share bookkeeping (in sweat), swat \bravo\bookkeeping in the Folder box and click Finish. Assuming you choose the drive letter J, you should be able to access the /home/jenny directory located on bravo as J (bookkeeping) on the MS Windows machine.

A lot of help is available from the local.swat/Samba home page (Figure 17-11) in addition to local documentation, there is the Diagnostic Utilities section, which lists useful utilities: smstatus displays a report on Samba connections, testcharm checks the /etc/samba/smb.conf file and displays its contents (only a check for initial correctness, not for service availability or correct/expected operation), and testprn checks the validity of the name of a printer. When you click the word Samba, swat displays the Samba man page, which defines each Samba program.

# DHCP Client

DHCP (Dynamic Host Configuration Protocol) dynamically allocates IP addresses to computers on a LAN. The administrator of the DHCP server provides a pool of IP addresses, and each client computer on the LAN has TCP/IP software configured to request an IP address from the DHCP server.

When you are not assigned a specific IP address, your provider uses DHCP to assign a temporary IP address to your machine each you establish a connection with your provider. The address remains the same as long as your machine is connected to the provider, but the address can be different each time you connect.

The client daemon, dhcpcd, communicates with the server daemon, dhcpd, to obtain the IP address, network, broadcast address, and so on, that it should use. DHCP is broadcast based, so the client and server must be on the same subnet (page 1495). To use DHCP as a client, start the dhcpcd daemon with redhat-config-services: Configures Services II on page 946 or chconfig: Configures Services III on page 947. For more information refer to “Static versus Dynamic IP addresses” on page 363. Under IPv4, autoconfiguration is optional and provided by DHCP. With IPv6, autoconfiguration is mandatory, making it easy for hosts to configure their IP addresses automatically (page 39).

# OpenSSH: Provides Secure Network Tools

| character-based | ssh |
| --- | --- |
| home | www.openssh.com |
| help | www.openssh.com/portable.html |
| security | securityfocus.com (mailing list) |
| newsgroup | news.security.com |

OpenSSH is a free version of the SSH protocol and is the basis for many secure network tools. Whereas telnet and login send all communications, as cleartext, OpenSSH performs the same functions while encrypting everything, that goes over the network. Its encryption eliminates eavesdropping, connection hijacking, and other attacks. OpenSSH also provide tunneling capabilities (page 375) and several methods of authentication. Both ssh (the client or one who logs on the server) and sshd (the server) are quite easy to set up. On the client side, give the command ssh when you have the same login name on both machines or ssh -l login name. The client machine must have permission to connect to the remote machine, and the user must present a valid password to the remote machine. In addition, the server must identify itself to the client to prevent person-in-the-middle attack (refer to footnote 3 on page 141). The easiest way to give a client access to a host is to put the client's host (and domain) names in the /etc/hosts file. The known_hosts file on the client machine contains electronic fingerprints of all the hosts you have connected to. We use this to identify a server. When you launch an ssh session, the client verifies the fingerprint and returns information stored in known_hosts. This process is normally transparent to you. However, the first time you attempt to connect to a server, your local machine cannot prove the identity of the server and displays a message as the following:

```
$ ssh -l alex kudos
The authenticity of host 'kudos (192.168.0.1)' can't be established. RSA key fingerprint is 4f:59:34:d0:92:47:84:5a:cd:60:cc:1c:19:60:aa:be. Are you sure you want to continue connecting (yes/no)?
Make sure that you are logging in the correct machine. When you are not sure, a phone call to someone who logs on that machine can locally help verify that you are the intended. When you answer, openSSH the server's fingerprint in ~/.ssh/known_hosts (ssh protocol with RSA [page 1491]) or ~/.ssh/known_hosts2 (ssh2 protocol with DSA [page 1465]) and associates it with the name of the machine that you are logging on. When you attempt to use one of the openSSH tools to communicate with this machine again, the key that the machine returns must match the one that your local machine has stored.

The following message tells you that the locally stored fingerprint does not match the one returned by the server:

```
$ ssh -l alex kudos
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack!)
It is also possible that the RSA host key has changed.
The fingerprint for the RSA key by the remote host is
ad96:5d:25:cc:f5:dc:0c:7d:d8:92:be:d0:db:82:
Please contact your system administrator.
Add correct host key in /home/alex/.ssh/known_hosts to get rid of this message.
Offending key in /home/alex/.ssh/known_hosts: 1
Host key for kudos has changed and you have requested strict checking.
```

Despite its frightening appearance, this message frequently means only that the fingerprint of the server has changed as the result of an openSSH or server upgrade. Again use the phone to verify the cause of the change. Assuming that it turn out to be innocuous, edit your ~/.ssh/known_hosts (or known_hosts2) file, find the line with the hostname of the server you are trying to connect with, delete that line, and run ssh again. Now you get the first message preceding; proceed as though this were your first connection with this server, and answer yes.

Refer to pages 374 and 1321 for more information on how to use ssh. Refer to pages 376 and 1308 for information on using sc.

# GnuPG: GNU Privacy Guard

| character-based | gpg |
| --- | --- |
| home | www.gnupg.org |
| help | www.gnupg.org/docs.html |

The GNU Privacy Handbook
Gnu Privacy Guard (GnuPG) Mini-HowTo
gpg info page
