# Hacking Exposed Web Applications

# NES Index Disclosure Countermeasures

The best way to prevent attacks of this nature is to disable the Directory Indexing feature via the Administration interface. Select Content Management | Document Preferences, and change Directory Indexing to "none.\ Manually editing the obj.conf file will accomplish the string fn="index-common" is replaced with fn="send-error" in the following:

```
Service&nbsp;method="(GET|HEAD)&nbsp;type="magnus-internal/directory"
="index-common"
```

# NES Web Publisher Administrative Interface Attack

| Popularity: | 9 |
| Simplicity: | 9 |
| Impact: | 7 |
| Risk Rating: | 8 |

NES' Web Publishing feature is installed by default in the /publisher directory, which is accessible by remote or local users without any authentication. Simply requesting the /publisher directory will load the Web publisher Java applet, which attempts to authenticate the user—but this challenge will accept any credentials, valid or not. Once "authenticated," a directory listing of the Enterprise Server's contents will be displayed, as well as controls for deletion, modification, download, and movement of files (these require valid authentication). This issue affects Netscape Server for Solaris 3.5 and 3.6.

# NES Web Publisher Countermeasures

Configure and enable the Access Control Module or apply file system ACLs to the /publisher directory.

# NES Reverse Proxy Vulnerability

| Popularity: | 8 |
| Simplicity: | 6 |
| Impact: | 7 |
| Risk Rating: | 7 |

Netscape Enterprise Server can be used as a reverse proxy so that a malicious attacker from the Internet can use the Web server as a proxy to access machines on internal