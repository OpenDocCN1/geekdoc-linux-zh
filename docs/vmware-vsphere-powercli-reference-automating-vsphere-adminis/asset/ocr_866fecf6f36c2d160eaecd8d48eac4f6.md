# CALLING VRO WORKFLOWS FROM POWERSHELL

```
[parameter (Mandatory=$true, ValueFromPipelinebyPropertyName=$true, 
ParameterSetName="C")
[parameter (ValueFromPipelinebyPropertyName=$true, ParameterSetName="D")
[parameter (ParameterSetName="E")]
ValidateNotNullOrEmpty())
[String] $ItemHref,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterName,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
[String] $ParameterValue,
```

```
[parameter (Mandatory=$false, ParameterSetName="A")
[parameter (ParameterSetName="C")
ValidateNotNullOrEmpty())
[String] $ParameterType,
```

```
[parameter (Mandatory=$false, ParameterSetName="B")
[parameter (ParameterSetName="D")
ValidateNotNullOrEmpty())
[String] $ParameterXML,
```

```
[parameter (Mandatory=$false, ParameterSetName="E")
ValidateNotNullOrEmpty())
[Switch] $NoParameters,
```

```
[parameter (Mandatory=$true)
ValidateNotNullOrEmpty())
[PSCredential] $Credential
}
```