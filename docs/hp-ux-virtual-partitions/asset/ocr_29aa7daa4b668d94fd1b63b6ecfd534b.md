device on which is l resides. Typically the device is identified by the Primary Boot Path that is maintained by pdc in Stable Storage. A path specification is an I/O subsystem mnemonic that varies according to hardware model.

When the processor is reset after initialization and self-test complete, pdc reads the Console Path from Stable Storage, and attempts to initialize the console device. If the initialization fails, pdc attempts to find and initialize a console device. Algorithms used to find a console device vary according to hardware model.

+   - If autoboot and autosearch (see is l (1M)) are enabled, pdc waits for approximately 10 seconds during which time the operator can override the autoboot sequence pressing and holding the ESC (escape) key on the console.

The system then begins a search for potentially bootable devices. If allowed to complete, a list of potentially bootable devices is displayed, labeled with abbreviated path identifiers (P0, P1, etc.). A simple menu is then displayed where the user can:

+   - Boot a specific device, using the abbreviated path identifier, or the full $Anomic.$
+   - Start a device search where the contents are searched for IPL images (note the first search only identified devices and did not check the contents)
+   - Enter the boot administration level.
+   - Exit the menu and return to autobooting
+   - Get help on choices

The search of potentially bootable devices can be aborted by pressing and holding the escape key. The search for device contents can also be aborted by pressing and holding the escape key.

If the operator does not interrupt the search process, pdc initializes and reads is l from the Primary Boot Path.

If the autoboot sequence is unsuccessful, overridden by the operator, or not enabled in the first place, pdc executes the device search and enters the menu described above.

The Primary Boot, Alternate Boot, and Console Paths as well as autoboot and autosearch enable can be modified via is l or at the pdc boot administration level.

**SEE ALSO**
boot(1M), hpxu boot(1M), is l(1M).