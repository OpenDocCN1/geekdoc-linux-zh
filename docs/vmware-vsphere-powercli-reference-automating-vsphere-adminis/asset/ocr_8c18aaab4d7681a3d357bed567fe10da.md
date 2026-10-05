# CHAPTER 18 · THE SDK

| | | |
|---|---|---|n| Browser | Property | VMware.Vim.ManagedObjectRe... |
| Capability | Property | VMware.Vim.DatastoreCapabi... |
| Client | Property | VMware.Vim.Client Cien... |
| ConfigIssue | Property | VMware.Vim.Event[] Configi... |
| ConfigStatus | Property | VMware.Vim.ManagedSyst... |
| CustomValue | Property | VMware.Vim.CustomFieldValue... |
| DeclaredAlarmState | Property | VMware.Vim.AlarmState[ De... |
| DisabledMethod | Property | string[] DisabledMethod(g... |
| EffectiveRole | Property | int[] EffectiveRole{get}; |
| Host | Property | VMware.Vim.DatastoreHostM... |
| Info | Property | VMware.Vim.DatastoreInfo... |
| IormConfiguration | Property | VMware.Vim.StorageORMInfo... |
| LinkedView | Property | VMware.Vim.Datastore Like... |
| MoRef | Property | VMware.Vim.ManagedObjectRe... |
| Name | Property | string Name{get}; |
| OverallStatus | Property | VMware.Vim.ManagedEntitySt... |
| Parent | Property | VMware.Vim.ManagedObjectRe... |
| Permission | Property | VMware.Vim.Permission[] Pe... |
| RecentTask | Property | VMware.Vim.ManagedObjectRe... |
| Summary | Property | VMware.Vim.DatastoreSummar... |
| Tag | Property | VMware.Vim.Tag[] {get}; |
| TriggeredAlarmState | Property | VMware.Vim.AlarmState[] Tr... |
| Value | Property | VMware.Vim.CustomFieldValue... |
| Vm | Property | VMware.Vim.ManagedObjectRe... |

# Data Objects and Their Methods

The properties in a managed object contains data objects. The data objects can be simple types—for example, the Name property is a String type—or they can be other data objects—like the AvailableField property, which is a CustomIDField type.

The methods in the managed objects are, simply said, functions you can invoke on these objects. For example, the RenameDatastore method on the Datastore managed object obviously renames a datastore. You can find all the details on this method in the vSphere API Reference if you select the Datastore object in the Managed Object entry.