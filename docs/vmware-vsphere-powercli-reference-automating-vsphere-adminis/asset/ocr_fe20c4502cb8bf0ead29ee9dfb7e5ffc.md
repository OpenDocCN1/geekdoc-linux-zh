Now that you have connected to your vDC and your connection information is stored in the $DcConnection variable, you can use values from the extended properties within your scripts. You can also use them as troubleshoot issues, should any arise. Further information can be listed about your connection, such as connection status, SessionId, connection port, and, if you use the Format-List cmdlet.

# Disconnecting from a Target Datacenter

Disconnecting from the target datacenter is very simple. Just like disconnecting from vCloud Director or from hosts in your on-premises environment, you use the Disconnect verb—in this case, Disconnect-PIDatacenter. There is currently no way to specify which vDC to disconnect from, so this command will disconnect each vDC session that you have:

```
Disconnect-PIDatacenter -Confirm:$false
```

Running this command disconnects you from your vDC(s) but keeps you authenticated against vCloud Air and allows you to connect to other vDCs within the same vCloud Air account.

# Disconnecting from vCloud Air

It is always best practice to close your connection when you finish running scripts or are finished with your current session. If you are connected to only one server, you can run Disconnect-PIServer -Confirm:$false. While the Disconnect-PIServer accepts the name, wildcard (*), or connection, it is wise to decide on a method that you and others agree on and use the chosen method for consistency. If you saved your connection as a variable at the beginning of yourCLI session, you can refer the same connection variable to disconnect:

```
$Connection = $global:DefaultPIServers
Disconnect-PIServer $Connection -Confirm:$false
```

# Set-PowerCLIConfiguration

Not all users need to adjust the PowerCLI configuration settings. In fact, many users forget the Set-PowerCLIConfiguration cmdlet even exists. However, there are a number of settings here that can help you as you leverage PowerCLI for connections to vCloud Air.