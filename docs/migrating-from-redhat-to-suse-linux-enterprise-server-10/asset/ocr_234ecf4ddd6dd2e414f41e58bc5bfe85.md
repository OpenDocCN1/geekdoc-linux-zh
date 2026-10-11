+   □ **Ignore.** Sometimes you want to have the system ignore this keystroke combination, especially when the system serves as both workstation and server. Nothing happens when the **Ctrl+Alt+Del** keystroke combination is pressed.
+   
+   □ **Reboot.** The system reboots when the **Ctrl+Alt+Del** keystroke combination is pressed.
+   
+   □ **Halt.** The system is shut down when the **Ctrl+Alt+Del** keystroke combination is pressed.

+   ■ **Shutdown Behavor of KDM.** You use this option to set who is allowed to shut down the computer from KDM.
+   
+      □ **Only Root.** To halt the system, the root password has to be entered.
+   
+      □ **All Users.** Everyone, even remotely connected users, can halt the system using KDM.
+   
+      □ **Nobody.** Nobody can halt the system with KDM.
+   
+      □ **Local Users.** Only locally connected users can halt the system with KDM.
+   
+      □ **Automatic.** The system is halted automatically after log out.

For a server system you should use **Only Root** or **Nobody** to prevent normal or even remote users from halting the system