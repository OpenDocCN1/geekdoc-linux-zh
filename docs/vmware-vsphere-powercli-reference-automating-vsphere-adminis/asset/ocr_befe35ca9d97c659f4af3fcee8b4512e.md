# CHAPTER 13 • HARDENING THE VSPHERE ENVIRONMENT

from a VMHost should be blocked. You can verify VMHosts' default firewall policy
by using this:

```
Get-VMHostvMixty0[56].dom.int | Get-VMHostFirewallDefaultPolicy

IncomingEnabled OutgoingEnabled

False            False
False            False
```

Should you ever need to configure ESXi host's firewall default policy, you could use something like the following code. This example assumes that someone changed the default firewall policies on the given VMHosts to $true at some point, and shows the resulting DefaultPolicy values are at $false:

```
Get-VMHostFirewallDefaultPolicy -vMixty0[56].dom.int |
Set-VMHostFirewallDefaultPolicy -AllowIncoming $false

IncomingEnabled OutgoingEnabled

False            False
False            False
```

The Hardening Guide has an assessment command example that allows you to get the current VMHost firewall exceptions using the Get-VMHostFirewallException cmdlet. You can use the Set-VMHostFirewallException cmdlet when you need to change an exception. For example, suppose that it is time to use Network Time Protocol (NTP) to synchronize the clocks in your environment around the network. You have used the Set-VMHostService cmdlet to set the policy of the network, but you need to enable a firewall exception for the related NTP communications. The following will enable the NTP exceptions on given VMHosts:

```
Get-VMHost vMixty0[56].* Get-VMHostFirewallException -Name "NTP Client" |
Set-VMHostFirewallException -Enabled:$true
```

| Enabled | IncomingPorts | OutgoingPorts | Protocols | ServiceRunning |
| --- | --- | --- | --- | --- |
| NTP Client | True | 123 | UDP | True |
| NTP Client | True | 123 | UDP | True |