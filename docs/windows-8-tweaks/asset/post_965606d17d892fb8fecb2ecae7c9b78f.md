
## 4. Without closing the new folder you just opened, Open the Start screen again and then run File Explorer. Navigate to the Local Disk (C:) drive again and to the Windows folder, and then to the Fonts folder.

## 5. Now that you have both the Fonts folder and your backup folder open, arrange the two windows on your screen so that they look like the two windows in Figure 13-7.

![](img/ea75090cfee8ac890f64c8c4f62f7285_242_0.png)

Figure 13-7: Arrange the Windows Fonts folder and a backup folder side by side on the screen.

## 6. Now that the two font folders are side by side, drag the fonts you want to back up to your backup folder.

## 7. After you have backed up the fonts you want to delete, right-click the font files in the Fonts folder and click Delete.

In the event that you want to reinstall a font, all you have to do is drag the font file from the backup folder back to the Fonts folder. An Installation dialog box flashes on the screen as it adds the font back to the library. After you drag the file back to the Fonts folder, the file remains in the backup directory because it just copies it there. After you have confirmed that it was actually installed, feel free to delete the font file from the backup folder.

# Disabling Unneeded Services

A service is a software application that runs continuously in the background while your computer is on. The Windows operating system has numerous services that run in the background that provide basic functions to the system. Network connectivity, visual support, and external device connectivity such as printer services are all examples of the types of services that the Windows services provide. Each service that is running in the background takes up system resources, such as memory and CPU time. Also, during the booting of the operating system, the service has to be loaded. On most computers, nearly 20 services are loaded upon startup. Of these 20 services, only a handful are system critical services; all the others can be disabled.

Disabling a service can disable a feature that you or applications installed on your PC depend on so it is important to know what the services in Windows 8 do. Table 13-2 will help you understand what the most common services are, what they do, and whether they can be disabled.

Table 13-2: Common Windows Services in Use

| NAME | USE |
| --- | --- |
| ActiveX Installer | Provides UAC validations for Internet-based ActiveX installs. This only runs when needed. |
| Application Experience | Provides a compatibility cache for older applications that caches requests when they are run. This service can be disabled, but I recommend leaving it started for application compatibility with the new architecture of Windows 8. |
| Application Identity | Verifies the identity of an application. Used by AppLocker. Does not run unless AppLocker is in use. |
| Application Information | Allows you to run applications with all administrative rights. Keep this service running. |
| Application Layer Gateway | Provides support for additional protocols for the Internet Connection Sharing service. You can safely disable this service. |
| Application Management | Used for software deployment and management through Group Policy. If you do not use Group Policy for software, you can safely disable this service. |
| Background Intelligent Transfer | Transfers data in the background when the connection is not in use. One use of this service is to download updates automatically in the background. This service is not system critical, but disabling it can impair other services such as Windows Update. I would keep this service enabled. |
| Base Filtering Engine | Provides support for the firewall, IPsec, and filtering. I recommend keeping this service running. |
| BitLocker Drive Encryption Service | Provides critical support for BitLocker drive encryption. Only disable if you are not using BitLocker. |
| Block Level Backup Engine Service | Used by Windows Backup. Disabling would disable the backup and recovery operations of Windows Backup. |
| Bluetooth Support Service | Provides support for Bluetooth wireless devices. Disable this service if you do not use Bluetooth devices with your computer. |
| BranchCache | Provides a local cache of a remote file share in a branch office. Disable if you are a home user and have not configured BranchCache. |
| Certificate Propagation | Utilizes certificates from smart cards. Most home users have no use for this service. |
| CNG Key Isolation | Isolates cryptographic operations to protect the cryptographic key. I recommend leaving this service as is because it runs only when needed. |
| COM+ Event System | Provides event notification to COM objects. Some applications depend on this service. I recommend experimenting with your applications to see whether you can disable it. |
| COM+ System Application | Used to configure and monitor COM object components. Leave as manual because it is started only when needed. |
| Computer Browser | Responsible for keeping the list of computers on your network and updating the list. If you have no need for this information, you can safely disable it if started. |
| Credential Manager | Provides secure storage and retrieval of passwords. This service runs only when needed and I would not disable it. |
| Cryptographic Services | The main provider of all encryption and decryption operations for all types of applications. It manages private keys, certificates, and other encryption operations. I recommend leaving this service running. |
| DCOM Server Process Launcher | Starts DCOM processes. Several other system-critical services use this service to start, so I do not recommend disabling. |
| Device Association Service | Provides the functionality to pair with various wired and wireless devices. I recommend leaving this service enabled. |
| Device Install Service | Allows your computer to detect and install detected hardware. I do not recommend disabling. |
| Device Setup Manager | Provides the ability to download and install device-related software upon detection. I do not recommend disabling. |
| DHCP Client | Provides automatic network address configuration. If you set a static IP address, gateway, and DNS servers, disable this service. |
| Diagnostic Policy | Provides automatic problem monitoring and troubleshooting of components. If this service is disabled, automatic diagnostics and searching for resolutions will be stopped. If you are an advanced user, you might be able to get away with disabling this service. |
| Diagnostic Service Host | Assists Diagnostic Policy service listed above. |
| Diagnostic System Host | Assists Diagnostic Policy service listed above. |
| Distributed Link Tracking Client | Used with NTFS file links across networks. If you have no need for this service, and not many do, you can safely disable it. |
| Distributed Transaction Coordinator | Provides support for managing transactions generated by applications. Some applications use this service, but it is not running unless it is in use. |
| DNS Client | Enables the computer to resolve a DNS address such as Tweaks.com to an IP address as needed by web browsers and other Internet tools. Unless your computer is not connected to the Internet or any other type of network, you should keep this service enabled. |
| Encrypting File System (EFS) | Provides filesystem encryption support. If disabled, you will not be able to enable or access any NTFS encrypted files. |
| Extensible Authentication Protocol | Provides authentication support to the Wired AutoConfig and WLAN AutoConfig services. Unless you use all manual network configurations, leave this service enabled. |
| Family Safety | Windows Parental Control functionality from Windows Vista. If you never used those features, disable it. |
| Fax | Provides support to send and receive faxes. No need for faxes? Disable this service. |
| File History Service | Protects your personal files from accidental deletion or changes by allowing you to go back in time. I do not recommend disabling this service. |
| Function Discovery Provider Host | Hosts other services that search the network for other devices such as the Media Center Extender service. If you have no need for these services, disable it. |
| Function Discovery Resource Publication | Allows this computer and devices connected to it to be published over the network so that other computers on your LAN can share them. This can be disabled but may affect usability. |
| Group Policy Client | Responsible for applying local and domain-based Group Policy settings and restrictions. This service cannot be disabled in Windows 8. |
| Health Key and Certificate Management | Manages the keys used by Network Access Protection. Disable this if your network is not using any sort of authentication-based access. |
| HomeGroup Listener | Provides basic HomeGroup client services. Disable if you do not use HomeGroups. |
| HomeGroup Provider | Provides basic HomeGroup server services. Disable if you do not use HomeGroups. |
| Human Interface Device Access | Supports Human Interface Devices (HID) expanded functionality such as additional buttons on a keyboard, remote controls, and more. Do not disable. |
| IKE and AuthIP IPsec Keying Modules | Manages the keys used by IP Security (IPsec) network access. Disable this if your network is not using any sort of authentication-based network access. |
| Interactive Services Detection | Provides notification and access to interactive dialog boxes. Do not disable this service. |
