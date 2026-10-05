```
[parameter(Mandatory=$true,ValueFromPipeline=$false)
[ValidateSet('NoAccess','ReadOnly', 'ReadWrite')]
[String]$AccessLevel,
```

```
[parameter(Mandatory=$false,ValueFromPipeline=$false)
[ValidateNotNullEmpty()]
[String]$Path = "/",
```

```
[parameter(Mandatory=$false,ValueFromPipeline=$false)
[Switch]$Append
)
```

```
begin {

# Set the Access Level value
switch ($AccessLevel)
{
    'NoAccess' {$AccessLevelNumber = 0}
    'ReadOnly' {$AccessLevelNumber = 1}
    'ReadWrite' {$AccessLevelNumber = 2}
}
```

```
process {

try {

foreach ($Repo in $Name){

    # Create the Repository Object
    $RepositoryObject = ([wmiclass]"root\VisualSVN\VisualSVN_Repository").CreateInstance()
    $RepositoryObject.Name = $Repo

    # Create the AD Object
    $ADObject = ([wmiclass]"root\VisualSVN\VisualSVN_WindowsAccount").CreateInstance()
    $ADObject.SID = $SID
}
```