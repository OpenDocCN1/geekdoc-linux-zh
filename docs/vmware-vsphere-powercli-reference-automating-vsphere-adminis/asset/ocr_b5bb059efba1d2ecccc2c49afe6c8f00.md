# CHAPTER 9 • ADVANCED VIRTUAL MACHINE FEATURES

# LISTING 9.7 Find snapshot creator

```
function Get-SnapshotCreator {
  Param(
    {parameter(Mandatory=$true,
      ValueFromPipeline=$true,
      ValueFromPipelinePropertyName=$true
    }
  )[VMware.VimAutomation.ViCore.Impl.V1.VM.SnapshotImpl=$Snapshot

  Begin {
    function Get-SnapshotTree {
      ($tree, $target)
      $found = $null
      foreach ($elem in $tree){
        if ($elem.Snapshot.Value -eq $target.Value){
          $found = $elem
          continue
        }
      }
      if ($found -eq $null and $elem.ChildSnapshotList -ne $null){
        $found = Get-SnapshotTree $elem.ChildSnapshotList $target
      }
      return $found
    }
    Process {
      $guestName = $Snapshot.VM.Name
      $tasknumber = 999
      $tMgr = Get-View TaskManager
      #Create hash table. Each entry is a create snapshot task
      $report = @{}

```