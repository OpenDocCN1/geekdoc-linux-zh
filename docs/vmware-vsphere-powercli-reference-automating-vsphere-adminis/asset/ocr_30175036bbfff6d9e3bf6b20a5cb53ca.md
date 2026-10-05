# CHAPTER 18 · THE SDK

| | | |
|---|---|---|
| ParentFolderId | Property | string FolderId {get}; |
| RemoteHost | Property | string RemoteHost {get}; |
| RemotePath | Property | string RemotePath {get}; |
| State | Property | VMware.VimAutomation.Core.T... |
| StorageIOControlEnabled | Property | bool StorageIOControlEnabled ... |
| Type | Property | string Type {get}; |
| Uid | Property | string Uid {get}; |
| UserName | Property | string UserName {get}; |

# EXTENSION DATA

Since PowerCLI 4.1, a property called Extensionondata is present on most of the VIOjects. Property maps to the vSphere object on which the VObject is based. That means you do not have to use the Get-View cmdlet anymore to get the managed object. For convenience, use the Extensionondata property to access the underlying vSphere objects.

To continue with the previous example, let's investigate the Extensionondata property of the DatastoreImpl. As you can see, the Extensionondata property is the managed object called Datastore.

```
$dsImpl.ExtensionData.GetType()
```

| IsPublic | IsSerial Name | BaseType |
|---|---|---|
| --- | --- | --- |
| True | False | Datastore VMware.Vim.ManagedEntity |

The vSphere objects typically have a lot more properties and methods attached to them, as the following closer look at a managed object that represents a Datastore

```
$ds | Get-Member
```

TypeName: VMware.Vim.Datastore