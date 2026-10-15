

drive with its corresponding AutChanger resource. The Name also helps you remember which piece of equipment the resource describes.

The AlwaysOpen parameter tells Bacula to keep the device open unless an administrator explicitly requests an unmount. This option saves time and tape stress because it avoids rewinding and positioning operations between jobs.

```
Device {
  Name = TL4000-Drive0
  Media Type = LTO-3
  Archive Device = /dev/nst0
  AutomaticMount = yes
  AlwaysOpen = yes
  RemovableMedia = yes
  RandomAccess = no
  AutChanger = yes
}
```

## Aut changer resources

The optional AutChanger resource definition is only required if you are lucky enough to have a tape changer. It associates the storage devices to the aut changer and specifies the command that makes the changer swap tapes.

```
AutChanger {
  Name = TL4000
  Device = TL4000-Drive0,TL4000-Drive1
  Changer Command = "/etc/bacula/mtx-changer %c %o %S %a %d"
  Changer Device = /dev/changer
}
```

## bconsole.conf: console configuration

The console program communicates with the director to schedule jobs, check the status of jobs, or restore data. bconsole.conf tells the console how to communicate with the director. The parameters in this file must correspond to those given in the Director resource in the director's configuration file (bacula-dir.conf), with the exception of the Address parameter.

```
# Console configuration file, bconsole.conf

Director {
  Name = bull-dir
  DIRport = 9101
  Address = bull
  Password = "2HpScUnHN9"
}
```

## Installing and configuring the client file daemon

The file daemon installed on backup clients communicates with the Bacula storage daemon as backups and restores are executed. A file daemon must be installed and configured on every computer that is to be backed up with Bacula.

Bacula is available in binary form for many platforms, including Windows and various Linux distributions. On UNIX systems, you can install the file daemon from the original source tree by running `./configure --enable-client-only` followed by `make` and `make install`. You can hard-code defaults for many file daemon options at configuration time, but maintenance is easier if you just list them in your `bacula-fd.conf` file. By default, binaries are installed in `/sbin` and configuration files in `/etc/bacula`.

After installing the file daemon, configure it by editing `bacula-fd.conf`, which is broken into three parts. The first part consists of the Director resource, which tells the file daemon which director is allowed to schedule backups for this client. The Director resource also includes a Password parameter, which must be identical to the password listed in the Client resource in the director’s own configuration file.

The second part of the `bacula-fd.conf` file is the FileDaemon resource, which names the client and specifies the port on which the file daemon listens for commands from the director daemon.

The final component is the Messages resource (refer back to page 323), which defines how local messages are to be handled.

## Starting the Bacula daemons

With the server daemons installed and a test client configured, the next step is to fire up the daemons by running the startup script in the server’s installation directory (`/bacula start`). This same command is also used on each client to start the client’s file daemon.

The bacula startup script should be configured to run at boot time. Depending on your system and installation method, this may or may not be done for you. See Chapter 3, Booting and Shutting Down, for some additional details on how to start services at boot time on our example systems.

Once the daemons are running, you can use the console program (`bconsole` in the installation directory) to check their status, add media to pools, and execute backup and restore jobs. You can run `bconsole` from any computer as long as it has been properly installed and configured.

```
$ sudo ./bconsole
Connecting to Director bull:9101
1000 OK: bull-dir Version: 2.4.4 (23 December 2009)
Enter a period to cancel a command.
*
```

Use the console’s help command to see a list of the commands it supports.

## Adding media to pools

Before you can run a backup job, you need to label a tape and assign it to one of the media pools defined in the director’s configuration file. Use the console’s label command to write a software "label" to a blank tape and assign it to a Bacula pool.

