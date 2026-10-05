# USE TEMPLATES

```
[parameter(Mandatory=$True)
,ValueFromPipeline=$True
HelpMessage='Template object to upgrade
)
VMware.ViAutomation.ViCore.Impl.V1.Inventory.TemplateImpl
$Template
```

```
[parameter()]
[ValidatePattern("vmx-\dd")]
[string]
$Version="vmx-11"
```

```
Process {
  # Convert our template back to a VM, and PowerOn.
  $VM = Set-Template -Template $Template -ToVM

  #check VM Hardware version
  if ($VM.ExtensionData.Config.Version -ne $Version)
  {
    Write-Host "VM Hardware version out of date!"
    -ForegroundColor 'RED'
    $VM = Start-VM -VM $VM | Wait-VMGuest Startup
  }

  # Check VMware tools version if tools are out of
  # date upgrade them.
  if ($VM.ExtensionData.Guest.Status -ne "ToolsOk")
  {
    Write-Host "VMware tools are out of date!"
    -ForegroundColor 'RED'
    #Kick off a tools update
    Try {
      Update-Tools -VM $VM
    }
    Catch {
      Write-Warning $_.Exception.Message
      break;
    }
  }
```

![](bbox=[0.893, 0.243, 0.963, 0.323])