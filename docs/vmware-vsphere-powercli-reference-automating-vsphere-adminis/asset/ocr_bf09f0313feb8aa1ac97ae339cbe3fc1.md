# GET-CIEVIY 709

or

$vm | Get-Member -MemberType Method
TypeName: VMware.VimAutomation.Cloud.Views.Vm

| Name | MemberType | Definition |
| AcquireMksTicket | Method | VMware.VimAutomation.Cloud.Views.Mks... |
| AcquireTicket | Method | VMware.VimAutomation.Cloud.Views.Scr... |
| Attach | Method | void Attach(System.Nullable[int] bus... |
| Attach_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CheckCompliance | Method | void CheckCompliance() |
| CheckCompliance_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Consolidate | Method | void Consolidate() |
| Consolidate_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| ControlAccess | Method | VMware.VimAutomation.Cloud.Views.Con... |
| CreateMetadata | Method | void CreateMetadata(VMware.Metadata(VimAutuma... |
| CreateMetadata_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CreateSnapshot | Method | void CreateSnapshot(System.Nullable[...... |
| CreateSnapshot_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| CustomizeNextPowerOn | Method | void CustomizeNextPowerOn() |
| Delete | Method | void Delete() |
| Delete_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Deploy | Method | void Deploy(System.Nullable[bool] po... |
| Deploy_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |
| Detach | Method | void Detach(System.Nullable[int] bus... |
| Detach_Task | Method | VMware.VimAutomation.Cloud.Views.Tas... |

Let's say that you wanted to create a snapshot of this virtual machine. No cmdlet available that can do this for you, but you do have the CreateSnapshot method. See the information required to run the CreateSnapshot method, add the method name to the end of your:

$vm.CreateSnapshot

OverloadDefinitions

```
void CreateSnapshot(System.Nullable[bool] memory, System.Nullable[bool] quiesce, string name, string description)
```

Integration PART V