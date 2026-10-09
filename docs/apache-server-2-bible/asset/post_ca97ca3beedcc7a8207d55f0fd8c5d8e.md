
**Tip**

Make sure you enter a fully qualified **domain** name instead of just a shortcut. For example, if you have a host called `wormhole.mycompany.com`, you should not set the `ServerName` to `wormhole`. The valid choice is:

```
ServerName wormhole.mycompany.com
```

## ServerRoot

The `ServerRoot` directive sets the directory in which the server files reside. Do not confuse this with `DocumentRoot` directive, which is used for pointing the server to your Web contents. The `ServerRoot` directory is used for locating all the server configuration files and log files. The standard distributions include `conf`, `bin`, `htdocs`, `icons`, `cgi-bin`, and `logs` directories under the `ServerRoot` directory. If you do not specify the `ServerRoot` directive, however, you can use the `-d` command-line option to tell Apache what your `ServerRoot` directory is.

Syntax: `ServerRoot directory`

Default setting: `ServerRoot /usr/local/apache`

Context: Server config

## ServerSignature

By using the `ServerSignature` directive you can create a simple footer for Apache-generated pages such as error messages and directory listings. This directive is not recommended unless you use Apache as a proxy server. On the other hand, when a user receives an error message, it is often difficult to determine which proxy server caused the error if there is a chain of proxies in the user’s network path. This footer acts as an identifier in such cases. You can include an e-mail address that will appear in the footer so that others can e-mail you if there is a problem.

Syntax: `ServerSignature On | Off | e-mail`

Default setting: `ServerSignature Off`

Context: All

## ServerTokens

In response to a request, Apache can send a **header** that includes an identifier that tells the client what server you are running. The `ServerTokens` directive lets you control that identifier token. When `Minimal` option is used, Apache sends "Apache/version"; when `ProductOnly` option is used, only the string "Apache" is sent; when `OS` is used "Apache/version (OS_Type)" is sent; when `Full` is used, Apache sends "Apache/version (OS_Type) _Available_Module_Info_".

Syntax: `ServerTokens` `Minimal` | `ProductOnly` | `OS` | `Full`

Default setting: `ServerTokens` `Full`

Context: Server config

![](img/e11fcbd2818a3495ac70085e5d8d1c26_100_0.png)

> I recommend using only the `Minimal` option if you want to avoid security issues from bug-based attacks; you don’t want to advertise what type of server you use to the world.

## SetInputFilter

The `SetInputFilter` directive sets the filters that will be used to process a request sent to the server. The filters are applied in the order that they appear in this directive.

Syntax: `SetInputFilter` `filter` [`filter` ...]

Default setting: None

Context: Directory

## SetOutputFilter

The `SetOutputFilter` directive sets the filters that will be used to process a response before it is sent to the Web client. The filters are applied in the order they appear in this directive.

Syntax: `SetOutputFilter` `filter` [`filter`] ...

Default setting: None

Context: Directory

In the following example, all files in the `/www/mysite/htdocs/parsed` directory will be processed using the `INCLUDES` output filter, which is the SSI filter:

```
<Directory "/www/mysite/htdocs/parsed">
    Options +Includes
    SetOutputFilter INCLUDES
</Directory>
```

## Performance and Resource Configuration Directives

These directives enable you to fine-tune Apache for higher performance and better control. You can fine-tune the Apache processes in many ways. Note that almost all of these directives require a clear understanding of how your system works in terms of the operating system, hardware, and so on; therefore, you should browse your operating system manuals and/or `man` pages to learn how your system limits system resources to processes, how it controls TCP/IP connectivity, and so on. The directives in this section are further divided into subfunctions.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_101_0.png)

See Chapter 22 for more info about how to speed up Apache.

### Controlling Apache processes

The following directives are used to control how Apache executes in your system. Using these directives enables you to control how Apache uses resources on your system. For example, you can decide how many child server processes to run on your system, or how many threads you should allow Apache to use on a Windows platform. A few things to remember when configuring these directives:

- The more processes you run, the more load your CPU(s) experiences.
- The more processes you run, the more RAM you need.
- The more processes you run, the more operating system resources (such as file descriptors and shared buffers) are used.

Of course, more processes also could mean more requests serviced, and thus more hits for your site. So, setting these directives should be based on a combination of experimentation, requirements, and available resources.

#### ListenBacklog

See the ListenBacklog directive under the “MPM threaded-Specific Directives” section.

#### MaxClients

See `MaxClients` directive under the “MPM threaded-Specific Directives” section.

#### MaxRequestsPerChild

See `MaxRequestsPerChild` directive under the “MPM threaded-Specific Directives” section.

#### MaxSpareServers

See `MaxSpareServers` directive under the “MPM prefork Specific Directives” section.

#### MinSpareServers

See `MinSpareServers` directive under the “MPM prefork Specific Directives” section.

#### SendBufferSize

See `SendBufferSize` directive under the “MPM threaded Specific Directives” section.

#### StartServers

See `StartServers` directive under the “MPM threaded Specific Directives” section.

#### TimeOut

Apache server responds to requests. The requests and responses are transmitted via packets of data. Apache must know how long to wait for a certain packet. The `TimeOut` directive enables you to configure the time in seconds. The time you specify here is the maximum time Apache will wait before it breaks a connection. The default setting enables Apache to wait for 300 seconds before it disconnects itself from the client. If you are on a slow network, however, you may want to increase the time out value to decrease the number of disconnects.

- **Syntax:** `TimeOut number`
- **Default setting:** `TimeOut 300`
- **Context:** Server config

Currently, this `TimeOut` setting applies to:

- The total amount of time it takes to receive a GET request.
- The amount of time between receipt of TCP packets on a POST or PUT request.
- The amount of time between ACKs on transmissions of TCP packets in responses.

#### Making persistent connections

By using the `KeepAlive` directives discussed in this section, you can instruct Apache to use persistent connections so that a single TCP connection can be used for multiple transactions. Normally, every HTTP request and response uses a separate connection. This means that every time the server gets a request, it opens a connection to retrieve the request and then closes it. After the server has received the request, it opens another TCP connection to respond, and finally closes the connection after completing the service. This method increases the toll on high performance. Reuse of a single connection for multiple transactions reduces the overhead needed for setting up and closing a TCP connection repeatedly, and thereby increases performance.

To establish a persistent connection, however, both the server and the client need to have the persistent connection facility. Most popular browsers, such as Netscape Navigator and Microsoft Internet Explorer, have `KeepAlive` features built in.

Not all transactions can take advantage of the persistent connections. A requirement for a persistent connection is that the resources being transmitted must have a known size. Because many CGI scripts, SSI commands, and other dynamically generated contents do not have a known length before transmission, they are unable to take advantage of this feature.

### KeepAlive

The KeepAlive directive enables you to activate/deactivate persistent use of TCP connections in Apache.

- Syntax: KeepAlive On | Off
- Default setting: KeepAlive On
- Context: Server config

Older Apache servers (prior to version 1.2) may require a numeric value instead of On/Off when using KeepAlive This value corresponds to the maximum number of requests you want Apache to entertain per request. A limit is imposed to prevent a client from taking over all your server resources. To disable KeepAlive in the older Apache versions, use 0 (zero) as the value.

### KeepAliveTimeout

If you have the KeepAlive directive set to on, you can use the KeepAliveTimeout directive to limit the number of seconds Apache will wait for a subsequent request before closing a connection. After a request is received, the timeout value specified by the Timeout directive applies.

- Syntax: KeepAliveTimeout seconds
- Default setting: KeepAliveTimeout 15
- Context: Server config

### MaxKeepAliveRequests

The MaxKeepAliveRequests directive limits the number of requests allowed per connection when KeepAlive is on. If it is set to 0 (zero), unlimited requests will be allowed. I recommend that this setting be kept to a high value for maximum server performance.

- Syntax: MaxKeepAliveRequests number
- Default setting: MaxKeepAliveRequests 100
- Context: Server config
