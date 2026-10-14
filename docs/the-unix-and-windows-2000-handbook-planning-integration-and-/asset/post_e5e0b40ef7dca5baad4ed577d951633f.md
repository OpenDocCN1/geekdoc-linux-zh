
the Internet Services Manager MMC snap-in, which can be launched as follows: from the Start menu → Administrative Tools → Internet Services Manager. The Internet Services Manager is shown in Figure 16.3.

To configure the options for the default Web site, select the Default Web Site from the list of your IIS sites on your system, and select Properties from the Action menu. The Default Web Site Properties window in Figure 16.4 will be displayed.

As you can see, there are several option tabs available. The following sections will describe the different option tabs and the options available.

### Web Site
This page allows you to configure the identification parameters for your entire Web site. Here you can configure the IP address and TCP ports for the site, connection limitations, and logging options. The default settings found on this page are acceptable for most sites. To host multiple sites from a single machine, or to create virtual sites, you should refer to the on-line documentation or to the IIS Resource Kit.

### Operators
This page allows you to specify which Windows 2000 user accounts are granted operator privileges on the Web site. Operators have the ability to change Web site settings, and to start and stop the Web site.

### Performance
This page allows you to configure memory, processor, and bandwidth usage parameters. Table 16.9 describes the properties available.

![](img/415c89a1ede71e11e5040a0038b6916c_673_0.png)

**Figure 16.3** Internet Services Manager MMC snap-in.

## Figure 16.4
Default Web Site Properties.

![](img/415c89a1ede71e11e5040a0038b6916c_674_0.png)

### ISAPI Filters
This page allows you to add, remove, and configure ISAPI filters, which are programs that are invoked in response to HTTP-generated events.

### Home Directory
This page allows you to configure the location of the Web site's home directory. By default, the location is C:\Inetpub\wwwroot. There are three types of directories:

| Table 16.9 Web Site Performance Properties |
| Property | Description |
| Performance Tuning | Allows you to configure the site for an expected number of daily connections. By properly configuring this setting, memory will be optimally used by the Web server service. |
| Bandwidth Throttling | Allows you to limit how much of the available network bandwidth is utilized by the Web site. |
| Process Throttling | Allows you to limit how much of the Web server's processor time can be utilized by this Web site. |

## Web Servers

- A directory located on this computer is physically located on the same server that the WWW service runs on.
- A share located on another computer is physically located on another server and shared over the network with the appropriate permissions.
- A redirection to a URL will send connections to another Web site, which can be hosted from the same server or another server on the network.

As part of the home directory configuration, you are also presented with options for configuring access permissions, browsing, and logging.

### Documents
This page allows you to configure the default document and document footer for your Web site. Default documents are automatically sent to clients when they connect to your Web site. Document footers are appended to every HTML document sent to clients when they connect.

### Directory Security
This page allows you to configure directory and file security for your Web site. NTFS permissions can be utilized to protect sensitive content on your Web site. This page allows you to tailor how security is implemented. Table 16.10 describes the different configuration options available.

### HTTP Headers
This page allows you to configure and add HTTP headers that will be returned to the client browser. This page includes configuration options for content expiration, custom HTTP headers, and MIME (Multipurpose Internet Mail Extensions) mappings.

**Table 16.10 Web Site Directory and File Security Configuration Options**

| Option | Description |
|---|---|
| Anonymous Access and Authentication Control | Allows you to configure how users will be authenticated, when required, during a connection. Users that do not connect anonymously must have a valid Windows 2000 user account and have been granted permissions to the files and directories via NTFS permissions. |
| IP Address and Domain Name Restrictions | Allows you to allow/deny access based on IP addresses and domain names. |
| Secure Communications | Allows you to install and configure Secure Sockets Layer (SSL) certificates to enable encrypted communications. |
