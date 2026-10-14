```
BOOT_SPLASH="yes"
```

Set no to turn off the splash screen on console 1 at boot (after kernel load).

```
devfs — devfs file system
USE_DEVFS="no"
```

# Start and Configuration of Network and Local Services

SuSEfirewall2 — Activating Firewall. See the readme file in package SuSE-firewall2.

news — Settings for access to NNTP servers.

```
ORGANIZATION=""
```

The text entered here will appear in every news posting sent from this machine.

```
NNTP_SERVER="news"
```

Address of the news server. If you receive news via UUCP and they are locally stored, set this variable to localhost.

proxy — Proxy settings

```
HTTP_PROXY=""
```

Some programs (e.g., lynx, arena, or wget) use a proxy server if this environment variable is set accordingly. SuSEconfig will set it in /etc/SuSEconfig/* (see SDB article file:/usr/share/doc/sdb/de/html/lynx_proxy.html). Example:
"http://proxy.me:3128/"

```
FTP_PROXY=""
```

Proxy for FTP. Example: "http://proxy.provider.com:3128/".

```
GOPHER_PROXY=""
```

Proxy for Gopher. Example: "http://proxy.provider.com:3128/".

```
NO_PROXY="localhost"
```

Exclude domains or subdomains from proxy use. Example: "www.me.de, do.main, localhost".

ssh — Before starting the “Secure Shell Daemon”, make sure a “host key” exists. Consult the documentation in /usr/share/doc/packages/ssh and the manual pages.

```
SSHD_OPTS=""
```

Options for sshd.