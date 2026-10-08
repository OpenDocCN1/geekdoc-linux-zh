# CHAPTER 6 | Every Service Is a Potential Risk

| TABLE 6-2 continued |
| SERVICE SCRIPT | DESCRIPTION | ACTION |
|---|---|---|
| saslauthd | Simple authentication and security layer service, used for some services such as sendmail. | |
| sendmail | An open source Simple Mail Transfer Protocol (SMTP) e-mail service. | Depends |
| smartd | Monitor for modern hard drives. | Enable |
| sshd | SSH server. | Enable |
| syslog | Log service. | Enable |
| wpa_supplicant | Wireless network access. | Disable |
| x11-common | Filesystem infrastructure for additional GUI software. | Disable |
| xinetd | Extended internet server. | Disable |
| ybind | Binding for NIS clients and servers. | Depends |
| yum-updatesd | Automatic updates. | |

If the service noted in Table 6-2 is to be disabled, look at the description. You may actually need the service; if so, be aware of the risks. If the rationale applies to your system, try to uninstall the first service. Unless the process also uninstalls something important, proceed with uninstalling the service. Otherwise, stop the service with the script in the /etc/init.d/ directory. Disable the service in all runlevels with the chconfig or update-rc command described earlier.

If you're having trouble identifying the name of the service, the rpm -q command can help. For example, on Red Hat systems, the following command identifies the bluez-utils package as the owner of the bluetooth service script in the /etc/init.d/ directory.

```
# rpm -qf /etc/init.d/bluetooth
```

The best-practice status of a few services is in dispute. For example, while the NSA suggests that the Hardware Abstraction Layer daemon be disabled, documentation from the Red Hat Magazine suggests otherwise. While many distributions are aggressively moving toward IPv6, the NSA suggests most administrators should avoid that network standard. In a similar fashion, while Red Hat recommends to keep the Kudos hardware-probing service active, the NSA disagrees.

Several services are related to NFS. If you do not have a reason to use NFS for sharing directories, you should disable NFS and related services, nfs, nfslock, rpcbind, rpcsvgssd, and rpcmbind.

> NOTE As of this writing, Red Enterprise Linux 6 suggests its beta release phase. Indications so far suggest that fewer services will be enabled by default this distribution release.