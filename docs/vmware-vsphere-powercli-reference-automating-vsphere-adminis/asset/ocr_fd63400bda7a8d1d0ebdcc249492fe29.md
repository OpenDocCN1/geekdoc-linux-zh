If you receive an error message in your PowerShell console that "Exclusive access could not be obtained because the database is in use," you may have to also stop the vmware-cis-config service and try again:

```
Stop-Service vmware-cis-config -Force
```

After the restore is finished, you can start vCenter Server using the Start-Service cmdlet:

```
Start-Service vpxd
```

If you stopped the vmware-cis-config service to restore the database, you will need to make sure that you start the service up as well.

# Reconnecting ESXI Hosts

When you restore your vCenter Server without a backup of the original SSL certificate, vCenter Server won't be able to decrypt the ESXi hosts. All ESXi hosts will show up as disconnected. In this case, you'll have to reauthenticate every host by reconnecting them. When replacing the vCenter Server certificates, you must also reconnect all ESXi hosts to update the ESXi host passwords.

You can reconnect an ESXi host using the Set-VMHost cmdlet is used to change the configuration of the host. Set the -State parameter to Connected to reconnect a disconnected host. To disconnect a host, set the -State parameter to Disconnected.

```
Set-VMHost esx01 -State Connected
```

You should understand that if the SSL certificates are valid, the Set-VMHost cmdlet won't let you reconnect the server and the following error is: "Cannot complete login due to an incorrect username or password."

When you have to deal with invalid SSL certificates and you're solely working with PowerCLI cmdlets, your only option is removing and adding the host again using the Remove-VMHost and Add-VMHost cmdlets.

```
Remove-VMHost -Name esx01 -Confirm:$false
```

```
Add-VMHost -Name esx01 -User root -Password VMware! -Location MainDC -Force
```

However, there is a drawback to this approach. Removing an ESXi host will remove all of the host's configuration, including resource pools, VM, and the like. This is something you definitely don't want to happen in a production environment or during a restore operation.

![](bbox=[0.903, 0.335, 0.976, 0.487])