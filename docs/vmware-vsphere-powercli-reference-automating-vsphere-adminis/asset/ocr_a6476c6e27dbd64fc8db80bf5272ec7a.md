# CHAPTER 15 REPORTING AND AUDITING

SessionOption = $optCIM

```
}
$session = New-CimSession @sessionCIMParams
}
process {
  $Class | Foreach-Object {
  $instanceCIMParams = @{
    CimSession = $session
  }
  if($_ -match "*CIM*") {
    $instanceCIMParams.Add("ClassName",$_)
  }
  if($ -match "*OMC*") {
    $instanceCIMParams.Add("ResourceUri",
    "http://schema.omc-project.org/wbem/wcim/1/cim-schema/2/$_")
  }
  if($_ -match "*VMware*") {
    $instanceCIMParams.Add("ResourceUri",
    "http://schemas.vmware.com/wbem/wcim/1/cim-schema/2/$_")
  }
  Get-CimInstance @instanceCIMParams
}
}
nRemove-CimSession -CimSession $session
```

With this function, you can easily query any CIM class and extract information. The next example queries are for all PCI devices on an ESXi server:

```
$ipaddress = 'esx1.local.test'
$username = 'root'
$pswd = 'password'
```

```
$pswdSecure = ConvertToSecureStringString $pswd -AsPlainText
-Force
$cred = New-Object -TypeName System.Management.Automation.PSCredential '
```