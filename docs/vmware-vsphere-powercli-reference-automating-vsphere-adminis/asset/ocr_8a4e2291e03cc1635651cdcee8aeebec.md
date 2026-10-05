# Use Templates

A template is a VM that has been placed in a protected, read-only state to be used as a master copy for subsequent virtual machine creation and provisioning tasks. Once a VM has been converted into a template, it cannot be modified in any way without first converted back into a virtual machine. There are many reasons to use templates, but they all boil down to one primary benefit: reduce the number of steps and the time needed to deploy a new virtual machine.

# Creating Templates

With the fundamentals of templates established, all that's needed to create a new template is a source VM. The source VM will have to be prepared by installing the desired operating system before conversion. With the source VM prepared, there are two ways to create a template:

+   * Convert the VM into a template.
* Clone the VM to a template.

The decision of which method to use is simple. Is the source VM needed for something else? If the answer is yes, then clone the source VM to a template. If the answer is no, then save time and input/output (I/O) operations by converting the source VM to a template.

For example, a web team just finished loading a brand-new Linux server and wants to use it for an upcoming deployment. If that server is needed for anything else, simply convert it to a template using the Set-VM cmdlet, as we've done in Listing 7.7.

# Listing 7.7 Converting a VM to a template

```
Get-VM WEBXX | Set-VM -ToTemplate
```

If any reason the source VM is needed for another task, create a new template by cloning the source to a template, as shown in Listing 7.8.

# Listing 7.8 Cloning a VM to a template

```
$VM = Get-VM WEB02
$Folder = Get-Folder WEB
New-Template -Name 'WEBMaster' -VM $VM -Location $Folder
```