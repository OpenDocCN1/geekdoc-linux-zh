
## 11. Managing RHEL 9 systemd Units

To gain proficiency in RHEL 9 system administration, it is essential to understand the concepts of systemd units with a particular emphasis on two specific types known as targets and services. This chapter aims to provide a basic overview of the different systemd units supported by RHEL 9 combined with an overview of how to configure the many services that run in the background of a running Linux system.

### 11.1 Understanding RHEL 9 systemd Targets

RHEL 9 can be configured to boot into one of several states (referred to as targets), each designed to provide a specific level of operating system functionality. The system administrator configures the target to which a system will boot by default based on the purpose for which the system is being used. A desktop system, for example, will likely be configured to boot using the graphical user interface target. In contrast, a cloud-based server system would be more likely to boot to the multi-user target level.

During the boot sequence, a process named systemd looks in the /etc/systemd/system folder to find the default target setting. Having identified the default target, it proceeds to start the systemd units associated with that target so that the system boots with all the necessary processes running.

For those familiar with older RHEL versions, systemd targets replace the older runlevel system.

### 11.2 Understanding RHEL 9 systemd Services

A service is a process, typically running in the background, that provides specific functionality. The sshd service, for example, is the background process (also referred to as a daemon) that provides secure shell access to the system. Different systemd targets are configured to automatically launch different collections of services, depending on the functionality to be provided by that target.

Targets and services are types of systemd unit, a topic that will be covered later in this chapter.

### 11.3 RHEL 9 systemd Target Descriptions

As previously outlined, RHEL 9 can be booted into one of several target levels. The default target to which the system is configured to boot will, in turn, dictate which systemd units are started. The targets that relate specifically to system startup and shutdown can be summarized as follows:

- **poweroff.target** - This target shuts down the system. It is unlikely you would want this as your default target.
- **rescue.target** – Causes the system to start up in a single-user mode under which only the root user can log in. The system does not start any networking, graphical user interface, or multi-user services in this mode. This run level is ideal for system administrators to perform system maintenance or repair activities.
- **multi-user.target** - Boots the system into a multi-user mode with text-based console login capability.
- **graphical.target** - Boots the system into a networked, multi-user state with X Window System capability. By default, the graphical desktop environment will start at the end of the boot process. This is the most common run level for desktop or workstation use.
- **reboot.target** - Reboots the system. Another target that, for obvious reasons, you are unlikely to want as your default.

In addition to the above targets, the system includes about 70 other targets, many of which are sub-targets used by the above main targets. Behind the scenes, for example, *multi-user.target* will also start a target named *basic.target* which will, in turn, start the *sockets.target* unit, which is required for communication between different processes. This ensures that all the services on which the multi-user target depends are also started during the boot process.

A list of the targets and services on which a specified target is dependent can be viewed by running the following command in a terminal window:

```bash
# systemctl list-dependencies <target>
```

Figure 11-1, for example, shows a partial listing of the systemd unit dependencies for the graphical target (the complete listing contains over 140 targets and services required for a fully functional multi-user system):

```
[demo@rhel-server ~]$ systemctl list-dependencies graphical.target
graphical.target
●─accounts-daemon.service
●─gdm.service
○─nvmefc-boot-connections.service
●─power-profiles-daemon.service
●─rtkit-daemon.service
●─switcheroo-control.service
○─systemd-update-utmp-runlevel.service
●─udisks2.service
●─upower.service
●─multi-user.target
●─atd.service
●─auditd.service
●─avahi-daemon.service
●─chronyd.service
```

Figure 11-1

The listing is presented as a hierarchical tree illustrating how some dependencies have sub-dependencies of their own. Scrolling to the bottom of the list, for example, would reveal that the graphical target depends on two network filesystem related targets (namely *nfs-client.target* and *remote-fs.target*), each with its own service and target sub-dependencies:

![](img/be1f159c3cc937d7b264dc5b134856dc_97_0.png)

Figure 11-2

The colored dots to the left of each entry in the list indicate the current status of that service or target as follows:

- **Green** - The service or target is active and running.
- **White** - The service or target is inactive (dead). Typically because the service or target has yet to be enabled, has been stopped for some reason, or a condition on which the service or target depends has not been met.
- **Red** - The service or target failed to start due to a fatal error.

To find out more details about the status of a systemd unit, use the systemctl status command followed by the unit name as follows:

```
# systemctl status systemd-machine-id-commit.service
○ systemd-machine-id-commit.service - Commit a transient machine-id on disk
    Loaded: loaded (/usr/lib/systemd/system/systemd-machine-id-commit.service; static)
    Active: inactive (dead)
    Condition: start condition failed at Thu 2023-03-30 08:41:05 EDT; 16min ago
      └─ ConditionPathIsMountPoint=/etc/machine-id was not met
    Docs: man:systemd-machine-id-commit.service(8)
```

### 11.4 Identifying and Configuring the Default Target

The current default target for a RHEL 9 system can be identified using the systemctl command as follows:

```
# systemctl get-default
multi-user.target
```

The system is configured to boot using the multi-user target by default in the above case. The default setting can be changed anytime using the systemctl command with the set-default option. The following example changes the default target to start the graphical user interface the next time the system boots:

```
# systemctl set-default graphical.target
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target.
```

The output from the default change operation reveals the steps performed in the background by the systemctl command to implement the change. The current default is configured by establishing a symbolic link from the default.target file located in /etc/systemd/system to point to the corresponding target file located in the /usr/lib/systemd/system folder (in this case the graphical.target file).

### 11.5 Understanding systemd Units and Unit Types

As previously mentioned, targets and services are both types of systemd unit. All the files within the /usr/lib/systemd/system folder are referred to as systemd unit configuration files, each representing a systemd unit. Each unit is, in turn, categorized as being of a particular unit type. RHEL 9 supports 12 different unit types, including the target and service unit types already covered in this chapter.

The type of a unit file is represented by the filename extension as outlined in Table 11-1 below:

| Unit Type | Filename Extension | Type Description |
|---|---|---|
| Service | .service | System service. |
| Target | .target | Group of systemd units. |
| Automount | .automount | File system auto-mount point. |
| Device | .device | Device file recognized by the kernel. |
| Mount | .mount | File system mount point. |
| Path | .path | File or directory in a file system. |
| Scope | .scope | Externally created process. |
| Slice | .slice | Group of hierarchically organized units that manage system processes. |
| Snapshot | .snapshot | Saved state of the systemd manager. |
| Socket | .socket | Inter-process communication socket. |
| Swap | .swap | Swap device or a swap file. |
| Timer | .timer | Systemd timer. |

Table 11-1

Note that the target unit type differs from other types in that it comprises a group of systemd units
