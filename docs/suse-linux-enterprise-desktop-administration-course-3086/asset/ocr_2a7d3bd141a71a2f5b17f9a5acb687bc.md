After a warning message, the next dialog allows you to enter the IP address or fully qualified domain name (FQDN) of the print server and to specify which queue to use. See Figure 12-10.

![](bbox=[0.02, 0.151, 0.941, 0.671])

The CUPS server that will be used is added to the /etc/cups/client.conf file.

```
```conf
# /etc/cups/client.conf
ServerName 10.0.0.2
```
```

This type of setup is a good choice if you have only one print server for the entire network.

+   - **CUPS Using Broadcasting**—Probably the best choice within a local network. With CUPS running locally, you can print on your locally connected printers as well as on those that are broadcasted by other servers within your network. New printers