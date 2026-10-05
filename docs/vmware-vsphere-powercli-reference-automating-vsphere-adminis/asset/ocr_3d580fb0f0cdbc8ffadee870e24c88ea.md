# CHAPTER 10 • USING VAPPS

```
vApp               : App01
StartOrder         : 3
StartDelay          : 120
WaitingGuest       : False
StartAction        : powerOn
StopDelay          : 120
StopAction         : powerOff
DestroyWithParent  : False
```

By default a vApp powers on and off based on the order in which the VMs were added. This will likely not be the desired order. To adjust these settings, use the Set-vAppStartOrder function (Listing 10.11).

# LISTING 10.11 The Set-vAppStartOrder function

```
. SYNOPSIS
Set the vApp Startup Order for a given VM
.DESCRIPTION
Set the vApp Startup Order for a given VM
.PARAMETER VM
VM to modify the startup order for.
.PARAMETER StartOrder
Specifies the start order for this entity. Entities are started from lower numbers to higher-numbers and reverse on shutdown. Multiple entities with the same start-order can be started in parallel and the order is unspecified. This value must be 0 or higher.
.PARAMETER StartDelay
Delay in seconds before continuing with the next entity in the order to be started
.PARAMETER WaitingForGuest
Determines if the virtual machine should start after receiving a heartbeat, from the guest. When a virtual machine is next in the start order, the system either waits a specified period of time for a virtual machine to power on or it waits until it receives a successful heartbeat from a powered virtual machine. By default, this is set to false
.PARAMETER StartAction
```