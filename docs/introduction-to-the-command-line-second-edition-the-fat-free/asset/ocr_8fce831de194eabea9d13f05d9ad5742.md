# mt

**Purpose:** Control tape devices.

**Usage syntax:** `mt -f [DEVICE] [OPERATION]`

```
# mt -f /dev/rmt0 rewind
Rewinding a tape using the mt command
```

The `mt` command controls removable tape devices. It can be used to display the status of the drive and manage its removable media. The example above demonstrates using the `mt` command to rewind the tape in the `/dev/rmt0` drive.

The following table lists the most common operations used with the `mt` utility.

| Operation | Function |
| :--- | :--- |
| `rewind` | Rewind the tape device |
| `retension` | Retension the tape |
| `erase` | Erase the tape |
| `status` | Display the tape device status |
| `offline` | Rewind and eject the tape |

Common mt operations

**Common usage examples:**

`mt -f [DEVICE] [OPERATION]` Execute the specified operation on a tape drive