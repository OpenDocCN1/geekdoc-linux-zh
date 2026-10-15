
## Samba: Sharing Files with DOS, Windows, and OS/2

1. Type this command to create an /etc/smbpasswd file with entries for each user, but invalid passwords:
   
   ```cat /etc/smbpasswd ; mkpasswd.sh > /etc/smbpasswd```
   
2. Edit the resulting /etc/smbpasswd file to remove accounts that won't be using Samba services. Such accounts include an assortment of accounts Linux uses internally, such as ftp and gopher.
   
3. For each user, issue the smbpasswd command to change the password. (Note that smbpasswd is both the name of a command and the name of a Samba password file.) For instance, typing smbpasswd larry results in a prompt for a new password for user larry.

If you have a large number of users and don't want to call them in to enter their passwords or assign passwords yourself, you can use cleartext passwords and migrate to encrypted passwords. Instead of performing step 3, configure Samba to use cleartext passwords and add the option update encrypted = yes to the /etc/smb.conf file. As users log on and use Samba shares, Samba will run smbpasswd itself, using the verified cleartext password to set the encrypted password value. After a while, you can change /etc/smb.conf to use encrypt passwords = yes and update encrypted = no. One caveat is that this procedure assumes that the clients can handle both encrypted and cleartext passwords. Recent versions of Windows insist on using encrypted passwords only, which can make this procedure more difficult.

To change Windows password in Red Hat 6.0, you can find the Winver_PlainPassword.reg file, where Winver is your version of Windows. You might find these files in some other directory if you're using a different distribution of Linux. Copy the appropriate file to your Windows computer and double-click on it. Windows should incorporate the change into the Registry, thus enabling cleartext passwords.

Another password-related issue is case SMB/CIFS servers generally use case-insensitive or all-uppercase passwords, but Linux uses case-sensitive passwords. To cope with this problem, Samba converts passwords to lowercase (because most users have mostly lowercase passwords). If no match is found, Samba can convert individual letters to uppercase, trying to find a match. Samba tries all possible permutations of upper- and lowercase letters, up to the number of uppercase letters specified by the password level option. Increasing this level can slow down logins, but may be necessary if your users have uppercase or mixed-case passwords. Similar comments apply to usernames, and there's a username level option that works the same way as password level.

## Limiting Samba Access

If your Linux server is accessible from the Internet, or even from computers in your organization that shouldn’t have access to your Samba shares, you might want to limit access on a machine-by-machine basis. You do this with the hosts allow and hosts deny options. The syntax for these options is very similar, but hosts allow lists machines from which access is permitted, whereas hosts deny lists computers that should not have access. In general, you use hosts allow when you want to provide Samba services to only a handful of computers, and you use hosts deny when you want to exclude known “troublemakers” or machines that belong to some less-trusted computers, such as public workstations.

You can specify machines for hosts allow and hosts deny in the following ways:

- As an Internet machine name—This generally means an FQDN, such as n400.erpLab.pangaea.edu. If your system is on the same network as the target, you might be able to give only the machine name, as in n400.
- As an IP address—A full IP address in dotted quad notation, such as 192.168.1.5.
- As a partial IP address—If you enter fewer than 4 bytes of the IP address and leave a period, Samba interprets this to mean all addresses in the network specified. For instance, 192.168.1. refers to all computers (up to 254 of them) in the 192.168.1.0 network.
- As an IP address/subnet mask pair—You can specify an IP address and subnet mask to specify a range of computers. For instance, 192.168.1.32/255.255.255.224 refers to hosts ranging from 192.168.1.32 through 192.168.1.63.
- Using except—You can exclude a machine or subnetwork from the rule by preceding its name with the keyword except. For instance, 192.168.1. except 192.168.1.23 allows or denies all computers in the 192.168.1.x network except for 192.168.1.23.

You can mix and match these methods by listing separate addresses or ranges separated by spaces. For instance, here’s a sample hosts allow line:

```
hosts allow = teela 192.168.1. 192.168.3.2
```

If you have so many hosts that they exceed one line’s length, you can place a backslash (\ ) at the end of one line to continue the list on another. This technique works with other /etc/smb.conf options, too.

### Tip

You can use the hosts allow and hosts deny options in individual shares, as well as use them in the [global] section of /etc/smb.conf.
