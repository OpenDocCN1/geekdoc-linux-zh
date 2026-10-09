
After you have reloaded the LIDS configuration (by using the `/sbin/lidsadm -S - + RELOAD_CONF` command) or rebooted the system and sealed the kernel (by using the `/sbin/lidsadm -i` command in the `/etc/rc.d/rc.local` script), you (as root) will not be able to kill the init children. This ensures that even if your system is compromised and an intruder gains root privileges, the intruder cannot kill the daemons and replace them with Trojan versions.

## Hiding processes from everyone

By default, the `CAP_HIDDEN` capability is turned on in the `/etc/lids/lids.cap` configuration file. You can hide a process from everyone by using the following command:

```
lidsadm -A -s /path/to/binary -t -o CAP_HIDDEN -j INHERIT
```

where `/path/to/binary` is the fully qualified path to the executable that you want to hide when running. For example, to hide the Apache server process `/usr/local/apache/bin/httpd` when running, simply run the following command:

```
lidsadm -A -s /usr/local/apache/bin/httpd -t -o CAP_HIDDEN -j INHERIT
```

This labels the process as hidden in the kernel and it cannot be found using any user-land tools such as `ps` or `top`, or even exploring files in the `/proc` file system.

## Disabling raw device access by processes

Normally, only special processes need access to raw devices. So it is a good idea to disable accesses to raw devices and to enable access to them as needed, which conforms to the overall security concept of “close all, open only what you need.”

The raw device access is controlled with the `CAP_SYS_RAWIO` capability, which is disabled by default in `/etc/lids/lids.cap` configuration file. If it was enabled, processes could access `/dev/mem`, `/dev/port`, `/dev/mem`, `/dev/kmem`, and other raw block devices. For example, when this capability is off (as in default) the `/sbin/lilo` program cannot function properly because it needs raw device-level access to the hard drive.

But some special programs, such as `XF86_SVGA`, might want this capability to run properly. In this case, you can add the program to the exception list as follows:

```
lidsadm -A -s /usr/X11R6/bin/XF86_SVGA -t -o CAP_SYS_RAWIO -j INHERIT
```

### Disabling network administration tasks

By default, the `CAP_NET_ADMIN` capability is turned off, which means that a network administrator (typically the root user) can no longer perform the following network administration tasks:

- Configuring the Ethernet interface
- Administering IP firewall, masquerading, and accounting
- Setting debug option on sockets
- Modifying routing tables
- Setting arbitrary process/process group ownership on sockets
- Binding to any address for transparent proxying
- Setting Type of Service (TOS)
- Setting promiscuous mode
- Clearing driver statistics
- Multicasting
- Setting the read/write of device-specific registers

The default setting is highly recommended. If you do need to perform one of the above tasks, simply turn off LIDS temporarily with the `/sbin/lidsadm -S -- -LIDS` command.

### Protecting the Linux immutable flag for files

The ext2 file system has an extended feature that enables you to flag a file as immutable. This is done with the `chattr` command. For example, the `chattr +i /path/to/myfile` turns `/path/to/myfile` into an immutable file. A file with the immutable attribute cannot be modified or deleted or renamed, nor can it be symbolically linked. However the root user is able to change the flag by using the `chattr -i /path/to/myfile` command. You can protect immutable files even from the superuser (root) by disabling the `CAP_LINUX_IMMUTABLE` capability. Note that the `CAP_LINUX_IMMUTABLE` is disabled by default in `/etc/lids/lids.cap`.

### Detecting scanners

If you have enabled the built-in port scanner during kernel compilation as recommended in the LIDS installation section discussed earlier, you can detect port scanners. This scanner can detect half-open scan, SYN stealth port scan, Stealth FIN, Xmas, or Null scan, among others. Tools such as `nmap` and Satan or Scan can be detected by the detector. It is useful when raw socket (`CAP_NET_RAW`) is disabled.

> **Note**
> When `CAP_NET_RAW` is turned off some user-land scanners based on sniffing will not work properly. But the kernel-based scanner provided by LIDS does not use any socket, which makes it more secure. You might want to consider using the LIDS supplied scanner.

## Responding to an intruder

When LIDS detect a violation of any of the ACL rules, it can respond to the action by following method.

- **Logging the message.** When someone violates an ACL rule, LIDS will log a message using the kernel log daemon (klogd).
- **Sending e-mail to the appropriate authority.** LIDS can send e-mail when a violation occurs. This feature is controlled by the `/etc/lids/lids.net` file, which is discussed in Step 5 of the “Compiling, installing, and configuring LIDS” section earlier in this chapter.
- **Hanging up the console.** If you enabled this option during kernel patching for LIDS as discussed in Step 9 in the LIDS installation section, the console will be dropped when a user violates a ACL rule.

Another similar system to LIDS is the OpenWall project (www.openwall.com/linux). The OpenWall project contains some security features that are different from those found in LIDS, and one particular OpenWall patch makes the stack area of a process nonexecutable. You should take a look at this work-in-progress project.

# HTTP 1.1 Status Codes

For each request from a Web client, the Web server must return to the client an HTTP status code, which consists of a three-digit number. A Web client can attempt to understand the server’s response by looking at this status code, sent in the HTTP Status-Line header. The code is accompanied by a short phrase, called a *reason phrase*, which is intended to provide a brief explanation for the user. For example, an HTTP Status-Line header might look like this:

```
HTTP/1.1 404 Not Found
```

Here, **404** is the status code and **Not Found** is the reason phrase. On a typical Web client, a Web browser will display the Not Found phrase in the browser window. Five different classes of status codes are available from the latest HTTP 1.1 specifications; these classes are discussed in the following sections.

## Informational Status Codes (100–199)

The purpose of this type of status code is to let the client know that the server is in the process of fulfilling a request. These status codes are only informational; the client does not have to act on any of them. Note that HTTP 1.0 does not define 1xx status codes, so 1xx status codes must not be sent to HTTP 1.0 clients. The currently defined 1xx status codes are:

- **100 Continue** — The server sends this code to let the client know it is ready to receive the rest of the request.
- **101 Switching Protocol** — The server sends this code when it is willing to switch the application protocol to one specified in an Upgrade request header provided by the client. Switching should take place only if the new protocol provides an advantage over the existing one. For example, the client may request that the server use a newer HTTP protocol than what it is currently using. In such a case, the server should switch if possible.

## Client Request Successful (200–299)

A returned status code in the range 200–299 indicates that the client's request was successfully received and accepted. The currently defined 2xx status codes are:

- **200 OK** — The server succeeded in processing the request, and the requested document is attached.
- **201 Created** — The server successfully created a new URL, specified in a Location header.
- **202 Accepted** — The request was accepted for processing, but the server has not yet completed processing it.
- **203 Non-Authoritative Information** — The metainformation in the response header did not originate with the server; it was copied from another server.
- **204 No Content** — The request is complete, but no new information needs to be sent back. The client should continue to display the current document.
- **205 Reset Content** — The client should reset the current document. This is useful when an HTML form needs to be reset to clear all existing values of input fields.
- **206 Partial Content** — The server has fulfilled the partial GET request for the resource. This code is used to respond to Range requests. The server sends a Content-Range header to indicate which data segment is attached.

## Request Redirected (300–399)

Status codes in the range 300–399 are sent to a client to let it know it needs to perform further action to complete the request. The currently defined 3xx status codes are:

- **300 Multiple Choices** — The requested resource corresponds to a set of documents. The server can send information about each document with its own specific location and content negotiation information so that the client can choose one.
- **301 Moved Permanently** — The requested resource does not exist on the server. A Location header is sent to redirect the client to the new URL. The client directs all future requests to the new URL.
