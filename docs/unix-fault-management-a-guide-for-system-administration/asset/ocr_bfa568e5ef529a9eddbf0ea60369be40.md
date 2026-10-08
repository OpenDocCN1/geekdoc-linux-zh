For example, critical disk events from a disk EMS Hardware Monitor cause the PSM to change the device's status to DOWN. The PSM then sends a single "disk device status = down" event, if a user had requested that event. This may be the only message visible to the user. Additional disk failure messages would not be forwarded, because they did not result in a status change (in other words, the status remained DOWN). This reduces the number of events that need to be processed by the user. The last event received should reflect the current device status.

Most of the Hardware Monitors can't automatically detect when a device has been fixed. When a problem is solved, the set_fixed command must be used to alert the PSM manually to set the device status back to UP.

When using an enterprise management tool such as IT/O, which receives messages from multiple systems, you should use the PSM to reduce information overload. However, make sure that stateless events are also configured to go somewhere (such as the system log file), because they provide valuable diagnostic information when a component has failed.

You can learn more about the Hewlett-Packard diagnostic tools on its Web site at http://docs.hp.com/hpux/systems/.

# HARAYMON and ARRAYMOND

The High Availability Disk Array Monitor (HARAYMON), available on HP-UX 9.x, notifies the system console of all failures of disk array FRUs in high availability disk array products. AutoRAID disk arrays have a similar monitor, called ARRAYMOND. Failures are reported to the system console and to a user-identified list of e-mail addresses (configured in an ASCII file. Each error message can optionally include the location of the array(s) connected to the host system, the event history of the array(s) connected to the host system, and the system administrator's phone number or mail stop.

Listings 5-10 and 5-11 show some messages displayed by HARAYMON for various error conditions. HARAYMON can detect disk failures, fan unit failures, controller module failures, power supply unit failures, and battery backup unit failures.

Listing 5-10 shows a disk module failure. Note that in addition to a timestamp and the failure type being displayed, the array and slot number (within the array) containing the failed device are also reported. The array containing the failed disk module is 48.0.1, and the slot number containing the failed disk is B2.

> Listing 5-10 Output from HARAYMON showing disk module failure.

```
===========================================
Mon Nov 23 10:58:50 PST 1998
High Availability Array Monitor
===========================================
Drive Failure
Product ID HP A3232A_RAID_5
Physical Device 48.0.1
Disk Position: B2
```