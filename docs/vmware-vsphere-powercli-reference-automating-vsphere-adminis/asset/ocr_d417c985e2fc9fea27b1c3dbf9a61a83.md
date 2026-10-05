# CALLING VRO WORKFLOWS FROM POWERSHELL 771

```
}
}
```

```
$Workflows = Invoke-RestMethod -Method Get -Uri $URI \
-Headers $Headers -ContentType "application/xml"
```

```
foreach ($Workflow in $Workflows.link) {
```

```
$Object = [psustomobject]@@(

Name = ($Workflow.attributes | \
Where-Object { $_.name -eq 'name' }).value
Server = $Server
ID = ($Workflow.attributes | \
Where-Object { $_.name -eq 'id' }).value
Description = ($Workflow.attributes | \
Where-Object { $_.name -eq 'description' }).value
ItemRef = ($Workflow.attributes | \
Where-Object { $_.name -eq 'itemHRef' }).value
Version = ($Workflow.attributes | \
Where-Object { $_.name -eq 'version' }).value
CategoryName = ($Workflow.attributes | \
Where-Object { $_.name -eq 'categoryName' }).value
CategoryHRef = ($Workflow.attributes | \
Where-Object { $_.name -eq 'categoryHRef' }).value
CustomIcon = ($Workflow.attributes | \
Where-Object { $_.name -eq 'customIcon' }).value
Execute = ($Workflow.attributes | \
Where-Object { $_.name -eq 'canExecute' }).value
CanEdit = ($Workflow.attributes | \
Where-Object { $_.name -eq 'canEdit' }).value

)

Write-Output $Object
}
```

```
catch [Exception] {
```

![](bbox=[0.903, 0.613, 0.952, 0.683])