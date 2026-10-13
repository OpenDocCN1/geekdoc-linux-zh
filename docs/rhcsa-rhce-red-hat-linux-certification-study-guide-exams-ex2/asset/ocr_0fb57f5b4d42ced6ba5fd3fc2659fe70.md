**TABLE 15-5 SWAT Base Options**

|  |  |
|---|---|
| workgroup | The workgroup or domain to which the system belongs. |
| realm | The Kerberos realm for the domain, set to the DNS name of the Kerberos server such as server1.example.com. May be used if a system is configured as a Kerberos client, as discussed in Chapter 12. |
| netbios name | Windows host name; may be different from the DNS host name. |
| netbios aliases | Additional host names for the server. |
| server string | Description of the server shown to clients who browse this server. |
| interfaces | Devices and IP addresses allowed to connect. |

# Security Options

A number of security options can be used both globally and for individual shares. Naturally, to use one of these options in a share, you should include it in the stanza associated with the share. The focus of this section is on those directives that can be used to help configure basic user- and host-based security for Samba. While these directives were discussed earlier in this chapter, the different perspective associated with SWAT may help you understand Samba better. As such, the following list is not comprehensive.

+   - **security** Basic directive for authentication on Samba systems; may be set to share, user, server, domain, or ads, as discussed earlier in this chapter.
+   - **password server** Reference to another system with the authentication database, usually a Samba or a pure Windows server.
+   - **guest account** Support for a nonprivileged account for connections.
+   - **invalid users** Users not allowed to access a system or share; for example, the following list prohibits users root, michael, and members of the project group:
+     ```
+     invalid users root michael @project
+     ```
+   - **valid users** Users allowed to access a system.
+   - **admin users** Users allowed administrative access, normally just to a share.
+   - **read list** Users given read-only access.
+   - **write list** Users given read/write access.
+   - **hosts allow** Hosts allowed access to a system (also known as allow hosts); for example, the following list supports access from all systems except one. May also use host and domain names.
+     ```
+     hosts allow 192.168. EXCEPT 192.168.0.100
+     ```
+   - **hosts deny** Hosts not allowed to access a system (also known as deny hosts).