```
If ($Poldertype -eq "Yellow") {
  $type = "host"
} Else {
  $type = "vm"
}
$report = @())
$report = Get-Datacenter $dc | Get-Folder $type |
  Get-Folder | Get-FolderPath
$report | ForEach-Object {
    if ($type -eq "vm") {
      $_.Path = ($_.Path).Replace($dc + "\","$type\")
    }
    $report | Export-Csv $filename -NoTypeInformation
  }
}
```

```
function Export-VMLocation {
#<
.SYNOPSIS
  Creates a csv file with the folder location of each VM.
.DESCRIPTION
  The function will export VM locations from vCenter Server
  and add them to a CSV file.
.NOTES
  Source: Automating vSphere Administration
n.PARAMETER DC
  The Datacenter where the folders reside
.PARAMETER Filename
  The path of the CSV file to use when exporting
.EXAMPLE
  Export-VMLocation -DC "DC01" -Filename "C:\\VMLocations.csv"
#>
param(
[String]$DC,
```