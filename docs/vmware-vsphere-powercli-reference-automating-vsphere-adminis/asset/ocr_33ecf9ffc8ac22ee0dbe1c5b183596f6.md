# LISTING 13.6 Reporting and updating standard switch/port group security policies

## Assess in more straightforward manner than the hardening guide:
Get-VMHost | Get-VirtualSwitch -Standard | Get-SecurityPolicy

```
VirtualSwitch AllowPromiscuous ForgedTransmits MacChanges
-------------------------------------------------------------
vSwitch0 False True True
vSwitch1 False True True

Get-VMHost | Get-VirtualSwitch -Standard | Get-VirtualPortGroup |
Get-SecurityPolicy

VirtualPortGroup AllowPromiscuous ForgedTransmits MacChanges
-------------------------------------------------------------
MgmtNet0 False True True
dNet0 False True True
VESXiNet0 True True True
```

## remediate
Get-VMHost | Get-VirtualSwitch -Standard | Get-SecurityPolicy |
Set-SecurityPolicy -AllowPromiscuous:$false -ForgedTransmits:$false \
-MacChanges:$false

```
VirtualSwitch AllowPromiscuous ForgedTransmits MacChanges
-------------------------------------------------------------
vSwitch0 False False False
vSwitch1 False False False

Get-VMHost | Get-VirtualSwitch -Standard | Get-VirtualPortGroup |
Get-SecurityPolicy | Set-SecurityPolicy -AllowPromiscuousInherited:$true \
-ForgedTransmitsInherited:$true -MacChangesInherited:$true
```