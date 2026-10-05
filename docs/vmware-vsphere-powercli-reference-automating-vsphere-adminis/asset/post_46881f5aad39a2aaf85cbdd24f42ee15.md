
[PSObject []]$VMHost,

[parameter(Mandatory=$true, ValueFromPipeline=$false)]
[ValidateNotNullOrEmpty()]
[String]$Name,

[parameter(Mandatory=$true, ValueFromPipeline=$false)]
[ValidateNotNullOrEmpty()]
[String[]]$NFHost,

[parameter(Mandatory=$true, ValueFromPipeline=$false)]
[ValidateNotNullOrEmpty()]
[String]$Path,

[parameter(Mandatory=$false, ValueFromPipeline=$false)]
[ValidateSet("AUTH_SYS", "SEC_KRB5")]
[String]$Security,

[parameter(Mandatory=$false, ValueFromPipeline=$false)]
[Switch]$ReadOnly,

[parameter(Mandatory=$false, ValueFromPipeline=$false)]
[Int]$Delay = 10
)

```powershell
begin {
  if ($($PSBoundParameters.ContainsKey('ReadOnly'))) {
    $ReadOnly = $false

    if ($NFHost.Count -gt 1) {
      $NFHost = $NFHost -join ","
    }
  }
}
process {
```

## SET UP THE STORAGE 135

```powershell
try {
    foreach ($ESXIHost in $VMHost) {
        if ($ESXIHost.GetType().Name -eq "string") {
            try {
                $ESXIHost = Get-VMHost $ESXIHost \
                -ErrorAction Stop
            } catch [Exception] {
                $ErrorText = "VMHost $ESXIHost \
does not exist"
                throw
            }
        }
        elseif ($ESXIHost -isnot [VMware.VimAutomation.ViCore.Impl.V1.Inventory.VMHostImpl]) {
            $ErrorText = "You did not pass a string or \
a VMHost object"
            throw
        }

        # -- Get ESXCli Object
        try {
            $ESXCli = Get-EsXCli -VMHost $ESXIHost \
            -ErrorAction Stop
        } catch [Exception] {
            $ErrorText = "Unable to get ESXCli object"
            for $ESXIHost
            throw
        }
    }

# -- Create NFS 4.1 Datastore
# $SecurityValue = if ($PSBoundParameters.ContainsKey('Security'))
{$Security} else {$null}
```

Install, Configure, and Manage the vSphere Environment

## $ESXCli.storage.nfs41.add($NFSHost,$ReadOnly,$SecurityValue,$Path,$Name) | Out-Null

```powershell
try {
    if ($PSCmdlet.ShouldProcess($ESXiHost)){
        $SecurityValue = if ($PSBoundParameters.ContainsKey('Security')) {$Security} else {`null}
        $ESXCli.storage.nfs41.add($ESXiHost,`
ReadOnly,$SecurityValue,$Path,$Name) |
        Out-Null

        # -- Get the Datastore Object (takes a `
while for vCenter to register the datastore)
        try {
            Start-Sleep -Seconds $Delay
            $Datastore = Get-Datastore -Name $Name `
            -ErrorAction Stop
            Write-Output $Datastore
        } catch [Exception]{
            $ErrorText = "Unable to retrieve `
created Datastore"
            throw
        }
    }
} catch [Exception] {
    $ErrorText = "Unable to create NFS 4.1 ``
Datastore"
    throw
}
```

## SET UP THE STORAGE

```powershell
catch [Exception]{
  if ($ErrorText){
    throw "Unable to create NFS 4.1 Datastore\n    for host $($ESXIHost). Error is: $($ErrorText)"
  }
  else {
    throw "Unable to create NFS 4.1 Datastore\n    for host $($ESXIHost)"
  }
}
end {
```

Typical use of the function would be similar to the following:

```powershell
PS C:\> Get-VMHost vsanesxi01* | New-NFS41Datastore -Name NFS26\n-NFSHost '192.168.0.106,192.168.0.107' -Path NFS26
```

| Name | FreeSpaceGB | CapacityGB |
| :--- | :--- | :--- |
| NFS26 | 2234 | 655 |

Once the NFS 4.1 datastore has created, you can use the standard PowerShell cmdlets Get-Datastore and Remove-Datastore to manage it, just as you would for other types of datastore. For example, let's look at our NFS 4.1 datastore NFS26 and its type (NFS41), compared to the type (NFS) reported for other datastores.

```powershell
PS C:\> Get-Datastore NFS* | Format-Table Name,AutoSize
```

| Name | Type |
| :--- | :--- |
| NFS12 | NFS |
| NFS26 | NFS41 |
| NFS11 | NFS |
| NFS01 | NFS |
| NFS10 | NFS |

## Creating Multiple Datores from a Data Source

In course, using PowerCLI you can automate the creation of single or multiple datastores. The data used to create a datastore is supplied to you by a data source. Let's take a look at a couple of examples to show how you can save time and effort when the information to create the datastores is available from that source.

In the first example, your storage team has created some LUNs on a Fibre Channel SAN and has supplied you with the necessary details via a CSV file. The CSV file contains the HostID, LunID, and Identifier for each Lun. It is a good idea to include the HostIDs and LunIDs in the vSphere datastore naming. The CSV file looks like the one in Figure 4.1.

FIGURE 4.1 Fibre Channel LUN details

![](img/62596f5acc979040608a4e511beb7d6_169_png)

You can use the standard PowerShell cmdlet Import-CSV to access the data source and then feed data into the New-Datastore cmdlet to create your stores. You can also use the supplied HostIDs and LunIDs to build the name of the datastore each time, store that in the $Name variable, and use it with the Name parameter of New-Datastore (Listing 4.11).

## LISTING 4.11 creating Fibre Channel datastores from a data source

```powershell
Import-CSV FibreLuns.csv | Foreach {$Name = 'Fibre_Host' + \
_.HostID + '_Lun' + $_.LunID; New-Datastore -VMfs -VMHost \
vesxi05* -Name $Name -Path $_.Identifier}
```

This code would create datastores named as follows:

```
Fibre_Host1_Lun102
Fibre_Host2_Lun97
Fibre_Host3_Lun263
Fibre_Host4_Lun195
Fibre_Host5_Lun123
```

In this example, we used only 5 datastores, but you can use exactly the same code to create 20 or 50 datastores; the only item that will need to change is the data source. Similarly, you can take the same approach with NFS datastores to create multiple datastores across different NFS hosts from a data source. For example, take a look at the CSV data supplied by an NFS storage administrator in Figure 4.2.

FIGURE 4.2 NFS storage details

![](img/62596f5acc979040608a4e511beb7d6_170_0.png)

To create these datastores, you can use code similar to Listing 4.12.

## LISTING 4.12 Creating multiple NFS datastores from a data source

```powershell
Import-Csv NFSLuns.csv | Foreach (New-Datastore -NFS -Name
$_.DatastoreName -VMHost vesxi05* -Path $_.Path -NFSHost
$_.NFSHost)
```

## CHAPTER 4

You've seen that the process of creating datastores based on information from an accessible data source is straightforward, saves you time, and can be repeated across different types of storage.

## Leveraging Get-ExScli for Storage-Related Functions

It is possible to carry out a significant number of storage-related tasks with PowerCLI. However, should there be a task not covered out of the box, then it will be feasible to use the extensive coverage supplied by the vSphere command-line tool escli via the Get-ExScli PowerCLI cmdlet. We have noted that this approach is used in the Get-VimScliBinding, Set-VimScliBinding, and New-NFS4IDastore functions in Listing 4.3, Listing 4.4, and Listing 4.10.

Any escli command is available via this approach, so let's take a look at an example to see how to convert a well-known escli command to its PowerCLI equivalent.

## Which VAAI Primitives Are Supported?

To query the vStorage API for Array Integration (VAAI) primitives for a L, the escli command would be as follows:

```
escli storage core device vaai status get -d naa.6001405b12d96cdeb01d3098d78cbd
```

To convert this to PowerCLI, we would do the following—that is, replace the spaces in the escli command with periods and supply a string to the Get method:

```powershell
$ExScli = Get-ExScli -VMHost vesxi05.sunydale.local
$ExScli.storage.core.device.vaai.status.get('naa.6001405b12d96cdeb01d3098d78cbd')
```

> TIP Using the PowerShell ISE with $ExScli makes for a very interactive experience; the built-IntSense provides onscreen prompts for available options at each step along completing the command. For example, typing $ExScli .storage.core, the user will be prompted with possible options for what should be next: adapter, claiming, claimrule, device, path, or plugin. In addition, the options (such as availability and type of parameters) for the typical get, set, or add method at the end of the command will be displayed to the user.
