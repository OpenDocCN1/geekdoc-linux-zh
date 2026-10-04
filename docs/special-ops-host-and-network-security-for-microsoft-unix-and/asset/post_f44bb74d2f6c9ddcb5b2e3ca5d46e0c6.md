
Analysis object in the left-hand pane, and choose Configure Computer Now, as shown in Figure 5.16.

## Figure 5.15 Customizing a Security Policy Template

![](img/729efc56f204a2ebffb8295c3a2dfdfb_221_0.png)

## Figure 5.16 The Security Configuration Console Configuration Choices Screen

![](img/729efc56f204a2ebffb8295c3a2dfdfb_221_1.png)

After making this selection, you're asked to verify the location of the log file that will be created, and then you are presented with the Configuring Computer Security screen shown in Figure 5.17.

## Chapter 5 • Attacking and Defending Windows 2000

## Figure 5.17 Computer Configuration Progress Screen

![](img/729efc56f204a2ebffb8295c3a2dfdfb_222_0.png)

At this point, you're almost done. The last step in the process is to verify that the desired changes were actually made to the system you're working on. To accomplish this, follow the analysis steps you previously went through and compare the final result to the template you created and applied to the system. If all is okay, it should look similar to Figure 5.18 in each section of the template.

## Figure 5.18 Security Configuration Management Console Verifying Application of Changes

![](img/729efc56f204a2ebffb8295c3a2dfdfb_222_1.png)

## Attacking and Defending Windows 2000 • Chapter 5

## Tools & Traps...

## It's Not All Manual Configurations

All of the procedures detailed in this section allow the administrator to more fully secure the operating system environment. This is a manual procedure for illustration purposes, and an administrator could certainly copy the desired templates across a network connection and apply them in this manner. However, when using Active Directory (Chapter 6), the administrator can distribute and install these templates via the Group Policy capabilities of Active Directory, thus saving time and effort. The original construction of the custom templates must still be done in the manner detailed here.

One of the great things about these templates is that mistakes are relatively easy to fix. If it is discovered that the adjustments made are too rigid, another security template can be imported and installed working out the kinks. Be aware that this capability exists, but the security template applied must also define the settings changed in the previous template to remove them completely and return to a base setting.

## Configuring the File System and Disks

After looking at a way to check out the basic security configuration and modify if it needed, let's take some time to look at basic security configuration of the file system and disks within the Windows 2000 area. I've discussed previously that the FAT system is not suitable for security in Windows 2000. That leaves you with the option to operate your systems with NTFS 5.0. This is the preferred file system to use in the Windows 2000 environment. If you have made the decision to change to NTFS after an installation with FAT or FAT32, you can use the convert.exe command in a command prompt to perform the conversion. For instance, converting drive C, open a command prompt (enter cmd in the Run window), and enter the command convert c: \ntfs and press Enter. This creates a prompt letting you know that the file system is in use and that a restart is needed for the conversion. Following the restart, it would change the file system to NTFS. No data is lost during this operation, but it is a one-way conversion process. (Of course, good practice would indicate that you back up data before performing any file operations).

![](img/729efc56f204a2ebffb8295c3a2dfdfb_223_0.png)

## Chapter 5 • Attacking and Defending Windows 2000

## NTFS File Systems

I mentioned earlier that the default setting in Windows 2000 gives the Everyone group control to the root of each logical drive. As discussed in the sidebar, the ACL must be set for the root of the drive to a much more secure setting than the default allows. Permissions that are set at the root are "inherited" down through the directory structure unless specifically blocked. If you are using the NTFS file system as recommended, it is normal to expect changes made to the upper level of the directory structure would be automatically applied to directories and files below that level. However, there are some default configurations in Windows 2000 with a clean install where Users are not allowed to write to Program directories or their contents. To accomplish this, inheriting permissions from upper levels are blocked by clearing the checkbox at the bottom left of the Properties page for the folder, as shown in Figure 5.19. Note that the default permissions have not been applied to Program directories.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_224_0.png)

## Defending and Windows 2000 • Chapter 5

As you can see, the Everyone group is not present in the structure of the Program directory. Further, any changes made at the root of the drive will not be applied to directories or any of its subfolders because inheritance is blocked. This prevents the administrator from inadvertently changing settings on files or folders that have been configured differently down from the root. Windows 2000 also differentiates the ability to secure files independently from the directory settings as needed. File access permissions will always override the permissions at the directory level. Figure 5.20 illustrates that file permissions are inherited from the parent. If it was desired to further modify the ACL to reflect different values, simply clear the checkbox at the lower left of the properties sheet for the file. In this view, grey boxes indicate that the permission levels were inherited (Directory Contents value is not inherited because this is a file, not a directory).

## Figure 5.20 File Inheritance within the Directory Structure

![](img/729efc56f204a2ebffb8295c3a2dfdfb_225_0.png)

## Encrypting File System

Encrypting file system (EFS) operation in Windows 2000 is mutually exclusive with compression-related functions on formatted drives, so both operations on a particular file or folder are not possible. Administrators and users alike

![](img/729efc56f204a2ebffb8295c3a2dfdfb_225_1.png)

## Chapter 5 • Attacking and Defending Windows 2000

can encrypt files stored on an NTFS partition. This capability is a good security tool, especially in the case of “eyes only” or confidential information. It is particularly valuable in the case of laptop operation, because EFS provides the ability to locally encrypt data, which is protected in the case of unauthorized use or theft of the machine. Data encryption is accomplished by simply setting an attribute value on the properties sheet for a particular file or folder. Recommended practices set the encryption at the folder level, which means the contents of the folder are automatically encrypted when saved in the folder and decrypted when removed. EFS can use either the Advanced Encryption Standard (AES) or Triple-DES (3DES) as the encryption algorithm, which is used in conjunction with a key pair for the user and the designated Recovery Agent. You do need to be aware that you can also encrypt remote NTFS drives. However, unless network encryption processes or the use of WebDAV is used in the Windows 2000 environment, the data could be intercepted on the wire because it is not encrypted by default while moving on the network.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_226_0.png)

## EFS Usage

Installations of Windows 2000 Professional and Server provide EFS capability on NTFS 5.0 drivers. When EFS is initially configured during OS installation or formatting, a Recovery Agent key is created and stored locally on the local machine in a protected store in the user’s profile. This Recovery Agent key creation defaults to the administrator account for machines not a member of a domain, and to the domain administrator for machines that are made members of a Windows 2000 Active Directory domain. In a basic configuration, knowledge of either the administrator credentials or the credentials of the user who encrypted data would allow access to that data, because the Recovery Agent would be present locally. A number of configuration changes can more fully protect the data that is encrypted:

- Export the Recovery Agent key and store in a secure location
- Use smart cards/PINs for better user credential security
- Establish alternate Recovery Agents instead of the default agents
