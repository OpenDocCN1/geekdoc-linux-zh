
## DHCP Host Configuration

Run `ifconfig` on each system that requires a static IP address. Once you have determined the MAC address of each of these systems, you can add a host section to the `/etc/dhcp/dhcpd.conf` file for each system, instructing the DHCP server to assign a specific address to the system. The following host section assigns the address 192.168.1.1 to the system with the MAC address of BA:DF:00:DF:C0:FF:

```bash
$ cat /etc/dhcp/dhcpd.conf
…
host router {
  hardware ethernet BA:DF:00:DF:C0:FF;
  fixed-address 192.168.1.1;
  option host-name router;
}
```

The name following `host` is used internally by `dhcpd`. The name specified after `option host-name` is passed to the client and can be a hostname or an FQDN.

After making changes to `dhcpd.conf`, restart `dhcpd` using the `service` utility and the `dhcpd` init script (page 453).

## NSSWITCH.CONF: WHICH SERVICE TO LOOK AT FIRST

With the advent of NIS and DNS, finding user and system information was no longer a simple matter of searching a local file. Where once you looked in `/etc/passwd` to get user information and in `/etc/hosts` to find system address information, you can now use several methods to find this type of information. The `/etc/nsswitch.conf` (name service switch configuration) file specifies the methods to use and the order in which to use them when looking for a certain type of information. You can also specify what action the system takes based on whether a method works or fails.

- Each line in `nsswitch.conf` specifies how to search for a piece of information, such as a user's password. A line in `nsswitch.conf` has the following format:

```text
info: method [[action]] [method [[action]]…]
```

where `info` is the type of information that the line describes, `method` is the method used to find the information, and `action` is the response to the return status of the preceding method. The action is enclosed within square brackets.

### How nsswitch.conf Works

When called upon to supply information that `nsswitch.conf` describes, the system examines the line with the appropriate `info` field. It uses the methods specified on the line starting with the method on the left. By default, when it finds the desired information, the system stops searching. Without an action specification, when a method fails to return a result, the system tries the next method. It is possible for the search to end without finding the requested information.

### Information

The `nsswitch.conf` file commonly controls searches for users (in `passwd`), passwords (in `shadow`), host IP addresses, and group information. The following list describes most of the types of information (*info*) in the format discussed earlier that `nsswitch.conf` controls searches for:

- `autoumount`: Automount (`/etc/auto.master` and `/etc/auto.misc`; page 744)
- `bootparams`: Diskless and other booting options (See the *bootparam* man page.)
- `ethers`: MAC address (page 1092)
- `group`: Groups of users (`/etc/group`; page 472)
- `hosts`: System information (`/etc/hosts`; page 472)
- `netgroup`: Netgroup information (`/etc/netgroup`; page 474)
- `networks`: Network information (`/etc/networks`)
- `passwd`: User information (`/etc/passwd`; page 475)
- `protocols`: Protocol information (`/etc/protocols`; page 476)
- `publickey`: Used for NFS running in secure mode
- `rpc`: RPC names and numbers (`/etc/rpc`; page 477)
- `services`: Services information (`/etc/services`; page 477)
- `shadow`: Shadow password information (`/etc/shadow`; page 477)

### Methods

Following is a list of the types of information that `nsswitch.conf` controls searches for (*method*) in the syntax shown on page 455. For each type of information, you can specify one or more of the following methods:

- `files`: Searches local files such as `/etc/passwd` and `/etc/hosts`
- `nis`: Searches the NIS database; *nis* is an alias for *nis*
- `dns`: Queries the DNS (DNS queries only)
- `compat`: ± syntax in `passwd`, `group`, and `shadow` files (page 458)

> There are other, less commonly used methods. See the default `/etc/nsswitch.conf` file and the `nsswitch.conf` man page for more information. Although NIS+ belongs in this list, it is not implemented for Linux and is not discussed in this book.

### Search Order

The information provided by two or more methods may overlap: For example, `files` and `nis` may each provide password information for the same user. With overlapping information, you need to consider which method you want to be authoritative (take precedence) and then put that method at the left of the list of methods.

The default `nsswitch.conf` file lists methods without actions, assuming no overlap (which is normal). In this case, the order is not critical: When one method fails, the system goes to the next one; all that is lost is a little time. Order becomes critical when you use actions between methods or when overlapping entries differ.

The first of the following lines from `nsswitch.conf` causes the system to search for password information in `/etc/passwd` and, if that fails, to use NIS to find the information. If the user you are looking for is listed in both places, the information in the local file would be used—it would be authoritative. The second line uses NIS; if that fails, it searches `/etc/hosts`; if that fails, it checks with DNS to find host information.

```text
passwd    files nis
hosts     nis files dns
```

### Action Items

Each method can optionally be followed by an action item that specifies what to do if the method succeeds or fails for any of a number of reasons. An action item has the following format:

```text
[!/]STATUS=action]
```

where the opening and closing square brackets are part of the format and do not indicate that the contents are optional; `STATUS` (by convention uppercase although it is not case sensitive) is the status being tested for; and `action` is the action to be taken if `STATUS` matches the status returned by the preceding method. The leading exclamation point (!) is optional and negates the status.

**STATUS** values may have the following definitions:

- `NOTFOUND`: The method worked but the value being searched for was not found. Default action is *continue*.
- `SUCCESS`: The method worked and the value being searched for was found; no error was returned. Default action is *return*.
- `UNAVAIL`: The method failed because it is permanently unavailable. For example, the required file may not be accessible or the required server may be down. Default action is *continue*.
- `TRYAGAIN`: The method failed because it was temporarily unavailable. For example, a file may be locked or a server overloaded. Default action is *continue*.

**ACTION** values for *action* are as follows:

- `return`: Returns to the calling routine with or without a value.
- `continue`: Continues with the next method. Any returned value is overwritten by a value found by the next method.

**Example**

The following line from `nsswitch.conf` causes the system first to use DNS to search for the IP address of a given host. (The action item following the DNS method tests whether the status returned by the method is not (!) `UNAVAIL`.)

```text
hosts     dns [!UNAVAIL=return] files
```

The system takes the action associated with the `STATUS` (`return`) if the DNS method does not return `UNAVAIL` (!UNAVAIL)—that is, if DNS returns `SUCCESS`, `NOTFOUND`, or `TRYAGAIN`. As a consequence, the following method (`files`) is used only when the DNS server is unavailable: If the DNS server is not unavailable (read the two negatives as “is available”), the search returns the domain name or reports that the domain name was not found. The search uses the `files` method (check the local `/etc/hosts` file) only if the server is not available.

## COMPAT METHOD: ± IN PASSWD, GROUP, AND SHADOW FILES

You can put special codes in the `/etc/passwd`, `/etc/group`, and `/etc/shadow` files that cause the system, when you specify the `compat` method in `nsswitch.conf`, to combine and modify entries in the local files and the NIS maps. That is, a plus sign (+) at the beginning of a line in one of these files adds NIS information; a minus sign (−) removes information.

For example, to use these codes in the `passwd` file, specify `passwd: compat` in `nsswitch.conf`. The system then goes through the `passwd` file in order, adding or removing the appropriate NIS entries when it reaches each line that starts with a + or −.

Although you can put a plus sign at the end of the `passwd` file, specify `passwd: compat` in `nsswitch.conf` to search the local `passwd` file, and then go through the NIS map, it is more efficient to put `passwd: files nis` in `nsswitch.conf` and not modify the `passwd` file.

## PAM

PAM (actually Linux-PAM, or Linux Pluggable Authentication Modules) allows a system administrator to determine how applications use authentication (page 1070) to verify the identity of a user. PAM provides shared libraries of modules (located in `/lib/security`) that, when called by an application, authenticate a user. The term “Pluggable” in PAM's name refers to the ease with which you can add and remove modules from the authentication stack. The configuration files kept in the `/etc/pam.d` directory determine the method of authentication and contain a list (i.e., stack) of calls to the modules. PAM may also use other files, such as `/etc/passwd`, when necessary.

Instead of building the authentication code into each application, PAM provides shared libraries that keep the authentication code separate from the application code. The techniques of authenticating users stay the same from application to application. In this way, PAM enables a system administrator to change the authentication mechanism for a given application without ever touching the application.

PAM provides authentication for a variety of system-entry services (login, ftp, and so on). You can take advantage of PAM's ability to stack authentication modules to integrate system-entry services with different authentication mechanisms, such as RSA, DCE, Kerberos, and smartcards.
