
## 4.3.7.2. Securing NFS Mount Options

The use of the mount command in the /etc/fstab file is explained in the Using the mount Command chapter of the Red Hat Enterprise Linux 7 Storage Administration Guide. From a security administration point of view it is worthwhile to note that the NFS mount options can also be specified in /etc/nfsmount.conf, which can be used to set custom default options.

### 4.3.7.2.1. Review the NFS Server

> **WARNING**
> Only export entire file systems. Exporting a subdirectory of a file system can be a security issue. It is possible in some cases for a client to “break out” of the exported part of the file system and get to unexported parts (see the section on subtree checking in the exports(5) man page).

Use the ro option to export the file system as read-only whenever possible to reduce the number of users able to write to the mounted file system. Only use the rw option when specifically required. See the man exports(5) page for more information. Allowing write access increases the risk from symlink attacks for example. This includes temporary directories such as /tmp and /usr/tmp.

Where directories must be mounted with the rw option avoid making them world-writable whenever possible to reduce risk. Exporting home directories is also viewed as a risk as some applications store passwords in clear text or weakly encrypted. This risk is being reduced as application code is reviewed and improved. Some users do not set passwords on their SSH keys so this too means home directories present a risk. Enforcing the use of passwords or using Kerberos would mitigate that risk.

Restrict exports only to clients that need access. Use the showmount -e command on an NFS server to review what the server is exporting. Do not export anything that is not specifically required.

Do not use the no_root_squash option and review existing installations to make sure it is not used. See Section 4.3.7.4, “Do Not Use the no_root_squash Option” for more information.

The secure option is the server-side export option used to restrict exports to “reserved” ports. By default, the server allows client communication only from “reserved” ports (ports numbered less than 1024), because traditionally clients have only allowed “trusted” code (such as in-kernel NFS clients) to use those ports. However, on many networks it is not difficult for anyone to become root on some client, so it is rarely safe for the server to assume that communication from a reserved port is privileged. Therefore the restriction to reserved ports is of limited value; it is better to rely on Kerberos, firewalls, and restriction of exports to particular clients.

Most clients still do use reserved ports when possible. However, reserved ports are a limited resource, so clients (especially those with a large number of NFS mounts) may choose to use higher-numbered ports as well. Linux clients may do this using the “noregport” mount option. If you want to allow this on an export, you may do so with the “insecure” export option.

It is good practice not to allow users to login to a server. While reviewing the above settings on an NFS server conduct a review of who and what can access the server.

### 4.3.7.2.2. Review the NFS Client

Use the nosuid option to disallow the use of a setuid program. The nosuid option disables the set-user-identifier or set-group-identifier bits. This prevents remote users from gaining higher privileges by running a setuid program. Use this option on the client and the server side.

The noexec option disables all executable files on the client. Use this to prevent users from inadvertently executing files placed in the file system being shared. The nosuid and noexec options are standard options for most, if not all, file systems.

Use the nodev option to prevent “device-files” from being processed as a hardware device by the client.

The resvport option is a client-side mount option and secure is the corresponding server-side export option (see explanation above). It restricts communication to a “reserved port”. The reserved or “well known” ports are reserved for privileged users and processes such as the root user. Setting this option causes the client to use a reserved source port to communicate with the server.

All versions of NFS now support mounting with Kerberos authentication. The mount option to enable this is: sec=krb5.

NFSv4 supports mounting with Kerberos using krb5i for integrity and krb5p for privacy protection. These are used when mounting with sec=krb5, but need to be configured on the NFS server. See the man page on exports (man 5 exports) for more information.

The NFS man page (man 5 nfs) has a “SECURITY CONSIDERATIONS” section which explains the security enhancements in NFSv4 and contains all the NFS specific mount options.

## 4.3.7.3. Beware of Syntax Errors

The NFS server determines which file systems to export and which hosts to export these directories to by consulting the /etc/exports file. Be careful not to add extraneous spaces when editing this file.

For instance, the following line in the /etc/exports file shares the directory /tmp/nfs/ to the host bob.example.com with read/write permissions.

```
/tmp/nfs/		bob.example.com(rw)
```

The following line in the /etc/exports file, on the other hand, shares the same directory to the host bob.example.com with read-only permissions and shares it to the world with read/write permissions due to a single space character after the host name.

```
/tmp/nfs/		bob.example.com (rw)
```

It is good practice to check any configured NFS shares by using the showmount command to verify what is being shared:

```
showmount -e <hostname>
```

## 4.3.7.4. Do Not Use the no_root_squash Option

By default, NFS shares change the root user to the nfsnobody user, an unprivileged user account. This changes the owner of all root-created files to nfsnobody, which prevents uploading of programs with the setuid bit set.

If no_root_squash is used, remote root users are able to change any file on the shared file system and leave applications infected by Trojans for other users to inadvertently execute.

## 4.3.7.5. NFS Firewall Configuration

NFSv4 is the default version of NFS for Red Hat Enterprise Linux 7 and it only requires port 2049 to be open for TCP. If using NFSv3 then four additional ports are required as explained below.

### Configuring Ports for NFSv3

The ports used for NFS are assigned dynamically by the rpcbind service, which might cause problems when creating firewall rules. To simplify this process, use the /etc/sysconfig/nfs file to specify which ports are to be used:

- MOUNTD_PORT – TCP and UDP port for mountd (rpc.mountd)
- STATD_PORT – TCP and UDP port for status (rpc.statd)

In Red Hat Enterprise Linux 7, set the TCP and UDP port for the NFS lock manager (nlockmgr) in the /etc/modprobe.d/lockd.conf file:

- nlm_tcpport – TCP port for nlockmgr (rpc.lockd)
- nlm_udpport – UDP port nlockmgr (rpc.lockd)

Port numbers specified must not be used by any other service. Configure your firewall to allow the port numbers specified, as well as TCP and UDP port 2049 (NFS). See /etc/modprobe.d/lockd.conf for descriptions of additional customizable NFS lock manager parameters.

Run the rpcinfo -p command on the NFS server to see which ports and RPC programs are being used.

## 4.3.7.6. Securing NFS with Red Hat Identity Management

Kerberos-aware NFS setup can be greatly simplified in an environment that is using Red Hat Identity Management, which is included in Red Hat Enterprise Linux.

See the [Red Hat Enterprise Linux 7 Linux Domain Identity, Authentication, and Policy Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/index) , in particular [Setting up a Kerberos-aware NFS Server](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/linux_domain_identity_authentication_and_policy_guide/setting-up-a-kerberos-aware-nfs-server) to learn how to secure NFS with Kerberos when using Red Hat Identity Management.

## 4.3.8. Securing HTTP Servers

### 4.3.8.1. Securing the Apache HTTP Server

The Apache HTTP Server is one of the most stable and secure services in Red Hat Enterprise Linux 7. A large number of options and techniques are available to secure the Apache HTTP Server – too numerous to delve into deeply here. The following section briefly explains good practices when running the Apache HTTP Server.

Always verify that any scripts running on the system work as intended before putting them into production. Also, ensure that only the root user has write permissions to any directory containing scripts or CGIs. To do this, enter the following commands as the root user:

```
chown root <directory_name>
```
