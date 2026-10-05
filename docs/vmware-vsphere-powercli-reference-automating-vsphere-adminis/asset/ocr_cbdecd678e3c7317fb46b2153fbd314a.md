# Tags

In vSphere 5.1, VMware introduced a tagging feature to vCenter Server. Tags allow administrators to add metadata to objects in their environment. Administrators now have the ability to create tags and tag categories to organize their virtual environment and for easier searching and sorting of objects based on the tagging criteria specified.

Tags can be used on a number of objects within the vSphere environment. Objects such as virtual machines, clusters, datastores, hosts, networks, and more can be tagged with additional metadata. The tag feature allows administrators to choose whether a tag can be used on more than one type of vSphere object or if multiple tags from a single tag category can be used on the same object.

Tagging is a fantastic feature, but the problem with tags is that in vCenter Server 5.1 through vCenter Server 5.5, the tags are stored in the Inventory Service Database and do not carry over if a host is connected to a dedicated vCenter Server. In vSphere 6, tagging has a dedicated database. With this knowledge, you can leverage PowerCLI to create backups of the tags categories, tags, and the relationships between vSphere objects and their attached metadata. Listing 12.4 can be used to export these objects.

# LISTING 12.4 Exporting tags and tag categories

```
function Export-Tag {
#
.SYNOPSIS
  Export Tags and Tag Categories
.DESCRIPTION
  This function exports Tags and Tag Categories from vCenter
.NOTES
  Source: Automating vSphere Administration
  PARAMETER Path
  Mandatory parameter used by the function to determine
  the destination of the Tags file.
  .EXAMPLE
  Export-Tag -path C:\Temp\exportedtags.xml
#>
[CmdletBinding()]\Param[Parameter (Mandatory = $True, Position = 1)]
```