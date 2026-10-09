reproducible—the only thing that had to happen to recreate the issue was for a customer to log in to the system. I spent the rest of the day struggling to master serial consoles and core dumps.

The problem with the panic message on my envelope was that it gave only a tiny scrap of the story. It was so vague, in fact, that it was like describing a stolen car as “red, with a scratch on the fender.” If you don’t give the car’s make, model, VIN, and license plate number, you can’t expect the police to make much headway. Similarly, without much more information from your crashing kernel, the FreeBSD developers can’t catch the criminal code.

The good news is, panic handling has vastly improved since those days. FreeBSD can automatically record crash dumps and capture everything about a panic. There’s even a toggle in the installer to enable it. I highly recommend testing the panic capture before putting a machine into production, however. This way, if you get a panic, you’re ready and you’ll be able to easily file a complete problem report.

# ## Preperations

Configuring crash dumps requires telling FreeBSD which swap device to save the dump on, through the `dumpdev` /etc/rc.conf variable. If you set `dumpdev` to `AUTO`, the kernel will automatically save the dump to the first swap device. You can specify a different swap device if needed, but the whole dump must fit in a single swap device. If your regular swap space doesn’t have enough space to hold the dump, add a disk to get sufficient swap space and set `dumpdev` to that partition.

# ## The Crash Dump in Action

When a system configured to capture panics crashes, it saves a copy of the kernel memory. The copy is called a *dump*. The system can’t save the dump straight to a file. The crashed kernel doesn’t know anything about filesystems, for one thing, and the filesystem might be corrupt or a write could corrupt it. A crashed kernel understands partitions, however, so it can write the dump to a partition. Most FreeBSD hosts have readily