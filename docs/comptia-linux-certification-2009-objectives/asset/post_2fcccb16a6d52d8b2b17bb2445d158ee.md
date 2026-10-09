
## How to Update and Refresh Packages

### Procedure Reference: Update Packages

To update packages:

- 1. Download the updated package.
- 2. Update the existing package using the `rpm -Uvh [file name.rpm]` command.
- 3. To verify that the package was updated, use `rpm -qi [package name]`.

## ACTIVITY 7-3

### Upgrading Packages

**Data Files:**
AdobeRdr9.1.0-1_i486linux_enu.rpm

**Before You Begin:**
- 1. You have logged as root in the GUI.
- 2. Navigate to the /085039Data/Managing_Packages directory. Copy AdobeRdr9.1.0-1_i486linux_enu.rpm to the /rpms directory.
- 3. Enter `clear` to clear the terminal window.

**Scenario:**
You installed the PDF software on a Linux system to enable users to view e-books. Some users encounter errors when they try to open the latest e-books. After checking the errors, you decide to upgrade the PDF software to the latest version.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Install the newer version of the Adobe Reader package. | a. Enter `rpm -Uvh AdobeRdr9.1.0-1_i486linux_enu.rpm` to upgrade the Acrobat Reader package. |
| | b. Observe that the progress bar is at **100%** for **AdobeReader_eni**, indicating that the package was successfully installed. |

- 2. Verify that the Adobe Reader package is upgraded.
  - a. Enter `rpm -qi AdobeReader_enu` to view information about the package.
  - b. Observe that the **Version** is 9.1.0 and the **Release** is 1.
  - c. Enter `cd /opt/Adobe/Reader9/bin` to change to the bin directory.
  - d. Enter `./acroread` to launch the application.
  - e. In the **Adobe Reader - License Agreement** dialog box, click **Accept** to accept the terms of the agreement.
  - f. Observe that the **Acrobat Reader** window is displayed.
  - g. Close the **Acrobat Reader** window.
  - h. Enter `clear` to clear the terminal window.

## TOPIC D

### Configure Repositories

You upgraded and refreshed installed packages. When managing a network, you may have to update the systems with the latest packages. You need to know where to obtain these packages. In this topic, you will examine repositories and how to use them to update systems.

Updating systems with the latest packages is one of the most important roles of a system administrator. To do this, you must know where the packages are available and how they can be downloaded.

## Repositories

**Definition:**

A *repository* is a database that holds source code and compilations. There are two types of repositories, local and online. Software can be installed on a system only when repositories for the software are present on the system. The packages for the software are found in their respective repositories and are directly installed from them.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_0.png)

Repositories

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_1.png)

*Figure 7-7: A local repository.*

## Types of Repositories

There are two types of repositories, *online repositories* and *local or private repositories*. Online repositories are found on the Internet. Packages can be directly downloaded from the Internet and installed on a system. Local or private repositories are stored on your system. The process of updating systems is greatly facilitated by repositories because the source files are readily available. Repositories make it easier for system administrators to update multiple systems simultaneously.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_288_2.png)

Types of Repositories

![](img/477ccb2f05b6ba1b2d563ea74f18c197_289_0.png)

## The createrepo Command

The createrepo command is used to create yum repositories. It generates XML metadata called repomd and creates a repository from existing rpm packages. The createrepo command has a number of options that facilitate the repository creation process.

Various options for the createrepo command are listed below.

| Option | Enables You To |
| :--- | :--- |
| -p | Generate the output in the xml format. |
| -s | Select the checksum to be used to create the repository. |
| -c | Compare the repository with the checksum and check package integrity. Creates a cache directory for the package checksum. |
| -x | Exclude the specified files from the repository. |
| -h | Show the help menu. |
| -v | Run the command verbosely. |

## Syntax

The syntax of the createrepo command is `createrepo [Options] <Directory>`.

## How to Configure Repositories

### Procedure Reference: Creating a Private Repository

To create a private repository:

- 1. Log in as root.
- 2. Enter `mkdir /(<directory name>)` to create a directory.
- 3. Populate the directory with packages.
- 4. Enter `createrepo -v /(<directory name>)` to create a private repository.
- 5. If you add or remove any packages from the directory, run the `createrepo` command again.

### Procedure Reference: Configuring Additional Repositories

To configure additional repositories:

- 1. Log in as root.
- 2. Enter `cd /etc/yum.repos.d` to navigate to the `/etc/yum.repos.d` directory.
- 3. Enter `vi (<file name>)` to create a file.
- 4. Switch to the insert mode.
- 5. Type the required information.
  - Enter `name = repository name` to set the repository name.
  - Enter `description of the repository` to give a description of the repository.
  - Enter `baseurl = {URL of the repository}` to set the repository's baseurl.
  - Enter `enabled = {0 | 1}` to control the status of the repository.
  - Enter `gpgcheck = {0 | 1}` to control the GPG signature verification.
- 6. Save and close the file.

## GPG

GnuPG (GPG) is free software used for encrypting and signing packages or files. The encryption or signature is used to verify the authenticity of any file shared on the network.

## ACTIVITY 7-4

### Configuring Repositories

**Before You Begin:**

- 1. You have logged in as root in the GUI.
- 2. The terminal window is displayed.
- 3. Enter `cd /rhelsource/Server` to change to the Server directory.
- 4. Enter `clear` to clear the terminal window.

**Scenario:**

You have been assigned the task of updating a few systems on the network with the kickstart application. While installing, you find that there are hundreds of packages in the installation folder, and you have to search for the kickstart packages every time. So, you decide to make your job easier by creating a kickstart repository with specific packages, so that you can call the repository instead of searching for the packages.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Install the createrepo package. | a. Enter `rpm -ivh createrepo-0.4.11-3.el5.noarch.rpm` to install the createrepo package. |
| | b. Observe that the progress bar is at **100%** indicating that the package was successfully installed. |
| | c. Enter `rpm -q createrepo` to verify that the package is installed. |
| | d. Observe that the **createrepo-0.4.11-3.el5** package is displayed. |
| | e. Enter `rpm -qi createrepo` to view information about the package. |
| | f. Observe that the **Version** is **0.4.11** and the **Release** is **3.el5**. |

- 2. Create a private repository.
  - a. Enter `cd /` to navigate to the / directory.
  - b. Enter `createrepo -v /rhelsource` to create a private repository.
  - c. Observe that the 2255 packages from /rhelsource/Server directory are entered into the repository.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_292_0.png)

- 3. Configure the new repository.
  - a. Enter `cd /etc/yum.repos.d` to navigate to the /etc/yum.repos.d directory.
  - b. Enter `vi rhelsource` to create the rhelsource file.
  - c. Switch to the insert mode.
  - d. Enter **name = rhelsource** to specify the repository name.
  - e. Enter **My Local Repository** to specify the repository description.
  - f. Enter **baseurl=file://rhelsource/Server/** to specify the base url.
  - g. Enter **enabled = 1** to enable the repository.
  - h. Type **gpgcheck = 0** to disable gpgcheck.
  - i. Press **Esc** to exit to the command mode.
  - j. Save and close the file.
