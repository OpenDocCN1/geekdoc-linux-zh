
-   **All Files And Programs That Users Open From The Share Will Be Automatically Available Offline.** This option replaces the previously mentioned Automatic Caching Of Programs And Documents and the Automatic Caching Of Documents options. All files that have been previously opened in the shared folder are available for offline use.
-   **Files Or Programs From The Share Will Not Be Available Offline.** This option stops any files in a shared folder from being available offline. This setting is particularly useful in preventing users from storing files for offline use.

Group Policy allows administrators to define the behavior of offline files for users in an Active Directory domain. For example, in Windows XP, Windows Server 2003, and Windows Server 2008, all redirected folders are automatically cached by default. This default behavior can be changed by enabling the Do Not Automatically Make Redirected Folders Available Offline policy setting in the User Configuration\Policies\Administrative Templates\Network\Offline Files extension. When this policy setting is enabled, users must manually choose which files to cache for offline use. Figure 8-14 displays the available User Configuration node Group Policy settings for Offline Files. Note that most of the policy settings are available in both the User Configuration and Computer Configuration nodes of Group Policy.

### Figure 8-14
Configuring Offline Files in Group Policy

![](img/a8ee53dbf1310726255b6fbb9f296fb2_215_0.png)

> ⚠ **WARNING** Allowing users to choose the files they want to cache locally can be a security concern. In high-security networks, offline file caching is disabled to prevent the possibility of sensitive data leaving the corporate environment. Consider exploring policy settings such as At Logoff, Delete Local Copy Of Users Offline Files, and Prohibit User Configuration Of Offline Files.

## Using Disk Quotas

> **Use disk quotas** to limit the amount of space available on the server for user data. By implementing disk quotas when folder redirection is also configured, administrators can control the amount of information that is stored on the server. This is important for a couple of reasons. For example, when information is stored on a server, your backup strategy and the amount of resources that it takes to implement it must take into account the amount of data that needs to be backed up. Disk quotas can minimize the resources required in this regard.

Backup resources include the hardware involved, such as a tape backup device, and tapes or media to store the data. A network backup strategy usually takes into consideration the time required to back up information, the amount of media that is used, and the time it takes to restore the information if necessary. Considering all of this, disk quotas allow administrators to have control over the amount of information that is backed up for each user. When a disk quota limit is reached, the users cannot store additional data until their limit is increased or they clean up allocated space by deleting unnecessary files or archiving old files to make room for new data.

> **TAKE NOTE**
> If a user compresses a file using the compression utility in Windows 2000, Windows XP, Server 2003, or Server 2008, the original uncompressed size of the file is used to determine the amount of data utilizing quota space because Windows will need at least that amount of space to uncompress the file.

Disk quotas can be implemented manually through the Properties dialog box of a drive volume, as shown in Figure 8-15. This requires individual configuration of quotas for each volume that the administrator wishes to limit. The disk quota feature is only available on volumes formatted with the NTFS file system.

### Figure 8-15
Configuring disk quotas at the volume level

![](img/a8ee53dbf1310726255b6fbb9f296fb2_216_0.png)

Using Group Policy to configure disk quotas enables all NTFS volumes on all computers running Windows 2000, Windows XP, Windows Server 2003, Windows Vista, and Windows Server 2008 affected by the GPO to be configured with consistent disk quota settings. This policy setting is located in the Computer Configuration\Policies\Administrative Templates\System\Disk Quotas extension of a GPO. Figure 8-16 shows the available settings within this GPO extension.

### Figure 8-16
Configuring disk quotas using Group Policy

![](img/a8ee53dbf1310726255b6fbb9f296fb2_216_1.png)

The following list describes each policy setting within this GPO area:

-   **Enable Disk Quotas**. This setting enables or disables disk quota management on all NTFS volumes of computers affected by the GPO.
-   **Enforce Disk Quota Limit**. Enabling this setting enforces the space limitations designated by the Default Quota Limit and Warning Level setting for all users on the volume from that point forward. Existing files on the volume owned by the user are not counted against the user's quota limit. When a limit is set, the same limit applies to all users on all volumes. If this setting is not configured and disk quotas are enabled, users are able to write data to the volume until it is full. Allowing this to occur defeats the purpose of enabling disk quotas.
-   **Default Quota Limit And Warning Level**. This setting requires that the previous setting of Enforce Disk Quota Limit is enabled. This setting allows administrators to determine the space limitation and warning settings when the limit is reached.
-   **Log Event When Quota Limit Exceeded**. When enabled, this setting allows quota limit events to be logged to the Application log in Event Viewer. This setting requires that the Default Quota Limit and Warning Level setting is configured.
-   **Log Event When Quota Warning Level Exceeded**. When enabled, this setting writes an event to the Application log that indicates when a user is approaching the user's disk quota limits.
-   **Apply Policy To Removable Media**. This setting allows the policy settings to be applied to NTFS volumes located on removable media such as external drives.

When applying disk quotas to your network, careful planning of the necessary amount of disk space required by each user is very important. Realistic expectations of drive usage should be calculated. Because the Group Policy settings for disk quota enforce the same limits to all users, it is better to plan for a larger space limit than to inconvenience users who need more space with error messages stating that the drive is full. When disk quota policy changes are made, you need to restart the server for them to take effect.

## Maintaining and Optimizing Group Policy

> The final sections of this lesson will discuss the Group Policy refresh process, manual policy refresh procedures, and recommendations for policy settings to increase performance. This includes understanding and configuring the Group Policy refresh rate for member servers and domain controllers, as well as modifying the configuration of GPOs to optimize logon performance for your users and workstations.

Computer Configuration policies are applied by default when a computer starts up. User Configuration policies are applied during user logon. Both of these policies are also refreshed at regular points throughout the day. When a policy is refreshed, all settings are reprocessed, enforcing all of their policy settings. For example, settings that were previously enabled and are set to disabled are overwritten by the new setting and vice versa. In addition, settings that were previously enabled and set to Not Configured are simply ignored, leaving the setting in the registry unchanged. Each policy type has a default refresh cycle that takes place in the background to ensure that the most recent policy changes are applied, even if the system is not restarted or the user does not log off and back on. Although this is generally true, some policy settings will only process on initial startup or during user logon. For example, a policy that is used to install an application may interfere with another application's files for a program that is currently running on the user's computer. This could cause the installation to be incomplete or to fail. For this reason, software installation policies are only processed during computer startup. In addition, Folder Redirection policies are only processed during user logon. In the next sections, you will look at each policy type, the default refresh period, and where administrators can change the default refresh period.

-   **Computer Configuration Group Policy Refresh Interval**. The setting for the refresh interval for computers is located in the Computer Configuration\Policies\Administrative
