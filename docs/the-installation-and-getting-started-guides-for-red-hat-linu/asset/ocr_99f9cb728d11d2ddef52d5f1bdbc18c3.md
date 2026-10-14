√ none — No boot-time protocol should be used.
√ bootp — The bootp protocol should be used.
√ dhcp — The dhcp protocol should be used.

The following values are common to all PPP and SLIP files:

+   - **PERSIST**=*answer*, where *answer* is one of the following:
+     - √ yes — This device should be kept active at all times, even if deactivated after a modem hangup.
+     - √ no — This device should not be kept active at all times.

+   - **MODEMPORT**=*port*, where *port* is the modem port's device name (for example, "*/dev/modem").

+   - **LINESPEED**=*baud*, where *baud* is the modem's linespeed (for example, "115200").

+   - **DEFABORT**=*answer*, where *answer* is one of the following:
+     - √ yes — Insert default abort strings when creating/editing the script for this interface.
+     - √ no — Do not insert default abort strings when creating/editing the script for this interface.

The following values are common to all PPP files:

+   - **DEFROUTE**=*answer*, where *answer* is one of the following:
+     - √ yes — Set this interface as the default route.
+     - √ no — Do not set this interface as the default route.

+   - **ESCAPECHARS**=*answer*, where *answer* is one of the following:
+     - √ yes — Use the pre-defined asyncmap.
+     - √ no — Do not use the pre-defined asyncmap

(This represents a simplified interface; it doesn't let people specify which characters to escape. However, almost everyone can use an asyncmap of 00000000 anyway, and it's possible to set PPPOPTIONS to use an arbitrary asyncmap if so desired.)