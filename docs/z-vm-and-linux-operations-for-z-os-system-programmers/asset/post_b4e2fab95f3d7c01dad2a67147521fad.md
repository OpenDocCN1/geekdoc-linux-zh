
Control (MAC). Therefore, class ANY users, together with class G users, cannot violate the security policy. In the Control Program, each level of privilege is discrete and not predicated on others. Furthermore, each privilege class (a subset of commands) is related to one or more function types (subsets of users).

## 6.1.6 System user IDs involved in security

Certain user IDs are defined as part of the installation process. The standard user IDs for the default system installation are:

- **OPERATOR:** System operator and high privilege user ID is similar to root in Linux systems.
- **MAINT:** System administration and maintenance is similar to OPERATOR from an authorization point of view.
- **EREP:** Environmental Record Editing and Printing Program (EREP) is a hardware anomaly detection and predictive failure system.
- **DISKACNT:** Records events such as logon and logoff.
- **OPERSYMP:** System dump analyzer and problem tracking system. Retrieves symptom records.

## 6.1.7 Security relevant statements

The system configuration file can be edited to control the system security. The configuration file is located on a partition of a volume allocated as PARM. This minidisk is normally under user ID MAINT, and it is on minidisk address CF1. The file is called SYSTEM CONFIG by default, although its name can be altered during installation. The file is read at IPL time by the CP program that uses the statements, contained in the file, to configure the system.

The following command statements relevant to security are contained in the configuration file:

### DEFINE command

Use the DEFINE command to:

- Change the configuration of your virtual machine.
- Change the configuration of your operating system.
- Add a new alias for an existing CP command on your system.
- Add a new CP command to your system.
- Add a new version of an existing CP command to your system.
- Add a new DIAGNOSE code to your system.
- Add a new guest LAN to your system.

- **USER_DEFAULTS:** Defines default attributes and permissions for all users on the system.

## 6.1.8 Resource Access Control Facility (RACF)

Resource Access Control Facility (RACF) licensed program can satisfy the preferences of the user without compromising any of the concerns raised by security personnel. The RACF approach to data security is to provide an access control mechanism that offers effective user verification, resource authorization, and logging capabilities. RACF supports the concept of user accountability. It is flexible, has little noticeable effect on the majority of end users, and little or no effect on an installation's current operation. RACF controls access to and protects resources on both multiple virtual storage (z/OS) and virtual machine systems. For a software access control mechanism to work effectively, it must be able to first identify the person who is trying to gain access to the system, and then verify that the user is really that person. With RACF, you are responsible for protecting the system resources, such as minidisks, terminals, and shared file system (SFS) files and directories, and for issuing the authorities by which those resources are made available to users.

RACF records your assignments in profiles stored in the RACF database. RACF then refers to the information in the profiles to decide if a user should be permitted to access a system resource. The ability to log information, such as attempted accesses to a resource, and to generate reports containing that information can prove useful to a resource owner, and is very important to a smoothly functioning security system. Because RACF can identify and verify a user's user ID and recognize which resources the user can access, RACF can record the events where user-resource interaction has been attempted. This function records actual access activities or variances from the expected use of the system.

RACF has a number of logging and reporting functions that allow a resource owner to identify users who attempt to access the resource. In addition, you or your auditor can use these functions to log all detected successful and unsuccessful attempts to access the RACF database and RACF-protected resources. Logging all access attempts allows you to detect possible security exposures or threats. The logging and reporting functions are:

- **Logging:** RACF writes audit records in a file for detected, unauthorized attempts to enter the system. Optionally, RACF can also write records for authorized attempts or detected, unauthorized attempts to:
  - Access RACF-protected resources
  - Issue RACF commands
  - Modify profiles on the RACF database
