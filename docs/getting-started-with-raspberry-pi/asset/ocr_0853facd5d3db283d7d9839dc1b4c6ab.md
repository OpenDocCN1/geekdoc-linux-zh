+   1. Start the HCI and service discovery daemons:

```
bash-sharp> hcid
bash-sharp> sdpd
```

Because this device possesses a UART interface, you have to attach the BlueZ stack to the appropriate serial port. In this case, assume that `serial_cs` has allotted `/dev/ttyS3` to the card:

```
bash-sharp> hcitattach ttyS3 any
```

+   2. Verify that the HCI interface is up:

```
bash-sharp> hci1:  Type: UART
BD Address: 08:00:1F:10:3B:13 ACL MTU: 60:20  SCO MTU: 31:1
UP RUNNING PSCAN ISCAN
...
Manufacturer: Silicon Wave (11)
```

+   3. Verify that basic BlueZ modules are loaded:

```
bash-sharp> lsmod

Module        Size    Used by
hci_uart      16728   3
l2cap         26144   2
bluetooth     47684   6 hci_uart, l2cap
...
```

+   4. Insert the BlueZ module that implements network encapsulation:

```
bash-sharp> modprobe bnep
```

+   5. Listen for incoming PAN connections:[1]

```
bash-sharp> pand -s
```

On the laptop with the Belkin USB Bluetooth adapter

+   1. Start daemons, such as hcid and sdpd, and insert necessary kernel modules, such as `bluetooth.ko` and `l2cap.ko` .

+   2. Because this is a USB device, you don't need to invoke hcitattach, but make sure that the `hci_usb.ko` module is inserted.

+   3. Verify that the HCI interface is up:

```
Code View:
bash-belkin> hci1:  Type: USB BD Address: 00:02:72:B0:33:AB ACL MTU: 192:8  SCO MTU: 64:8
UP RUNNING PSCAN ISCAN
```