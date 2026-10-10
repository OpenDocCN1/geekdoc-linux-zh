
make_net_recovery -s myserver -x inc_entire=vg00

Create a system recovery archive that includes all of the vg00 and vg01 volume groups, but that excludes the /depots directory.

make_net_recovery -s myserver -x inc_entire=vg00 -x inc_entire=vg01 -x exclude=/depots

Below is an example shell script that can be run on each client. It can help you to keep from ever having to update Ignite-UX on each client when a new release is loaded on the server. It will automatically update the network recovery software if the server has a newer version. It may be suitable for use in a crontab entry. This example assumes that the /var/opt/ignite/deposits/recovery_cmds software depot has been created. This depot is created by running ignite OQI at least once to make a recovery archive of a system (see also pkg_rec_depot(1W)). Once created, this depot will automatically be updated each time Ignite-UX is updated on the server.

```bash
myserver=luxserver
/opt/ignite/bin/check_version -s $myserver
if [ $? != 0 ]
then
    swinstall -s
    $myserver:/var/opt/ignite/deposits/recovery_cmds `*`
fi
/opt/ignite/bin/make_net_recovery -s $myserver
```

## WARNINGS

### Disks Will be Reformatted

If any files from a disk or volume group is included in the recovery archive, that disk (or all disks in the volume group) will be reformatted during the recovery, and only the files included will be recovered. Any files that were not included in the archive, will have to be restored from your normal backups.

Disks and volume groups that did not have any files included in the archive are not reformatted during a recovery and are re-imported and re-mounted at the end of the recovery.

### Logical Volume Physical Extent Allocation Not Preserved

The make_net_recovery tool captures enough information from the system so that during a recovery it can reconstruct most all visible aspects of the prior LVM configuration. This includes logical volume and volume group names, attributes, and even minor number values. The tool also ensures that the new logical volumes reside on the same disks within the volume group as they did before.

make_net_recovery does not, however, ensure that logical volumes are extended in the same exact order as they were originally. This means the LVM physical extents allocated to a logical volume may be in a different location on the disk than before. The recovery tools use a very specific and complex algorithm for extending logical volumes to ensure success (such as extending contiguous volumes before non-contiguous). An example effect of this is that swap/dump volumes will reside on the root disk ahead of some other volumes even though that may not have been the original layout.

### VxVM disk groups not included

The disk groups managed by VERITAS Volume Manager (VxVM) cannot be included in the Ignite-UX archive. If they are included, make_net_recovery will error out. Those disk groups will be left undisturbed and re-integrated to the system after the recovery is complete.

### LVM Disk Mirrors not Restored

The make_net_recovery tool will create a recovery backup for a system with mirrored disks but it will not restore the mirrored disk configuration. If the system is later recovered, previously mirrored volumes will no longer be mirrored. They can be manually re-mirrored after the system is up. Using the config.local file in the clients directory, you can specify the LVM commands to restore mirrored disks to be executed automatically after the system has been restored. For more details, see the white paper /opt/ignite/share/doc/diskmirror.pdf.

## DEPENDENCIES

The Ignite-UX GUI must be run from the Ignite-UX Server. See Ignite(5). make_net_recovery depends on several other Ignite-UX tools. When running the Ignite-UX server GUI, Ignite-UX checks whether the client system, that make_net_recovery runs on, has the same versions of Ignite-UX tools.

If running make_net_recovery from the command line without ever interacting with the Ignite-UX GUI, commands will need to be installed using swinstall(1M) from the Ignite-UX server to the client system that make_net_recovery will run on.

## AUTHOR

Ignite-UX and make_net_recovery were developed by the Hewlett-Packard company.

## DIAGNOSTICS

All major steps within network recovery are logged on the server and displayed via the Ignite-UX Server GUI.

## FILES

- **/opt/ignite/recovery/mr_essentials** Lists the files and directories that are considered essential and are always included in the archive if they exist on the system.

- **/var/opt/ignite/recovery/mr_essentials** lists the files and directories that are essentials, but actual the user modifiable version, so that the original mr_essentials file can be maintained. When this file exists, its contents are checked before the file /opt/ignite/recovery/mr_essentials.

- **/var/opt/ignite/clients/0x[LLA]/CIMDex** This file contains a list of Ignite-UX configurations that are specific to the particular client with a network LAN link address (LLA) as shown in the path. This file supplies Ignite-UX with the config files created by make_net_recovery and provides a list of client-specific selections a user can pick from during a system recovery.

- **/var/opt/ignite/clients/0x[LLA]/recovery** The per-clients recovery directory. It holds the client's recovery configuration files as described below.

- **/var/opt/ignite/clients/0x[LLA]/recovery/defaults** Supplies the default options to make_net_recovery. Created by the Ignite GUI.

- **/var/opt/ignite/clients/0x[LLA]/recovery/archive_content** Supplies files and directories to be included or excluded. Using the -x command line arguments will cause this file to be ignored.

- **/var/opt/ignite/clients/0x[LLA]/recovery/client_status** File used to communicate the status of the make_net_recovery command back to the Ignite GUI running on the Ignite-UX server.

- **/var/opt/ignite/clients/0x[LLA]/recovery/latest** A symlink to the <date_time> directory containing the newest set of recovery files as described below.

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>** Directory containing files pertaining to the make_net_recovery command that was run at the date and time indicated in the directory name. An example path looks like: /var/opt/ignite/clients/0xd0000192486/1999-12-20,13:50

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/system_cfg** Configuration file which describes the file system and networking configuration of the system (generated by the save_config(M) command).

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/archive_cfg** Configuration file which supplies the location and access method to the archive containing the files to be restored.

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/control_cfg** Configuration file which supplies control parameters and the command scripts to import volume groups that will be preserved and not created during the recovery.

- **/var/opt/ignite/clients/0x[LLA]/recovery/config.local** An optional config file that the user may create to add configuration information to be used during the recovery of the client. For example, you may want to add to this file a post_config.cmd to re-mirror disks that the recovery process un-mirrored. (See the document: /opt/ignite/share/doc/diskmirror.pdf for an example). Once this file is created, make_net_recovery will automatically add it to any new configurations that it adds to the CINDBX file.

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/recovery.log** Default logfile location for make_net_recovery.

- **/var/opt/ignite/clients/0x[LLA]/recovery/<date_time>/manifest** Software and Hardware manifest information installed and configured for the system at the time the archive was created (See print_manifest(M)).

- **/var/opt/ignite/recovery/archives/<hostname>** The default location on the Ignite-UX server for the client to store the recovery archive. The <hostname> directory must be NFS exported to the individual client with the matching hostname.
