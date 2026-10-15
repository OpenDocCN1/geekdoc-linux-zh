
The following lists the possible variables in a device configuration file:

## Table 3-1

| Variable | Description |
|---|---|
| STARTMODE | This determines when and how a device will be started: <br> - **auto.** The device is automatically started at boot time or by udev when the device is connected to the system. <br> - **manual.** The device should not be started automatically, but it can be started manually. <br> - **off.** The device should never be started. |
| MODULE | The value of this variable determines the name of the kernel module that should be loaded for the device. <br> If multiple modules have to be loaded, you can use this variable multiple times with any suffix appended. <br> You must then use the same suffixes for multiple MODULE_OPTIONS variables. <br> Example: <br> **MODULE_A="foo"** <br> **MODULE_B="bar"** <br> **MODULE_OPTIONS_A="foo-opt"** <br> **MODULE_OPTIONS_B="bar-opt1=x yz"** |
| MODULE_OPTIONS | With this variable, options can be passed to the kernel module. |

### (continued) Table 3-1

| Variable | Description |
|---|---|
| SCRIPT{UP,DOWN}_[type] | This specifies the script to be called for initialization and deconfiguration of a specific device type. <br> This script is called if the type of the device to be initialized matches the type given in this parameter. |
| SCRIPT{UP,DOWN} | This specifies the script to be called for initialization and deconfiguration of the device. <br> It will be called only if no matching type-specific scripts are configured. |

The following is an example of a configuration file for a network adapter:

```
MODULE='e100'
MODULE_OPTIONS=''
STARTMODE='auto'
```

The module e100 is loaded, there are no options for this module and the device is started automatically at boot time.

The hwup command is usually called by udev, but you can also use it manually. For example, the following command starts the network card shown in the previous:

```
hwup bus-pci-0000:02:08.0
```

The last 3 elements of the configuration filename specify the device.

You can use the command hwdown to deconfigure devices, as in the following:

```
hwdown bus-pci-0000:02:08.0
```

## From sysfs

When there is no configuration file for a device under /etc/hardware, hwup uses sysfs to find out more about the required driver.

In the file /sys/bus/devices/<pci_device_id>/modalias a unique id for a device can be found. The following is the content of the file modalias for a network adapter:

```
pci:v00008086d00001039sv00001734sd00001001bc02sc00i00 ....
```

Now udev calls the command modprobe and uses the modalias as parameter.

The file /lib/modules/<kernel_version>/modules.aliases contains a list with modalias IDs and their corresponding kernel driver modules. The information about which driver module handles which modalias ID is included in the source files of the modules. The command depmod is used to extract the information from the modules and to write them into the file modules.aliases.

Therefore you can consider the file modules.aliases as a kind of driver database, which is used to find out, which device is handled by which driver.

When called from udev with the modalias parameter, modprobe looks for the driver in modules.aliases and load the associated driver.

To prevent udev/hwup/modprobe from loading a driver automatically in the described way, a driver can be entered in the file /etc/modprobe.d/blacklist. By default the ALSA sound drivers are for example entered here, because these drivers are loaded by the ALSA init script (alsasound).

## Exercise 3-3 Explore Hardware Initialization

In this exercise, you learn how to shutdown a device with hwdown and how to start it again manually. The exercise consists of the following parts:

- Part I: Stop the Ethernet Adapter with hwdown
- Part II: Unload the Driver Module
- Part III: Load the Driver Module with a modalias

### Part I: Stop the Ethernet Adapter with hwdown

Do the following:

- 1. Open a terminal window and su- to the root user.
- 2. Enter the command ip a. You should see a list with your network interfaces. (At least eth0).
- 3. Enter the command lspci.
- 4. Look for a device with the description Ethernet controller and note the PCI ID of this device below this step. If you have more than one ethernet adapter, choose the first one
- 5. Enter the command:
  hwdown bus-pci-0000:<network_adapter_pci_id>
- 6. Enter the command ip a again. The interface of the device which has been shutdown with hwdown should not be visible anymore.

### Part II: Unload the Driver Module

- 1. Change into the directory /etc/sysconfig/hardware/.
