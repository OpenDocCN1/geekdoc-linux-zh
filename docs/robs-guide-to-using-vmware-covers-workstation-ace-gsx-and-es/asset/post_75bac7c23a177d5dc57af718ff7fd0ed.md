
## Installing ACE Manager

The software for VMware ACE can be downloaded from VMware’s website at the following URL: www.vmware.com/download. You can obtain an evaluation copy that is valid for 30 days. VMware ACE is licensed on a per user basis. You can buy a Starter Pack containing ACE manager, and four user licenses for USD 995. A separate ACE Manager license is USD 795 and individual user licenses cost USD 99 (prices are as of September 2005). The most recent version at the time of writing this book is version 1.0.1 (VMware-ACE-1.0.1-14996.exe).

Compared to the initial release in January 2005, version 1.0.1 includes the following new features:

- BIOS password
- Drag and Drop Support
- Enhanced full screen display
- New guest operating system support

The installation itself is rather straightforward. It does not require a reboot, so you can get started right away.

![](img/25fe75b93b97a021effaba85db112a52_73_0.png)

Figure 5.1: VMware ACE Manager settings.

One of the things you want to look into after the installation is complete, is the basic settings for VMware ACE Manager. You access these from the Edit menu under Preferences.

You can configure the default path where you would like to place the ACE project configuration files and the location of your virtual machines. VMware ACE Manager can also check for updates automatically.

You can also configure the same memory settings as for VMware Workstation.

## 5.3 Creating VMware ACE Projects

Virtual machines do not run inside ACE directly; they must be organized in projects. To start a new project, click the icon in the ACE Manager home window or select File → New Project.

- 1. Provide a name for your project and a location where you would like to store the project files.
- 2. Next, you are asked if you want to start the Add Virtual Machine Wizard. For this example, I have selected to do so.
- 3. The wizard that is used to add new virtual machines is very much like the one in VMware Workstation. An important difference is that you can choose to create an entire new machine or to use an existing machine. Creating a new virtual machine is identical to this process in VMware Workstation, except that you can not use raw physical partitions for your virtual machine since these can not be copied to end user computers.
- If you choose to use an existing virtual machine, browse to the .vmx file of that machine to add it to your project.
- 4. When the Add Virtual Machine Wizard is complete, you will be prompted to configure policies for the virtual machines in the newly created project. Configuring policies is discussed later in this chapter.

![](img/25fe75b93b97a021effaba85db112a52_75_0.png)

Figure 5.2: A default VMware ACE project typically contains one virtual machine.

## 5.4 Customizing a VMware ACE Project

In the main project window, click Edit project settings or select Settings from the Project menu. You can configure typical settings such as the project name and a description for the project. Other, more advanced topics are:

### Selecting a policy domain

VMware ACE machines can be configured to read their authentication and policy information from an Active Directory domain. Configure the domain in the Policies Domain tab of the Project Settings window.

### Defining offline policies

- Authentication policy: The key only
- Expiration policy: The expiration date only
- Devices policy: The list of allowed users only
- Network quarantine policy: All settings

### Enable a recovery key for your project

If you will be using password protection for your virtual machines, you need to create a recovery key for this project. The recovery key enables you to process password changes. I will discuss how to do this later. At this point, select Create New Recovery Key in the Recovery Key tab of the Project Settings window. Or, select Browse for existing key if you want to use another project's key for this project.

![](img/25fe75b93b97a021effaba85db112a52_76_0.png)

Figure 5.3: Create a recovery key for your project if you will be using password control.

To create a new key, specify a name for the key that will help you identify it later and specify the path where you would like to store the file that contains the key.

Enter a password that will be assigned to the key file and that will protect the private portion of this public/private key pair. You need this password later when you need to process a password request from a user.

## 5.5 Configuring Policies for a VMware ACE Project

An important reason to use VMware ACE for deploying virtual machines to end users instead of using regular VMware Workstation machines is that you can configure policies for your ACE environment. With normal virtual machines, the use of a machine can not be restricted. With VMware ACE, policies can be defined to:

- Allow only specified users to work with the virtual machine
- Specify what network resources can be used from within the virtual machine
- Configure the use of removable devices for a virtual machine
- Control the life cycle of the virtual machine

![](img/25fe75b93b97a021effaba85db112a52_77_0.png)

Figure 5.4: An overview of the available policies in VMware ACE.

There are two policy categories: VMware ACE policies that define how the ACE application works and virtual machine policies which define the behavior of the virtual machine that runs in ACE. Table 5.1 contains a brief description of the available policies.

### Table 5.1: A brief description of all available ACE Policies.

| VMware ACE Policy | Default | Description |
|---|---|---|
| Hot fix | Disabled | Use this policy to allow a user to request help with a lost password or an expired or copy protected machine. They can send an e-mail directly with an installed e-mail application through MAP I or create a file and send it themselves. Requires recovery to be enabled for the virtual machine. |
| Administrator access | Disabled | With this special Administrator password you can run the virtual machine on the end users' computer in a special application to change its configuration. Start this mode with the `vmware -k` command and provide the path and filename for the `.vmx` file. |
| Troubleshooting | Power | Power and reset controls are enabled by default. Reverting to the original state is disabled by default. When enabled the original image is created when the virtual machine is deployed to the user. |
| Easy printer setup | Disabled | When enabled, it allows users to select host printers to assign them to the virtual machine. |
| VMware ACE Window | Disabled | When enabled, it runs the VMware ACE machine in full screen mode. |
| Preferences | Enabled | Allows users to change these settings for the virtual machine: Confirm before exit yes/no, either suspend or power off the virtual machine and specify where to display the device connection icons. |
| Virtual Machine Policies |  |  |
| Encryption and authentication |  | Use this policy to define security for the end user's virtual machine. This policy is described in detail later. |
| Expiration |  | Use this policy to specify if the policy will expire and if it does expire, specify the length of time such as how many days or the expiration date. |
| Copy protection |  | Users can copy the virtual machine files to a different location or another computer. With this policy enabled they can not run the virtual machine when copied to another location. |
| Network quarantine |  | Control access to the network from the virtual machine. This policy will be described in detail later. |
| Device connection CD-ROM | Everyone | Defines who can connect CD-ROM devices to the virtual machine: everyone, selected users, or defined by a script. |
| Device connection floppy | Everyone | Defines who can connect floppy devices to the virtual machine: everyone, selected users, or defined by a script. |
