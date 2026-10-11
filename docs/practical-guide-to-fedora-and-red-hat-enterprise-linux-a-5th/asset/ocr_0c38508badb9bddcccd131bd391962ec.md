Assuming the global parameters in **smb.conf** are set properly, you need to add a share for a **Windows** system to be able to access a directory on the local **Linux** system. Add the following simple share to the end of the **smb.conf** file to enable a user on a **Windows** system to be able to read from and write to the local `/tmp` directory:

```
[tmp]  
    comment = temporary directory  
    path = /tmp  
    writable = yes  
    guest ok = yes
```

The name of the share under **Windows** is **tmp**; the path under **Linux** is `/tmp`. Any **Windows** user, including **guest**, who can log in on **Samba**, can read from and write to this directory, assuming that the user's **Linux** permissions allow it. The **Linux** permissions that apply to a **Windows** user using **Samba** are the permissions that apply to the **Linux** user that the **Windows** user maps to.

# PARAMETERS IN THE **smbd.conf** FILE

The `smb.conf` man page and the **Help** feature of **swat** list all the parameters you can set in `smb.conf`. The following sections identify some of the parameters you are likely to want to change.

# GLOBAL PARAMETERS

+   interfaces A **SPACE**-separated list of the networks that **Samba** uses. Specify as interface names (such as `eth0`) or as **IP** address/net mask pairs (page 443).

Default: all active interfaces except 127.0.0.1

+   server string The string that is displayed in various places on the **Windows** machine. Within the string, **Samba** replaces `%v` with the **Samba** version number and `%h` with the hostname.

Default: **Samba** %v  
Fedora/RHEL: **Samba** Server

+   workgroup The workgroup that the server belongs to. Set to the same workgroup as the **Windows** clients that use the server. This parameter controls the domain name that **Samba** uses when `security` (page 762) is set to **DOMAIN**.

Default: **WORKGROUP**  
Fedora/RHEL: **MYGROUP**

# SECURITY PARAMETERS

+   encrypt passwords YES accepts only encrypted passwords from clients. **Windows** 98 and **Windows** NT 4.0 **Service** Pack 3 and later use encrypted passwords by default. This parameter uses **smbpasswd** to authenticate passwords unless you set `security` to **SERVER** or **DOMAIN**, in which case **Samba** authenticates using another server.

Default: **YES**