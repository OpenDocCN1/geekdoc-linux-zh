
10. Test the configuration by completing the following:
    - a. In Mozilla, select **File > New > Navigator Window** to open a new browser window.
    - b. Enter `https://your_server_DNS/NetStorage`.
    - c. When prompted, authenticate as **JGoldman** (or some other ACCTUSERS group member) with a password of **novell**; then select **OK**.

    You should see the ProjectFiles storage location displayed.

    You should also be able to upload files to the ProjectFiles folder. If you cannot, make sure that JGoldman is Samba enabled, then try again.

    - d. Select the **Logout** icon on the NetStorage menu bar; then close the browser window.
    - e. (Optional) Explore and see who can access the ProjectFiles folder and who can’t.

*(End of Exercise)*

## Summary

| Objective | Summary |
| :--- | :--- |
| 1. Describe the Purpose and Architecture of iFolder | Novell iFolder is a Net services software solution that lets mobile professionals access their local files from anywhere—online, offline, all the time—across multiple workstations and the Net. iFolder automatically and intelligently updates your files across desktop computers, laptops, and other connected devices you use, letting you use them wherever you happen to be—at the office, at home, or in a hotel. All you need is an active network or Internet connection and the iFolder client, a Web browser, or NetDrive. To describe the purpose and architecture of iFolder, you need to know the following:<br>- iFolder Benefits<br>- iFolder Features<br>- iFolder Components<br>- iFolder Architecture |
| **2. Install and Configure iFolder** | You install and configure iFolder on Linux in 4 basic stages:<ol><li>Install the first iFolder server.</li><li>Configure Global settings, default policies, LDAP authentication sources, and iFolder servers.</li><li>Provision iFolder users.</li><li>Install additional iFolder servers (as needed).</li></ol> To complete these phases and manage iFolder, you need to know the following:<ul><li>Prerequisites for Installing on Linux Servers</li><li>How to Install iFolder from NNLS</li><li>How to Configure Your iFolder Server</li><li>How to Access the iFolder Web Sites</li><li>How to Install and Configure the iFolder Client</li><li>How to Manage iFolder User Accounts</li><li>How to Manage iFolder Servers</li><li>How to Manage LDAP Servers</li><li>How to Monitor Your iFolder System</li><li>How to Generate Reports</li></ul> |
| 3. **Describe the Purpose and Architecture of Samba** | Samba is a software package that implements Microsoft's SMB/CIFS networking protocols on Linux.<br><br>It allows a Linux machine to function as a Windows-compatible file server and to act as a client to other Windows servers.<br><br>To describe the purpose and architecture of Samba, you need to know the following:<br>- What Server Message Block (SMB) Is<br>- What Common Internet File System (CIFS) Is<br>- Samba and NNLS |
| 4. **Install and Configure Samba** | To install and configure Samba, you need to know the following:<br>- Steps for Installing Samba<br>- How to Configure Samba<br>- How to Access Files Through Samba |
| 5. Describe the Role and Function of NetStorage | NetStorage provides secure Internet-based access to files and folders on Linux, Windows, and NetWare servers in your network through a browser.<br><br>NetStorage authentication relies on Novell eDirectory authentication to provide secure access, so Internet-based access is as secure as accessing files from within the network.<br><br>To describe the role and function of NetStorage, you need to understand the following:<br>- NetStorage Benefits<br>- How NetStorage Works<br>- What Users See When They Access NetStorage |
| 6. Install and Configure NetStorage | To install and configure NetStorage, you need to know the following:<br>- Steps for Installing NetStorage<br>- Creating Storage Location Objects and Lists<br>- Configuring NetStorage<br>- Accessing NetStorage Files and Folders |

## SECTION 7

## Manage Printers with NNLS

In this section, you learn how to set up and configure iPrint on a Linux® server and how to print from a Windows® workstation.

### Objectives

- 1. Identify the Benefits of iPrint
- 2. Describe How iPrint Works
- 3. Install and Configure iPrint
- 4. Print with iPrint

### Introduction

Novell iPrint is a printing solution based on the industry standard Internet Printing Protocol (IPP), which eliminates the complexities of printing over the Internet.

iPrint lets employees, mobile employees, business partners, and customers access printers from a variety of remote locations using existing Internet connections.

Whether users are working in an office building, telecommuting from home, or attending a sales meeting in another country, iPrint ensures that they can print documents quickly, easily, and reliably.

![](img/d63035f3fce0eaaf97203dde900affb7_132_0.png)

> For additional details on installing and configuring iPrint, see the *Novell iPrint Administration Guide* for Novell® Netrprise™ Linux® Services.

### Objective 1

### Identify the Benefits of iPrint

The following are the benefits and features of iPrint:

- **Global access to printers.** iPrint allows mobile employees, business partners, and customers to access your printers from anywhere with a web browser.

For example, suppose you are attending a sales meeting at your company’s regional office and you discover that you did not bring enough copies of the monthly sales report.

Using your laptop and a web browser, you can browse to a floor plan of the building, select the printer next to the conference room, and print additional copies of the sales report.

- **Reduced communication costs.** Printing to a remote location can be challenging. Faxing can be expensive and inefficient.

If you email a document, you have to be sure the recipient has a compatible word processing or page-layout application.

By contrast, iPrint enables you to use existing printers to print high-quality, legible documents.

- **Secure printing.** eDirectory integrates with iPrint to ensure that only authorized users can access your printers.

Print jobs are submitted to the iPrint Manager via SSL to prevent unauthorized users from accessing your documents.

- **Unified management.** You can control all your printers from a single location, even if the printers are made by different manufacturers and are in different locations.

You can even use customized management features to create a common interface to access your company’s print resources.

- **Customized viewing of printers.** Users can immediately view available printers from a web page. Network administrators can customize this page to meet specific business requirements.

For example, using the Map Design tool, you can insert a floor plan of your building into a corporate web page. You can then easily drag and drop icons to the floor plan that represent the actual locations of your printers. You can access the map through a browser and select a printer icon to install the printer and its drivers.

### Objective 2 Describe How iPrint Works

To describe how iPrint works, you need to know how the following components work:

- iPrint Manager
- iPrint Driver Store
- iPrint Client
- iPrint Map Designer

The following illustrates how the iPrint Manager, iPrint Driver Store, and iPrint client components provide print services:

**Figure 7-1**

![](img/d63035f3fce0eaaf97203dde900affb7_135_0.png)

#### *iPrint Manager*

The iPrint Manager is an object in the eDirectory™ tree as well as a daemon that runs on your Linux server. Print jobs are submitted to the iPrint Manager and then forwarded to the printer, when the printer is ready:

**Figure 7-2**

![](img/d63035f3fce0eaaf97203dde900affb7_135_1.png)
