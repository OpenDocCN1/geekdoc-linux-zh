# SET UP YOUR VCENTER SERVER FOLDER STRUCTURE

```
[String]$Filename
)
Process {
  $report = @()
  $report = Get-Datacenter $dc | Get-VM | Get-FolderPath
  $report | Export-Csv $filename -NoTypeInformation
}
```

Export-Folders "Blue" "DC01" "C:\BlueFolders.csv"
Export-VMLocation "DC01" "C:\VMLocation.csv"
Export-Folders "Yellow" "DC01" "C:\YellowFolders.csv"

# Importing a Folder Structure

You can import an existing blue or yellow folder structure into vCenter Server using the Import-Folders function previously shown in Listing 1.5. You can also choose if you would like your VMs moved into their correct blue folders by using the Import-VMLocation function, as shown in Listing 1.7.

# LISTING 1.7 Importing VMs to their blue folders

```
function Import-VMLocation {
<#n.SYNOPSIS
  Imports the VMs back into their Blue Folders based on
  the data from a csv file.
.DESCRIPTION
  The function will import VM locations from CSV file
  and add them to their correct Blue Folders.
.NOTES
  Source: Automating vSphere Administration

.PARAMETER DC
  The Datacenter where the folders reside
.PARAMETER Filename
  The path of the CSV file to use when importing
.EXAMPLE
```