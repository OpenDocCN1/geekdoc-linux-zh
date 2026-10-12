The server-status page can also perform automatic updates to provide even closer monitoring of the server. If the URL `http://localhost/server-status?refresh=40` is specified, the server-status page displayed in your browser will be updated every 40 seconds. This enables a browser window to be devoted entirely to continually monitoring the activities of the Web server.

By default, only basic status information is generated. If you would like to generate full status information, you need to turn on the *ExtendedStatus* directive by uncommenting the last line in the following code:

```
#
# ExtendedStatus: controls whether Apache will generate "full" status
# information (ExtendedStatus On) or basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.
#
#ExtendedStatus On
```

# Further security of server-info and server-status

Because both the server-info and server-status pages contain private information that should not be accessible to just anyone on the network, there are a few extra ways you can secure that information. You can restrict that information only to the local host; however, in some environments that may not be practical.

If you must allow other machines or networks access to such detailed configuration information, allow only as many machines as is necessary, and preferably only those machines on your local network. Also, be aware that, in the wrong hands, the information displayed by the server-info and server-status pages can make it much easier for the security of your entire machine to be compromised. Figure 21-4 shows the error message that should be presented to hosts that do not have access to the server-status page.

![](bbox=[0.05, 0.61, 0.94, 0.87])

It may also be beneficial to change the URL used to reference both of the aforementioned pages. This is an example of “security through obscurity,” which should not be relied on but