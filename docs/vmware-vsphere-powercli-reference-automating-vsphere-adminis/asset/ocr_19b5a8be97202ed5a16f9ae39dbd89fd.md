Notice the method returned an error. You can't leave out the parameter, even though you don't pass any information. Whenever you want to pass an empty parameter, pass the $null value. Let's try again:

```
$pm.QueryHostPatch($null) | Format-List
```

Version : 1.40
Status : 
XmlResult : <exsupdate-response>
<version>1.40</version>
</exsupdate-response>

> The sample used the QueryHostPatch method, which is available courtesy of the PowerCLI Development Team, instead of QueryHostPatch-Task. Remember that doing so provides a synchronous call to the method.

# Finding the Host HWuptime

Suppose you want to know how long the hardware hosting one of your ESX hosts has been powered. If you enter uptime in the All Methods entry, you will find the RetrieveHardwareUptime method. From the SDK Reference, you find that the method is available on a HostSystem managed object, that the method has no required parameters, and that the time is returned the number of seconds. Using the method, calculating the HWuptime is now rather straightforward:

```
$exs = Get-VMHost exs.test.local
$exs.ExtensionData.RetrieveHardwareUptime()
30148
```

# Changing the vCenter Logging Options

By now, you are probably thinking that the SDK Reference is the ultimate resource, but not all information you will ever require while you're working with vSphere is so readily available in the SDK Reference. Let's look at another example.

In the Managed Object Types, you will find the OptionManager, which is obviously what you would look for is to change vCenter Server Options. If you further investigate the UpdateOptions method, you will find that the OptionValue parameter is required. Now, here's the problem: There seems to be no list of accepted values for the Key and Value fields.